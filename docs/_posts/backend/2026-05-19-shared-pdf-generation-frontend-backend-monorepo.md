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

**Component 1: Invoice Header**

```tsx
// packages/pdf-templates/src/components/InvoiceHeader.tsx
import { View, Text, Image, StyleSheet } from '@react-pdf/renderer';

interface InvoiceHeaderProps {
  merchantName: string;
  merchantLogo?: string;
  invoiceNumber: string;
  invoiceDate: Date;
}

export const InvoiceHeader: React.FC<InvoiceHeaderProps> = ({
  merchantName,
  merchantLogo,
  invoiceNumber,
  invoiceDate
}) => {
  return (
    <View style={styles.header}>
      {/* Logo */}
      {merchantLogo && (
        <Image
          src={merchantLogo}
          style={styles.logo}
        />
      )}

      {/* Merchant name */}
      <Text style={styles.merchantName}>
        {merchantName}
      </Text>

      {/* Invoice info */}
      <View style={styles.invoiceInfo}>
        <Text style={styles.label}>INVOICE</Text>
        <Text style={styles.invoiceNumber}>#{invoiceNumber}</Text>
        <Text style={styles.date}>
          {invoiceDate.toLocaleDateString('en-US', {
            year: 'numeric',
            month: 'long',
            day: 'numeric'
          })}
        </Text>
      </View>
    </View>
  );
};

const styles = StyleSheet.create({
  header: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    marginBottom: 20,
    paddingBottom: 10,
    borderBottomWidth: 2,
    borderBottomColor: '#333'
  },
  logo: {
    width: 80,
    height: 80,
    objectFit: 'contain'
  },
  merchantName: {
    fontSize: 24,
    fontWeight: 'bold',
    flex: 1,
    marginLeft: 20
  },
  invoiceInfo: {
    alignItems: 'flex-end'
  },
  label: {
    fontSize: 10,
    color: '#666',
    marginBottom: 4
  },
  invoiceNumber: {
    fontSize: 18,
    fontWeight: 'bold'
  },
  date: {
    fontSize: 10,
    color: '#666',
    marginTop: 4
  }
});
```

**Component 2: Line Items Table**

```tsx
// packages/pdf-templates/src/components/LineItemsTable.tsx
import { View, Text, StyleSheet } from '@react-pdf/renderer';

interface LineItem {
  description: string;
  quantity: number;
  unitPrice: number;
  total: number;
}

interface LineItemsTableProps {
  items: LineItem[];
}

export const LineItemsTable: React.FC<LineItemsTableProps> = ({ items }) => {
  return (
    <View style={styles.table}>
      {/* Table Header */}
      <View style={styles.tableHeader}>
        <Text style={[styles.cell, styles.descriptionCell]}>Description</Text>
        <Text style={[styles.cell, styles.quantityCell]}>Qty</Text>
        <Text style={[styles.cell, styles.priceCell]}>Unit Price</Text>
        <Text style={[styles.cell, styles.totalCell]}>Total</Text>
      </View>

      {/* Table Rows */}
      {items.map((item, index) => (
        <View key={index} style={styles.tableRow}>
          <Text style={[styles.cell, styles.descriptionCell]}>
            {item.description}
          </Text>
          <Text style={[styles.cell, styles.quantityCell]}>
            {item.quantity}
          </Text>
          <Text style={[styles.cell, styles.priceCell]}>
            ${item.unitPrice.toFixed(2)}
          </Text>
          <Text style={[styles.cell, styles.totalCell]}>
            ${item.total.toFixed(2)}
          </Text>
        </View>
      ))}
    </View>
  );
};

const styles = StyleSheet.create({
  table: {
    marginTop: 20,
    marginBottom: 20
  },
  tableHeader: {
    flexDirection: 'row',
    backgroundColor: '#f0f0f0',
    padding: 8,
    fontWeight: 'bold',
    borderTopLeftRadius: 4,
    borderTopRightRadius: 4
  },
  tableRow: {
    flexDirection: 'row',
    borderBottomWidth: 1,
    borderBottomColor: '#e0e0e0',
    padding: 8
  },
  cell: {
    fontSize: 10
  },
  descriptionCell: {
    flex: 3
  },
  quantityCell: {
    flex: 1,
    textAlign: 'center'
  },
  priceCell: {
    flex: 1.5,
    textAlign: 'right'
  },
  totalCell: {
    flex: 1.5,
    textAlign: 'right',
    fontWeight: 'bold'
  }
});
```

