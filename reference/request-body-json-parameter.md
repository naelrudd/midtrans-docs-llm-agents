---
updatedAt: 2026-04-13T16:58:01.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Request Body (JSON Parameter)

```json Minimum request
{
  "transaction_details": {
    "order_id": "ORDER-101",
    "gross_amount": 10000
  }
}
```
```json Complete request
{
  "transaction_details": {
    "order_id": "ORDER-101",
    "gross_amount": 10000
  },
  "item_details": [{
    "id": "ITEM1",
    "price": 10000,
    "quantity": 1,
    "name": "Midtrans Bear",
    "brand": "Midtrans",
    "category": "Toys",
    "merchant_name": "Midtrans",
    "url": "http://toko/toko1?item=abc"
  }],
  "customer_details": {
    "first_name": "TEST",
    "last_name": "MIDTRANSER",
    "email": "test@midtrans.com",
    "phone": "+628123456",
    "billing_address": {
      "first_name": "TEST",
      "last_name": "MIDTRANSER",
      "email": "test@midtrans.com",
      "phone": "081 2233 44-55",
      "address": "Sudirman",
      "city": "Jakarta",
      "postal_code": "12190",
      "country_code": "IDN"
    },
    "shipping_address": {
      "first_name": "TEST",
      "last_name": "MIDTRANSER",
      "email": "test@midtrans.com",
      "phone": "0 8128-75 7-9338",
      "address": "Sudirman",
      "city": "Jakarta",
      "postal_code": "12190",
      "country_code": "IDN"
    }
  },
  "enabled_payments": ["credit_card", "cimb_clicks",
    "bca_klikbca", "bca_klikpay", "bri_epay", "echannel", "permata_va",
    "bca_va", "bni_va", "bri_va","cimb_va", "other_va", "gopay", "indomaret",
    "danamon_online", "akulaku", "shopeepay", "kredivo", "uob_ezpay","other_qris" ],
  
  "credit_card": {
    "secure": true,
    "channel": "migs",
    "bank": "bca",
    "installment": {
      "required": false,
      "terms": {
        "bni": [3, 6, 12],
        "mandiri": [3, 6, 12],
        "cimb": [3],
        "bca": [3, 6, 12],
        "offline": [6, 12]
      }
    },
    "whitelist_bins": [
      "48111111",
      "41111111"
    ],
    "dynamic_descriptor": {
      "merchant_name" : "Fuji Apple Inc",
      "city_name": "Jakarta",
      "country_code": "ID"
    }
  },
  "bca_va": {
    "va_number": "12345678911",
    "sub_company_code": "00000",
    "free_text": {
      "inquiry": [
        {
          "en": "text in English",
          "id": "text in Bahasa Indonesia"
        }
      ],
      "payment": [
        {
          "en": "text in English",
          "id": "text in Bahasa Indonesia"
        }
      ]
    }
  },
  "bni_va": {
    "va_number": "12345678"
  },
  "bri_va": {
    "va_number": "1234567891234"
  },
  "cimb_va": {
    "va_number": "1234567891234567"
  },  
  "permata_va": {
    "va_number": "1234567890",
    "recipient_name": "SUDARSONO"
  },
  "shopeepay": {
    "callback_url": "http://shopeepay.com"
  },
  "gopay": {
    "enable_callback": true,
    "callback_url": "http://gopay.com"
  },
  "callbacks": {
    "finish": "https://demo.midtrans.com"
  },
  "uob_ezpay": {
    "callback_url": "http://uobezpay.com"
  }, 
  "expiry": {
    "start_time": "2018-12-13 18:11:08 +0700",
    "unit": "minutes",
    "duration": 1
  },
"page_expiry": {
    "duration": 3,
    "unit": "hours"
},
"recurring": {
    "required": true,
    "start_time": "2024-06-09 15:07:00 +0700",
    "interval_unit": "week"
},  
  "custom_field1": "custom field 1 content",
  "custom_field2": "custom field 2 content",
  "custom_field3": "custom field 3 content"
}
```

