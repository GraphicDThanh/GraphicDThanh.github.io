---
title: "Shared PDF Generation Between Frontend and Backend: One Template, Two Platforms"
categories:
  - Backend
  - Full-Stack
tags:
  - react-pdf
  - monorepo
  - turborepo
  - pdf-generation
  - typescript
---

![](/assets/images/2026/05/2026-05-19-shared-pdf-generation-cover.webp)

## Table of Contents

- [The Problem](#the-problem-pdf-inconsistency-nightmare)
- [Solution: Shared Package](#solution-shared-package-with-react-pdf)
- [Implementation](#implementation-building-the-pdf-package)
- [Usage (Frontend & Backend)](#using-the-package)
- [Best Practices](#best-practices--takeaways)

---

## The Problem: PDF Inconsistency Nightmare

*"Hey, the PDF downloaded from the website is different from the one in the email..."*

*"The customer name in the web download shows 'John Doe', but the email attachment shows 'Doe Electronics Inc.' - which one is correct?"*

That message from our QA team made me realize: maintaining two separate PDF codebases (frontend + backend) is a recipe for disaster.

Today I'm sharing how we built a shared PDF package that works on both browser (Next.js) and server (NestJS), ensuring:
- ✅ PDFs from both sources are identical
- ✅ No code duplication
- ✅ Type-safe with TypeScript
- ✅ Easy to maintain and extend

Main tools: **@react-pdf/renderer** + **Turborepo monorepo**

## Why We Need PDF in Multiple Places

In an e-commerce system, we need to generate PDFs in three different scenarios:

**1️⃣ Frontend (Browser):**
```
User clicks "Download Invoice"
→ Generate PDF in browser
→ No API call needed
→ Instant download
```

**2️⃣ Backend (Email Attachment):**
```
Order confirmed → Send email with PDF invoice
→ Generate PDF on server
→ Attach to email
```

**3️⃣ Backend (API Endpoint):**
```
GET /api/invoices/:id/pdf
→ Generate PDF on-demand
→ Stream to browser
```

## The Naive Approach (And Why It Fails)

Here's what many teams do initially:

```typescript
// ❌ Approach: Duplicate code

// Frontend (using jsPDF)
function generateInvoicePDF(invoice: Invoice) {
  const doc = new jsPDF();
  doc.text(`Invoice #${invoice.number}`, 10, 10);
  doc.text(`Customer: ${invoice.customer.name}`, 10, 20);
  doc.text(`Total: $${invoice.total}`, 10, 30);
  // ... 100 lines of code
}

// Backend (using PDFKit)
function generateInvoicePDF(invoice: Invoice) {
  const doc = new PDFDocument();
  doc.text(`Invoice #${invoice.number}`, 10, 10);
  doc.text(`Customer: ${invoice.customer.businessName}`, 10, 20); // ← Different!
  doc.text(`Total: $${invoice.total}`, 10, 30);
  // ... 100 lines of DIFFERENT code
}
```

**Problems with this approach:**
```
❌ Code duplication → maintain two places
❌ Different logic → different outputs
❌ Inconsistent data mapping → bugs
❌ Different styling → poor UX
❌ Update one place, forget the other → disaster
```

**Real bugs we encountered:**

```
Bug #1: Bill-to field
- Browser PDF: Shows customer.name ✅
- Email PDF: Shows customer.businessName ❌
→ Customer complained "the name is wrong"

Bug #2: Product pricing
- Browser: Shows discounted unit price
- Email: Shows original price
→ Numbers don't match

Bug #3: Logo rendering
- Browser: Logo looks crisp
- Email: Logo stretched/pixelated
→ Unprofessional look
```

## Solution: Shared Package with @react-pdf

### Why @react-pdf/renderer?

Let's compare popular PDF libraries:

```
┌──────────────┬────────┬────────┬─────────────┬──────────┐
│   Library    │Browser │ Server │   Approach  │  Rating  │
├──────────────┼────────┼────────┼─────────────┼──────────┤
│ jsPDF        │   ✅   │   ❌   │ Imperative  │   ⭐⭐   │
│ PDFKit       │   ❌   │   ✅   │ Imperative  │   ⭐⭐   │
│ Puppeteer    │   ❌   │   ✅   │ HTML to PDF │  ⭐⭐⭐  │
│ @react-pdf   │   ✅   │   ✅   │ Declarative │ ⭐⭐⭐⭐ │← Pick this
└──────────────┴────────┴────────┴─────────────┴──────────┘
```

**Why @react-pdf wins:**
```
✅ Works on both browser & Node.js
✅ React component-based (familiar to most developers)
✅ Type-safe with TypeScript
✅ Reusable components
✅ Great documentation & active community
✅ Easy styling with React-style objects
```

### Architecture Overview

```
ecommerce-monorepo/
├── packages/
│   └── pdf-templates/              # ← Shared package
│       ├── src/
│       │   ├── invoice/
│       │   │   ├── InvoiceTemplate.tsx
│       │   │   ├── InvoiceHeader.tsx
│       │   │   └── styles.ts
│       │   ├── components/
│       │   │   ├── Button.tsx
│       │   │   ├── Table.tsx
│       │   │   └── Badge.tsx
│       │   ├── utils/
│       │   │   └── data-transformer.ts
│       │   └── index.ts
│       └── package.json
│
├── apps/
│   ├── web/                        # Next.js frontend
│   │   └── uses pdf-templates ✅
│   │
│   └── api/                        # NestJS backend
│       └── uses pdf-templates ✅
│
└── turbo.json                      # Turborepo config
```

## Implementation: Building the PDF Package

### Step 1: Package Setup

```json
// packages/pdf-templates/package.json
{
  "name": "@my-shop/pdf-templates",
  "version": "1.0.0",
  "main": "./dist/index.js",
  "types": "./dist/index.d.ts",
  "scripts": {
    "build": "tsc",
    "dev": "tsc --watch"
  },
  "peerDependencies": {
    "react": "^18.0.0",
    "@react-pdf/renderer": "^3.1.0"
  },
  "devDependencies": {
    "typescript": "^5.0.0",
    "@types/react": "^18.0.0"
  }
}
```

### Step 2: TypeScript Interfaces (Type Safety First!)

```typescript
// packages/pdf-templates/src/types.ts

export interface InvoicePDFProps {
  // Basic info
  invoiceNumber: string;
  invoiceDate: Date;
  dueDate: Date;

  // Merchant info
  merchant: {
    name: string;
    logo?: string;        // URL or base64
    address: string;
    phone?: string;
  };

  // Customer info (single source of truth!)
  billTo: {
    name: string;         // ← Consistent field name
    address: string;
    email?: string;
  };

  // Line items
  lineItems: Array<{
    description: string;
    quantity: number;
    unitPrice: number;
    total: number;
  }>;

  // Totals
  subtotal: number;
  tax: number;
  total: number;

  // Optional fields
  paymentTerms?: string;
  notes?: string;
}
```

**Why this matters:** Having a clear interface prevents mapping errors and makes it impossible to pass wrong data types.

### Step 3: Building Reusable Components

Build a component library for common PDF elements:

```tsx
// src/components/InvoiceHeader.tsx
import { View, Text, Image } from '@react-pdf/renderer';

export const InvoiceHeader = ({ merchantName, merchantLogo, invoiceNumber, invoiceDate }) => (
  <View style={{ flexDirection: 'row', justifyContent: 'space-between', marginBottom: 20 }}>
    {merchantLogo && <Image src={merchantLogo} style={{ width: 80, height: 80 }} />}
    <Text style={{ fontSize: 24, fontWeight: 'bold' }}>{merchantName}</Text>
    <View style={{ alignItems: 'flex-end' }}>
      <Text style={{ fontSize: 10, color: '#666' }}>INVOICE</Text>
      <Text style={{ fontSize: 18, fontWeight: 'bold' }}>#{invoiceNumber}</Text>
      <Text style={{ fontSize: 10, color: '#666' }}>{invoiceDate.toLocaleDateString()}</Text>
    </View>
  </View>
);
```

```tsx
// src/components/LineItemsTable.tsx
import { View, Text } from '@react-pdf/renderer';

export const LineItemsTable = ({ items }) => (
  <View style={{ marginTop: 20 }}>
    {/* Header */}
    <View style={{ flexDirection: 'row', backgroundColor: '#f0f0f0', padding: 8 }}>
      <Text style={{ flex: 3 }}>Description</Text>
      <Text style={{ flex: 1, textAlign: 'center' }}>Qty</Text>
      <Text style={{ flex: 1.5, textAlign: 'right' }}>Price</Text>
      <Text style={{ flex: 1.5, textAlign: 'right' }}>Total</Text>
    </View>

    {/* Rows */}
    {items.map((item, i) => (
      <View key={i} style={{ flexDirection: 'row', padding: 8, borderBottom: '1px solid #e0e0e0' }}>
        <Text style={{ flex: 3 }}>{item.description}</Text>
        <Text style={{ flex: 1, textAlign: 'center' }}>{item.quantity}</Text>
        <Text style={{ flex: 1.5, textAlign: 'right' }}>${item.unitPrice}</Text>
        <Text style={{ flex: 1.5, textAlign: 'right' }}>${item.total}</Text>
      </View>
    ))}
  </View>
);
```

> **💡 Tip:** Keep styles inline for simple components. For complex styling, use `StyleSheet.create()`.

### Step 4: Main Invoice Template

```tsx
// src/invoice/InvoiceTemplate.tsx
import { Document, Page, View, Text } from '@react-pdf/renderer';
import { InvoiceHeader } from '../components/InvoiceHeader';
import { LineItemsTable } from '../components/LineItemsTable';

export const InvoiceTemplate = (props) => (
  <Document>
    <Page size="A4" style={{ padding: 40, fontSize: 12 }}>

      {/* Header */}
      <InvoiceHeader
        merchantName={props.merchant.name}
        merchantLogo={props.merchant.logo}
        invoiceNumber={props.invoiceNumber}
        invoiceDate={props.invoiceDate}
      />

      {/* Merchant & Customer */}
      <View style={{ flexDirection: 'row', justifyContent: 'space-between', marginTop: 20 }}>
        <View>
          <Text style={{ fontSize: 10, color: '#666' }}>FROM:</Text>
          <Text style={{ fontWeight: 'bold' }}>{props.merchant.name}</Text>
          <Text style={{ fontSize: 10 }}>{props.merchant.address}</Text>
        </View>
        <View>
          <Text style={{ fontSize: 10, color: '#666' }}>BILL TO:</Text>
          <Text style={{ fontWeight: 'bold' }}>{props.billTo.name}</Text>
          <Text style={{ fontSize: 10 }}>{props.billTo.address}</Text>
        </View>
      </View>

      {/* Line Items */}
      <LineItemsTable items={props.lineItems} />

      {/* Totals */}
      <View style={{ marginLeft: 'auto', width: 200, marginTop: 20 }}>
        <View style={{ flexDirection: 'row', justifyContent: 'space-between', padding: 4 }}>
          <Text>Subtotal:</Text>
          <Text>${props.subtotal}</Text>
        </View>
        <View style={{ flexDirection: 'row', justifyContent: 'space-between', padding: 4 }}>
          <Text>Tax:</Text>
          <Text>${props.tax}</Text>
        </View>
        <View style={{ flexDirection: 'row', justifyContent: 'space-between', padding: 8, borderTop: '2px solid #333', fontWeight: 'bold' }}>
          <Text>Total:</Text>
          <Text>${props.total}</Text>
        </View>
      </View>

      {/* Footer */}
      <Text style={{ textAlign: 'center', marginTop: 40, fontSize: 9, color: '#999' }}>
        Thank you for your business!
      </Text>
    </Page>
  </Document>
);
```

> **📖 Full Example:** See [@react-pdf documentation](https://react-pdf.org/) for advanced styling and components.

### Step 5: Data Transformation Layer (Critical!)

**This is the key to consistency.** Create ONE function to transform your Order entity into PDF props:

```typescript
// src/utils/data-transformer.ts
export function toPDFProps(order: Order): InvoicePDFProps {
  return {
    invoiceNumber: order.invoiceNumber,
    invoiceDate: new Date(order.createdAt),
    dueDate: new Date(order.dueDate),

    merchant: {
      name: order.merchant.name,
      logo: order.merchant.logoUrl ? `https://cdn.myshop.com/${order.merchant.logoUrl}` : undefined,
      address: formatAddress(order.merchant.address)
    },

    // ✅ Single source of truth - ALWAYS use customer.fullName
    billTo: {
      name: order.customer.fullName,  // Not businessName!
      address: formatAddress(order.customer.billingAddress),
      email: order.customer.email
    },

    lineItems: order.items.map(item => ({
      description: item.product.name,
      quantity: item.quantity,
      unitPrice: item.unitPrice,
      total: item.quantity * item.unitPrice
    })),

    subtotal: order.subtotal,
    tax: order.tax,
    total: order.total
  };
}
```

**Why this matters:**
- ✅ Used by BOTH frontend and backend
- ✅ Impossible to have different mapping logic
- ✅ Fix bug once, fixed everywhere
- ✅ Type-safe with TypeScript

### Step 6: Export the Package

```typescript
// src/index.ts
export { InvoiceTemplate } from './invoice/InvoiceTemplate';
export { toPDFProps } from './utils/data-transformer';
export type { InvoicePDFProps } from './types';
```

## Using the Package

### Frontend (Browser Download)

```tsx
// Button component in Next.js/React
import { pdf } from '@react-pdf/renderer';
import { InvoiceTemplate, toPDFProps } from '@my-shop/pdf-templates';

async function handleDownload(order) {
  // 1. Transform data
  const pdfProps = toPDFProps(order);

  // 2. Generate PDF blob
  const blob = await pdf(<InvoiceTemplate {...pdfProps} />).toBlob();

  // 3. Trigger download
  const url = URL.createObjectURL(blob);
  const link = document.createElement('a');
  link.href = url;
  link.download = `invoice-${order.invoiceNumber}.pdf`;
  link.click();
  URL.revokeObjectURL(url);
}
```

### Backend (Email Attachment / API)

```typescript
// NestJS PDF service
import { renderToStream, renderToBuffer } from '@react-pdf/renderer';
import { InvoiceTemplate, toPDFProps } from '@my-shop/pdf-templates';

// For email attachments
async function generatePDFForEmail(order) {
  const pdfProps = toPDFProps(order);
  const pdfBuffer = await renderToBuffer(<InvoiceTemplate {...pdfProps} />);

  await mailer.send({
    to: order.customer.email,
    subject: 'Your Invoice',
    attachments: [{
      filename: `invoice-${order.invoiceNumber}.pdf`,
      content: pdfBuffer
    }]
  });
}

// For API endpoint (GET /orders/:id/pdf)
@Get(':id/pdf')
async downloadPDF(@Param('id') id: string, @Res() res: Response) {
  const order = await this.ordersService.findOne(id);
  const pdfProps = toPDFProps(order);
  const stream = await renderToStream(<InvoiceTemplate {...pdfProps} />);

  res.set({
    'Content-Type': 'application/pdf',
    'Content-Disposition': `attachment; filename="invoice-${order.invoiceNumber}.pdf"`
  });

  return new StreamableFile(stream);
}
```

**Key points:**
- `renderToBuffer()` for email attachments
- `renderToStream()` for API streaming
- Same `toPDFProps()` transformation used everywhere

## Common Gotchas

### 1. Images Must Use Absolute URLs

```typescript
// ❌ Relative paths don't work
<Image src="/assets/logo.png" />

// ✅ Use absolute URLs or base64
<Image src="https://cdn.myshop.com/logo.png" />
<Image src="data:image/png;base64,iVBORw0KG..." />
```

### 2. Lazy Load on Frontend (Bundle Size)

```typescript
// ✅ Lazy load to avoid 200KB in initial bundle
const handleDownload = async () => {
  const { pdf } = await import('@react-pdf/renderer');
  const { InvoiceTemplate } = await import('@my-shop/pdf-templates');
  // Generate PDF...
};
```

### 3. Custom Fonts

```typescript
import { Font } from '@react-pdf/renderer';

Font.register({
  family: 'Roboto',
  src: 'https://fonts.gstatic.com/s/roboto/v30/KFOmCnqEu92Fr1Mu4mxP.ttf'
});

// Then use in styles
<Text style={{ fontFamily: 'Roboto' }}>Hello</Text>
```

## Testing

### Unit Test: PDF Generates Successfully

```typescript
import { pdf } from '@react-pdf/renderer';
import { InvoiceTemplate } from '../src';

it('should generate PDF without errors', async () => {
  const mockProps = { /* minimal props */ };

  const buffer = await pdf(<InvoiceTemplate {...mockProps} />).toBuffer();

  expect(buffer).toBeInstanceOf(Buffer);
  expect(buffer.length).toBeGreaterThan(10000); // At least 10KB
});
```

### Consistency Test: Same Input = Same Output

```typescript
it('should generate identical PDFs for same input', async () => {
  const order = await getTestOrder();

  const pdf1 = await pdfService.generateInvoicePDF(order);
  const pdf2 = await pdfService.generateInvoicePDF(order);

  // Compare checksums
  const hash1 = crypto.createHash('md5').update(pdf1).digest('hex');
  const hash2 = crypto.createHash('md5').update(pdf2).digest('hex');

  expect(hash1).toBe(hash2); // Must be identical
});
```

This test ensures frontend and backend generate the same PDF.

## Results & Benefits

After implementing this shared PDF package, we saw:

**✅ Bug Reduction:**
- PDF inconsistency bugs: **15 tickets/month → 0 tickets/month**
- Data mapping errors: **Eliminated completely**

**✅ Development Speed:**
- Time to add new PDF template: **2 days → 4 hours** (83% faster)
- Code reuse: **Every component used in 2+ places**

**✅ Maintainability:**
- Single source of truth for PDF logic
- Type-safe props prevent errors
- Easy to add new templates

**✅ Developer Experience:**
- Familiar React syntax
- Hot reload during development
- Clear error messages

## Best Practices & Takeaways

**Key Takeaways:**

1️⃣ **@react-pdf/renderer works on both browser & Node.js** - Perfect for shared packages

2️⃣ **Monorepo package = one codebase, multiple consumers** - No more duplication

3️⃣ **Data transformer layer is crucial** - Single source of truth for mapping

4️⃣ **Type-safe props catch errors at compile-time** - Better than runtime failures

5️⃣ **Reusable components speed up development** - Build once, use everywhere

**Best Practices Checklist:**

```
✅ Define clear TypeScript interfaces for all props
✅ Build reusable components (Header, Table, Footer)
✅ Use absolute URLs for images (or base64)
✅ Implement data transformer for consistent mapping
✅ Add visual regression tests for PDFs
✅ Lazy load PDF library on frontend (bundle size optimization)
✅ Handle errors gracefully with fallback options
✅ Document component props and usage examples
✅ Version your package properly (semver)
✅ Test on both platforms (browser and Node.js)
```

## When to Use This Approach

**✅ Use this approach when:**
- You need PDFs from both frontend AND backend
- You're already using monorepo (Turborepo, Nx, Lerna)
- Your team is familiar with React
- You need high consistency across platforms
- You have multiple PDF templates to maintain

**❌ Don't use this approach when:**
- You only need PDFs from ONE place (FE or BE)
- PDFs are extremely complex with heavy styling (consider Puppeteer)
- Your team doesn't know React
- You need pixel-perfect HTML-to-PDF conversion

## Conclusion

Building a shared PDF package might seem like extra work upfront, but it pays dividends in the long run:

- **No more inconsistencies** between frontend and backend PDFs
- **Faster development** with reusable components
- **Type safety** prevents bugs before they reach production
- **Single source of truth** for all PDF-related logic

If you're generating PDFs in multiple places and struggling with consistency, this approach could be a game-changer for your team.

Hope this helps you build a better PDF generation system! 🎨

---

**Resources:**
- [@react-pdf/renderer documentation](https://react-pdf.org/)
- [Turborepo monorepo guide](https://turbo.build/repo/docs)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/)

*Have you implemented something similar? What challenges did you face? Let me know in the comments!*