### Step 4: Main Invoice Template

```tsx
// packages/pdf-templates/src/invoice/InvoiceTemplate.tsx
import {
  Document,
  Page,
  View,
  Text,
  StyleSheet
} from '@react-pdf/renderer';
import { InvoiceHeader } from '../components/InvoiceHeader';
import { LineItemsTable } from '../components/LineItemsTable';
import { InvoicePDFProps } from '../types';

export const InvoiceTemplate: React.FC<InvoicePDFProps> = (props) => {
  return (
    <Document>
      <Page size="A4" style={styles.page}>
        {/* Header with logo & invoice info */}
        <InvoiceHeader
          merchantName={props.merchant.name}
          merchantLogo={props.merchant.logo}
          invoiceNumber={props.invoiceNumber}
          invoiceDate={props.invoiceDate}
        />

        {/* Merchant & Customer Info */}
        <View style={styles.parties}>
          {/* From (Merchant) */}
          <View style={styles.party}>
            <Text style={styles.partyLabel}>From:</Text>
            <Text style={styles.partyName}>{props.merchant.name}</Text>
            <Text style={styles.partyDetails}>{props.merchant.address}</Text>
            {props.merchant.phone && (
              <Text style={styles.partyDetails}>
                Phone: {props.merchant.phone}
              </Text>
            )}
          </View>

          {/* Bill To (Customer) */}
          <View style={styles.party}>
            <Text style={styles.partyLabel}>Bill To:</Text>
            <Text style={styles.partyName}>{props.billTo.name}</Text>
            <Text style={styles.partyDetails}>{props.billTo.address}</Text>
            {props.billTo.email && (
              <Text style={styles.partyDetails}>
                Email: {props.billTo.email}
              </Text>
            )}
          </View>
        </View>

        {/* Due Date */}
        <View style={styles.dueDateSection}>
          <Text style={styles.dueDateLabel}>Due Date:</Text>
          <Text style={styles.dueDate}>
            {props.dueDate.toLocaleDateString('en-US', {
              year: 'numeric',
              month: 'long',
              day: 'numeric'
            })}
          </Text>
        </View>

        {/* Line Items Table */}
        <LineItemsTable items={props.lineItems} />

        {/* Totals */}
        <View style={styles.totals}>
          <View style={styles.totalRow}>
            <Text>Subtotal:</Text>
            <Text>${props.subtotal.toFixed(2)}</Text>
          </View>
          <View style={styles.totalRow}>
            <Text>Tax:</Text>
            <Text>${props.tax.toFixed(2)}</Text>
          </View>
          <View style={[styles.totalRow, styles.grandTotal]}>
            <Text>Total:</Text>
            <Text>${props.total.toFixed(2)}</Text>
          </View>
        </View>

        {/* Payment Terms */}
        {props.paymentTerms && (
          <View style={styles.footer}>
            <Text style={styles.footerLabel}>Payment Terms:</Text>
            <Text style={styles.footerText}>{props.paymentTerms}</Text>
          </View>
        )}

        {/* Notes */}
        {props.notes && (
          <View style={styles.footer}>
            <Text style={styles.footerLabel}>Notes:</Text>
            <Text style={styles.footerText}>{props.notes}</Text>
          </View>
        )}

        {/* Footer */}
        <View style={styles.pageFooter}>
          <Text style={styles.footerSmall}>
            Thank you for your business!
          </Text>
        </View>
      </Page>
    </Document>
  );
};

const styles = StyleSheet.create({
  page: {
    padding: 40,
    fontSize: 12,
    fontFamily: 'Helvetica'
  },
  parties: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    marginTop: 20,
    marginBottom: 20
  },
  party: {
    flex: 1
  },
  partyLabel: {
    fontSize: 10,
    color: '#666',
    marginBottom: 4,
    textTransform: 'uppercase'
  },
  partyName: {
    fontSize: 14,
    fontWeight: 'bold',
    marginBottom: 4
  },
  partyDetails: {
    fontSize: 10,
    color: '#333',
    marginBottom: 2
  },
  dueDateSection: {
    marginBottom: 20,
    padding: 10,
    backgroundColor: '#fff3cd',
    borderRadius: 4
  },
  dueDateLabel: {
    fontSize: 10,
    color: '#856404',
    fontWeight: 'bold'
  },
  dueDate: {
    fontSize: 12,
    color: '#856404',
    marginTop: 2
  },
  totals: {
    marginLeft: 'auto',
    width: 200,
    marginTop: 20
  },
  totalRow: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    paddingVertical: 4,
    borderBottomWidth: 1,
    borderBottomColor: '#e0e0e0'
  },
  grandTotal: {
    marginTop: 8,
    paddingTop: 8,
    borderTopWidth: 2,
    borderTopColor: '#333',
    borderBottomWidth: 0,
    fontSize: 14,
    fontWeight: 'bold'
  },
  footer: {
    marginTop: 20,
    padding: 10,
    backgroundColor: '#f9f9f9',
    borderRadius: 4
  },
  footerLabel: {
    fontSize: 10,
    fontWeight: 'bold',
    marginBottom: 4
  },
  footerText: {
    fontSize: 10,
    color: '#333'
  },
  pageFooter: {
    position: 'absolute',
    bottom: 30,
    left: 40,
    right: 40,
    textAlign: 'center',
    borderTopWidth: 1,
    borderTopColor: '#e0e0e0',
    paddingTop: 10
  },
  footerSmall: {
    fontSize: 9,
    color: '#999'
  }
});
```

