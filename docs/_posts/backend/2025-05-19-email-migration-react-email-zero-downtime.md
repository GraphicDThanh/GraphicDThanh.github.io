---
title: "Email System Migration: From HTML Hell to React Email with Zero Downtime"
categories:
  - Backend
  - Architecture
tags:
  - email
  - react-email
  - nestjs
  - migration
  - strategy-pattern
---

![](/assets/images/2026/05/2026-05-19-email-migration-cover.webp)

## Table of Contents

- [The Pain of Legacy Email Templates](#the-pain-of-legacy-email-templates)
- [The Search for a Better Way](#the-search-for-a-better-way)
- [Architecture: The Strategy Pattern Solution](#architecture-the-strategy-pattern-solution)
- [Building the React Email Component Library](#building-the-react-email-component-library)
- [The Migration Process](#the-migration-process)
- [Pitfalls We Encountered](#pitfalls-we-encountered)
- [The Results](#the-results)

---

## The Pain of Legacy Email Templates

Ever looked at an email template in your codebase that's just a massive string of HTML with variables sprinkled throughout, and thought: *"Who wrote this?"*

Then you check `git blame` and see your own name. 😅

That was my exact situation when I got tasked with "migrate the email system" for a payment platform sending thousands of emails daily.

Today I'm sharing how we migrated our entire email infrastructure from plain HTML strings to React Email - **without any downtime** - and more importantly, without breaking production.

(Spoiler: This isn't your typical React Email tutorial. This is about **migrating a live system** safely.)

## The Legacy "HTML Hell"

Our old system: plain HTML strings with template literals.

```typescript
const invoiceEmailHtml = `
  <div><h1>Invoice #${invoiceNumber}</h1>
  <p>Hi ${customerName},</p>
  ${lineItems.map(item => `<tr><td>${item.name}</td></tr>`).join('')}
  <p>Total: $${total}</p></div>
`;
```

**Problems:** No reusability, no type safety, hard to test.

**Production incident:** Bug #1692 - Emails with 10+ products exceeded provider's 2KB limit and failed silently.

That was our wake-up call.

## The Search for a Better Way

We evaluated: Provider templates (variable limits), Handlebars (maintenance hell), MJML (steep curve).

**Winner: React Email**
- Component-based (reuse everything)
- TypeScript support (catch errors at compile-time)
- Works in browser AND Node.js
- Team already knows React

Perfect for our needs.

## The Challenge: Zero-Downtime Migration

### The Big Problem

```
We're sending 10,000+ emails/day to customers
- Can't stop production
- Can't rewrite everything at once
- Need to test incrementally
- Must be able to rollback quickly
```

**The question:** How do we migrate piece by piece without breaking things?

**The answer:** **Strategy Pattern**

## Architecture: The Strategy Pattern Solution

### Why Strategy Pattern?

Simple if/else doesn't work when:
- You have 10+ email types
- Migration takes months
- Need to mix old + new systems
- Want gradual rollout

**Strategy Pattern lets you:**
- Migrate emails one type at a time
- Test new and old side-by-side
- Easy rollback (just change strategy)

> **💡 Skip this if:** <5 email types + 1-2 week migration. Just replace all at once.

### The Core Idea

Instead of having one way to render emails, we'll support **three different strategies** simultaneously:

```
1. Legacy Strategy: Old HTML strings (existing emails)
2. Provider Strategy: Hosted templates (migration path)
3. Component Strategy: React Email (future goal)
```

All three can coexist. We migrate emails one type at a time.

### Implementation

**Step 1: Define the Interface**

```typescript
// Strategy interface - all rendering methods must implement this
interface EmailRenderingStrategy {
  render(payload: EmailPayload): Promise<EmailRenderOutput>;
}

interface EmailRenderOutput {
  html: string;
  subject: string;
  templateId?: string; // For provider-hosted templates
}

interface EmailPayload {
  to: string;
  data: Record<string, any>;
}
```

**Step 2: Implement Three Strategies**

```typescript
// Strategy #1: Legacy HTML (existing system)
class InlineFunctionStrategy implements EmailRenderingStrategy {
  async render(payload: EmailPayload): Promise<EmailRenderOutput> {
    // Call old functions that generate HTML strings
    const html = generateLegacyInvoiceHtml(payload.data);

    return {
      html,
      subject: `Invoice #${payload.data.invoiceNumber}`
    };
  }
}

// Strategy #2: Provider-Hosted Templates (migration path)
class ProviderHostedStrategy implements EmailRenderingStrategy {
  async render(payload: EmailPayload): Promise<EmailRenderOutput> {
    return {
      html: '', // Provider renders it
      subject: payload.data.subject,
      templateId: 'invoice-v1' // ← Resend template ID
    };
  }
}

// Strategy #3: React Email Components (goal)
class ComponentBasedStrategy implements EmailRenderingStrategy {
  async render(payload: EmailPayload): Promise<EmailRenderOutput> {
    // Render React component to HTML
    const html = await renderToString(
      <InvoiceEmail {...payload.data} />
    );

    return {
      html,
      subject: `Invoice #${payload.data.invoiceNumber}`
    };
  }
}
```

**Step 3: Email Service with Strategy Pattern**

```typescript
@Injectable()
export class EmailService {
  private strategies = new Map<EmailType, EmailRenderingStrategy>();

  constructor(
    private readonly emailProvider: EmailProviderService
  ) {
    this.registerStrategies();
  }

  private registerStrategies() {
    // Configure which strategy each email type uses
    this.strategies.set(
      'invoice',
      new ComponentBasedStrategy() // ← Already migrated
    );
    this.strategies.set(
      'receipt',
      new InlineFunctionStrategy() // ← Not migrated yet
    );
    this.strategies.set(
      'reminder',
      new ComponentBasedStrategy() // ← Already migrated
    );
  }

  async sendEmail(type: EmailType, payload: EmailPayload): Promise<void> {
    // Get appropriate strategy
    const strategy = this.strategies.get(type);

    if (!strategy) {
      throw new Error(`No strategy found for email type: ${type}`);
    }

    // Render email using strategy
    const { html, subject, templateId } = await strategy.render(payload);

    // Send via provider
    await this.emailProvider.send({
      to: payload.to,
      subject,
      html,
      templateId
    });
  }
}
```

**Why This Architecture Rocks:**

```
✅ Migrate emails one type at a time (invoice first, then receipt, etc.)
✅ Easy rollback (just change the strategy)
✅ Test new and old side-by-side
✅ Zero changes to business logic
✅ Each strategy is independent
✅ Can A/B test different approaches
```

## Building the React Email Component Library

Structure: `emails/` for preview, `src/templates/` for production code.

**Reusable Button Component:**

```tsx
// src/templates/components/Button.tsx
import { Button as EmailButton } from '@react-email/components';

export const Button = ({ href, children }) => (
  <EmailButton href={href} style={{ padding: '12px 24px', backgroundColor: '#007bff' }}>
    {children}
  </EmailButton>
);
```

**Invoice Email Template:**

```tsx
// src/templates/InvoiceEmail.tsx
import { Html, Body, Container, Text } from '@react-email/components';
import { Button } from './components/Button';

interface InvoiceEmailProps {
  customerName: string;
  invoiceNumber: string;
  lineItems: Array<{ description: string; amount: number }>;
  total: number;
  invoiceUrl: string;
}

export const InvoiceEmail = ({ customerName, invoiceNumber, lineItems, total, invoiceUrl }) => (
  <Html>
    <Body style={{ backgroundColor: '#f6f9fc' }}>
      <Container>
        <Text>Hi {customerName}, Invoice #{invoiceNumber}</Text>
        <table>
          {lineItems.map((item, i) => (
            <tr key={i}>
              <td>{item.description}</td>
              <td>${item.amount}</td>
            </tr>
          ))}
        </table>
        <Text>Total: ${total}</Text>
        <Button href={invoiceUrl}>View Invoice</Button>
      </Container>
    </Body>
  </Html>
);
```

**Use in Backend:**

```typescript
import { render } from '@react-email/render';
import { InvoiceEmail } from '../templates/InvoiceEmail';

const html = await render(<InvoiceEmail {...invoiceData} />);
await emailService.sendEmail('invoice', { to: email, data: { html } });
```

> See [React Email examples](https://react.email/examples) for full templates.

## The Migration Process

### Phase 1: Preview Server

```bash
npm run dev  # Start preview at localhost:3000
```

Preview all templates locally with hot reload - no more "send and check Gmail"!

### Phase 2: Migrate by Priority

**Order:**
1. High-volume emails with bugs (invoices)
2. Customer-facing emails (confirmations)
3. Internal emails (reports)
4. Low-volume emails (password reset)

**Per Email Type:**
```
1. Build React component (4 hours)
2. Test in preview + send to Gmail/Outlook/Apple Mail (1 hour)
3. Deploy to staging (30 min)
4. Deploy to production (30 min)
5. Monitor for 24 hours
```

### Phase 3: Feature Flags (Optional)

For high-risk migrations, use environment variable:

```typescript
const useReactEmail = process.env.REACT_EMAIL_ENABLED === 'true';

this.strategies.set(
  'invoice',
  useReactEmail ? new ComponentBasedStrategy() : new InlineFunctionStrategy()
);
```

**Rollout:** OFF → Staging ON → Production ON → Remove flag after 7 days.

**Monitor:** Delivery rate (99.9%), bounce rate (0.1%), render time (<500ms).

**Rollback if any metric degrades by >1%.**

## Pitfalls We Encountered

### Pitfall #1: Not Testing Across Email Clients Early

**Mistake:** Built all React Email components, tested only in Gmail, deployed to production.

**Result:** Outlook users saw broken layouts (Word rendering engine), Apple Mail didn't load logos.

**Lesson:** Test in Gmail, Outlook, Apple Mail BEFORE deploying each template. 30 minutes of testing saves days of emergency fixes.

**Common fixes:**

```tsx
// ❌ Outlook doesn't support flexbox
<div style={{ display: 'flex' }}>...</div>

// ✅ Use tables instead
<table width="100%">
  <tr><td width="50%">Column 1</td><td>Column 2</td></tr>
</table>

// ✅ Add alt text for images (Gmail blocks by default)
<img src="https://cdn.example.com/logo.png" alt="Company Logo" />
```

**Tools:** Litmus ($99/mo), Email on Acid ($99/mo), or send to real test accounts (free).

### Pitfall #2: Image Paths

```tsx
// ❌ Relative paths don't work in emails
<img src="/assets/logo.png" />

// ✅ Use absolute URLs
<img src="https://cdn.example.com/logo.png" />
```

### Pitfall #3: CSS Limitations

```tsx
// ❌ CSS classes don't work
<div className="card">...</div>

// ✅ Use inline styles
<div style={{ padding: '20px', backgroundColor: '#fff' }}>...</div>

// ✅ Use tables for layout
<table><tr><td>...</td></tr></table>
```

### Pitfall #4: Large Template Bundles

```typescript
// ✅ Lazy load to avoid importing React Email on every request
export async function sendEmail() {
  const { render } = await import('@react-email/render');
  const { InvoiceEmail } = await import('@my-company/email-templates');
  const html = await render(<InvoiceEmail {...props} />);
}
```

## The Results

After 3 months of migration:

### Metrics That Improved

```
✅ Email delivery rate: 97.5% → 99.9%
✅ Bugs related to emails: 15 tickets/month → 1 ticket/month
✅ Development time: -60% (component reuse)
✅ Test coverage: 40% → 85%
✅ Time to add new email: 2 days → 4 hours
```

### Developer Experience

```
✅ Component library → Consistent design
✅ TypeScript → Catch errors at compile time
✅ Preview server → No more "send and check Gmail"
✅ Hot reload → Instant feedback
✅ Version control → Track template changes in git
✅ Reusable components → Write once, use everywhere
```

### Business Impact

```
✅ Customer satisfaction up (better email experience)
✅ Support tickets down (fewer email issues)
✅ New email templates ship faster
✅ Design consistency across all emails
```

## Key Takeaways

1️⃣ **Don't rewrite everything at once** - Migrate incrementally using Strategy Pattern

2️⃣ **Strategy Pattern enables parallel approaches** - Old and new can coexist

3️⃣ **Feature flags are your best friend** - Easy rollout and rollback

4️⃣ **Monitor metrics before committing 100%** - Catch issues early

5️⃣ **Component-based approach pays long-term dividends** - Reusability saves massive time

6️⃣ **Preview server is a game-changer** - Speeds up development by 10x

7️⃣ **TypeScript catches bugs before production** - Type-safe templates prevent errors

8️⃣ **Test in multiple email clients** - Gmail, Outlook, Apple Mail all render differently

---

## What's Next?

After successfully migrating your email system, consider these follow-up topics:

### 🧪 **Testing & Quality**
If your email templates are critical (invoices, receipts), invest in automated testing:
- Automated screenshot testing across email clients (Litmus, Email on Acid)
- Visual regression testing (catch unintended style changes)
- Load testing (can your system handle 10K+ emails/hour?)

### 🏗️ **Production Infrastructure**
For high-volume email systems (>100K emails/day):
- Queue-based processing with Bull/BullMQ (handle spikes, retries)
- Email provider failover (Resend → SendGrid backup)
- Rate limiting to avoid provider throttling

### 🔐 **Security & Compliance**
Before going to production at scale:
- SPF, DKIM, DMARC configuration (prevent your emails from being marked as spam)
- GDPR compliance for email data retention
- Preventing email injection attacks

Want to learn more? Check out the [React Email documentation](https://react.email/docs/introduction) for advanced patterns.

## Best Practices Checklist

```
Pre-Migration:
✅ Set up preview server for local development
✅ Build component library with reusable parts
✅ Define TypeScript interfaces for all email props
✅ Implement Strategy Pattern in email service
✅ Create feature flags for gradual rollout

During Migration:
✅ Migrate high-priority emails first
✅ Test thoroughly in preview before deploying
✅ Use feature flags for A/B testing
✅ Monitor delivery rates and error logs
✅ Keep old code for quick rollback

Post-Migration:
✅ Remove old code only after 100% rollout
✅ Document component usage for team
✅ Set up automated screenshot tests
✅ Create email template guidelines
✅ Celebrate with team! 🎉
```

## When Should You Migrate?

**✅ Migrate to React Email if:**
- Your team knows React
- You have multiple email templates
- You need design consistency
- You want type safety
- You have complex dynamic emails
- You're tired of email bugs

**❌ Don't migrate if:**
- You only have 1-2 simple emails
- Team doesn't know React
- Email templates rarely change
- Current system works well

## Conclusion

Migrating a production email system is scary, but with the right architecture (Strategy Pattern), proper planning (incremental migration), and good tooling (React Email), it's totally manageable.

The key lessons:
- **Don't change everything at once**
- **Make it reversible**
- **Monitor closely**
- **Invest in reusable components**

If you're struggling with unmaintainable email templates, this approach could transform your email system from a maintenance nightmare into a joy to work with.

Hope this helps you build a better email infrastructure! 📧

---

**Resources:**
- [React Email Documentation](https://react.email/docs/introduction)
- [React Email - Monorepo Setup](https://react.email/docs/getting-started/monorepo-setup/pnpm) (for pnpm/Turborepo/Nx)
- [Strategy Pattern Explained](https://refactoring.guru/design-patterns/strategy)
- [Email on Acid - Testing Tools](https://www.emailonacid.com/)

*Have you migrated an email system before? What challenges did you face? Share your experience in the comments!*
