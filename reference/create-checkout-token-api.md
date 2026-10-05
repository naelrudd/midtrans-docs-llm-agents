---
updatedAt: 2026-09-28T12:00:08.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Create Checkout Token API

This API can be used to create a checkout token which is used to open a checkout page where a transaction happens. Details regarding the transaction can be passed here, such as list of enabled payments on checkout page, transaction expiry time, callback URL from checkout page, and some more which can be seen below.

Endpoints: `/api/v1/checkout/transactions`

HTTP Method: `POST`

## Request Body

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
  "expiry": {
    "start_time": "2018-12-13 18:11:08 +0700",
    "unit": "minutes",
    "duration": 1
  },
  "page_expiry": {
      "duration": 3,
      "unit": "hours"
  },
  "custom_field1": "custom field 1 content",
  "custom_field2": "custom field 2 content",
  "custom_field3": "custom field 3 content"
}
```

<Table align={[null,"left","left",null]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Attribute
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        transaction\_details         <br /> [Transaction Details](/reference/json-objects#transaction-details-object) 
      </td>

      <td>
        Object
      </td>

      <td>
        Mandatory
      </td>

      <td>
        Specific information regarding the transaction
      </td>
    </tr>

    <tr>
      <td>
        item\_details                <br /> Array of [Item Details](/reference/json-objects#item-details-object) 
      </td>

      <td>
        Object
      </td>

      <td>
        Mandatory
      </td>

      <td>
        Shopping item details will be paid by customer
      </td>
    </tr>

    <tr>
      <td>
        customer\_details            <br />[Customer Details](/reference/json-objects#customer-details-object) 
      </td>

      <td>
        Object
      </td>

      <td>
        Mandatory
      </td>

      <td>
        Specific information regarding the customer
      </td>
    </tr>

    <tr>
      <td>
        enabled\_payments            
      </td>

      <td>
        Array of String
      </td>

      <td>
        Optional
      </td>

      <td>
        List of payment types that should be enabled. If `enabled_payments:` field is not passed, all active payment types are included. <br />**Card Payment**:<br /> `credit_card`. <br />**VA**:<br />  `echannel` (Mandiri Bill Payment), `permata_va`, `bca_va`, `bni_va`, `bri_va`, `cimb_va`. <br />**E-wallets**:<br />  `gopay`, and `shopeepay`. <br />**Other QRIS**:<br />  `other_qris` <br />**<br /><br />Aliasing refers to a list of payment types. Passing an alias is the equivalent of passing all the the payment types it refers to.<br />**&#x53;upported aliases\*\*:<br />`bank_transfer` =>  e.g. `permata_va`, `bca_va`, `bni_va`.<br /><br />If you want to use `other_va`, either `permata_va` or `bni_va` or `bri_va` because Midtrans handles other bank transfer as either Permata or BNI VA or BRI VA.
      </td>
    </tr>

    <tr>
      <td>
        credit\_card                 <br /> [CreditCard](/reference/json-objects#credit-card-object)
      </td>

      <td>
        Object
      </td>

      <td>
        Optional
      </td>

      <td>
        Card payment method
      </td>
    </tr>

    <tr>
      <td>
        bca\_va                      <br /> [BCA Virtual Account](/reference/json-objects#bca-virtual-account-object) 
      </td>

      <td>
        Object
      </td>

      <td>
        Optional
      </td>

      <td>
        BCA Virtual Account payment method
      </td>
    </tr>

    <tr>
      <td>
        permata\_va                  <br /> [Permata Virtual Account](/reference/json-objects#permata-virtual-account-object) 
      </td>

      <td>
        Object
      </td>

      <td>
        Optional
      </td>

      <td>
        Permata Virtual Account payment method
      </td>
    </tr>

    <tr>
      <td>
        bni\_va                      <br /> [BNI Virtual Account](/reference/json-objects#bni-virtual-account-object) 
      </td>

      <td>
        Object
      </td>

      <td>
        Optional
      </td>

      <td>
        BNI Virtual Account payment method
      </td>
    </tr>

    <tr>
      <td>
        cimb\_va                      <br /> [CIMB Virtual Account](/reference/json-objects#cimb-virtual-account-object) 
      </td>

      <td>
        Object
      </td>

      <td>
        Optional
      </td>

      <td>
        CIMB Virtual Account payment method
      </td>
    </tr>

    <tr>
      <td>
        bri\_va                      <br /> [BRI Virtual Account](/reference/json-objects#bri-virtual-account-object) 
      </td>

      <td>
        Object
      </td>

      <td>
        Optional
      </td>

      <td>
        BRI Virtual Account payment method
      </td>
    </tr>

    <tr>
      <td>
        other\_va                      <br /> [Other Banks Virtual Account](/reference/other-banks) 
      </td>

      <td>
        Object
      </td>

      <td>
        Optional
      </td>

      <td>
        Other Banks payment method. See Other Bank page for more details on how it works.
      </td>
    </tr>

    <tr>
      <td>
        gopay                       <br /> [GoPay](https://midtrans-docs.readme.io/reference/json-objects#gopay-object) 
      </td>

      <td>
        Object
      </td>

      <td>
        Optional
      </td>

      <td>
        GoPay e-wallet & GoPay QRIS payment methods.
      </td>
    </tr>

    <tr>
      <td>
        shopeepay                   <br /> [ShopeePay](/reference/json-objects#shopeepay-object)
      </td>

      <td>
        Object
      </td>

      <td>
        Optional
      </td>

      <td>
        ShopeePay & ShopeePay QRIS payment methods.
      </td>
    </tr>

    <tr>
      <td>
        callbacks	                 <br /> [Callbacks](/reference/json-objects#callbacks-object) 
      </td>

      <td>
        Object
      </td>

      <td>
        Optional
      </td>

      <td>
        Redirect URL after transaction is successfully paid (can be overridden by JS callback). Can also be set via Snap Preference menu in your dashboard. <br />Partner merchant (multi-outlet) can use [cross auth](https://docs.midtrans.com/docs/merchant-administration-portal-partner-multi-outlet#d-you-can-also-login-to-your-merchants-dashboard-which-you-arent-able-to-do-on-the-previous-dashboard) to access merchant dashboard and configure this.
      </td>
    </tr>

    <tr>
      <td>
        expiry                      <br /> [Expiry](/reference/json-objects#expiry-object) 
      </td>

      <td>
        Object
      </td>

      <td>
        Optional
      </td>

      <td>
        Custom payment method expiry
      </td>
    </tr>

    <tr>
      <td>
        page\_expiry                      <br /> [Page Expiry](/reference/json-objects#page-expiry-object)
      </td>

      <td>
        Object
      </td>

      <td>
        Optional
      </td>

      <td>
        Customize Checkout page expiry
      </td>
    </tr>

    <tr>
      <td>
        custom\_field1
      </td>

      <td>
        String
      </td>

      <td>
        Optional
      </td>

      <td>
        Custom field 1 for custom parameter from merchant
      </td>
    </tr>

    <tr>
      <td>
        custom\_field2
      </td>

      <td>
        String
      </td>

      <td>
        Optional
      </td>

      <td>
        Custom field 2 for custom parameter from merchant
      </td>
    </tr>

    <tr>
      <td>
        custom\_field3
      </td>

      <td>
        String
      </td>

      <td>
        Optional
      </td>

      <td>
        Custom field 3 for custom parameter from merchant
      </td>
    </tr>
  </tbody>
</Table>

> 📘 Specifying payment methods via API using `enabled_payments`
>
> Other than from Snap Preference settings in Dashboard, you can also specify which payment method to show in Snap via API using `enabled_payments`. This is useful if you want to maintain your own payment list; you can then bind each payment method list in your checkout page with individual Snap checkout page containing the specified payment method. See [Supported Payment Channels](/reference/payment-channels) page for more details on the param value for each payment channel.

<br />

## Sample Curl

```curl
curl --location 'https://partner-api.stg.midtrans.com/api/v1/checkout/transactions' \
--header 'x-partner-id: 370' \
--header 'x-merchant-id: G167720338' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic key' \
--data '{
    "transaction_details": {
        "order_id": "order-1720773628",
        "gross_amount": 50000
    }
}'
```

<br />

## Response Body

### Success

```json 201 - Success
{
  "token": "d379aa71-99eb-4dd1-b9bb-eefe813746e9",
  "redirect_url": "https://app.sandbox.midtrans.com/snap/v3/redirection/071e0c3d-dade-4148-a1b5-296ee8735b79"
}
```

| Field         | Type       | Description                                          |
| ------------- | :--------- | ---------------------------------------------------- |
| token         | String(36) | Snap token for [opening the Snap popup](https://docs.midtrans.com/reference/snap-js) |
| redirect\_url | String(75) | URL for [redirection](https://docs.midtrans.com/reference/window-redirection)        |

### Failed

```json 400 - Validation Error
{
  "error_messages": [
    "transaction_details.gross_amount is not equal to the sum of item_details"
  ]
}
```
```json 400 - Duplicate Order ID
{
  "error_messages": [
    "transaction_details.order_id has been paid and utilized, please use another order ID"
  ]
}
```
```json 401 - Authentication Failed
{
  "error_messages": [
    "Access denied due to unauthorized transaction, please check client or server key",
    "Visit https://snap-docs.midtrans.com/#request-headers for more details"
  ]
}
```
```json 500 - Internal Server Error
{
  "error_messages": [
    "Sorry, we encountered internal server error. We will fix this soon."
  ]
}
```

| Field           | Type            | Description    |
| --------------- | :-------------- | -------------- |
| error\_messages | Array of String | Error messages |