### Step 5: Data Transformation Layer

This is crucial! We need a single place to transform database entities into PDF props.

```typescript
// packages/pdf-templates/src/utils/data-transformer.ts
import type { InvoicePDFProps } from '../types';

// Import Order type from your main app
// This would be defined in a shared types package
interface Order {
  id: string;
  invoiceNumber: string;
  createdAt: string;
  dueDate: string;
  customer: {
    fullName: string;
    businessName?: string;
    billingAddress: Address;
    email: string;
  };
  merchant: {
    name: string;
    logoUrl?: string;
    address: Address;
    phone?: string;
  };
  items: Array<{
    product: { name: string };
    quantity: number;
    unitPrice: number;
  }>;
  subtotal: number;
  tax: number;
  total: number;
  paymentTerms?: string;
  notes?: string;
}

interface Address {
  street: string;
  city: string;
  state: string;
  zipCode: string;
  country: string;
}

/**
 * Single source of truth for transforming Order to PDF props
 * Used by both frontend and backend
 */
export function toPDFProps(order: Order): InvoicePDFProps {
  return {
    invoiceNumber: order.invoiceNumber,
    invoiceDate: new Date(order.createdAt),
    dueDate: new Date(order.dueDate),

    merchant: {
      name: order.merchant.name,
      logo: order.merchant.logoUrl
        ? `https://cdn.myshop.com/${order.merchant.logoUrl}`
        : undefined,
      address: formatAddress(order.merchant.address),
      phone: order.merchant.phone
    },

    // ✅ Single source of truth for bill-to
    // Always use fullName, never businessName
    billTo: {
      name: order.customer.fullName,
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
    total: order.total,

    paymentTerms: order.paymentTerms,
    notes: order.notes
  };
}

function formatAddress(address: Address): string {
  return [
    address.street,
    address.city,
    `${address.state} ${address.zipCode}`,
    address.country
  ].filter(Boolean).join(', ');
}
```

**Why this is important:**
- ✅ Single transformation logic
- ✅ Used by both frontend & backend
- ✅ Easy to update (one place)
- ✅ Type-safe with TypeScript
- ✅ No more mapping bugs!

### Step 6: Export the Package

```typescript
// packages/pdf-templates/src/index.ts
export { InvoiceTemplate } from './invoice/InvoiceTemplate';
export { InvoiceHeader } from './components/InvoiceHeader';
export { LineItemsTable } from './components/LineItemsTable';

