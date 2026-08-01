---
updatedAt: 2026-05-20T09:31:51.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Create Invoice

**Endpoints:** /v1/invoices\
**HTTP Method:** POST\
**Headers:**

Production: `https://api.midtrans.com/v1/invoices`

Sandbox: `https://api.sandbox.midtrans.com/v1/invoices`

| Key           | Description                            |
| :------------ | :------------------------------------- |
| Authorization | Basic Base64Encode(merchantServerKey:) |

<br />

### Idempotency Key

<Callout icon="🚧" theme="warn">
  To prevent duplicate invoice creation during retries, send an **X-Idempotency-Key** header in your request.

  Requests sent with the same idempotency key within **5 minutes** will be treated as the same create operation, so the invoice will only be created once.

  Use a unique and hard-to-guess value such as a UUID for each new invoice creation request.
</Callout>

<br />

## Request Body

```json Payment Link
{
    "order_id": "7950c36a-d267-4f25-bb03-7a82b00z168t",
    "invoice_number": "7128c81b-cde5-4c33-8777-4d1d0fcd6377",
    "due_date": "2025-08-06 20:03:04 +0700",
    "invoice_date": "2025-01-06 20:03:04 +0700",
    "invoice_title": "INVOICE",
    "invoice_paid_title": "INVOICE",
    "customer_details": {
        "id": "customer_id",
        "name": "merchant A",
        "email": "merchant@midtrans.com",
        "phone": "82313123123"
    },
    "payment_type": "payment_link",
    "reference": "reference",
    "item_details": [
        {
            "item_id": "SKU1111",
            "description": "midtrans pillow",
            "quantity": 1,
            "price": 2000
        }
    ],
    "notes": "just a notes",
    "payment_link": {
        "is_custom_expiry": true,
        "enabled_payments": [
            "bca_va"
        ],
        "credit_card": {
            "secure": true,
            "type": "authorize",
            "bank": "bni",
            "whitelist_bins": [
                "48111111"
            ],
            "installment": {
                "required": true,
                "terms": {
                    "mandiri": [
                        3
                    ],
                    "bca": [
                        3
                    ],
                    "bni": [
                        3
                    ],
                    "bri": [
                        3
                    ],
                    "cimb": [
                        3
                    ],
                    "maybank": [
                        3
                    ],
                    "offline": [
                        3
                    ]
                }
            }
        },
        "bca_va": {
            "number": "12345678901",
            "free_text": {
                "inquiry": [
                    {
                        "id": "id inquiry",
                        "en": "en inquiry"
                    }
                ],
                "payment": [
                    {
                        "id": "id payment",
                        "en": "en payment"
                    }
                ]
            }
        },
        "bni_va": {
            "number": "12312312312"
        },
        "permata_va": {
            "number": "12312312312",
            "recipient_name": "name"
        },
        "bri_va": {
            "number": "12312312312"
        },
        "cimb_va": {
            "number": "12312312312"
        },
        "expiry": {
            "unit": "months",
            "duration": 1,
            "start_time": "2025-02-21 09:48:29 +0700"
        },
        "callbacks": {
            "finish": "https://google.com"
        }
    },
    "amount": {
        "discount": "1000",
        "shipping": "11"
    },
    "tax_mode": "exclusive",
    "taxes": [
        {
            "name": "PPN",
            "type": "percentage",
            "value": 0.2
        }
    ]
}
```
```json Virtual Account
{
    "order_id": "7950c36a-d267-4f25-bb03-7a82b00z168t",
    "invoice_number": "7128c81b-cde5-4c33-8777-4d1d0fcd6377",
    "due_date": "2025-08-06 20:03:04 +0700",
    "invoice_date": "2025-01-06 20:03:04 +0700",
    "invoice_title": "INVOICE",
    "invoice_paid_title": "INVOICE",
    "customer_details": {
        "id": "customer_id",
        "name": "merchant A",
        "email": "merchant@midtrans.com",
        "phone": "82313123123"
    },
    "payment_type": "virtual_account",
    "reference": "reference",
    "item_details": [
        {
            "item_id": "SKU1111",
            "description": "midtrans pillow",
            "quantity": 1,
            "price": 2000
        }
    ],
    "notes": "just a notes",
    "virtual_accounts": [
        {
            "bank": "bca_va"
        }
    ],
    "amount": {
        "vat": "12313",
        "discount": "1000",
        "shipping": "11"
    }
}
```
```json Quotation
{
  "document_type": "quotation",
  "quotation_date": "2026-07-06T20:03:04Z",
  "quotation_validity_date": "2026-08-06T20:03:04Z",
  "order_id": "7128c81b-cde5-4c33-8777-4d1d0fcd6377",
  "invoice_number": "7128c81b-cde5-4c33-8777-4d1d0fcd6377",
  "due_date": "2026-08-06T20:03:04Z",
  "invoice_date": "2026-07-20T20:03:04Z",
  "customer_details": {
    "id": "customer_id",
    "name": "merchant A",
    "email": "test@test.com",
    "phone": "6281398220123"
  },
  "item_details": [
    {
      "item_id": "SKU1111",
      "description": "Metal Gear REX",
      "quantity": "1",
      "price": "200"
    }
  ],
  "currency": "IDR",
  "notes": "just a notes",
  "payment_type": "payment_link",
  "payment_link": {
    "is_custom_expiry": true,
    "enabled_payments": [
      "bca_va"
    ],
    "credit_card": {
      "bank": "bni",
      "type": "authorize",
      "secure": false,
      "installment": {
        "required": true,
        "terms": {
          "mandiri": [
            3
          ],
          "bca": [
            3
          ],
          "bni": [
            3
          ],
          "bri": [
            3
          ],
          "cimb": [
            3
          ],
          "maybank": [
            3
          ],
          "offline": [
            3
          ]
        }
      }
    },
    "expiry": {
      "unit": "months",
      "duration": 5
    },
    "callbacks": {
      "finish": "https://google.com"
    }
  },
  "virtual_accounts": [
    {
      "number": "12345678901",
      "bank": "bca_va"
    }
  ],
  "amount": {
    "discount": "1000",
    "shipping": "11"
  },
  "tax_mode": "exclusive",
  "taxes": [
    {
      "name": "PPN",
      "type": "percentage",
      "value": 0.2
    }
  ]
}
```

