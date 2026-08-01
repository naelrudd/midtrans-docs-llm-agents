---
updatedAt: 2026-05-11T08:17:38.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# JSON Objects

Collection of JSON objects that are used in [Create Snap Token](https://docs.midtrans.com/reference/request-body-json-parameter) parameter.

**Note:** More JSON objects exists for each specific [payment channels](/reference/payment-channels).

<br />

***

<br />

## Transaction Details Object

<br />

```json
"transaction_details": {
  "order_id": "ORDER-101",
  "gross_amount": 10000
}
```

| Parameter                                                                                                            | Description                                                                                                                                                     |
| -------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| transaction\_details.order\_id    (required) <br /> String(50) for Snap Checkout <br /> String (36) for Payment Link | Unique transaction ID. A single ID could be used only once by a Merchant. <br /> **NOTE:** Allowed Symbols are dash(-), underscore(\_), tilde (\~), and dot (.) |
| transaction\_details.gross\_amount <br /> Integer (required)                                                         | Amount to be charged                                                                                                                                            |

<br />

***

<br />

## Item Details Object

<br />

```json
"item_details": [{
  "id": "ITEM1",
  "price": 10000,
  "quantity": 1,
  "name": "Midtrans Bear",
  "brand": "Midtrans",
  "category": "Toys",
  "merchant_name": "Midtrans",
  "url": "https://tokobuah.com/apple-fuji"
}]
```

| Parameter                                   | Description                                                          |
| ------------------------------------------- | -------------------------------------------------------------------- |
| id <br /> String(50) (optional)             | Item ID                                                              |
| price <br /> Integer (required)             | Price of the item <br />**NOTE:** Don't add decimal                  |
| quantity <br /> Integer (required)          | Quantity of the item <br />**NOTE:** Must be greater than or equal 1 |
| name <br /> String(50) (required)           | Name of the item                                                     |
| brand <br /> String(50) (optional)          | Brand of the item                                                    |
| category <br /> String(50) (optional)       | Category of the item                                                 |
| merchant\_name <br /> String(50) (optional) | Merchant selling the item                                            |
| url <br /> String(50) (optional)            | HTTP URL of the item in the merchant site                            |

<br />

<Callout icon="🚧" theme="warn">
  * Subtotal (item price multiplied by quantity) of all the item details needs to be exactly the same as the gross_amount inside transaction_details object* Please avoid using vertical line (`|`) for Alfamart payment type* **item_details** field is required for Akulaku payment type and does not allow duplicate item IDs (item_details.id) in one request
</Callout>

> 📘 Tips
>
> You can actually make an item with minus price to be presented as discount

<br />

***

<br />

## Customer Details Object

<br />

```json
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
}
```

| Parameter                                                     | Description |
| ------------------------------------------------------------- | ----------- |
| first\_name      <br /> String(255) (optional)                |             |
| last\_name       <br /> String(255) (optional)                |             |
| email 	         <br /> String(255) (optional)                 |             |
| phone 	         <br /> String(255) (optional).                |             |
| billing\_address <br /> [Address](#address-object) (optional) |             |
| shipping\_address<br /> [Address](#address-object) (optional) |             |

<br />

> 🚧 Tips
>
> Customer Details object is mandatory to be passed for Akulaku Paylater, if not passed, transaction will fail.

> 📘 Specific bank requirements
>
> For BCA VA, limit the customer names (**first\_name** and **last\_name**), to only 30 characters.
>
> For BNI VA, phone number format should start with +62 or 0 +\[area code] with max char = 30. If passed incorrectly, trx will be rejected.

<br />

***

<br />

## Address Object

<br />

```json billing_address
"billing_address": {
  "first_name": "TESTER",
  "last_name": "MIDTRANSER",
  "email": "test@midtrans.com",
  "phone": "081 2233 44-55",
  "address": "Sudirman",
  "city": "Jakarta",
  "postal_code": "12190",
  "country_code": "IDN"
}
```
```json shipping_address
"shipping_address": {
  "first_name": "TESTER",
  "last_name": "MIDTRANSER",
  "email": "test@midtrans.com",
  "phone": "081 2233 44-55",
  "address": "Sudirman",
  "city": "Jakarta",
  "postal_code": "12190",
  "country_code": "IDN"
}
```

| Parameter                                   | Description |
| ------------------------------------------- | ----------- |
| first\_name  <br /> String(255) (optional)  |             |
| last\_name  <br /> String(255) (optional)   |             |
| email  <br /> String(255) (optional)        |             |
| phone  <br /> String(255) (optional)        |             |
| address  <br /> String(255) (optional)      |             |
| country\_code  <br /> String(10) (optional) |             |
| postal\_code  <br /> String(10) (optional)  |             |
| city  <br /> String(100) (optional)         |             |

<br />

***

<br />

## Credit Card Object

<br />

```json
"credit_card": {
  "save_card": true,
  "secure": true,
  "channel": "migs",
  "bank": "maybank",
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
    "41111111",
    "bni"
  ],
  "dynamic_descriptor": {
    "merchant_name" : "Fuji Apple Inc",
    "city_name": "Jakarta",
    "country_code": "ID"
  }
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
        secure <br /> Boolean (optional)
      </td>

      <td>
        Use 3D-Secure authentication when using credit card. Default: false
      </td>
    </tr>

    <tr>
      <td>
        bank <br /> String (optional)
      </td>

      <td>
        Acquiring bank. Options: `bca`, `bni`, `mandiri`, `cimb`, `bri`, `danamon`, `maybank`, `mega`
      </td>
    </tr>

    <tr>
      <td>
        channel <br /> String (optional)
      </td>

      <td>
        Acquiring channel. Options: `migs`
      </td>
    </tr>

    <tr>
      <td>
        type <br /> String (optional)
      </td>

      <td>
        Credit card transaction type.  Options: `authorize`, `authorize_capture`. Default: "authorize_capture"
      </td>
    </tr>

    <tr>
      <td>
        whitelist_bins <br /> Array (optional)
      </td>

      <td>
        Allowed credit card BIN numbers. The bin value can be either a prefix(upto 8 digits) of card number or the name of a bank, in which case all the cards issued by that bank will be allowed. The supported bank names are `bni` `bca` `mandiri` `cimb` `bri` and `maybank`. Default: allow all cards
      </td>
    </tr>

    <tr>
      <td>
        installment.required <br /> Boolean (optional)
      </td>

      <td>
        Force installment when using credit card. Default: `false`.
        If not forced, installment becomes optional.
      </td>
    </tr>

    <tr>
      <td>
        installment.disabled <br /> Boolean (optional)
      </td>

      <td>
        Disable installment when using credit card. Default: `false`.  
        Use this to hide installment menu on checkout page.
      </td>
    </tr>

    <tr>
      <td>
        installment.terms <br /> Object (optional)
      </td>

      <td>
        Available installment terms
      </td>
    </tr>

    <tr>
      <td>
        dynamic_descriptor.merchant_name <br /> String(25) (optional)
      </td>

      <td>
        First 25 digit on customer's billing statement. Mostly used to show the merchant or product name. Only works for `BNI`.
      </td>
    </tr>

    <tr>
      <td>
        dynamic_descriptor.city_name <br /> String(13) (optional)
      </td>

      <td>
        Next 13 digit on customer's billing statement. It works as secondary metadata on the statement. Mostly used to show city name or region. Only works for `BNI`.
      </td>
    </tr>

    <tr>
      <td>
        dynamic_descriptor.country_code <br /> String(2) (optional)
      </td>

      <td>
        Last 2 digit on customer's billing statement. Mostly used to show country code. The format is ISO 3166-1 alpha-2. Only works for `BNI`.
      </td>
    </tr>
  </tbody>
</Table>

<br />

***

## BCA Virtual Account Object

<br />

```json
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
}
```

| Parameter                                           | Description                                                                     |
| --------------------------------------------------- | ------------------------------------------------------------------------------- |
| va\_number <br /> String (optional)                 | Length should be within 6 to 11.                                                |
| sub\_company\_code <br /> String (optional)         | BCA sub company code directed for this transactions. **NOTE:** Default is 00000 |
| free\_text <br /> [FreeText](#free-text) (optional) |                                                                                 |

<br />

### Free Text

<br />

| Parameter                                                          | Description                |
| ------------------------------------------------------------------ | -------------------------- |
| inquiry <br /> Array of [FreeTextItem](#free-text-item) (optional) | Size should not exceed 10. |
| payment <br /> Array of [FreeTextItem](#free-text-item) (optional) | Size should not exceed 10. |

<br />

### Free Text Item

<br />

| Parameter                   | Description                      |
| --------------------------- | -------------------------------- |
| en <br /> String (required) | Size should not exceed 50 chars. |
| id <br /> String (required) | Size should not exceed 50 chars. |

<br />

***

<br />

## Permata Virtual Account Object

<br />

```json
"permata_va": {
  "va_number": "1234567890",
  "recipient_name": "SUDARSONO"
}
```

| Parameter                                | Description                                                                                                                                                                             |
| ---------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| va\_number <br /> String (optional)      | Length should be 10. Only supported for b2b transactions.                                                                                                                               |
| recipient\_name <br /> String (optional) | Recipient name shown on the on the bank's payment prompt. It is shown as 20 character uppercase string. Anyting over 20 character will be truncated. **NOTE:** Default is merchant name |

<br />

***

<br />

## BNI Virtual Account Object

<br />

```json
"bni_va": {
  "va_number": "12345678"
}
```

| Parameter                           | Description                     |
| ----------------------------------- | ------------------------------- |
| va\_number <br /> String (optional) | Length should be within 1 to 8. |

<br />

***

<br />

## Mandiri Bill Object

<br />

```json JSON
    "echannel" : {
        "bill_info1" : "Payment:",
        "bill_info2" : "Grocery Items",
    }
```

| JSON Attribute | Description                                                                                         | Type        | Required |
| -------------- | --------------------------------------------------------------------------------------------------- | ----------- | -------- |
| bill\_info1    | Label 1. Mandiri allows only *10 characters*. Exceeding characters will be **truncated**.           | String(255) | Optional |
| bill\_info2    | Value for Label 1. Mandiri allows only *30 characters*. Exceeding characters will be **truncated**. | String(255) | Optional |

***

<br />

## BRI Virtual Account Object

<br />

```json
"bri_va": {
  "va_number": "12345678"
}
```

| Parameter                           | Description                      |
| ----------------------------------- | -------------------------------- |
| va\_number <br /> String (optional) | Length should be within 1 to 13. |

<br />

***

<br />

## CIMB Virtual Account Object

<br />

```json
"cimb_va": {
  "va_number": "12345678"
}
```

| Parameter                           | Description                      |
| ----------------------------------- | -------------------------------- |
| va\_number <br /> String (optional) | Length should be within 1 to 12. |

<br />

***

## Danamon Virtual Account Object

```json
"danamon_va": {
  "va_number": "123456789012"
}
```

| Parameter                           | Description                      |
| ----------------------------------- | -------------------------------- |
| va\_number <br /> String (optional) | Length should be within 1 to 12. |

***

<br />

## BSI Virtual Account Object

```json
"bsi_va": {
  "va_number": "123456789012"
}
```

| Parameter                           | Description                      |
| ----------------------------------- | -------------------------------- |
| va\_number <br /> String (optional) | Length should be within 1 to 12. |

<br />

***

## SeaBank Virtual Account Object

```json
"seabank_va": {
  "va_number": "1234567890123456789"
}
```

| Parameter                           | Description                      |
| ----------------------------------- | -------------------------------- |
| va\_number <br /> String (optional) | Length should be within 1 to 19. |

<br />

***

<br />

## GoPay Object

<br />

```json
"gopay": {
  "enable_callback": true,
  "callback_url": "http://gopay.com",
  "tokenization": true,
  "enforce_tokenization": true,
  "phone_number": "8123456789",
  "country_code": "62"
}
```

| Parameter                                       | Description                                                                                                                                                                                             |
| ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| enable\_callback <br /> Boolean (optional)      | Enable redirect back to merchant from GoJek apps. Default: false                                                                                                                                        |
| callback\_url <br /> String (optional)          | Determine where should customer be redirected from GoJek apps. It supports both HTTP and deeplink. Default: same value as finish url                                                                    |
| tokenization <br /> Boolean (optional)          | Determine whether GoPay Tokenization feature is enabled or not. Default: false                                                                                                                          |
| enforce\_tokenization <br /> Boolean (optional) | When set to true, the fallback mechanism for GoPay tokenization is disabled. The transaction must be completed using the tokenization flow, unless multiple payment methods are enabled. Default: false |
| phone\_number <br /> String (optional)          | Determine the phone number that will be used on gopay tokenization. Default: null                                                                                                                       |
| country\_code <br /> String (optional)          | Determine the country code that will be used on gopay tokenization. Default: same value as finish url. Default: null                                                                                    |

<br />

***

<br />

## ShopeePay Object

<br />

```json
"shopeepay": {
  "callback_url": "http://midtrans.com/finish-url?order_id=order-123"
}
```

| Parameter                              | Description                                                                                                                                                                                                                                    |
| -------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| callback\_url <br /> String (optional) | The URL to redirect the customer back from the ShopeePay app. It supports both HTTP and deeplink. Default: same value as [finish url](#callbacks-object). If it's also empty, value is the finish URL and configured on your Snap Preferences. |

<br />

***

<br />

## Cstore (Over the Counter) Object

<br />

```json
"cstore": {
  "alfamart_free_text_1" : "qwerty",
  "alfamart_free_text_2" : "asdfg",
  "alfamart_free_text_3" : "zxcvb"
}
```

| Parameter                                            | Description                               |
| ---------------------------------------------------- | ----------------------------------------- |
| alfamart\_free\_text\_1 <br /> String(40) (optional) | First row of printed receipt description  |
| alfamart\_free\_text\_2 <br />String(40) (optional)  | Second row of printed receipt description |
| alfamart\_free\_text\_3 <br /> String(40) (optional) | Third row of printed receipt description  |

*Note* : Indomaret doesn't use Cstore object.

<br />

***

<br />

## Callbacks Object

<br />

```json
"callbacks": {
    "finish" : "https://example.com/",
    "error": "https://example1.com"
}
```

| Parameter                                       | Description                                                                                                                                                                                                                                                           |
| ----------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| finish	           <br /> String(255) (optional) | Redirect URL after transaction is successfully paid. Applicable for all payments that will redirect from payment partner app/web back to Midtrans. Can also be set via Snap Settings menu in your dashboard. For GoPay, use the finish parameter in the GoPay object. |
| error	           <br /> String(255)(optional)   | Redirect URL after transaction failed to be paid by customer. Applicable for all payments that will redirect from payment partner app/web back to Midtrans (except for BNPL and GoPay payment method). Can also be set via Snap Settings menu in your dashboard.      |

<br />

***

<br />

## Expiry Object

<br />

```json
"expiry":  {
  "start_time": "2018-12-13 18:11:08 +0700",
  "unit": "minutes",
  "duration": 1
}
```

| Parameter                                     | Description                                                                                                                       |
| --------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| start\_time <br /> String(255) (optional)     | Timestamp in `yyyy-MM-dd HH:mm:ss Z` format. If not specified, transaction time will be used as start time (when customer charge) |
| duration <br /> Integer (required for expiry) | Expiry duration                                                                                                                   |
| unit <br /> String (required for expiry)      | Expiry unit. Options: `day`, `hour`, `minute` (plural term also accepted)                                                         |

<br />

<Callout icon="🚧" theme="warn">
  * If this parameter is not sent, the default expiry will use expiry setting on Snap preferences on merchant dashboard. Furthermore, if only `unit` and `duration` is given, `start_time` will equal the timestamp of the transaction time (when customer charge).* The Maximum expiry for the Snap token is 7 days. If the expiry sent is more than 7 days after the token is created. The Snap token will still expire 7 days after creation.* The minimum expiry for the Snap token is 20 seconds. If the expiry sent is less than 20 seconds. The Snap will respond to validation errors.* See [this guide](/reference/expire-a-snap-session) for more details.
</Callout>

<br />

## Page Expiry Object

<br />

```json JSON Parameters
...
"page_expiry": {
    "duration": 3,
    "unit": "hours"
}
...
```

| Parameter  | Description                                                             | Type    | Required |
| ---------- | ----------------------------------------------------------------------- | ------- | -------- |
| `duration` | Page expiry duration in numbers                                         | Integer | Required |
| `unit`     | Expiry unit. Options: `day, hour, minute` (plural terms also accepted). | String  | Required |

<br />

Note :\
If not specified, default is 24 hours. See [this guide](/reference/expire-a-snap-session) for more details.

<br />

## Recurring/Subscription Object

<br />

Use this object to show a dedicated recurring flow UI in Snap - differences include card will be automatically saved without having user manually tick the checkbox and adjusted copy to better suit recurring payments. Snap will then return the information passed here back in HTTP notification, for you to utilize when calling the [Subscription API](/reference/api-methods-1).

Use this object in conjunction with Subscription API - add this object to alter the Snap customer UI, then convert the transaction to recurring payments using Subscription API. Make sure to also have the prerequisites to accept Subscription (e.g. [One Click feature](/reference/one-click)) - otherwise transactions might fail.

Note that if you do choose to pass the `start_time` and `interval_unit` within the object, make sure to use the same information when calling the Subscription API - otherwise, information presented to user and actual subscription charge schedule will be different, which might result in chargeback.

<br />

```json JSON Parameters
...
"recurring": {
    "required": true,
    "start_time": "2024-06-09 15:07:00 +0700",
    "interval_unit": "week"
}
...
```

| Parameter       | Description                                                                                                               | Type    | Required                                 |
| --------------- | ------------------------------------------------------------------------------------------------------------------------- | ------- | ---------------------------------------- |
| `required`      | Specify the intent whether payment will be utilizing recurring payments or not.                                           | Integer | Required (if recurring object is passed) |
| `start_time`    | Start of the subscription schedule. Passed information will be shown in Snap Checkout UI & returned in HTTP Notification. | String  | Optional                                 |
| `interval_unit` | Subscription charge internal unit                                                                                         | String  | Optional                                 |