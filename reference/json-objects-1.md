---
updatedAt: 2026-04-30T05:35:20.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# JSON Objects

# Amount

<br />

```json
{
      "vat_type": "fixed",
      "vat": "12313",
      "discount": "1000",
      "shipping": "11"
}
```

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
        vat_type  
        String  Optional
      </td>

      <td>
        Tax type for the `vat` field.  
        **Deprecated. Please use `taxes` instead for tax calculation.**
      </td>
    </tr>

    <tr>
      <td>
        vat Integer Required from 0 - 99999999999
      </td>

      <td>
        Tax amount  
        **Deprecated. Please use taxes instead for tax calculation. **
      </td>
    </tr>

    <tr>
      <td>
        discount  
        Integer Required from 0 - 99999999999
      </td>

      <td>
        Discount amount in positive integer
      </td>
    </tr>

    <tr>
      <td>
        shipping  
        Integer Optional from 0 - 99999999999
      </td>

      <td>
        Shipping amount
      </td>
    </tr>
  </tbody>
</Table>

<br />

> 📘 Note
>
> Product gross amount total + VAT + shipping - discount should not be less than 0

<br />

***

<br />

# Customer Details

<br />

```json
{
   "id": "customer_id",
   "name": "merchant A",
   "email": "merchant@midtrans.com",
   "phone": "82313123123"
 }

```

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
        Id String(36) Optional
      </td>

      <td>
        Id of the customer
      </td>
    </tr>

    <tr>
      <td>
        Name  
        String(40) **Required**
      </td>

      <td>
        Name of the customer
      </td>
    </tr>

    <tr>
      <td>
        Email  
        String(255) Optional
      </td>

      <td>
        Email of the customer
      </td>
    </tr>

    <tr>
      <td>
        Phone  
        String (15) Optional
      </td>

      <td>
        Phone number of the customer and not start with “0”
      </td>
    </tr>
  </tbody>
</Table>

<br />

***

<br />

# Payment Link

<br />

```json
{
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
}
```

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
        Is_custom_expiry Boolean, default: false
      </td>

      <td>
        Indicate payment link to use custom expiry. If  false then the payment link expiry will be same as invoice due_date
      </td>
    </tr>

    <tr>
      <td>
        Enabled_payments  
        array\<string> **Required**
      </td>

      <td>
        Payment methods that will be used in payment link. Please refer to [here ](/reference/request-body-json-parameter)for the available payments.
      </td>
    </tr>

    <tr>
      <td>
        bca_va  
        Object: Optional
      </td>

      <td>
        BCA VA properties for payment link. Please refer to [here ](/reference/json-objects#bca-virtual-account-object) for more details. (Note: sub_company_code will not be used).
      </td>
    </tr>

    <tr>
      <td>
        bni_va  
        Object: Optional
      </td>

      <td>
        BNI VA properties for payment link. Please refer to [here ](/reference/json-objects#bna-virtual-account-object) for more details.
      </td>
    </tr>

    <tr>
      <td>
        permata_va  
        Object: Optional
      </td>

      <td>
        Permata VA properties for payment link. Please refer to [here ](/reference/json-objects#permata-virtual-account-object) for more details.
      </td>
    </tr>

    <tr>
      <td>
        bri_va  
        Object: Optional
      </td>

      <td>
        BRI VA properties for payment link. Please refer to [here ](/reference/json-objects#bri-virtual-account-object) for more details.
      </td>
    </tr>

    <tr>
      <td>
        cimb_va  
        Object: Optional
      </td>

      <td>
        CIMB VA properties for payment link. Please refer to [here ](/reference/json-objects#cimb-virtual-account-object) for more details.
      </td>
    </tr>

    <tr>
      <td>
        Expiry  
        Object: Optional
      </td>

      <td>
        Payment link expiry property. Please refer to [here ](/reference/json-objects#expiry-object) for more details. (Note: either duration or start_time must be 2 years or 730 days from now)
      </td>
    </tr>

    <tr>
      <td>
        credit_card  
        Object: Optional
      </td>

      <td>
        Payment link credit card property. Please refer to [here ](/reference/json-objects#credit-card-object)for more details.
      </td>
    </tr>

    <tr>
      <td>
        callbacks  
        Object: Optional
      </td>

      <td>
        Callback URLs object for payment link flow.
      </td>
    </tr>

    <tr>
      <td>
        callbacks.finish  
        String: Optional
      </td>

      <td>
        Redirect URL after customer completes payment link process. Must be a valid HTTPS URL.
      </td>
    </tr>
  </tbody>
</Table>

<br />

***

<br />

# Virtual Account

<br />

```json
{
   "name": "bca_va",
   "number": "12345678901"
}
```

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
        Name String **Required**
      </td>

      <td>
        Bank provider name, should be either `bca_va`, `mandiri_bill`, `bni_va`, `bri_va`, `cimb_va`,  
        `permata_va`
      </td>
    </tr>

    <tr>
      <td>
        Number  
        String Optional
      </td>

      <td>
        Custom va number with different min and max length for each bank provider  
        bca_va: min 11 and max 11  
        mandiri_bill: min 1 and max 12  
        bni_va: min 1 and max 8  
        bri_va: min 1 and max 13  
        cimb_va: min 1 and max 16  
        permata_va: min 10 and max 10
      </td>
    </tr>
  </tbody>
</Table>

<br />

***

<br />

# Item Detail

<br />

```json
{
  "item_id": "SKU1111",
  "description": "midtrans pillow",
  "quantity": 1,
  "price": 2000,
  "discount_percentage": 50
}
```

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
        Item_id String(30) Optional
      </td>

      <td>
        Id of the item
      </td>
    </tr>

    <tr>
      <td>
        description  
        String(150) **Required**
      </td>

      <td>
        Name or description of the item
      </td>
    </tr>

    <tr>
      <td>
        quantity  
        Integer **Required**
      </td>

      <td>
        Number of items (max: 99999999)
      </td>
    </tr>

    <tr>
      <td>
        price  
        Integer **Required**
      </td>

      <td>
        Price of items (max: 99999999)
      </td>
    </tr>

    <tr>
      <td>
        discount_percentage Integer Optional
      </td>

      <td>
        Discount applied to the item. Must be a value between **0** and **100**.
      </td>
    </tr>
  </tbody>
</Table>

<br />

***

<br />

# Tax

```json
{
  "name": "PPN",
  "type": "percentage",
  "value": 10
}
```

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
        name  
        String **Required**
      </td>

      <td>
        Tax label shown in the invoice, for example PPN.
      </td>
    </tr>

    <tr>
      <td>
        type  
        String **Required**
      </td>

      <td>
        Tax calculation type. Supported values are percentage or fixed.
      </td>
    </tr>

    <tr>
      <td>
        value  
        Integer **Required**
      </td>

      <td>
        Tax amount value. If type is percentage, use percent value (for example 10 means 10%). If type is fixed, use nominal amount.
      </td>
    </tr>
  </tbody>
</Table>