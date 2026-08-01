---
updatedAt: 2026-04-30T04:32:44.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Get Invoice

**Endpoints:** /v1/invoices/\{invoice\_id}\
**HTTP Method:** GET\
**Headers:**

Production: `https://api.midtrans.com/v1/invoices/{invoice_id}`

Sandbox: `https://api.sandbox.midtrans.com/v1/invoices/{invoice_id}`

| Key           | Description                            |
| :------------ | :------------------------------------- |
| Authorization | Basic Base64Encode(merchantServerKey:) |

<br />

***

<br />

# Response

<br />

```json 200 - OK
{
    "order_id": "7950c36a-d267-4f25-bb03-7a82b00z168t",
    "invoice_number": "7128c81b-cde5-4c33-8777-4d1d0fcd6377",
    "invoice_title": "INVOICE",
    "invoice_paid_title": "INVOICE",
    "published_date": "2024-03-06 10:54:14 +0700",
    "due_date": "2025-08-06 20:03:04 +0700",
    "invoice_date": "2025-01-06 20:03:04 +0700",
    "reference": "reference",
    "customer_details": {
        "id": "customer_id",
        "name": "merchant A",
        "email": "merchant@midtrans.com",
        "phone": "82313123123"
    },
    "item_details": [
        {
            "item_id": "SKU1111",
            "description": "midtrans pillow",
            "quantity": 1,
            "price": 2000
        }
    ],
    "id": "65e7e8e657389830d04836fc",
    "status": "pending",
    "gross_amount": 13324,
    "pdf_url": "https://assets.midtrans.com/invoices/pdf/5a76417e-be8e-437a-8e16-38c916aea614",
    "payment_type": "payment_link",
    "virtual_accounts": [],
    "payment_link_url": "https://app.midtrans.com/payment-links/b1000b26-a311-42d4-9dc7-51a00ec8c681",
    "tax_mode": "exclusive",
    "taxes": [
        {
            "name": "PPN",
            "type": "percentage",
            "value": 10,
            "calculated_amount": 100
        }
    ]
}
```
```json 200 - OK Quotation
{
    "order_id": "1777432336",
    "invoice_number": "7128c81b-cde5-4c33-8777-4d1d0fcd6377",
    "invoice_title": null,
    "invoice_paid_title": null,
    "published_date": null,
    "due_date": "2026-08-07 03:03:04 +0700",
    "invoice_date": "2026-07-21 03:03:04 +0700",
    "paid_date": null,
    "reference": null,
    "customer_details": {
        "id": "customer_id",
        "name": "merchant A",
        "email": null,
        "phone": null,
        "notes": null
    },
    "item_details": [
        {
            "item_id": "SKU1111",
            "description": "Metal Gear REX",
            "quantity": 1,
            "price": 200,
            "discount_percentage": null,
            "discount_amount": null
        }
    ],
    "id": "69f1770fd083f01f1976f0e0",
    "status": "published",
    "gross_amount": 11524,
    "pdf_url": null,
    "paid_pdf_url": null,
    "payment_type": "payment_link",
    "virtual_accounts": [
        {
            "number": "12345678901",
            "bank": "bca_va"
        }
    ],
    "payment_link_url": null,
    "amount": {
        "vat": 12313,
        "discount": 1000,
        "shipping": 11,
        "vat_type": "fixed",
        "total_tax": null,
        "base_amount": null
    },
    "external_group_id": null,
    "tax_mode": "exclusive",
    "taxes": [
        {
            "name": "PPN",
            "type": "percentage",
            "value": 10,
            "calculated_amount": 100
        }
    ],
    "document_type": "quotation",
    "quotation_date": "2026-07-07 03:03:04 +0700",
    "quotation_title": "QUOTATION TITLE",
    "quotation_validity_date": "2026-08-07 03:03:04 +0700",
    "quotation_pdf_url": "https://assets.stg.midtrans.com/quotations/6dJ6EvGb",
    "quotation_terms_conditions": "QUOTATION TERMS & CONDITION",
    "converted_at": null,
    "created_as": "quotation",
    "quotation_published_date": "2026-04-29 10:12:15 +0700"
}
```
```json 404 - Not Found
{
   "error_messages": [
       "Not Found"
   ]
}

```
```json 500 - Internal Server Error
{
   "error_messages": [
       "Internal server error"
   ]
}

```