export type { InvoicePDFProps } from './types';

export { toPDFProps } from './utils/data-transformer';
```

## Using the Package in Frontend (Next.js)

### Install Dependencies

```json
// apps/web/package.json
{
  "dependencies": {
    "@my-shop/pdf-templates": "workspace:*",
    "@react-pdf/renderer": "^3.1.0",
    "react": "^18.0.0",
    "next": "^15.0.0"
  }
}
```

### Download Button Component

```tsx
// apps/web/app/orders/[id]/components/DownloadInvoiceButton.tsx
'use client';

import { useState } from 'react';
import { pdf } from '@react-pdf/renderer';
import { InvoiceTemplate, toPDFProps } from '@my-shop/pdf-templates';
import type { Order } from '@/types';

interface DownloadInvoiceButtonProps {
  order: Order;
}

export function DownloadInvoiceButton({ order }: DownloadInvoiceButtonProps) {
  const [generating, setGenerating] = useState(false);

  const handleDownload = async () => {
    setGenerating(true);

    try {
      // Convert order data to PDF props
      const pdfProps = toPDFProps(order);

      // Generate PDF blob (browser-side)
      const blob = await pdf(
        <InvoiceTemplate {...pdfProps} />
      ).toBlob();

      // Trigger download
      const url = URL.createObjectURL(blob);
      const link = document.createElement('a');
      link.href = url;
      link.download = `invoice-${order.invoiceNumber}.pdf`;
      link.click();

      // Clean up
      URL.revokeObjectURL(url);

    } catch (error) {
      console.error('PDF generation failed:', error);
      alert('Failed to generate PDF. Please try again.');
    } finally {
      setGenerating(false);
    }
  };

  return (
    <button
      onClick={handleDownload}
      disabled={generating}
      className="px-4 py-2 bg-blue-600 text-white rounded hover:bg-blue-700 disabled:opacity-50"
    >
      {generating ? 'Generating PDF...' : 'Download Invoice'}
    </button>
  );
}
```

### Usage in Order Page

```tsx
// apps/web/app/orders/[id]/page.tsx
import { DownloadInvoiceButton } from './components/DownloadInvoiceButton';

export default async function OrderPage({
  params
}: {
  params: { id: string }
}) {
  const order = await getOrder(params.id);

  return (
    <div className="container mx-auto p-6">
      <div className="flex justify-between items-center mb-6">
        <h1 className="text-3xl font-bold">
          Order #{order.invoiceNumber}
        </h1>

        <DownloadInvoiceButton order={order} />
      </div>

      {/* Order details */}
      <div className="bg-white rounded-lg shadow p-6">
        {/* ... order content ... */}
      </div>
    </div>
  );
}
```

## Using the Package in Backend (NestJS)

### Install Dependencies

```json
// apps/api/package.json
{
  "dependencies": {
    "@my-shop/pdf-templates": "workspace:*",
    "@react-pdf/renderer": "^3.1.0",
    "react": "^18.0.0",
    "@nestjs/core": "^10.0.0"
  }
}
```

### PDF Service

```typescript
// apps/api/src/pdf/pdf.service.ts
import { Injectable } from '@nestjs/common';
import { renderToStream } from '@react-pdf/renderer';
import { InvoiceTemplate, toPDFProps } from '@my-shop/pdf-templates';
import { Order } from '../orders/entities/order.entity';
import { Readable } from 'stream';

@Injectable()
export class PdfService {
  /**
   * Generate PDF as Buffer (for email attachments)
   */
  async generateInvoicePDF(order: Order): Promise<Buffer> {
    // Convert order to PDF props using shared transformer
    const pdfProps = toPDFProps(order);

    // Render to stream
    const stream = await renderToStream(
      <InvoiceTemplate {...pdfProps} />
    );

    // Convert stream to buffer
    return this.streamToBuffer(stream);
  }

  /**
   * Generate PDF as Stream (for API response)
   */
  async generateInvoicePDFStream(order: Order): Promise<Readable> {
    const pdfProps = toPDFProps(order);

    return renderToStream(
      <InvoiceTemplate {...pdfProps} />
    );
  }

