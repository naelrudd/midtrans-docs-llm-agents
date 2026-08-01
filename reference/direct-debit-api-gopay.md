---
updatedAt: 2026-04-21T06:30:50.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Payment Method: GoPay/ShopeePay/Dana

> 📘 GoPay Media Kit
>
> To have a consistent and standardized GoPay branding across platform, we highly recommend merchants to refer to our media kit. Please refer to this page <https://gopay.co.id/media-kit> to access our brand guideline and image bank.

This section will explain how merchants can initiate GoPay deeplink transactions using SNAP-based CoreAPI specification.

## 1. Access Token B2B

| Path              | /\{version}/access-token/b2b |
| :---------------- | :--------------------------- |
| SNAP service code | 73                           |
| HTTP Method       | POST                         |
| Version           | v1.0                         |

<br />

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
      Created using asymmetric signature SHA256withRSA algorithm
    </td>
  </tr>

  <tr>
    <td>
      X-CLIENT-KEY
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Client’s client\_id (PJP Name) (given at completion registration process).
    </td>
  </tr>
</table>

```
Content-type: application/json
X-TIMESTAMP: 2024-03-19T14:30:00+07:00
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
X-CLIENT-KEY:962489e9-de5d-4eb7-92a4-b07d44d64bf4 
```

<br />

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
      grantType
    </td>

    <td>
      String(64)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      client\_credentials: The client can request an access token using only its client credentials (or other supported means of authentication) when the client is requesting access to the protected resources under its control (OAuth 2.0: RFC 6749 & 6750)
    </td>
  </tr>
</table>

```
{
   "grantType":"client_credentials"
}
```

<br />

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
Content-type:application/json
X-TIMESTAMP:2024-03-19T14:30:00+07:00
```

<br />

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
      String(7)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Error code to specify the error returned
    </td>
  </tr>

  <tr>
    <td>
      responseMessage
    </td>

    <td>
      String(150)
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
      accessToken
    </td>

    <td>
      String(2048)
    </td>

    <td>
      C
    </td>

    <td colspan="2">
      A string representing an authorization issued to the client that used to access protected resources
    </td>
  </tr>

  <tr>
    <td>
      tokenType
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      The access token type provides the client with the information required to successfully utilize the access token to make a protected resource request
    </td>
  </tr>

  <tr>
    <td>
      expiresIn
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Time duration when the accessToken will be expired. (default in second).
    </td>
  </tr>
</table>

```
{
   "responseCode":"2007400",
   "responseMessage":"Successful",
  "accessToken":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIyMTFlZThiMi1hN2FlLTRhZGUtYmJlYS1mNzI3MDk3ZmQ0NmEiLCJjbGllbnRJZCI6IjZhZTk1N2M0LTI4NjMtNDcxMy1hY2NlLWJhMTJkZTYzNmNmYyIsIm5iZiI6MTYxMTQ2ODk3OCwiZXhwIjoxNjExNDY5ODc4LCJpYXQiOjE2MTE0Njg5Nzh9.KM7yz9GvuUaDR1bXwei4iO0h4e3g4o1Hct5Ie9VoBdo",
   "tokenType":"Bearer",
   "expiresIn":"900"
}
```

<br />

### Response Body Error Case

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
      String(7)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Error code to specify the error returned
    </td>
  </tr>

  <tr>
    <td>
      responseMessage
    </td>

    <td>
      String(150)
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
      String
    </td>

    <td>
      C
    </td>

    <td colspan="2">
      Debug id to provide more information.
    </td>
  </tr>
</table>

```
{
   "responseCode":"5007300",
   "responseMessage":"Timeout",
   "referenceNo":"19352694-0ef6-4439-8ad1-b1dfb8bbb85f"
}
```

<br />

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
      2007300
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
      4017300
    </td>

    <td>
      401
    </td>

    <td>
      Unauthorized. Signature
    </td>
  </tr>

  <tr>
    <td>
      5007300
    </td>

    <td>
      500
    </td>

    <td>
      Internal Server Error
    </td>
  </tr>
</table>

<br />

# 2. Creating GoPay/ShopeePay/Dana deeplink transaction

![](https://files.readme.io/41f1a02-image.png)

<br />

## GoPay/ShopeePay/Dana deeplink - Direct Debit API

| Path              | /\{version}/debit/payment-host-to-host |
| :---------------- | :------------------------------------- |
| HTTP Method       | POST                                   |
| Version           | v1.0                                   |
| SNAP service code | 54                                     |

<br />

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
      Represents access\_token of a request; string starts with keyword “Bearer ” followed by access\_token. Can get this from Access Token B2B API response.
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
      Unique identifier for partner
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
      Alphanumeric string. Preferably UUID.
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
Content-type: application/json
X-TIMESTAMP: 2024-03-19T14:30:00+07:00
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
Authorization: Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
X-PARTNER-ID: BMRI
X-EXTERNAL-ID: 12345678901234567890
CHANNEL-ID: 12345
```

