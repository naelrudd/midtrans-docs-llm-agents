---
updatedAt: 2026-04-21T06:33:07.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Payment Method: GoPay Tokenization (Pre Auth)

<Callout icon="📘" theme="info">
  Merchant can now test CoreAPI BI-SNAP flow on Sandbox!

  For more details, go [here](https://docs.midtrans.com/reference/testing-bi-snap-on-sandbox-environment).

  This new sandbox will be rolled out to all merchant from **October 22nd, 2024**. Please contact your sales representative for early access.
</Callout>

<br />

> 📘 GoPay Media Kit
>
> To have a consistent and standardized GoPay branding across platform, we highly recommend merchants to refer to our media kit. Please refer to this page <https://gopay.co.id/media-kit> to access our brand guideline and image bank.

This section will explain how merchant can initiate GoPay Tokenization (Pre-Auth) transactions using SNAP-based CoreAPI specification.

1. In order to do GoPay Tokenization transaction, merchant should link the customer's GoPay account first by initiating the [Account Linking API](https://docs.midtrans.com/reference/account-linking-api).
2. Once linked, merchant can reserve user's balance by initiating auth payment (auth API)
3. To actually deduct user's balance merchant will need to capture the authorized transaction (capture API)
4. If merchant wants to release user's balance without actually deduct the balance, merchant will need to void the transaction by calling Void API. Authorized transaction that is not captured after its expiry time will be auto canceled.
5. Merchant can also do other subsequent actions such as Refund, and Get Status.

<Callout icon="📘" theme="info">
  Currently GoPay Tokenization pre-auth only supports No PIN transaction. Please contact your Midtrans sales representative to enable pre-auth transaction.
</Callout>

<Callout icon="📘" theme="info">
  GoPay Tokenization in BI-SNAP flow can also support both GoPay & GoPay Later payment. Merchant should pass the corresponding payment option token as **payOptionDetails.additionalInfo.paymentoptiontoken** in the request body. The payment option token can be retrieved from [Binding Inquiry API](https://docs.midtrans.com/reference/binding-inquiry-api).
</Callout>

# Creating GoPay Tokenization Pre-Auth transaction

<Image align="center" src="https://files.readme.io/afd0c92-SNAP_based_account_linking_flow-tokenization_preauth.drawio.png" />

## Reserving user's balance - Auth Payment API

This section describes how merchants can reserve user's balance without actually deducting it from the start by calling Auth Payment API.

| Path              | /\{version}/auth/payment |
| :---------------- | :----------------------- |
| HTTP Method       | POST                     |
| Version           | v1.0                     |
| SNAP service code | 63                       |

### Request Header

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td colspan="2">
      <strong>Field Description</strong>
    </td>
  </tr>

  <tr>
    <td>
      Content-type
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Media type of the resource, i.e. application/json
    </td>
  </tr>

  <tr>
    <td>
      X-TIMESTAMP
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Client’s current local time in ISO-8601 format
    </td>
  </tr>

  <tr>
    <td>
      X-SIGNATURE
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Created using symmetric signature HMAC\_SHA512 algorithm
    </td>
  </tr>

  <tr>
    <td>
      Authorization
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Represents access\_token of a request; string starts with keyword “Bearer ” followed by access\_token. Can get this token from Access Token B2B API response.
    </td>
  </tr>

  <tr>
    <td>
      Authorization-Customer
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      accessToken which Gopay will be sharing once linking is complete. string starts with keyword “Bearer ”followed by access\_token.
    </td>
  </tr>

  <tr>
    <td>
      X-PARTNER-ID
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Unique identifier for caller
    </td>
  </tr>

  <tr>
    <td>
      X-EXTERNAL-ID
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Alphanumeric string. We suggest merchant to use UUID format. The value should be unique. <br /> In case of timeout, merchant can do:

      1. Use this value in get status API to get status transaction or <br />
      2. Retry this request with the same X-EXTERNAL-ID and request body to avoid creating duplicate transaction
    </td>
  </tr>

  <tr>
    <td>
      CHANNEL-ID
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Mandatory field from Bank Indonesia that can take any value with correct format 5 digits numeric string
    </td>
  </tr>

  <tr>
    <td>
      X-DEVICE-ID
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Device identification on which the API services are currently being accessed by the end user (customer).

      Sample:\
      Web Application:\
      Mozilla / 5.0(Windows NT 10.0; Win64; x64)AppleWebKit / 537.36(KHTML, like Gecko)Chrome / 75.0.3770.100 Safari / 537.36 OPR / 62.0.3331.99

      Mobile Application:\
      Android: android-20013adf6cdd8123f\
      iOS: 72635bdfd223yvjm7246nsdj34hd4559393kjh42
    </td>
  </tr>
</table>

```
Content-type:application/json
X-TIMESTAMP:2024-03-19T14:30:00+07:00
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
Authorization: Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
Authorization-Customer: Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
X-PARTNER-ID: BMRI
X-DEVICE-ID: 0987ADCASA
X-EXTERNAL-ID:12345678901234567890
CHANNEL-ID:12345
```

### Request Body

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td colspan="2">
      <strong>Field Description</strong>
    </td>
  </tr>

  <tr>
    <td>
      partnerReferenceNo
    </td>

    <td>
      String (64)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Merchant order-id.<br /><b>Note:</b> Allowed Symbols are dash(-), underscore(\_), tilde (\~), and dot (.). Any request containing unauthorized symbols will be automatically declined.

      <p>
        Only used for debugging purposes on the server side.
      </p>
    </td>
  </tr>

  <tr>
    <td>
      merchantId
    </td>

    <td>
      String(64)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Merchant’s unique ID provided by Midtrans.
    </td>
  </tr>

  <tr>
    <td>
      amount
    </td>

    <td>
      Object
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Transaction amount
    </td>
  </tr>

  <tr>
    <td>
      amount.value
    </td>

    <td>
      String (ISO4217)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Net amount of the transaction. If it's IDR then value includes 2 decimal digits. e.g. IDR 10.000,- will be placed with 10000.00
    </td>
  </tr>

  <tr>
    <td>
      amount.currency
    </td>

    <td>
      String(3)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Currency
    </td>
  </tr>

  <tr>
    <td>
      title
    </td>

    <td>
      String(256)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Order title
    </td>
  </tr>

  <tr>
    <td>
      items
    </td>

    <td>
      Array of Object
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Item details
    </td>
  </tr>

  <tr>
    <td>
      items.id
    </td>

    <td>
      String(32)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Item ID
    </td>
  </tr>

  <tr>
    <td>
      items.price
    </td>

    <td>
      Object
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Price of the item
    </td>
  </tr>

  <tr>
    <td>
      items.price.value
    </td>

    <td>
      String (ISO4217)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Item price value
    </td>
  </tr>

  <tr>
    <td>
      items.price.currency
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Item price currency
    </td>
  </tr>

  <tr>
    <td>
      items.quantity
    </td>

    <td>
      String(16)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Item quantity
    </td>
  </tr>

  <tr>
    <td>
      items.name
    </td>

    <td>
      String(64)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Item name
    </td>
  </tr>

  <tr>
    <td>
      items.brand
    </td>

    <td>
      String(64)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Brand name of the item
    </td>
  </tr>

  <tr>
    <td>
      items.category
    </td>

    <td>
      String(64)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Category of the item
    </td>
  </tr>

  <tr>
    <td>
      items.merchantName
    </td>

    <td>
      String(64)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Name of the merchant selling the item.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo
    </td>

    <td>
      Object
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Additional Information
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.merchantCrossReferenceId
    </td>

    <td>
      String (64)
    </td>

    <td>
      C
    </td>

    <td colspan="2">
      Merchant cross reference id (payment flow identifier). Will be <b>mandatory</b> for Midtrans merchants with custom integration. Midtrans team will let you know when you need to pass this indentifier.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.payOptionDetails.payOption
    </td>

    <td>
      String (64)
    </td>

    <td>
      C
    </td>

    <td colspan="2">
      Payment option which shows the provider of this payment. This parameter is <b>mandatory</b> unless merchants have custom integration with Midtrans. Midtrans team will let you know if this parameter is optional in the case of custom integration.

      <p>
        Possible value: GOPAY\_WALLET, GOPAY\_WALLET\_POCKET
      </p>
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.payOptionDetails.payMethod
    </td>

    <td>
      String (64)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Possible value: `GOPAY`
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.payOptionDetails.transAmount
    </td>

    <td>
      Object
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Payment transaction amount
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.payOptionDetails.transAmount.value
    </td>

    <td>
      String (16,2)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Transaction amount that will be paid using this payment method If it's IDR then value includes 2 decimal digits.

      <p>
        e.g. IDR 10.000,- will be placed with 10000.00
      </p>
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.payOptionDetails.transAmount.currency
    </td>

    <td>
      String (3)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      IDR
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.payOptionDetails.additionalInfo.paymentOptionToken
    </td>

    <td>
      String
    </td>

    <td>
      C
    </td>

    <td colspan="2">
      Payment option token . This parameter is <b>mandatory</b> unless merchants have custom integration with Midtrans. Midtrans team will let you know if this parameter is optional in the case of custom integration.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails
    </td>

    <td>
      Object
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Customer detail information
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails.phone
    </td>

    <td>
      String(15)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Customer phone number
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails.email
    </td>

    <td>
      String(255)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Customer email
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails.firstName
    </td>

    <td>
      String(255)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Customer first name
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails.lastName
    </td>

    <td>
      String(255)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Customer last name
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails.billingAddress
    </td>

    <td>
      Object
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Billing address information
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails.billingAddress.firstName
    </td>

    <td>
      String(255)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Billing address first name
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails.billingAddress.lastName
    </td>

    <td>
      String(255)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Billing address last name
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails.billingAddress.phone
    </td>

    <td>
      String(15)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Billing address phone number
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails.billingAddress.address
    </td>

    <td>
      String(255)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Billing address detail
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails.billingAddress.city
    </td>

    <td>
      String(255)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Billing address city
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails.billingAddress.postalCode
    </td>

    <td>
      String(255)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Billing address postal code
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails.billingAddress.countryCode
    </td>

    <td>
      String(15)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Billing address country code
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails.shippingAddress
    </td>

    <td>
      Object
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Shipping address information
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails.shippingAddress.firstName
    </td>

    <td>
      String(255)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Shipping address first name
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails.shippingAddress.lastName
    </td>

    <td>
      String(255)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Shipping address last name
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails.shippingAddress.phone
    </td>

    <td>
      String(15)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Shipping address phone number
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails.shippingAddress.address
    </td>

    <td>
      String(255)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Shipping address detail
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails.shippingAddress.city
    </td>

    <td>
      String(255)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Shipping address city
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails.shippingAddress.postalCode
    </td>

    <td>
      String(255)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Shipping address postal code
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customerDetails.shippingAddress.countryCode
    </td>

    <td>
      String(15)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Shipping address country code
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.validUpTo
    </td>

    <td>
      String(25)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      The time when the payment will be automatically expired. Using ISO 8601 format

      <p>
        (Maximum value: 180 days from trx time, Minimum value: 20 second, default value: 7 days)
      </p>
    </td>
  </tr>
</table>

```
{
    "partnerReferenceNo": "merchant-order-id",
    "merchantId": “aMerchantId",
    "amount": {
                "value": "12345678.00",
                "currency": "IDR"
            },
     "items": [
                  {
                          "id": "8za1ieleavwusxn6u5re60ri",
                          "price":  {
                                "value": "12345678.00",
                                "currency": "IDR"
                            },
                          "quantity": “1”,
                          "name": "subscription ",
                          "brand": "brand ",
                          "category": "Subsciption ",
                          "url": "www.google.com ",
                          "merchantName": "amazon prime"
                  }
                 ],
    "additionalInfo": {
    		  "merchantCrossReferenceId": "303b4f89-xxxx-xxxx-xxxx-62a8ffaefaf3",
          "payOptionDetails": [
         {
            "payMethod": "GOPAY",
            "payOption": "GOPAY_WALLET",
            "transAmount": {
                "value": "12345678.00",
                "currency": "IDR"
            },
            "additionalInfo": {
                    "paymentOptionToken": "aGoPayWalletToken / aPayLaterToken"
                }
        }
    ],
          "customerDetail": {
                "phone": "81234532422",
                "firstName": "farz",
                "lastName": "zsasa",
                "email": "something@gmail.com",
                "billingAddress": {
                        "firstName": "billingFirstName",
                        "lastName": "billingLastName",
                        "phone": "billingPhone",
                        "address": "billingAddress",
                        "city": "billingCity",
                        "postalCode": "12790",
                        "countryCode": "CZH"
                 },
                "shippingAddress": {
                        "firstName": "shippingFirstName",
                        "lastName": "shippingLastName",
                        "phone": "shippingPhone",
                        "address": "shippingAddress",
                        "city": "shippingCity",
                        "postalCode": "12790",
                        "countryCode": "CZH"
                 
                 },
            }
        
    }
}
```

### Response Header

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td colspan="2">
      <strong>Field Description</strong>
    </td>
  </tr>

  <tr>
    <td>
      Content-type
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Media type of the resource, i.e. application/json
    </td>
  </tr>

  <tr>
    <td>
      X-TIMESTAMP
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Client’s current local time in ISO-8601 format
    </td>
  </tr>
</table>

```
Content-type: application/json
X-TIMESTAMP: 2024-03-19T14:30:00+07:00
```

### Response Body

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td colspan="2">
      <strong>Field Description</strong>
    </td>
  </tr>

  <tr>
    <td>
      responseCode
    </td>

    <td>
      String (7)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Error code to specify the error returned.
    </td>
  </tr>

  <tr>
    <td>
      responseMessage
    </td>

    <td>
      String (150)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Debug message to provide more information.
    </td>
  </tr>

  <tr>
    <td>
      referenceNo
    </td>

    <td>
      String (256)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Unique transaction identifier from payment provider system e.g : <strong>Gopay order ID. </strong>
    </td>
  </tr>

  <tr>
    <td>
      partnerReferenceNo
    </td>

    <td>
      String (32)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Unique transaction identifier from Merchant (Merchant order ID).
    </td>
  </tr>

  <tr>
    <td>
      paidTime
    </td>

    <td>
      String (25)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Transaction paid time. ISO 8601 YYYY-MM-DDThh:mm:ss
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo
    </td>

    <td>
      Object
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Additional information
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.amount
    </td>

    <td>
      Object
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Transaction Total Amount Object
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.amount.value
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Net amount of the refund. If it's IDR then the value includes 2 decimal digits.

      <p>
        e.g. IDR 10.000,- will be placed with 10000.00
      </p>
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.amount.currency
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Currency
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.transactionTime
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Timestamp of transaction in ISO 8601 format. Time zone: GMT+7.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.transactionStatus
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Status of GoPay transaction.

      <p>
        <strong>Possible Values: </strong>
      </p>

      <ul>
        <li>00 - Success</li>

        <li>01 - Authorize</li>

        <li>04 - Refunded</li>

        <li>05 - Canceled</li>

        <li>06 - Failed</li>
      </ul>
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.fraudStatus
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Fraud status
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.payOptionDetails
    </td>

    <td>
      Array of Object
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Payment option detail
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.payOptionDetails.payMethod
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Gopay
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.payOptionDetails.payOptions
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Gopay payment option used
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.validUpTo
    </td>

    <td>
      String(25)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      The time when the payment will be automatically expired. Using ISO 8601 format
    </td>
  </tr>
</table>

```Text Succesful response
{
   "responseCode":"20054000",
   "responseMessage":"Request has been processed successfully",
   "referenceNo":"Gopay-order-id",
   "partnerReferenceNo":"merchant-order-id",
   "paidTime":"2009-07-03T12:08:56+07:00",
   "additionalInfo":{
      "grossAmount":"10000.00",
      "currency":"IDR" 
      "paymentType":"Gopay",
      "transactionTime":"2024-05-22T07:48:08.56Z",
      "transactionStatus":"settlement"  
      "fraudStatus":"some-fraud-status"  ,
       “payOptionDetails” : [{
            "payMethod":"GOPAY",
            "payOption": "GOPAY_WALLET"
        }], 
     "validUpTo":"2024-05-22T16:00:00.00Z"

   }
}
```
```Text Error response
{
   "responseCode":"4006301",
   "responseMessage":"There is some issue with the transaction request"
}
```

### List of Response code

<table>
  <tr>
    <td>
      <strong>Response Code</strong>
    </td>

    <td>
      <strong>HTTP Status Code</strong>
    </td>

    <td>
      <strong>Response Message</strong>
    </td>
  </tr>

  <tr>
    <td>
      2006300
    </td>

    <td>
      200
    </td>

    <td>
      Success
    </td>
  </tr>

  <tr>
    <td>
      4006302
    </td>

    <td>
      400
    </td>

    <td>
      Invalid Mandatory Field \{Field Name}
    </td>
  </tr>

  <tr>
    <td>
      4016300
    </td>

    <td>
      401
    </td>

    <td>
      Unauthorized. Auth token required
    </td>
  </tr>

  <tr>
    <td>
      4016301
    </td>

    <td>
      401
    </td>

    <td>
      Invalid Token (B2B)
    </td>
  </tr>

  <tr>
    <td>
      4016302
    </td>

    <td>
      401
    </td>

    <td>
      Invalid Customer Token
    </td>
  </tr>

  <tr>
    <td>
      4031003
    </td>

    <td>
      403
    </td>

    <td>
      Suspected Fraud
    </td>
  </tr>

  <tr>
    <td>
      4031014
    </td>

    <td>
      403
    </td>

    <td>
      Insufficient Funds
    </td>
  </tr>

  <tr>
    <td>
      5006301
    </td>

    <td>
      500
    </td>

    <td>
      Internal Server Error
    </td>
  </tr>

  <tr>
    <td>
      5046300
    </td>

    <td>
      504
    </td>

    <td>
      Timeout
    </td>
  </tr>
</table>

***

## Capturing user's balance - Capture API

This section describes how merchants can capture a transaction that has been reserved/authorized and deduct user balance by calling Capture API.

| Path              | /\{version}/auth/capture |
| :---------------- | :----------------------- |
| HTTP Method       | POST                     |
| Version           | v1.0                     |
| SNAP service code | 65                       |

### Request Header

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td colspan="2">
      <strong>Field Description</strong>
    </td>
  </tr>

  <tr>
    <td>
      Content-type
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Media type of the resource, i.e. application/json
    </td>
  </tr>

  <tr>
    <td>
      X-TIMESTAMP
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Client’s current local time in ISO-8601 format
    </td>
  </tr>

  <tr>
    <td>
      X-SIGNATURE
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Created using symmetric signature HMAC\_SHA512 algorithm
    </td>
  </tr>

  <tr>
    <td>
      Authorization
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Represents access\_token of a request; string starts with keyword “Bearer ” followed by access\_token. Can get this token fromAccess Token B2B API response.
    </td>
  </tr>

  <tr>
    <td>
      X-PARTNER-ID
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Unique identifier for caller  (client\_id)
    </td>
  </tr>

  <tr>
    <td>
      X-EXTERNAL-ID
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Alphanumeric string. We suggest merchant to use UUID format. The value should be unique. <br /> In case of timeout, merchant can do:

      1. Use this value in get status API to get status transaction or <br />
      2. Retry this request with the same X-EXTERNAL-ID and request body to avoid creating duplicate transaction
    </td>
  </tr>

  <tr>
    <td>
      CHANNEL-ID
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Mandatory field from Bank Indonesia that can take any value with correct format 5 digits numeric string
    </td>
  </tr>
</table>

```
Content-type:application/json
X-TIMESTAMP:2024-03-19T14:30:00+07:00
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
Authorization: Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
X-PARTNER-ID: BMRI
X-EXTERNAL-ID:12345678901234567890
CHANNEL-ID:12345
```

### Request Body

<table>
  <tr>
    <td>
      originalReferenceNo
    </td>

    <td>
      String(64)
    </td>

    <td>
      C
    </td>

    <td colspan="2">
      Transaction identifier on service provider system. For e.g: GopayOrderId<strong> </strong>

      <p>
        Note: either additionalInfo.originalExternalId or OriginalReferenceNo need to be filled
      </p>

      <p>
        If both fields have value, will use originalReferenceNo as the main identifier.
      </p>
    </td>
  </tr>

  <tr>
    <td>
      originalPartnerReferenceNo
    </td>

    <td>
      String (64)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Merchant order id
    </td>
  </tr>

  <tr>
    <td>
      merchantId
    </td>

    <td>
      String(64)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Merchant’s unique ID provided by Midtrans.
    </td>
  </tr>

  <tr>
    <td>
      partnerCaptureNo
    </td>

    <td>
      String (64)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Capture identifier generated by the partner
    </td>
  </tr>

  <tr>
    <td>
      captureAmount
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Transaction amount that merchant wants to capture. Currently only full capture is supported.
    </td>
  </tr>

  <tr>
    <td>
      captureAmount.value
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Capture amount value
    </td>
  </tr>

  <tr>
    <td>
      captureAmount.currency
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Capture amount currency
    </td>
  </tr>

  <tr>
    <td>
      title
    </td>

    <td>
      String(256)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Order title
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo
    </td>

    <td />

    <td />

    <td colspan="2" />
  </tr>

  <tr>
    <td>
      additionalInfo.originalExternalId
    </td>

    <td>
      String (36)
    </td>

    <td>
      C
    </td>

    <td colspan="2">
      If merchant got a timeout from the auth endpoint, merchant can use this field using the X-EXTERNAL-ID value in the direct debit request header.

      <p>
        Note: either originalExternalId or OriginalReferenceNo need to be filled
      </p>
    </td>
  </tr>
</table>

```
{
    "originalReferenceNo": "2020102900000000000001",
    "originalPartnerReferenceNo": "123123123123",
    "partnerCaptureNo": "asdv-asdasdv-addasd-1231ewqqw-aaaa",
    "merchantId": "merch00001",
    "captureAmount": {
        "value": "12345678.00",
        "currency": "IDR"
    },
    "title": "aTitle",
    "additionalData": {
        "originalExternalId": "aId"
    }
}
```

### Response Header

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td colspan="2">
      <strong>Field Description</strong>
    </td>
  </tr>

  <tr>
    <td>
      Content-type
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Media type of the resource, i.e. application/json
    </td>
  </tr>

  <tr>
    <td>
      X-TIMESTAMP
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Client’s current local time in ISO-8601 format
    </td>
  </tr>
</table>

```
Content-type: application/json
X-TIMESTAMP: 2024-03-19T14:30:00+07:00
```

### Response Body

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td colspan="2">
      <strong>Field Description</strong>
    </td>
  </tr>

  <tr>
    <td>
      responseCode
    </td>

    <td>
      String (7)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Error code to specify the error returned.
    </td>
  </tr>

  <tr>
    <td>
      responseMessage
    </td>

    <td>
      String (150)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Debug message to provide more information.
    </td>
  </tr>

  <tr>
    <td>
      originalReferenceNo
    </td>

    <td>
      String (256)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Transaction identifier on service provider system. For e.g: GopayOrderId
    </td>
  </tr>

  <tr>
    <td>
      originalPartnerReferenceNo
    </td>

    <td>
      String (32)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Transaction identifier on service consumer system
    </td>
  </tr>

  <tr>
    <td>
      captureNo
    </td>

    <td>
      String (64)
    </td>

    <td>
      C
    </td>

    <td colspan="2">
      PJSP's capture identifier. Used to trace the capture when there's any issue occurred.
    </td>
  </tr>

  <tr>
    <td>
      partnerCaptureNo
    </td>

    <td>
      String (64)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Capture identifier generated by the partner
    </td>
  </tr>

  <tr>
    <td>
      captureAmount
    </td>

    <td />

    <td />

    <td colspan="2" />
  </tr>

  <tr>
    <td>
      captureAmount.value
    </td>

    <td>
      String (16,2)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Transaction amount that will be paid using this payment method If it's IDR then value includes 2 decimal digits.

      <p>
        e.g. IDR 10.000,- will be placed with 10000.00
      </p>
    </td>
  </tr>

  <tr>
    <td>
      captureAmount.currency
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Currency For e.g: IDR
    </td>
  </tr>

  <tr>
    <td>
      captureTime
    </td>

    <td>
      String(25)
    </td>

    <td>
      C
    </td>

    <td colspan="2">
      Capture time. Format capture time: (ISO 8601) YYYY-MM-DDThh:mm:ss. Must be filled upon successful transaction
    </td>
  </tr>
</table>

```Text Succesful Response
{
   "responseCode":"20054000",
   "responseMessage":"Successful",
    "originalReferenceNo":"2020102900000000000001",
   "originalPartnerReferenceNo":"123123123123",
   "captureNo":"asdv-asdasdv-addasd-1231ewqqw-aaaa",
   "partnerCaptureNo":"asdv-asdasdv-addasd-1231ewqqw-aaaa",
   "captureAmount":{
  	"value":"12345678.00",
  	"currency":"IDR"
   },
   "captureTime": "2009-07-03T12:08:56+07:00"
}
```
```Text Error Response
{
   "responseCode":"4006501",
   "responseMessage":"There is some issue with the transaction request"
}
```

### List of Response code

<table>
  <tr>
    <td>
      <strong>Response Code</strong>
    </td>

    <td>
      <strong>HTTP Status Code</strong>
    </td>

    <td>
      <strong>Response Message</strong>
    </td>
  </tr>

  <tr>
    <td>
      2006500
    </td>

    <td>
      200
    </td>

    <td>
      Successful
    </td>
  </tr>

  <tr>
    <td>
      4006502
    </td>

    <td>
      400
    </td>

    <td>
      Invalid Mandatory Field `{Field Name}`
    </td>
  </tr>

  <tr>
    <td>
      4016500
    </td>

    <td>
      401
    </td>

    <td>
      Unauthorized. Auth token required
    </td>
  </tr>

  <tr>
    <td>
      4016501
    </td>

    <td>
      401
    </td>

    <td>
      Invalid Token (B2B)
    </td>
  </tr>

  <tr>
    <td>
      4036515
    </td>

    <td>
      403
    </td>

    <td>
      Transaction Not Permitted.\[reason].
    </td>
  </tr>

  <tr>
    <td>
      5006501
    </td>

    <td>
      500
    </td>

    <td>
      Internal Server Error
    </td>
  </tr>

  <tr>
    <td>
      5046500
    </td>

    <td>
      504
    </td>

    <td>
      Timeout
    </td>
  </tr>
</table>

# Additional APIs

1. [Refund API](https://docs.midtrans.com/reference/refund-api)
2. [Cancel API](https://docs.midtrans.com/reference/cancel-api)
3. [Get Transaction Status API](https://docs.midtrans.com/reference/get-transaction-status-api)