<br />

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        order_id String
      </td>

      <td>
        Id for the order
      </td>
    </tr>

    <tr>
      <td>
        id  
        String
      </td>

      <td>
        invoice id
      </td>
    </tr>

    <tr>
      <td>
        invoice_number  
        String
      </td>

      <td>
        Number of the invoice
      </td>
    </tr>

    <tr>
      <td>
        invoice_title  
        String
      </td>

      <td>
        Title of the Invoice on creation. This will be used on Invoice PDF when the Invoice is not paid yet.
      </td>
    </tr>

    <tr>
      <td>
        invoice_paid_title  
        String
      </td>

      <td>
        Title of the Invoice when status is Paid. This will be used on Invoice PDF when the Invoice is paid.
      </td>
    </tr>

    <tr>
      <td>
        published_date  
        String
      </td>

      <td>
        Date of invoice is published/created in ISO 8601 format. Default time zone: GMT+7.
      </td>
    </tr>

    <tr>
      <td>
        due_date  
        String
      </td>

      <td>
        Due date of transaction in ISO 8601 format. Default time zone: GMT+7.
      </td>
    </tr>

    <tr>
      <td>
        invoice_date  
        String
      </td>

      <td>
        Date of Invoice and will be used in email and pdf created in ISO 8601 format. Default time zone: GMT+7.
      </td>
    </tr>

    <tr>
      <td>
        customer_details  
        Object
      </td>

      <td>
        Refer to [Customer Details object](/reference/json-objects-1#customer-details) section.
      </td>
    </tr>

    <tr>
      <td>
        item_details  
        Array\<item_detail>
      </td>

      <td>
        Refer to [Item Detail object](/reference/json-objects-1#item-detail) section
      </td>
    </tr>

    <tr>
      <td>
        payment_type  
        String
      </td>

      <td>
        Either payment_link or virtual_account
      </td>
    </tr>

    <tr>
      <td>
        payment_link_url  
        String
      </td>

      <td>
        URL for payment link and only filled when payment_type is payment_link
      </td>
    </tr>

    <tr>
      <td>
        virtual_accounts  
        array \<virtual_account>
      </td>

      <td>
        Invoice virtual account and only filled when payment_type is virtual_account. Refer to [Virtual Account object](/reference/json-objects-1#virtual-account) section.
      </td>
    </tr>

    <tr>
      <td>
        pdf_url  
        String
      </td>

      <td>
        pdf_url of the invoice
      </td>
    </tr>

    <tr>
      <td>
        gross_amount  
        Integer
      </td>

      <td>
        Total amount in invoice
      </td>
    </tr>

    <tr>
      <td>
        status  
        String
      </td>

      <td>
        Status of the invoice, can be `draft`,  
        `pending`, `expired`, `overdue`, `paid`, or `voided`
      </td>
    </tr>

    <tr>
      <td>
        document_type  
        String
      </td>

      <td>
        Type of document returned by the API. Possible values are `quotation` or `invoice`(default)
      </td>
    </tr>

    <tr>
      <td>
        quotation_date  
        String
      </td>

      <td>
        Quotation issue date in ISO 8601 format with default time zone GMT+7.
      </td>
    </tr>

    <tr>
      <td>
        quotation_title  
        String
      </td>

      <td>
        Title displayed on the quotation document (PDF/view).
      </td>
    </tr>

    <tr>
      <td>
        quotation_validity_date  
        String
      </td>

      <td>
        Quotation expiration date in ISO 8601 format with default time zone GMT+7. After this date, the quotation is no longer valid.
      </td>
    </tr>

    <tr>
      <td>
        quotation_pdf_url  
        String
      </td>

      <td>
        Public URL to access/download the generated quotation PDF file.
      </td>
    </tr>

    <tr>
      <td>
        quotation_terms_conditions  
        String
      </td>

      <td>
        Terms and conditions text attached to the quotation document.
      </td>
    </tr>

    <tr>
      <td>
        converted_at  
        String
      </td>

      <td>
        Timestamp when the quotation was converted to another document type (for example, invoice). null means it has not been converted.
      </td>
    </tr>

    <tr>
      <td>
        created_as  
        String
      </td>

      <td>
        Original document mode when first created. Value quotation indicates this record was initially created as a quotation.
      </td>
    </tr>

    <tr>
      <td>
        quotation_published_date  
        String
      </td>

      <td>
        Timestamp when the quotation was published/generated and made available (for example for PDF sharing), in ISO 8601 format with default time zone GMT+7.
      </td>
    </tr>

    <tr>
      <td>
        tax_mode  
        String
      </td>

      <td>
        Tax calculation mode for the invoice.  
        Possible values are `exclusive` or `inclusive`
      </td>
    </tr>

    <tr>
      <td>
        taxes  
        Array\<tax>
      </td>

      <td>
        List of tax entries applied to the invoice. Optional, but required when tax_mode is inclusive.
      </td>
    </tr>
  </tbody>
</Table>