<br />

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
      String(64)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Merchant order id. <br /><b>Note:</b> Allowed Symbols are dash(-), underscore(\_), tilde (\~), and dot (.). Any request containing unauthorized symbols will be automatically declined.

      <p>
        Only used for debugging purpose in server side
      </p>
    </td>
  </tr>

  <tr>
    <td>
      chargeToken
    </td>

    <td>
      String(40)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Authorization token. Same as the Authorization header.
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
      O
    </td>

    <td colspan="2">
      Merchant identifier that is unique per each merchant
    </td>
  </tr>

  <tr>
    <td>
      validUpTo
    </td>

    <td>
      String(25)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      The time when the payment will be automatically expired. The format is defined by ISO 8601.

      <p>
        (Minimum value : 20 second, default value : 15 min)
      </p>

      Maximum value for gopay: 180 days from trx time,\
      Maximum value for shopeepay: 5 days from trx time

      Maximum value for dana: 1 days from trx time
    </td>
  </tr>

  <tr>
    <td>
      urlParams
    </td>

    <td>
      Array of Object
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Merchant redirect URL. After completing payment, user will be redirected back to this URL.

      if it's not provided, the system will fallback to using the callback url from the dashboard configuration. In case the Midtrans dashboard configuration value is also unavailable, the system will return an error.
    </td>
  </tr>

  <tr>
    <td>
      urlParams.url
    </td>

    <td>
      String(512)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      URL value
    </td>
  </tr>

  <tr>
    <td>
      urlParams.type
    </td>

    <td>
      String(32)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      URL type\
      Possible value : PAY\_RETURN
    </td>
  </tr>

  <tr>
    <td>
      urlParams.isDeeplink
    </td>

    <td>
      String(1)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      This parameter defines the type of URL to use. Set it to "<b>Y</b>" for a deeplink, or choose "<b>N</b>" if you prefer a standard URL (HTTP/HTTPS)

      <p>
        Possible Value: Y, N
      </p>
    </td>
  </tr>

  <tr>
    <td>
      payOptionDetails
    </td>

    <td>
      Array of Object
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Payment option that will be used for this payment.
    </td>
  </tr>

  <tr>
    <td>
      payOptionDetails.payMethod
    </td>

    <td>
      String(64)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Payment method for the transaction.

      Possible value : GOPAY, SHOPEEPAY, DANA
    </td>
  </tr>

  <tr>
    <td>
      payOptionDetails.payOption
    </td>

    <td>
      String(64)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Payment option which shows the provider of this payment

      Possible value : GOPAY, SHOPEEPAY, DANA
    </td>
  </tr>

  <tr>
    <td>
      payOptionDetails.transAmount
    </td>

    <td>
      Object
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Payment Transaction Amount
    </td>
  </tr>

  <tr>
    <td>
      payOptionDetails.transAmount.value
    </td>

    <td>
      String(ISO 4217)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Transaction amount that will be paid using this payment method. If it's IDR then value includes 2 decimal digits.

      <p>
        e.g. IDR 10.000 will be placed as 10000.00
      </p>

      <p>
        Minimum value: 1.00
      </p>

      <p>
        Maximum value : 99999999999.00
      </p>
    </td>
  </tr>

  <tr>
    <td>
      payOptionDetails.transAmount.currency
    </td>

    <td>
      String(3)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Transaction currency that will be paid using this payment method.

      Possible Value: IDR
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
      Additional information field which merchants need to pass to support current API contracts.
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
      Customer Detail Information
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
      Customer Phone number
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
      Customer First Name
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
      Customer Last Name
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
      Customer billing address
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
      Billing address phone
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
      Customer shipping address
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
      Shipping address phone
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
      additionalInfo.items
    </td>

    <td>
      Array Of Object
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Item Details
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.items.id
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
      additionalInfo.items.price
    </td>

    <td>
      Object
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Price of the item in IDR.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.items.price.value
    </td>

    <td>
      String (ISO4217)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Item Price value
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.items.price.currency
    </td>

    <td>
      String(3)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Item Price currency
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.items.quantity
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Quantity of the item purchased by the customer.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.items.name
    </td>

    <td>
      String(64)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Name of the item.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.items.merchantName
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
      additionalInfo.items.brand
    </td>

    <td>
      String(64)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Brand name of the item.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.items.category
    </td>

    <td>
      String(64)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Category of the item.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.items.url
    </td>

    <td>
      String(64)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      HTTP URL of the item in the merchant site
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.metadata
    </td>

    <td>
      Object
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Transaction metadata
    </td>
  </tr>
</table>

