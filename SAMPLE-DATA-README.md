# Zuri Inc. Sample Company Data

This directory contains sample data for the myBooks application to demonstrate app functionality.

## Files

- **zuri-inc-sample-data.json** - Complete sample data set for Zuri Inc. company
- **generate-zuri-sample.js** - Documentation script (reference only)

## Sample Data Overview

**Company:** Zuri Inc  
**Period:** January - March 2025  

### Financial Summary

| Month | Sales | Expenses | Net |
|-------|-------|----------|-----|
| January | $61,100 | $44,900 | $16,200 |
| February | $59,500 | $45,500 | $14,000 |
| March | $59,200 | $45,600 | $13,600 |
| **Total** | **$179,800** | **$136,000** | **$43,800** |

### Sample Data Includes

1. **Chart of Accounts** - Complete accounting structure with all standard account types
2. **Customers** - 5 business customers (Acme Corp, TechFlow Inc, etc.)
3. **Vendors** - 4 suppliers (Supplier One Ltd, Vendor Materials Inc, etc.)
4. **Items/Services** - 9 different service and product types
5. **Sales Invoices** - 39 invoices across the three months (~60k revenue per month)
6. **Purchase Invoices** - 20 invoices across the three months (~45k expenses per month)

## How to Import This Data

### Option 1: Manual Import via App UI (Recommended for Demo)

1. Open the myBooks application
2. Create a new company named "Zuri Inc"
3. Go through the onboarding wizard and set the country to US
4. After completing the wizard, manually add:
   - Account chart (see below)
   - Customers and vendors (see data file)
   - Items/services (see data file)
   - Sample invoices (dates from zuri-inc-sample-data.json)

### Option 2: Programmatic Import (For Development)

The JSON file can be programmatically imported via a backend script that uses the Fyo framework. Here's a conceptual example:

```typescript
// This would be a Node.js/backend script
import { Fyo } from 'fyo';
import sampleData from '../fixtures/zuri-inc-sample-data.json';

async function importSampleData() {
  const fyo = new Fyo();
  
  // Import accounts
  for (const acc of sampleData.accounts) {
    await fyo.db.insert('Account', acc);
  }
  
  // Import parties (customers/vendors)
  for (const customer of sampleData.customers) {
    await fyo.db.insert('Party', {
      ...customer,
      partyType: 'Customer'
    });
  }
  
  // Import items
  for (const item of sampleData.items) {
    await fyo.db.insert('Item', item);
  }
  
  // Import sales invoices
  for (const invoice of sampleData.salesInvoices) {
    await fyo.db.insert('SalesInvoice', {
      name: `INV-${String(invoice.number).padStart(5, '0')}`,
      party: invoice.customer,
      date: invoice.date,
      grandTotal: invoice.total,
      status: 'Submitted'
    });
  }
  
  // Import purchase invoices
  for (const invoice of sampleData.purchaseInvoices) {
    await fyo.db.insert('PurchaseInvoice', {
      name: `PI-${String(invoice.number).padStart(5, '0')}`,
      party: invoice.vendor,
      date: invoice.date,
      grandTotal: invoice.total,
      status: 'Submitted'
    });
  }
}
```

## Use Cases

This sample company is perfect for:

- **Product Demos** - Show stakeholders a realistic business scenario
- **Training** - Teach users how to navigate reports and transactions
- **Testing** - Verify features work with realistic data volumes
- **Screenshots** - Capture meaningful reports and views

## Data Characteristics

- **Realistic Transactions** - Mix of service sales and equipment purchases
- **Multi-customer Base** - Diverse customer portfolio
- **Seasonal Variation** - Slight revenue variations across months
- **Healthy Margins** - ~24% net profit margin demonstrates viable business
- **Complete Accounting** - Full chart of accounts needed for real reporting

## Customization

To adjust the sample data:

1. Edit `zuri-inc-sample-data.json` directly
2. Modify transaction counts, dates, or amounts as needed
3. Add additional customers, vendors, or account types
4. Re-import into the application

## Technical Notes

- All dates are in UTC (YYYY-MM-DD format)
- Amounts are in USD currency
- Invoice numbers are formatted as INV-##### and PI-##### for uniqueness
- Customer and vendor names are generic and reusable

## Contact

For questions about sample data integration, see the main README or contributing guidelines.
