---
updatedAt: 2026-10-06T04:20:35.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Mark as Paid

**Endpoints:** /v1/invoices/{invoice_id}/paid<br />**HTTP Method:** PATCH<br />**Headers:**

Production: `https: //api.midtrans.com/v1/invoices/{invoice_id}/paid`

Sandbox: `https: //api.sandbox.midtrans.com/v1/invoices/{invoice_id}/paid`

| Key           | Description                            |
| :------------ | :------------------------------------- |
| Authorization | Basic Base64Encode(merchantServerKey:) |

<br />

Marks an invoice as paid outside of Midtrans, for example when your customer settled the amount by cash or by a direct bank transfer you reconciled yourself.

When the invoice was published with a `payment_type` other than `manual_payment`, Midtrans **cancels the active payment channel first**, the payment link, virtual account, or QRIS created for that invoice is voided so the customer can no longer pay it twice. Only after that cancellation succeeds is the invoice marked as paid.

The invoice status becomes `manual_paid`, `paid_date` is set to the time of the call, and a `manual_paid_audit` object records who marked it and what the status was beforehand.

<Callout icon="🚧" theme="warn">
  Only an invoice whose status is **pending** or **overdue** can be marked as paid, and only a document whose `document_type` is `invoice`.

  A quotation, or an invoice that is already `paid`, `manual_paid`, `expired`, `cancelled` or still `draft`, is rejected with **409 Conflict**.

  This also means the call is **not** safe to retry blindly a second call on the same invoice returns 409, because the first one already moved it to `manual_paid`.
</Callout>

<br />

## Request Body

This endpoint takes **no request body**. The invoice is identified by the `invoice_id` path parameter.

```text No body
PATCH /v1/invoices/65e7e8e657389830d04836fc/paid
Authorization: Basic <Base64Encode(merchantServerKey:)>
```

<br />

## Request Path Parameter Details

| Parameter                                 | Description                                                                                                                                                   |
| :---------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| invoice\_id<br />String<br />**Required** | The Midtrans invoice id, as returned in the `id` field when the invoice was created. Note this is the invoice id, not the `order_id` or the `invoice_number`. |

<br />

## Response sample