```
{
 "partnerReferenceNo": "merchant-order-id",
 "chargeToken": "accessToken",
 "merchantId": "G169749203",
 "urlParams": [{
   "url": "merchantapp://payments/callback/12345",
   "type": "PAY_RETURN",
   "isDeeplink": "Y"
 }],
 "validUpTo": "2023-09-24T20:34:15.452305Z",
 "payOptionDetails": [
   {
     "payMethod": "GOPAY" or "DANA" or "SHOPEEPAY",
     "payOption": "GOPAY" or "DANA" or "SHOPEEPAY",
     "transAmount": {
       "value": "12345678.00",
       "currency": "IDR"
     }
   }
 ],
 "additionalInfo": {
   "customerDetails": {
     "phone": "080123456789",
     "firstName": "john",
     "lastName": "doe",
     "email": "john.doe@email.com",
     "billingAddress": {
       "firstName": "john",
       "lastName": "doe",
       "phone": "080123456789",
       "address": "jalan maju mundur",
       "city": "jakarta",
       "postalCode": "12345",
       "countryCode": "IDN"
     },
     "shippingAddress": {
       "firstName": "john",
       "lastName": "doe",
       "phone": "080123456789",
       "address": "jalan maju mundur",
       "city": "jakarta",
       "postalCode": "12345",
       "countryCode": "IDN"
     }
   },
   "items": [
     {
       "id": "ID012345",
       "price":  {
         "value": "12345678.00",
         "currency": "IDR"
       },
       "quantity":"1",
       "name": "someItemName",
       "brand": "someBrand",
       "category": "someCategory",
       "merchantName": "someMerchant",
       "url": "someItemUrl"
     }
   ],
   "metadata": {}
 }
}
```

<br />

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
Content-type:application/json
X-TIMESTAMP:2024-03-19T14:30:00+07:00
```

<br />

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
      String(7)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Status code of transaction charge result.
    </td>
  </tr>

  <tr>
    <td>
      responseMessage
    </td>

    <td>
      String(150)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Description of transaction charge result.
    </td>
  </tr>

  <tr>
    <td>
      referenceNo
    </td>

    <td>
      String(256)
    </td>

    <td>
      C
    </td>

    <td colspan="2">
      Transaction identifier on service provider system. The field is filled upon successful transaction
    </td>
  </tr>

  <tr>
    <td>
      partnerReferenceNo
    </td>

    <td>
      String(64)
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
      appRedirectUrl
    </td>

    <td>
      String(2048)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Reserved for future purposes.
    </td>
  </tr>

  <tr>
    <td>
      webRedirectUrl
    </td>

    <td>
      String(2048)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Returns a universal link to the PJP AIS payment page. This link is recommended when the Client is unable to implement a check for whether the PJP AIS app is installed on the user's device before redirection.
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
      additionalInfo.gross\_amount
    </td>

    <td>
      Object
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Transaction amount that will be paid using this payment method. The format defined by ISO 4217.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.gross\_amount.value
    </td>

    <td>
      String (ISO4217)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Gross amount value
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.gross\_amount.currency
    </td>

    <td>
      String(3)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Gross amount currency
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.paymentType
    </td>

    <td>
      String(64)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Transaction payment method
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.transactionTime
    </td>

    <td>
      String(ISO 8601)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Timestamp of transaction in ISO 8601 format using GMT+7.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.validUpTo
    </td>

    <td>
      String(ISO 8601)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      The time when the payment will be automatically expired. Using ISO 8601 format
    </td>
  </tr>
</table>

```
{
 "responseCode":"2005400",
 "responseMessage":"Successful",
 "referenceNo":"GOPAY012345678",
 "partnerReferenceNo":"merchant-order-id",
 "webRedirectUrl":"https://some-url.for/redirect-to-gopay-app",
 "appRedirectUrl":""
 "additionalInfo":{
   "paymentType": "GOPAY",
   "grossAmount":{
     "value": "12345678.00",
     "currency": "IDR"
   },
   "transactionTime":"2023-09-25T02:59:19.517854Z",
   "validUpTo":"2023-09-26T02:59:19Z"
 }
```

<br />

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
      4005402
    </td>

    <td>
      400
    </td>

    <td>
      Invalid Mandatory Field chargeToken , partnerReferenceNo
    </td>
  </tr>

  <tr>
    <td>
      4015400
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
      4015401
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
      4015402
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
      4035403
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
      4035414
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
      4035415
    </td>

    <td>
      403
    </td>

    <td>
      Transaction Not Permitted. Url not whitelisted.
    </td>
  </tr>

  <tr>
    <td>
      5005401
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
      5045400
    </td>

    <td>
      504
    </td>

    <td>
      Timeout
    </td>
  </tr>
</table>

<br />

# Additional APIs

1. [Refund API](https://docs.midtrans.com/reference/refund-api)
2. [Cancel API](https://docs.midtrans.com/reference/cancel-api)
3. [Get Transaction Status API](https://docs.midtrans.com/reference/get-transaction-status-api)
4. [Payment Notification API](https://docs.midtrans.com/reference/payment-notification-api)