<Table>
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
        transaction_details         <br /> [Transaction Details](/reference/json-objects#transaction-details-object) (required)
      </td>

      <td>
        Specific information regarding the transaction
      </td>
    </tr>

    <tr>
      <td>
        item_details                <br /> Array of [Item Details](/reference/json-objects#item-details-object) (optional)
      </td>

      <td>
        Shopping item details will be paid by customer

        * Please avoid using vertical line (|) for Alfamart payment type
        * item_details is required for Akulaku payment type.
        * Akulaku payment type doesn't allow duplicate item ID (item_details.id) in one request.
      </td>
    </tr>

    <tr>
      <td>
        customer_details            <br />[Customer Details](/reference/json-objects#customer-details-object) (optional)
      </td>

      <td>
        Specific information regarding the customer
      </td>
    </tr>

    <tr>
      <td>
        enabled_payments            <br /> Array (optional)
      </td>

      <td>
        List of payment types that should be enabled. If `enabled_payments:` field is not passed, all active payment types are included. <br />**Card Payment**:<br /> `credit_card`. <br />**VA**:<br />  `echannel` (Mandiri Bill Payment), `permata_va`, `bca_va`, `bni_va`, `bri_va`, `cimb_va`, `danamon_va` ,`bsi_va`, `seabank_va`, and `saqu_va`. <br />**E-wallets**:<br />  `gopay`, `ovo`, `dana` and `shopeepay`. <br />**Other QRIS**:<br />  `other_qris` <br />**Over The Counter**:<br /> `alfamart`, and `indomaret`.<br />**Cardless Credit/BNPL**:<br /> `akulaku`, and `kredivo`. <br /><br />Aliasing refers to a list of payment types. Passing an alias is the equivalent of passing all the the payment types it refers to. <br />**Supported aliases**:<br />`bank_transfer` =>  e.g. `permata_va`, `bca_va`, `bni_va` <br />`cstore` => e.g. `alfamart`, `indomaret`.<br /><br />If you want to use `other_va`, either `permata_va` or `bni_va` or `bri_va`, or `cimb_va`, or`danamon_va` because Midtrans handles other bank transfer as either Permata or BNI VA or BRI VA or Danamon VA.
      </td>
    </tr>

    <tr>
      <td>
        credit_card                 <br /> [CreditCard](/reference/json-objects#credit-card-object) (optional)
      </td>

      <td>
        Card Payment payment method
      </td>
    </tr>

    <tr>
      <td>
        bca_va                      <br /> [BCA Virtual Account](/reference/json-objects#bca-virtual-account-object) (optional)
      </td>

      <td>
        BCA Virtual Account payment method
      </td>
    </tr>

    <tr>
      <td>
        permata_va                  <br /> [Permata Virtual Account](/reference/json-objects#permata-virtual-account-object) (optional)
      </td>

      <td>
        Permata Virtual Account payment method
      </td>
    </tr>

    <tr>
      <td>
        bni_va                      <br /> [BNI Virtual Account](/reference/json-objects#bni-virtual-account-object) (optional)
      </td>

      <td>
        BNI Virtual Account payment method
      </td>
    </tr>

    <tr>
      <td>
        cimb_va                      <br /> [CIMB Virtual Account](/reference/json-objects#cimb-virtual-account-object) (optional)
      </td>

      <td>
        CIMB Virtual Account payment method
      </td>
    </tr>

    <tr>
      <td>
        bri_va                      <br /> [BRI Virtual Account](/reference/json-objects#bri-virtual-account-object) (optional)
      </td>

      <td>
        BRI Virtual Account payment method
      </td>
    </tr>

    <tr>
      <td>
        danamon_va  
        [Danamon Virtual Account](/reference/json-objects#danamon-virtual-account-object)   (optional)
      </td>

      <td>
        Danamon Virtual Account payment method
      </td>
    </tr>

    <tr>
      <td>
        bsi_va  
        [BSI Virtual Account](/reference/json-objects#bsi-virtual-account-object)  (optional)
      </td>

      <td>
        BSI Virtual Account payment method
      </td>
    </tr>

    <tr>
      <td>
        other_va                      <br /> [Other Banks Virtual Account](/reference/other-banks) (optional)
      </td>

      <td>
        Other Banks payment method. See Other Bank page for more details on how it works.
      </td>
    </tr>

    <tr>
      <td>
        gopay                       <br /> [GoPay](https://midtrans-docs.readme.io/reference/json-objects#gopay-object) (optional)
      </td>

      <td>
        GoPay e-wallet & GoPay QRIS payment methods.
      </td>
    </tr>

    <tr>
      <td>
        shopeepay                   <br /> [ShopeePay](/reference/json-objects#shopeepay-object) (optional)
      </td>

      <td>
        ShopeePay & ShopeePay QRIS payment methods.
      </td>
    </tr>

    <tr>
      <td>
        callbacks	                 <br /> [Callbacks](/reference/json-objects#callbacks-object) (optional)
      </td>

      <td>
        Redirect URL after transaction is successfully paid (can be overridden by JS callback). Can also be set via Snap Preference menu in your dashboard.
      </td>
    </tr>

    <tr>
      <td>
        expiry                      <br /> [Expiry](/reference/json-objects#expiry-object) (optional)
      </td>

      <td>
        Custom payment method expiry
      </td>
    </tr>

    <tr>
      <td>
        page_expiry                      <br /> [Page Expiry](/reference/json-objects#page-expiry-object) (optional)
      </td>

      <td>
        Customize Snap's page expiry
      </td>
    </tr>

    <tr>
      <td>
        custom_field1               <br /> String(255) (optional)
      </td>

      <td>
        Custom field 1 for custom parameter from merchant
      </td>
    </tr>

    <tr>
      <td>
        custom_field2               <br /> String(255) (optional)
      </td>

      <td>
        Custom field 2 for custom parameter from merchant
      </td>
    </tr>

    <tr>
      <td>
        custom_field3               <br /> String(255) (optional)
      </td>

      <td>
        Custom field 3 for custom parameter from merchant
      </td>
    </tr>

    <tr>
      <td>
        recurring               <br /> [Recurring](/reference/json-objects#recurringsubscription-object) (optional)
      </td>

      <td>
        Recurring object to show a dedicated UI for Recurring payment flow using [Subscription API](/reference/api-methods-1). Use this only if your account is configured by Midtrans to accept recurring/subscription payment.
      </td>
    </tr>
  </tbody>
</Table>

<br />

> 📘 Specifying payment methods via API using `enabled_payments`
>
> Other than from Snap Preference settings in Dashboard, you can also specify which payment method to show in Snap via API using `enabled_payments`. This is useful if you want to maintain your own payment list; you can then bind each payment method list in your checkout page with individual Snap checkout page containing the specified payment method. See [Supported Payment Channels](/reference/payment-channels) page for more details on the param value for each payment channel.