```json 200 OK
{
    "order_id": "7950c36a-d267-4f25-bb03-7a82b00z168t",
    "invoice_number": "7128c81b-cde5-4c33-8777-4d1d0fcd6377",
    "published_date": "2024-03-06 10:54:14 +0700",
    "due_date": "2025-08-06 20:03:04 +0700",
    "invoice_date": "2025-01-06 20:03:04 +0700",
    "paid_date": "2025-02-14 09:12:33 +0700",
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
    "status": "manual_paid",
    "gross_amount": 2000,
    "pdf_url": "https://assets.midtrans.com/invoices/pdf/5a76417e-be8e-437a-8e16-38c916aea614",
    "paid_pdf_url": "https://assets.midtrans.com/invoices/pdf/5a76417e-be8e-437a-8e16-38c916aea614",
    "payment_type": "payment_link",
    "virtual_accounts": [],
    "payment_link_url": "https://app.midtrans.com/payment-links/b1000b26-a311-42d4-9dc7-51a00ec8c681",
    "tax_mode": "exclusive",
    "taxes": [
        {
            "name": "PPN",
            "type": "percentage",
            "value": 0.2,
            "calculated_amount": 4
        }
    ],
    "manual_paid_audit": {
        "actor": "public-api",
        "at": "2025-02-14 09:12:33 +0700",
        "previous_status": "pending"
    }
}
```
```json 401 Unauthorized
{
    "error_messages": [
        "Invalid auth token"
    ]
}

```
```json 404 Not Found
{
    "error_messages": [
        "Invoice not found"
    ]
}

```
```json 409 Conflict
--Occurred when the invoice is not in a status that can be marked as paid (only pending and overdue are allowed), when the document is a quotation, or when the existing payment channel could not be cancelled.

{
    "error_messages": [
        "Invoice cannot be marked as paid"
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
```text 200 QRIS
{
    "success": true,
    "errors": [],
    "data": {
        "order_id": "1791260297",
        "invoice_number": "123231312213",
        "published_date": "2026-10-06T04:18:18.891Z",
        "due_date": "2026-12-05T13:03:04.000Z",
        "invoice_date": "2026-07-06T13:03:04.000Z",
        "paid_date": "2026-10-06T04:18:25.032Z",
        "reference_text": "payment for Metal Gear Rex",
        "client": {
            "id": "Snake01",
            "name": "Naked Snake",
            "email": "bigboss@outerheaven.org",
            "phone": "628128888888"
        },
        "item_details": [
            {
                "item_id": "SKU1111",
                "description": "Metal Gear REX",
                "quantity": 1,
                "price": 1000000
            }
        ],
        "currency": "IDR",
        "notes": "the weapon that can surpass metal gear",
        "payment_type": "qris",
        "payment_link": {
            "is_custom_expiry": true,
            "enabled_payments": [
                "credit_card"
            ],
            "credit_card": {
                "whitelist_bins": [
                    "481111"
                ],
                "bank": "bni",
                "type": "authorize",
                "secure": true,
                "installment": {
                    "required": false,
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
                "number": "87654367891",
                "free_text": {
                    "inquiry": [
                        {
                            "id": "Teks Inquiry dalam Bahasa Indonesia",
                            "en": "English Inquiry Text"
                        }
                    ],
                    "payment": [
                        {
                            "id": "Teks Payment dalam Bahasa Indonesia",
                            "en": "English Payment Text"
                        }
                    ]
                }
            },
            "bni_va": {
                "number": "87654367"
            },
            "permata_va": {
                "number": "8765436789",
                "recipient_name": "string"
            },
            "bri_va": {
                "number": "8765436723412"
            },
            "cimb_va": {
                "number": "8765436723412765"
            },
            "danamon_va": {},
            "seabank_va": {},
            "saqu_va": {},
            "bsi_va": {},
            "callbacks": {},
            "expiry": {
                "unit": "days",
                "duration": 3,
                "start_time": "2024-07-06T13:03:04.000Z"
            }
        },
        "virtual_accounts": [],
        "qris": {
            "acquirer": "gopay",
            "qr_string": "00020101021226620014COM.GO-JEK.WWW011993600914377234911250210G7723491120303UKE51440014ID.CO.QRIS.WWW0215AID2945998244280303UKE520417615303360540710010005802ID5915Toko Test Farah6013JAKARTA PUSAT61051011062395028A120261006041819s4m9FWVxZGID0703A016304681A",
            "expiry": {
                "unit": "days",
                "duration": 120
            }
        },
        "qris_url": "https://api.stg.midtrans.com/v2/qris/011b79fb-c92d-4a5a-be2d-f2eb8214d508/qr-code",
        "transaction_id": "011b79fb-c92d-4a5a-be2d-f2eb8214d508",
        "amount": {
            "total_tax": 1000
        },
        "tax_mode": "exclusive",
        "taxes": [
            {
                "name": "PPN",
                "type": "fixed",
                "value": 1000,
                "calculated_amount": 1000
            }
        ],
        "id": "6ac476888d2e730e6d871d08",
        "status": "manual_paid",
        "gross_amount": 1001000,
        "pdf_url": "https://al-mp-id-s-invoice-service-assets.oss-ap-southeast-5.aliyuncs.com/G772349112/INVOICE-PDF/6ac476888d2e730e6d871d08.pdf?Expires=1791346705&OSSAccessKeyId=STS.NXo1bnYYxpi8zRv17Wf3HiPL9&Signature=C79sD%2Fk6zuXF9Is2hXt424rJEPU%3D&security-token=CAIS3wJ1q6Ft5B2yfSjIr5vaetjatIZZx6vTeHTH1TcCarxkhpXn2zz2IHhNdXBvAekatfQ0mmtQ7%2F8dlrd4UZJJSErYbMJ09dFV%2BB2oJtOe6pXss%2BJY18D7QjLL3dR1SDeOMYvDV9r4VqqHSTKtz11eo9bTcTGlQCbWU%2FmggoJmadI6RxSxaSE8av5dOgplrr1xVxKTT4HPVCTnmW3NFkFllxNhgGdkk8SFz9ab9wDVgS%2BRqIZXhfysfsn%2BM5M8ZM0kA4jkhbwmTMebjn4Auyot3bxtkalJ9Q3AutygGFRL632ESbGMq4w2c1cgOvNqQPAf9KGlyucHu%2BrNkIX8xlNWMPtLUi%2FSAYm42I7LA%2BO5yhKU9wZ5sxUnu%2FD41fmd22tMCRpzv7NVp1m%2BRgQ5j5B4%2F7s%2Bhns7HPzuI17FZeHs69oVmuE%2BrD6j9rmRBHPsINj3nFheVNZSAE1A%2FTUqJjCJGscagAEBAedg%2B%2F4rY5wgNkd6nnBwHXHD%2BbRr5OMGpq9kW4Zp%2Bjkyb5RVlPtv%2Bwj3yWw4B6y22pgJ6R6IwNlprMM4O9x7BlhmDe6AFzXCgTho0cwVJpO3kETIDZfYVzY%2BLaD%2F%2FYhjjQHX5QzpmP4p6Vo%2FzAhETihOHb1et%2BYIrFRwKcfrJCAA",
        "paid_pdf_url": "https://assets.stg.midtrans.com/invoices/e0WzvgLK",
        "quotation_pdf_url": null,
        "payment_link_url": null,
        "created_at": "2026-10-06T04:18:16.898+00:00",
        "updated_at": "2026-10-06T04:18:25.032+00:00",
        "external_group_id": null,
        "business": {
            "name": "Demo Midtrans",
            "email": "farah.rahmadiani@gojek.com",
            "phone": "+622188221000",
            "address": "Kebayoran lama, South Jakarta",
            "vat_number": "8271761525321898",
            "url": "https://tokomidtrans.com?debug=1"
        },
        "business_logo": null,
        "signature": null,
        "signatory_name": "Farah Rahmadiani",
        "signatory_role": "Leader of Patriots",
        "terms_conditions": "**Terms & Conditions**\n\n1. Payment is due within 14 days of the invoice date\n2. Goods remain our property until paid in full\n3. Returns accepted within 7 days, in original packaging\n4. Late payment incurs a *2% monthly* charge\n\n**Shipping**\n\n- Orders confirmed before 15:00 ship the same day\n- ~~Free shipping on all orders~~ free above Rp500.000\n- Delivery takes 2-5 working days\n\nFull policy: [example.com/terms](https://example.com/terms) @, #, &, %, こんにちは 你好 مرحبا بالعالم 👩‍💻\n\n<img src=\"logo.png\">",
        "enabled_virtual_account_banks": [
            "bca_va",
            "mandiri_bill",
            "bni_va",
            "bri_va",
            "cimb_va",
            "permata_va",
            "danamon_va",
            "seabank_va",
            "saqu_va",
            "bsi_va"
        ],
        "invoice_title": null,
        "invoice_paid_title": null,
        "business_logo_url": null,
        "signature_url": null,
        "default_bank": "bca_va",
        "include_stamp": false,
        "shortened_pdf_url": "https://assets.stg.midtrans.com/invoices/e0WzvgLK",
        "shortened_quotation_pdf_url": null,
        "document_type": "invoice",
        "quotation_date": null,
        "quotation_validity_date": null,
        "quotation_published_date": null,
        "quotation_terms_conditions": null,
        "created_as": "invoice",
        "converted_at": null,
        "quotation_title": null,
        "manual_paid_audit": {
            "actor": "",
            "at": "2026-10-06T04:18:25.032Z",
            "previous_status": "pending"
        }
    }
}
```

| Field                                            | Description                                                                                                                                                                                                              |
| :----------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| order\_id<br />String                            | Id for the order                                                                                                                                                                                                         |
| id<br />String                                   | invoice id                                                                                                                                                                                                               |
| invoice\_number<br />String                      | Number of the invoice                                                                                                                                                                                                    |
| published\_date<br />String                      | Date the invoice was published in ISO 8601 format. Default time zone: GMT+7.                                                                                                                                             |
| due\_date<br />String                            | Due date of transaction in ISO 8601 format. Default time zone: GMT+7.                                                                                                                                                    |
| invoice\_date<br />String                        | Date of Invoice and will be used in email and pdf created in ISO 8601 format. Default time zone: GMT+7.                                                                                                                  |
| paid\_date<br />String                           | Time the invoice was marked as paid, in ISO 8601 format. Default time zone: GMT+7. Set by this endpoint to the time of the call.                                                                                         |
| reference<br />String                            | Reference of the invoice                                                                                                                                                                                                 |
| customer\_details<br />Object                    | Refer to [Customer Details object](https://docs.midtrans.com/reference/json-objects-1#customer-details) section.                                                                                                                                  |
| item\_details<br />Array\<item\_detail>          | Refer to [Item Detail object](https://docs.midtrans.com/reference/json-objects-1#item-detail) section                                                                                                                                             |
| status<br />String                               | Status of the invoice. Always `manual_paid` in a successful response to this endpoint.                                                                                                                                   |
| gross\_amount<br />Integer                       | Total amount in invoice                                                                                                                                                                                                  |
| pdf\_url<br />String                             | pdf\_url of the invoice                                                                                                                                                                                                  |
| paid\_pdf\_url<br />String                       | URL of the paid invoice PDF, generated once the invoice is marked as paid                                                                                                                                                |
| payment\_type<br />String                        | The payment type the invoice was published with. Retained after the invoice is marked as paid.                                                                                                                           |
| payment\_link\_url<br />String                   | URL for payment link and only filled when payment\_type is payment\_link. The link itself is cancelled by this endpoint and can no longer be paid.                                                                       |
| virtual\_accounts<br />array \<virtual\_account> | Invoice virtual account and only filled when payment\_type is virtual\_account. Refer to [Virtual Account object](https://docs.midtrans.com/reference/json-objects-1#virtual-account) section. The virtual account is cancelled by this endpoint. |
| amount<br />Object                               | Refer to [Amount object](https://docs.midtrans.com/reference/json-objects-1#amount) section                                                                                                                                                       |
| tax\_mode<br />String                            | Tax calculation mode for the invoice.<br />Possible values are `exclusive` or `inclusive`                                                                                                                                |
| taxes<br />Array\<tax>                           | List of tax entries applied to the invoice.<br />Refer to [Tax object](https://docs.midtrans.com/reference/json-objects-1#tax) section                                                                                                            |
| manual\_paid\_audit<br />Object                  | Audit information recorded when the invoice was marked as manually paid. Refer to the table below.                                                                                                                       |
| qris\_url<br />Optional                          | URL used to retrieve the QRIS QR code image.                                                                                                                                                                             |
| qris<br />Optional                               | Refer to QRIS object.                                                                                                                                                                                                    |

<br />

### manual\_paid\_audit object

| Field                        | Description                                                                                                                                            |
| :--------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------- |
| actor<br />String            | Who marked the invoice as paid. `public-api` when marked through this endpoint, or the dashboard user's email when marked from the Midtrans dashboard. |
| at<br />String               | Time the invoice was marked as paid, in ISO 8601 format. Default time zone: GMT+7.                                                                     |
| previous\_status<br />String | The invoice status immediately before it was marked as paid, either `pending` or `overdue`.                                                            |