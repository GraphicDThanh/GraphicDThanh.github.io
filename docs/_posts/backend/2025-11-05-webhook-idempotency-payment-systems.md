---
title: "Webhook Idempotency: Lessons from a 'Double Charge' Production Bug"
categories:
  - Backend
  - Payment Systems
tags:
  - webhook
  - idempotency
  - payment
  - race-condition
  - distributed-systems
---

![](/assets/images/2026/05/2026-05-19-webhook-idempotency-cover.webp)

## Table of Contents

- [The Production Incident](#the-production-incident)
- [Understanding Webhook Delivery Guarantees](#understanding-webhook-delivery-guarantees)
- [What is Idempotency?](#what-is-idempotency)
- [Implementation: 3 Patterns](#implementation-3-patterns-for-idempotency)
- [Webhook Security](#critical-webhook-security)
- [Testing Idempotency](#testing-idempotency)
- [Best Practices](#best-practices-checklist)

---

## The 3 AM Wake-Up Call

*Phone buzzes at 3 AM.*

*"Hey, merchants are reporting they've been charged payout fees twice. I checked and found several merchants with double charges..."*

That message from our support team was my introduction to the harsh reality of webhook idempotency in payment systems.

Today I'm sharing the story of this production bug, why it happened, and more importantly - how to build systems that handle webhooks being sent "at least once" while ensuring your logic runs "exactly once."

(Spoiler: It's not as simple as checking the database.)

## The Production Incident

### The Context

Our payment system integrates with a payment gateway (let's call it "PaymentProvider"). Here's how payouts worked:

```
Flow:
1. Merchant requests payout (withdraw money to bank)
2. PaymentProvider processes payout
3. PaymentProvider sends webhook: "Payout successful"
4. Our system charges 0.5% payout fee
5. Update merchant balance
```

### The Naive Implementation

Here's what our code looked like initially:

```typescript
@Controller('webhooks')
export class WebhookController {
  @Post('payment-provider')
  async handlePayoutWebhook(@Body() event: PayoutEvent) {
    const payout = await this.payoutService.findOne(event.payoutId);

    // ❌ What's wrong with this logic?
    if (payout.status !== 'completed') {
      // Charge 0.5% fee
      const fee = payout.amount * 0.005;
      await this.feeService.createPayoutFee({
        payoutId: payout.id,
        amount: fee
      });

      // Update status
      await this.payoutService.update(payout.id, {
        status: 'completed'
      });
    }

    return { received: true };
  }
}
```

Looks reasonable, right? We check the status before charging the fee. What could go wrong?

### The Incident Timeline

```
10:15:00 - Merchant A requests payout of $10,000
10:15:30 - PaymentProvider processes payout, sends webhook #1
10:15:30 - Webhook #1 arrives at our server, starts processing
10:15:30 - Code checks status: 'pending' ✅
10:15:30 - Charges fee: $50
10:15:31 - PaymentProvider retries webhook (didn't get response in time)
10:15:31 - Webhook #2 arrives at our server
10:15:31 - Code checks status: still 'pending' ✅ (first request hasn't finished!)
10:15:31 - Charges ANOTHER fee: $50 ❌

Result: Merchant charged $100 instead of $50
```

### Root Cause Analysis

**Problem #1: Race Condition**
```
- Webhook #1 is processing (hasn't updated status yet)
- Webhook #2 arrives and checks status
- Both see status = 'pending'
- Both decide "haven't charged fee yet"
- Both charge the fee → DOUBLE CHARGE
```

**Problem #2: Webhook Delivery Semantics**
```
Payment providers guarantee "at-least-once delivery"
- They don't guarantee "exactly-once"
- Webhooks can be sent multiple times due to:
  → Network timeouts
  → Retry logic
  → Provider-side failures
  → Our server being slow to respond
```

This is not a bug in the payment provider - **it's by design**.

## Understanding Webhook Delivery Guarantees

### Three Types of Delivery Semantics

```
┌─────────────────┬──────────────────┬────────────────────┐
│   Type          │   Behavior       │   Real World       │
├─────────────────┼──────────────────┼────────────────────┤
│ At-most-once    │ Send once, no    │ Unreliable, rarely │
│                 │ retry if fails   │ used for webhooks  │
├─────────────────┼──────────────────┼────────────────────┤
│ At-least-once ← │ Send until gets  │ Stripe, PayPal,    │
│ (Most common)   │ success response │ Shopify, Square    │
│                 │ May duplicate    │ ← STANDARD         │
├─────────────────┼──────────────────┼────────────────────┤
│ Exactly-once    │ Guaranteed once  │ Expensive/complex  │
│                 │ (theoretical)    │ (Apache Kafka)     │
└─────────────────┴──────────────────┴────────────────────┘
```

### Why "At-Least-Once" is Standard

Imagine you're a payment provider:

**Scenario 1: At-Most-Once**
```
Provider: "I'm sending webhook for $10,000 payout"
*Network timeout*
Provider: "Oh well, not retrying"
→ Merchant never knows payout succeeded ❌
```

**Scenario 2: At-Least-Once**
```
Provider: "I'm sending webhook for $10,000 payout"
*Network timeout*
Provider: "No response, retrying in 5 seconds..."
Provider: "Sending again..."
*Server responds OK*
→ Merchant gets notified (might receive duplicates) ✅
```

**Conclusion:** At-least-once delivery is the best trade-off for reliability.

### Who's Responsible for What?

```
Payment Provider's job: "Webhook will arrive at least once"
Our job: "Logic runs EXACTLY once"

→ This is called IDEMPOTENCY
```

## What is Idempotency?

### Definition

**Idempotency:** Performing an operation multiple times produces the same result as performing it once.

```
Real-world examples:

✅ Idempotent:
   SET temperature = 25°C
   (set 10 times → still 25°C)

❌ Not idempotent:
   INCREMENT temperature +5°C
   (increment 10 times → 50°C increase!)

✅ Idempotent:
   UPDATE users SET name = 'John' WHERE id = 1

❌ Not idempotent:
   INSERT INTO payments (amount) VALUES (100)
```

### Idempotency in Webhooks

```typescript
// ❌ Not idempotent
function chargePayoutFee(payoutId: string) {
  await db.insert('fees', {
    payoutId,
    amount: 50
  });
  // Called twice → 2 records → wrong
}

// ✅ Idempotent
function chargePayoutFee(payoutId: string, idempotencyKey: string) {
  await db.insert('fees', {
    payoutId,
    amount: 50,
    idempotencyKey // ← Unique constraint
  });
  // Called twice → second fails with duplicate key → idempotent
}
```

### The Idempotency Key

An **idempotency key** is a unique identifier for each webhook event.

```
Common implementations:

Stripe:   event.id (e.g., "evt_1ABC...")
PayPal:   event_id
Shopify:  X-Shopify-Webhook-Id header
Square:   event_id

→ Use this key to detect duplicate webhooks
```

## Implementation: 3 Patterns for Idempotency

### Pattern #1: Database Unique Constraint (Recommended)

This is the simplest and most reliable approach.

**Step 1: Database Schema**

```sql
CREATE TABLE payout_fees (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  payout_id UUID NOT NULL,
  amount DECIMAL(10, 2) NOT NULL,
  idempotency_key VARCHAR(255) NOT NULL UNIQUE, -- ← The magic
  created_at TIMESTAMP DEFAULT NOW()
);

-- Ensure idempotency key is unique
CREATE UNIQUE INDEX idx_payout_fees_idempotency
  ON payout_fees(idempotency_key);

-- Also ensure one payout = one fee
CREATE UNIQUE INDEX idx_payout_fees_payout_id
  ON payout_fees(payout_id);
```

**Step 2: Service Implementation**

```typescript
@Injectable()
export class PayoutFeeService {
  constructor(
    private readonly feeRepository: FeeRepository,
    private readonly logger: Logger
  ) {}

  async chargePayoutFee(
    payoutId: string,
    amount: number,
    idempotencyKey: string
  ): Promise<PayoutFee> {
    try {
      // Attempt to insert with idempotency key
      const fee = await this.feeRepository.create({
        payoutId,
        amount,
        idempotencyKey
      });

      this.logger.log(`Fee charged successfully: ${fee.id}`);
      return fee;

    } catch (error) {
      // Check if it's a duplicate key error
      if (this.isDuplicateKeyError(error)) {
        this.logger.log(
          `Duplicate webhook detected and ignored: ${idempotencyKey}`
        );

        // Return existing fee (idempotent response)
        const existingFee = await this.feeRepository.findOne({
          idempotencyKey
        });

        return existingFee;
      }

      // Re-throw other errors
      throw error;
    }
  }

  private isDuplicateKeyError(error: any): boolean {
    // PostgreSQL unique violation code
    return error.code === '23505';
  }
}
```

**Step 3: Webhook Handler**

```typescript
@Controller('webhooks')
export class WebhookController {
  constructor(
    private readonly webhookService: WebhookService,
    private readonly payoutService: PayoutService,
    private readonly feeService: PayoutFeeService,
    private readonly logger: Logger
  ) {}

  @Post('payment-provider')
  async handlePayoutWebhook(
    @Body() event: PayoutWebhookEvent,
    @Headers('x-webhook-signature') signature: string
  ) {
    // Step 1: Verify webhook signature (security)
    await this.webhookService.verifySignature(event, signature);

    // Step 2: Use event ID as idempotency key
    const idempotencyKey = event.id; // e.g., "evt_123abc"

    // Step 3: Get payout details
    const payout = await this.payoutService.findOne(event.payoutId);

    // Step 4: Calculate fee
    const feeAmount = payout.amount * 0.005; // 0.5%

    // Step 5: Charge fee (idempotent!)
    await this.feeService.chargePayoutFee(
      payout.id,
      feeAmount,
      idempotencyKey // ← Magic happens here
    );

    return { received: true };
  }
}
```

**Why This Works:**

```
First webhook arrives:
- Insert with idempotency_key = "evt_123"
- Success → Fee charged

Second webhook arrives (duplicate):
- Try to insert with idempotency_key = "evt_123"
- Fails: Unique constraint violation
- Catch error, return existing fee
- No double charge! ✅
```

**Pros:**
```
✅ Simple to implement
✅ Database enforces uniqueness (single source of truth)
✅ Atomic operation (no race conditions)
✅ No external dependencies (Redis, etc.)
✅ Works with any SQL database
```

**Cons:**
```
❌ Relies on database constraint
❌ Less flexible for complex scenarios
```

---

### Pattern #2: Redis Distributed Lock

> **⚠️ Warning:** This pattern is more complex than Pattern #1. Only use it if you have specific requirements.

**When you might need this:**
- You're processing webhooks on multiple servers simultaneously
- Webhook processing takes >5 seconds (long operations)
- You want to wait for first request to finish instead of failing fast

**Core concept:**

```typescript
async chargePayoutFee(payoutId: string, amount: number, idempotencyKey: string) {
  const lockKey = `lock:payout-fee:${idempotencyKey}`;

  // Try to acquire lock
  const lockAcquired = await redis.set(lockKey, '1', 'EX', 30, 'NX');

  if (!lockAcquired) {
    // Another server is processing, wait for it to finish
    await this.waitForCompletion(lockKey);
    return this.feeRepository.findOne({ idempotencyKey });
  }

  try {
    // We got the lock - check if already processed
    const existing = await this.feeRepository.findOne({ idempotencyKey });
    if (existing) return existing;

    // Process fee
    return await this.feeRepository.create({ payoutId, amount, idempotencyKey });

  } finally {
    // Always release lock
    await redis.del(lockKey);
  }
}
```

**Pros:**
```
✅ Handles concurrent requests across multiple servers
✅ Prevents race conditions completely
✅ Second request waits instead of failing
```

**Cons:**
```
❌ Significantly more complex than Pattern #1
❌ Requires Redis (external dependency)
❌ What if Redis goes down? (need fallback)
❌ Lock timeout needs careful tuning
❌ Waiting logic can be tricky
```

**Reality check:** Pattern #1 (unique constraint) is enough for 95% of use cases. Only implement Redis locks if you have a proven need.

---

### Pattern #3: State Machine with Pessimistic Locking

For workflows with complex state transitions:

```typescript
// Database schema with state tracking
enum PayoutState {
  PENDING = 'pending',
  FEE_CHARGED = 'fee_charged',
  COMPLETED = 'completed'
}

// Entity
class Payout {
  id: string;
  amount: number;
  status: PayoutState;
  version: number; // For optimistic locking
}
```

```typescript
@Injectable()
export class PayoutFeeService {
  async chargePayoutFee(payoutId: string): Promise<PayoutFee> {
    // Use database transaction
    return this.entityManager.transaction(async (em) => {
      // Lock the payout row (SELECT FOR UPDATE)
      const payout = await em.findOne(Payout, payoutId, {
        lock: { mode: 'pessimistic_write' }
      });

      // Check state - only charge if pending
      if (payout.status !== PayoutState.PENDING) {
        this.logger.log('Fee already charged, skipping');
        return em.findOne(PayoutFee, { payoutId });
      }

      // Create fee
      const fee = em.create(PayoutFee, {
        payoutId: payout.id,
        amount: payout.amount * 0.005
      });
      await em.save(fee);

      // Update state atomically
      payout.status = PayoutState.FEE_CHARGED;
      await em.save(payout);

      return fee;
    });
  }
}
```

**Pros:**
```
✅ State machine is easy to reason about
✅ Transaction guarantees consistency
✅ No separate idempotency key needed
✅ Works well for complex workflows
```

**Cons:**
```
❌ Tight coupling with payout entity
❌ Pessimistic lock can slow things down
❌ Harder to scale horizontally
```

---

### Comparison Table

```
┌────────────┬─────────────┬──────────────┬─────────────┐
│ Pattern    │ Complexity  │  Performance │   Use Case  │
├────────────┼─────────────┼──────────────┼─────────────┤
│ Unique     │   Simple    │    Fast      │ ✅ Default  │
│ Constraint │   ⭐⭐       │    ⭐⭐⭐     │   choice    │
├────────────┼─────────────┼──────────────┼─────────────┤
│ Redis Lock │   Complex   │    Medium    │ High conc.  │
│            │   ⭐⭐⭐     │    ⭐⭐       │ multi-server│
├────────────┼─────────────┼──────────────┼─────────────┤
│ State      │   Medium    │    Fast      │ Complex     │
│ Machine    │   ⭐⭐⭐     │    ⭐⭐⭐     │ workflows   │
└────────────┴─────────────┴──────────────┴─────────────┘
```

**Recommendation:** Start with Pattern #1 (Unique Constraint). It's simple, reliable, and covers 90% of use cases.

## Critical: Webhook Security

Before processing ANY webhook, you MUST verify its signature:

```typescript
@Post('webhooks/payment-provider')
async handleWebhook(
  @Body() event: WebhookEvent,
  @Headers('x-webhook-signature') signature: string
) {
  // Step 1: ALWAYS verify signature first
  const isValid = this.verifyWebhookSignature(
    JSON.stringify(event),
    signature,
    process.env.WEBHOOK_SECRET
  );

  if (!isValid) {
    throw new UnauthorizedException('Invalid webhook signature');
  }

  // Step 2: Process webhook (idempotent)
  await this.processWebhook(event);
}

private verifyWebhookSignature(
  payload: string,
  signature: string,
  secret: string
): boolean {
  const hmac = crypto.createHmac('sha256', secret);
  const digest = hmac.update(payload).digest('hex');

  return crypto.timingSafeEqual(
    Buffer.from(signature),
    Buffer.from(digest)
  );
}
```

**Why this is critical:**

```
❌ Without verification:
- Attackers can send fake webhooks
- Charge fees arbitrarily
- Manipulate balances
- Steal money

✅ With verification:
- Only legitimate provider can send webhooks
- Webhooks are cryptographically verified
- System is secure
```

**Never skip signature verification in production!**

## Handling Out-of-Order Webhooks

Webhooks can arrive out of order:

```
Timeline (reality):
10:00 - Payout created (webhook #1)
10:01 - Payout processing (webhook #2)
10:02 - Payout completed (webhook #3)

Timeline (webhooks arrive):
10:00:10 - Webhook #1 arrives ✅
10:01:05 - Webhook #3 arrives ❌ (too early!)
10:01:15 - Webhook #2 arrives ❌ (delayed)
```

**Solution: Use timestamp or version number:**

```typescript
async processPayoutWebhook(event: PayoutWebhookEvent) {
  const payout = await this.payoutRepo.findOne(event.payoutId);

  // Ignore outdated webhooks
  if (event.timestamp <= payout.lastWebhookTimestamp) {
    this.logger.log('Outdated webhook, ignoring');
    return;
  }

  // Process and update timestamp
  await this.updatePayoutStatus(payout, event);
  payout.lastWebhookTimestamp = event.timestamp;
  await this.payoutRepo.save(payout);
}
```

## Idempotency Window: How Long to Store Keys?

**Question:** How long should we keep idempotency keys?

**Recommended: 24-72 hours**

```
Why 24-72 hours?
✅ Long enough for all webhook retry scenarios
✅ Most providers stop retrying after 24 hours
✅ Prevents database bloat from old keys
```

**Clean up old keys with a cron job:**

```typescript
@Cron('0 0 * * *') // Daily at midnight
async cleanupOldIdempotencyKeys() {
  const threeDaysAgo = subDays(new Date(), 3);

  await this.db.query(`
    DELETE FROM payout_fees
    WHERE created_at < $1
  `, [threeDaysAgo]);
}
```

Most payment providers (Stripe, PayPal) stop retrying webhooks after 3 days, so this window is safe.

## Testing Idempotency

### Local Testing: Simulate Webhooks with curl

Before writing automated tests, verify your implementation works locally:

```bash
# Step 1: Start your server locally
npm run dev

# Step 2: Send the same webhook 5 times concurrently
for i in {1..5}; do
  curl -X POST http://localhost:3000/webhooks/payout \
    -H "Content-Type: application/json" \
    -H "x-webhook-signature: test_signature" \
    -d '{
      "id": "evt_test_duplicate",
      "payoutId": "payout_123",
      "amount": 10000,
      "status": "completed"
    }' &
done
wait

# Step 3: Check database - should have only 1 fee
psql -d mydb -c "SELECT COUNT(*) FROM payout_fees WHERE idempotency_key = 'evt_test_duplicate';"
# Expected: 1 (not 5!)
```

**Testing with a real payment provider:**

```bash
# Use ngrok to expose local server
ngrok http 3000

# Update webhook URL in payment provider dashboard to:
https://your-ngrok-url.ngrok.io/webhooks/payout

# Trigger test webhook from provider dashboard
# Then check your logs and database
```

---

### Unit Test: Duplicate Webhooks

```typescript
describe('PayoutFeeService', () => {
  it('should charge fee only once for duplicate webhooks', async () => {
    const payoutId = 'payout_123';
    const idempotencyKey = 'evt_abc';
    const amount = 50;

    // First webhook
    const fee1 = await service.chargePayoutFee(
      payoutId,
      amount,
      idempotencyKey
    );

    // Duplicate webhook (same idempotency key)
    const fee2 = await service.chargePayoutFee(
      payoutId,
      amount,
      idempotencyKey
    );

    // Should return same fee object
    expect(fee1.id).toBe(fee2.id);

    // Should only have 1 record in database
    const count = await feeRepo.count({ payoutId });
    expect(count).toBe(1);
  });
});
```

### Integration Test: Concurrent Webhooks

```typescript
describe('PayoutWebhookController (Integration)', () => {
  it('should handle 10 concurrent duplicate webhooks', async () => {
    const event = {
      id: 'evt_duplicate_test',
      payoutId: 'payout_123',
      amount: 10000,
      status: 'completed'
    };

    // Send 10 webhooks concurrently
    const promises = Array(10).fill(null).map(() =>
      request(app.getHttpServer())
        .post('/webhooks/payout')
        .set('x-webhook-signature', generateSignature(event))
        .send(event)
        .expect(200)
    );

    await Promise.all(promises);

    // Should only create 1 fee
    const fees = await feeRepo.find({
      payoutId: 'payout_123'
    });
    expect(fees).toHaveLength(1);
    expect(fees[0].amount).toBe(50); // 0.5% of 10000
  });
});
```

### Manual Testing

```bash
# Test duplicate webhooks manually
for i in {1..5}; do
  curl -X POST http://localhost:3000/webhooks/payout \
    -H "Content-Type: application/json" \
    -H "x-webhook-signature: <signature>" \
    -d '{
      "id": "evt_test_123",
      "payoutId": "payout_xyz",
      "amount": 10000,
      "status": "completed"
    }' &
done
wait

# Check database
psql -d mydb -c "
  SELECT COUNT(*) FROM payout_fees
  WHERE payout_id = 'payout_xyz';
"
# Expected: 1
```

## Best Practices Checklist

```
Webhook Idempotency Checklist:

✅ Verify webhook signature BEFORE processing
✅ Use idempotency key (event.id) with unique constraint
✅ Handle duplicate key errors gracefully
✅ Return 200 OK even for duplicate webhooks
✅ Log duplicate webhooks for monitoring
✅ Handle out-of-order webhooks (timestamp check)
✅ Test with concurrent duplicate webhooks
✅ Clean up old idempotency keys (24-72h window)
✅ Use transactions for multi-step operations
✅ Monitor duplicate webhook rate

Security Checklist:

✅ Verify HMAC signature on every webhook
✅ Use timing-safe comparison (crypto.timingSafeEqual)
✅ Store webhook secret in environment variables
✅ Rotate webhook secrets periodically
✅ Rate limit webhook endpoints
✅ Log failed signature verifications (potential attacks)
```

## The Results

After implementing idempotency with Pattern #1:

**✅ Zero duplicate charges** since deployment (6 months and counting)

**✅ Handled 50,000+ webhooks** without issues

**✅ Processed 1,247 duplicate webhooks** correctly (2.5% duplicate rate)

**✅ No production incidents** related to webhook processing

**Monitoring metrics:**
```
- Webhook success rate: 99.97%
- Duplicate webhook rate: 2.5% (normal)
- Average processing time: 120ms
- Failed signature verifications: 3 (potential attacks, blocked)
```

## Key Takeaways

1️⃣ **Payment providers send webhooks "at-least-once"** → Prepare for duplicates

2️⃣ **Idempotency key = event.id** → Use it with unique constraint

3️⃣ **Database unique constraint is simple & effective** → Pattern #1 covers 90% of cases

4️⃣ **ALWAYS verify webhook signatures** → Security is not optional

5️⃣ **Test with concurrent requests** → Race conditions are real

6️⃣ **Clean up old keys** → 24-72 hour window is enough

7️⃣ **Log duplicate webhooks** → Monitor for abnormal patterns

8️⃣ **Return idempotent responses** → Same input = same output

**Remember:** "Webhooks being sent multiple times is normal. Your system processing them exactly once is your responsibility."

---

## Resources

- [Stripe Webhook Best Practices](https://stripe.com/docs/webhooks/best-practices)
- [Idempotency Keys - RFC Draft](https://datatracker.ietf.org/doc/html/draft-idempotency-header)
- [AWS Builders Library: Making Retries Safe with Idempotent APIs](https://aws.amazon.com/builders-library/making-retries-safe-with-idempotent-APIs/)

*Have you dealt with webhook idempotency issues? What patterns have worked for you? Share your experience in the comments!*