  private async streamToBuffer(stream: Readable): Promise<Buffer> {
    const chunks: Buffer[] = [];

    return new Promise((resolve, reject) => {
      stream.on('data', (chunk) => chunks.push(Buffer.from(chunk)));
      stream.on('error', reject);
      stream.on('end', () => resolve(Buffer.concat(chunks)));
    });
  }
}
```

### API Endpoint for PDF Download

```typescript
// apps/api/src/orders/orders.controller.ts
import {
  Controller,
  Get,
  Param,
  Res,
  StreamableFile,
  NotFoundException
} from '@nestjs/common';
import { Response } from 'express';
import { OrdersService } from './orders.service';
import { PdfService } from '../pdf/pdf.service';

@Controller('orders')
export class OrdersController {
  constructor(
    private readonly ordersService: OrdersService,
    private readonly pdfService: PdfService
  ) {}

  @Get(':id/pdf')
  async downloadInvoicePDF(
    @Param('id') id: string,
    @Res({ passthrough: true }) res: Response
  ): Promise<StreamableFile> {
    // Get order
    const order = await this.ordersService.findOne(id);
    if (!order) {
      throw new NotFoundException(`Order ${id} not found`);
    }

    // Generate PDF stream
    const stream = await this.pdfService.generateInvoicePDFStream(order);

    // Set headers
    res.set({
      'Content-Type': 'application/pdf',
      'Content-Disposition': `attachment; filename="invoice-${order.invoiceNumber}.pdf"`
    });

    // Stream to client
    return new StreamableFile(stream);
  }
}
```

### Email Service with PDF Attachment

```typescript
// apps/api/src/email/email.service.ts
import { Injectable } from '@nestjs/common';
import { MailerService } from '@nestjs-modules/mailer';
import { PdfService } from '../pdf/pdf.service';
import { Order } from '../orders/entities/order.entity';

@Injectable()
export class EmailService {
  constructor(
    private readonly mailer: MailerService,
    private readonly pdfService: PdfService
  ) {}

  async sendOrderConfirmation(order: Order): Promise<void> {
    // Generate PDF as buffer
    const pdfBuffer = await this.pdfService.generateInvoicePDF(order);

    // Send email with attachment
    await this.mailer.sendMail({
      to: order.customer.email,
      subject: `Order Confirmation #${order.invoiceNumber}`,
      template: 'order-confirmation',
      context: {
        customerName: order.customer.fullName,
        orderNumber: order.invoiceNumber,
        total: order.total.toFixed(2)
      },
      attachments: [
        {
          filename: `invoice-${order.invoiceNumber}.pdf`,
          content: pdfBuffer,
          contentType: 'application/pdf'
        }
      ]
    });
  }
}
```

## Handling Edge Cases

### Edge Case #1: Image Loading Differences

```typescript
// ❌ Problem: Relative paths don't work
<Image src="/assets/logo.png" />

// ✅ Solution 1: Use absolute URLs
<Image src="https://cdn.myshop.com/logo.png" />

// ✅ Solution 2: Convert to base64 (for offline use)
import { convertToBase64 } from './utils';

const logoBase64 = await convertToBase64(logoUrl);
<Image src={logoBase64} />

// Utility function
async function convertToBase64(url: string): Promise<string> {
  const response = await fetch(url);
  const buffer = await response.arrayBuffer();
  const base64 = Buffer.from(buffer).toString('base64');
  const mimeType = response.headers.get('content-type') || 'image/png';
  return `data:${mimeType};base64,${base64}`;
}
```

### Edge Case #2: Bundle Size Optimization (Frontend)

```typescript
// apps/web/app/orders/[id]/page.tsx

// ❌ Don't import directly (large bundle ~200KB)
import { pdf } from '@react-pdf/renderer';

// ✅ Lazy load PDF generation
const generatePDF = async (order: Order) => {
  const { pdf } = await import('@react-pdf/renderer');
  const { InvoiceTemplate, toPDFProps } = await import('@my-shop/pdf-templates');

  const props = toPDFProps(order);
  return pdf(<InvoiceTemplate {...props} />).toBlob();
};
```

### Edge Case #3: Custom Fonts

```typescript
// packages/pdf-templates/src/fonts.ts
import { Font } from '@react-pdf/renderer';