<br />

## Request JSON Body Details

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Parameter
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        order_id String (36) **Required**
      </td>

      <td>
        Id for the order, must be unique for each invoice  
        NOTE: only consist of alphanumeric characters [a-z, 0-9 ], hyphens [- ], underscores [_ ], tilde [~ ] and dot [. ]
      </td>
    </tr>

    <tr>
      <td>
        invoice_number  
        String (40)  
        **Required**
      </td>

      <td>
        Number of the invoice
      </td>
    </tr>

    <tr>
      <td>
        due_date  
        String (40)  
        **Required**
      </td>

      <td>
        Due date of transaction in ISO 8601 format. Default time zone: GMT+7 and has to be after invoice_date. For example: `2025-08-06 20: 03: 04 +0700`
      </td>
    </tr>

    <tr>
      <td>
        invoice_date  
        String (40)  
        **Required**
      </td>

      <td>
        Date of Invoice and will be used in email and PDF created in ISO 8601 format. Default time zone: GMT+7. For example: `2025-08-06 20: 03: 04 +0700`
      </td>
    </tr>

    <tr>
      <td>
        invoice_title  
        String (20)
      </td>

      <td>
        Title of the Invoice on creation. This will be used on Invoice PDF when the Invoice is not paid yet.
      </td>
    </tr>

    <tr>
      <td>
        invoice_paid_title  
        String (20)
      </td>

      <td>
        Title of the Invoice when status is Paid. This will be used on Invoice PDF when the Invoice is paid.
      </td>
    </tr>

    <tr>
      <td>
        customer_details  
        **Required**
      </td>

      <td>
        Refer to [Customer Details object ](/reference/json-objects-1#customer-details) section.
      </td>
    </tr>

    <tr>
      <td>
        reference  
        String(90): Optional
      </td>

      <td>
        Reference of the invoice
      </td>
    </tr>

    <tr>
      <td>
        item_details  
        Array:  
        **Required** (Min 1)
      </td>

      <td>
        Refer to [Item Detail object ](/reference/json-objects-1#item-detail) section  
        (NOTE: total price must not be 0)
      </td>
    </tr>

    <tr>
      <td>
        Notes  
        String(1000): Optional
      </td>

      <td>
        Notes of the invoice
      </td>
    </tr>

    <tr>
      <td>
        payment_type  
        String:  
        **Required**
      </td>

      <td>
        Either payment_link or virtual_account
      </td>
    </tr>

    <tr>
      <td>
        payment_link  
        Optional
      </td>

      <td>
        Refer to [Payment Link object ](/reference/json-objects-1#payment-link) section, nullable when payment_type is payment_link
      </td>
    </tr>

    <tr>
      <td>
        virtual_accounts  
        array\<virtual_account> Optional (Min 1)
      </td>

      <td>
        Refer to [Virtual Account object ](/reference/json-objects-1#virtual-account) section, required and must not empty when payment_type is virtual_account
      </td>
    </tr>

    <tr>
      <td>
        amount  
        Optional
      </td>

      <td>
        Refer to [Amount object ](/reference/json-objects-1#amount) section
      </td>
    </tr>

    <tr>
      <td>
        document_type  
        Optional
      </td>

      <td>
        Type of document to be created. Use quotation to generate a quotation document. If this field is set to quotation, then `quotation_date` and `quotation_validity_date` are required.  
        Possible values are `quotation` or `invoice`(default).
      </td>
    </tr>

    <tr>
      <td>
        quotation_date  
        String (40)  
        **Required**  
        (if document_type: quotation)
      </td>

      <td>
        Date when the quotation is issued, in ISO 8601 format. Default time zone: GMT+7. For example: `2025-08-06 20: 03: 04 +0700`
      </td>
    </tr>

    <tr>
      <td>
        quotation_validity_date  
        String (40)  
        **Required**  
        (if document_type: quotation)
      </td>

      <td>
        Expiration date of the quotation, in ISO 8601 format. Default time zone: GMT+7 and must be after quotation_date. For example: `2025-08-20 23: 59: 59 +0700`
      </td>
    </tr>

    <tr>
      <td>
        tax_mode  
        Optional
      </td>

      <td>
        Tax calculation mode for the invoice.  
        Possible values are `exclusive` or `inclusive`.  
        Note: If tax_mode is passed as null, no tax will be applied to the invoice. This will override any default invoice tax settings configured in your dashboard.
      </td>
    </tr>

    <tr>
      <td>
        taxes  
        Array\<tax>
      </td>

      <td>
        List of tax entries applied to the invoice. Optional, but required when tax_mode is inclusive.  
        Refer to [Tax object ](/reference/json-objects-1#tax) section  
        Note: The taxes and vat parameters cannot be used in the same request. The vat parameter is currently deprecated; please use taxes for all new implementations.
      </td>
    </tr>
  </tbody>
</Table>

<br />

## Response sample

```json 201 Created
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
      "value": 0.2,
      "calculated_amount": 38
    }
  ],
  "document_type": "quotation",
  "quotation_date": "2026-07-07 03:03:04 +0700",
  "quotation_title": "QUOTATION TITLE",
  "quotation_validity_date": "2026-08-07 03:03:04 +0700",
  "quotation_pdf_url": "https://assets.stg.midtrans.com/quotations/8P1lnAJx",
  "quotation_terms_conditions": "QUOTATION TERMS & CONDITION",
  "converted_at": null,
  "created_as": "quotation",
  "quotation_published_date": "2026-04-28 16:45:43 +0700"
}
```
```json 201 Created Quotation
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
      "value": 0.2,
      "calculated_amount": 38
    }
  ],
  "document_type": "quotation",
  "quotation_date": "2026-07-07 03:03:04 +0700",
  "quotation_title": "QUOTATION TITLE",
  "quotation_validity_date": "2026-08-07 03:03:04 +0700",
  "quotation_pdf_url": "https://assets.stg.midtrans.com/quotations/8P1lnAJx",
  "quotation_terms_conditions": "QUOTATION TERMS & CONDITION",
  "converted_at": null,
  "created_as": "quotation",
  "quotation_published_date": "2026-04-28 16:45:43 +0700"
}
```
```json 400  Bad Request
{
 "error_messages": [
   "item must not be empty",
   "gross_amount must be more than 0"
 ]
}

```
```json 409 Conflict
--Occurred when creating an invoice using the same order id that was used previously.

{
   "error_messages": [
       "Duplicate order id"
   ]
}

```
```json 500 Internal Server Error
{
   "error_messages": [
       "Internal server error"
   ]
}

```

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
        `pending`,`published`,  `expired`, `overdue`, `paid`, `voided`, `rejected` or `canceled`.
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
        quotation_title  
        String
      </td>

      <td>
        Title displayed on the quotation document (PDF/view).
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
        quotation_validity_date  
        String
      </td>

      <td>
        Quotation expiration date in ISO 8601 format with default time zone GMT+7. After this date, the quotation is no longer valid.
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
        List of tax entries applied to the invoice.  
        Refer to [Tax object ](/reference/json-objects-1#tax)  section
      </td>
    </tr>
  </tbody>
</Table>

<br />