// Register custom fonts (do this once at package initialization)
Font.register({
  family: 'Roboto',
  fonts: [
    {
      src: 'https://fonts.gstatic.com/s/roboto/v30/KFOmCnqEu92Fr1Mu4mxP.ttf'
    },
    {
      src: 'https://fonts.gstatic.com/s/roboto/v30/KFOlCnqEu92Fr1MmWUlfBBc9.ttf',
      fontWeight: 'bold'
    }
  ]
});

// Usage in styles
const styles = StyleSheet.create({
  text: {
    fontFamily: 'Roboto'
  }
});
```

### Edge Case #4: Error Handling

```typescript
// Wrapper with graceful fallback
async function generateInvoicePDF(order: Order): Promise<Buffer> {
  try {
    const pdfProps = toPDFProps(order);

    // Validate props before rendering
    validatePDFProps(pdfProps);

    const stream = await renderToStream(
      <InvoiceTemplate {...pdfProps} />
    );

    return await streamToBuffer(stream);

  } catch (error) {
    this.logger.error('PDF generation failed', {
      orderId: order.id,
      error: error.message
    });

    // Fallback: Generate simple text-only PDF
    return generateFallbackPDF(order);
  }
}

function validatePDFProps(props: InvoicePDFProps): void {
  if (!props.invoiceNumber) {
    throw new Error('Invoice number is required');
  }
  if (props.lineItems.length === 0) {
    throw new Error('At least one line item is required');
  }
  // ... more validations
}
```

## Testing Strategy

### Unit Tests

```typescript
// packages/pdf-templates/tests/invoice-template.test.tsx
import { pdf } from '@react-pdf/renderer';
import { InvoiceTemplate } from '../src';

describe('InvoiceTemplate', () => {
  const mockProps = {
    invoiceNumber: 'INV-001',
    invoiceDate: new Date('2026-05-01'),
    dueDate: new Date('2026-05-31'),
    merchant: {
      name: 'Test Shop',
      address: '123 Main St, City, State 12345'
    },
    billTo: {
      name: 'John Doe',
      address: '456 Oak Ave, Town, State 67890'
    },
    lineItems: [
      {
        description: 'Product A',
        quantity: 2,
        unitPrice: 50,
        total: 100
      }
    ],
    subtotal: 100,
    tax: 10,
    total: 110
  };

  it('should generate PDF without errors', async () => {
    await expect(
      pdf(<InvoiceTemplate {...mockProps} />).toBuffer()
    ).resolves.toBeInstanceOf(Buffer);
  });

  it('should generate PDF with correct size', async () => {
    const buffer = await pdf(<InvoiceTemplate {...mockProps} />).toBuffer();

    // PDF should be between 10KB and 500KB
    expect(buffer.length).toBeGreaterThan(10000);
    expect(buffer.length).toBeLessThan(500000);
  });
});
```

### Integration Tests (Cross-Platform)

```typescript
// apps/api/test/pdf-consistency.e2e-spec.ts
import { Test } from '@nestjs/testing';
import { PdfService } from '../src/pdf/pdf.service';
import * as crypto from 'crypto';

describe('PDF Consistency (E2E)', () => {
  let pdfService: PdfService;

  beforeAll(async () => {
    const moduleRef = await Test.createTestingModule({
      providers: [PdfService]
    }).compile();

    pdfService = moduleRef.get<PdfService>(PdfService);
  });

  it('should generate identical PDFs for same input', async () => {
    const order = await getTestOrder();

    // Generate PDF twice
    const pdf1 = await pdfService.generateInvoicePDF(order);
    const pdf2 = await pdfService.generateInvoicePDF(order);

    // Compare checksums (should be identical)
    const hash1 = crypto.createHash('md5').update(pdf1).digest('hex');
    const hash2 = crypto.createHash('md5').update(pdf2).digest('hex');

    expect(hash1).toBe(hash2);
  });
});
```

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
