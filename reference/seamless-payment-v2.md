---
updatedAt: 2026-07-28T07:06:42.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Seamless Payment (Bi-Snap)

This method explains how merchants can receive payments on the Mini App using the BI-SNAP Core API Redirection Deeplink.

<Anchor label="Payment Video Introduction" target="_blank" href="https://gotocompany.sg.larksuite.com/wiki/WJ5cwejLQiF0Amk66yDll2HJgHg?from=from_copylink">Payment Video Introduction</Anchor>

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        **Integration Needed**
      </th>

      <th style={{ textAlign: "left" }}>
        **Details**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        Mini App Frontend
      </td>

      <td style={{ textAlign: "left" }}>
        Opens the redirection url provided by backend.  
        SDK integration will be available in upcoming version.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Mini App Backend
      </td>

      <td style={{ textAlign: "left" }}>
        Calls GoPay backend to obtain redirection url.
      </td>
    </tr>
  </tbody>
</Table>

# Sequence Diagram:

**Mini app payments Flow diagram**

<Image border={false} src="https://files.readme.io/564666df5cb0f726c95b17adae251f64b289d7aeb39ca0332809d54cdb431632-image.png" />

**1. User Initiate Order**

* The user decides to place an order in the mini app front end process for order.

**2.\[Merchant owned]**

* Merchant mini app frontend to call their own backend to initiate the payment

**Step 3:\[BI-SNAP Core API] Fetch Merchant Access Token**

* In order to initiate order with Super App Backend Merchant access token is needed for verification purposes. This access token can be fetched by  **v1.0/access-token/b2b** \[BI-SNAP Core API]
* The Api returns the access token which can be used for all other payment oriented APIs.
* The contract of the API can be found [here](https://docs.midtrans.com/reference/seamless-payment-v2#1-access-token-b2b)

**Step 4:\[Merchant owned]**

* Merchant mini app frontend to call their backend to initiate the payment

**Step 5:\[BI-SNAP Core API] Payment Host to Host**

* Using Merchant Access token from step 3, Payment Creation with Super App backend can be initiated by **V1.0/debit/payment-host-to-host** \[BI-SNAP Core API]
* The contract of the API can be found [here](https://docs.midtrans.com/reference/seamless-payment-v2#2-payment-host-to-host)
* The merchant payment can be Guest Checkout Payment with Payer information unknown at the point.
* The merchant guest payment should have **additionalInfo.pointOfPurchaseId** which is shared by GoPay upfront.

**Step 6: Super App Payment creation response**

* Super App Backend returns response to the merchant backend with necessary info for payments
  * webRedirectUrl -> Payment deeplink
  * ReferenceNo     -> GoPay Order Id

**Step 7: Merchant payment creation response**

* Merchant Backend returns response to Merchant Frontend with contract owned by Merchant team.

**Step 8: FE Pay**

* The Mini App front end can open the Super App Payment page using the [launchPayment](https://docs.midtrans.com/reference/seamless-payment-v2#3-launch-payment) from step 5.\
  SDK: `MiniAppSDK version: 0.3.19`\
  Gopay App Version - 1.45.0
* Once the payment is completed, the Super App front end automatically redirects to the merchant page with payment status.

**Step 9:\[BI-SNAP Core API] Notify**

* Once the payment is complete. Super App backend will notify the Mini App Backend by **v1.0/debit/notify** \[BI-SNAP Core API]
* The contract for the api can be found [here](https://docs.midtrans.com/reference/seamless-payment-v2#4-notify).

# New GoPay Merchants:

If you have not integrated with GoPay or have integrated without following the **BI-SNAP Core API** convention, the following points apply :

* You must first onboard **BI-SNAP Core API** convention first using this section **Onboard to BI-SNAP Core API**.
* Once the **BI-SNAP Core API** onboarding is complete, you can follow **Existing GoPay Merchant**.

# Existing GoPay Merchants:

If you have already integrated with GoPay and follow the BI-SNAP Core API convention, the following points apply :

* There is no change in the already integrated v1.0/access-token/b2b BI-SNAP Core API.
* For v1.0/debit/payment-host-to-host api, the new field in the existing contract needs to be added under **additionalInfo.pointOfPurchaseId**. The value for this is shared by the GoPay Team.
* There is no change in the already integrated v1.0/debit/notify BI-SNAP Core API.

<br />

***

# 1. Access Token B2B

| Path              | /{version}/access-token/b2b |
| :---------------- | :-------------------------- |
| SNAP service code | 73                          |
| HTTP Method       | POST                        |
| Version           | v1.0                        |

### Request Header

<table>
  <tr>
    <td><strong>Field Name</strong></td>
    <td><strong>Field Type</strong></td>
    <td><strong>Mandatory</strong></td>
    <td colspan="2"><strong>Field Description</strong></td>
  </tr>

  <tr>
    <td>Content-type</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Media type of the resource, i.e. application/json</td>
  </tr>

  <tr>
    <td>X-TIMESTAMP</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Client's current local time in ISO-8601 format</td>
  </tr>

  <tr>
    <td>X-SIGNATURE</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Created using asymmetric signature SHA256withRSA algorithm</td>
  </tr>

  <tr>
    <td>X-CLIENT-KEY</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Client’s client\_id (PJP Name) (given at completion registration process).</td>
  </tr>
</table>

```
Content-type: application/json
X-TIMESTAMP: 2024-03-19T14:30:00+07:00
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
X-CLIENT-KEY:962489e9-de5d-4eb7-92a4-b07d44d64bf4 
```

### Request Body

<table>
  <tr>
    <td><strong>Field Name</strong></td>
    <td><strong>Field Type</strong></td>
    <td><strong>Mandatory</strong></td>
    <td colspan="2"><strong>Field Description</strong></td>
  </tr>

  <tr>
    <td>grantType</td><td>String(64)</td><td>M</td><td colspan="2">client\_credentials: The client can request an access token using only its client credentials (or other supported means of authentication) when the client is requesting access to the protected resources under its control (OAuth 2.0: RFC 6749 & 6750)</td>
  </tr>
</table>

```
{
   "grantType":"client_credentials"
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
    <td>Content-type</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Media type of the resource, i.e. application/json</td>
  </tr>

  <tr>
    <td>X-TIMESTAMP</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Client's current local time in ISO-8601 format</td>
  </tr>
</table>

```
Content-type:application/json
X-TIMESTAMP:2024-03-19T14:30:00+07:00
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
      String(7)
    </td>

    <td>M</td>

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

    <td>M</td>

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

    <td>C</td>

    <td colspan="2">
      A string representing an authorization issued to the client that used to access protected resources
    </td>
  </tr>

  <tr>
    <td>
      tokenType
    </td>

    <td>String</td>
    <td>O</td>

    <td colspan="2">
      The access token type provides the client with the information required to successfully utilize the access token to make a protected resource request
    </td>
  </tr>

  <tr>
    <td>
      expiresIn
    </td>

    <td>String</td>
    <td>O</td>

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

    <td>M</td>

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

    <td>M</td>

    <td colspan="2">
      Debug message to provide more information.
    </td>
  </tr>

  <tr>
    <td>
      referenceNo
    </td>

    <td>String</td>
    <td>C</td>

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
    <td>5007300</td>

    <td>
      500
    </td>

    <td>
      Internal Server Error
    </td>
  </tr>
</table>

<br />

# 2. Payment Host to Host

![](https://files.readme.io/41f1a02-image.png)

Note: This API allows you to create GoPay Payment Deeplink which when triggered correctly user's will be redirected to GoPay Payment Review Page.

## GoPay deeplink - Direct Debit API

| Path              | /{version}/debit/payment-host-to-host |
| :---------------- | :------------------------------------ |
| HTTP Method       | POST                                  |
| Version           | v1.0                                  |
| SNAP service code | 54                                    |

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
    <td>Content-type</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Media type of the resource, i.e. application/json</td>
  </tr>

  <tr>
    <td>X-TIMESTAMP</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Client's current local time in ISO-8601 format</td>
  </tr>

  <tr>
    <td>X-SIGNATURE</td>
    <td>String</td>
    <td>M</td>

    <td colspan="2">
      Created using symmetric signature HMAC\_SHA512 algorithm
    </td>
  </tr>

  <tr>
    <td>
      Authorization
    </td>

    <td>String</td>
    <td>M</td>

    <td colspan="2">
      Represents access\_token of a request; string starts with keyword “Bearer ” followed by access\_token. Can get this from Access Token B2B API response.
    </td>
  </tr>

  <tr>
    <td>
      X-PARTNER-ID
    </td>

    <td>String</td>
    <td>M</td>

    <td colspan="2">
      Unique identifier for partner
    </td>
  </tr>

  <tr>
    <td>
      X-EXTERNAL-ID
    </td>

    <td>String</td>
    <td>M</td>

    <td colspan="2">
      Alphanumeric string. Preferably UUID.  Reference number that should be unique in the same day or 1 day idempotency key
    </td>
  </tr>

  <tr>
    <td>
      CHANNEL-ID
    </td>

    <td>String</td>
    <td>M</td>

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

References on [X-Signature docs](https://docs.midtrans.com/reference/signature-generation-payouts)

### Request Body

<table>
  <tr>
    <td><strong>Field Name</strong></td>
    <td><strong>Field Type</strong></td>
    <td><strong>Mandatory</strong></td>
    <td colspan="2"><strong>Field Description</strong></td>
  </tr>

  <tr>
    <td>partnerReferenceNo</td>
    <td>String(64)</td>
    <td>M</td>
    <td colspan="2">Merchant order id<p>Only used for debugging purpose in server side</p></td>
  </tr>

  <tr>
    <td>chargeToken</td>
    <td>String(40)</td>
    <td>M</td>
    <td colspan="2">Authorization token. Same as the Authorization header.</td>
  </tr>

  <tr>
    <td>merchantId</td>
    <td>String(64)</td>
    <td>O</td>
    <td colspan="2">Merchant identifier that is unique per each merchant</td>
  </tr>

  <tr>
    <td>validUpTo</td>
    <td>String(25)</td>
    <td>O</td>

    <td colspan="2">
      The time when the payment will be automatically expired. The format is defined by ISO 8601. <p>
      (Minimum value : 20 second, default value : 15 min) Maximum value for gopay: 180 days from trx time, </p>
    </td>
  </tr>

  <tr>
    <td>
      urlParam
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
<p>
      For MiniApp-use case, we don't support callback as we redirect back to the miniapp in the previous state </p>
    </td>
  </tr>

  <tr>
    <td>
      urlParam.url
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
      urlParam.type
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
      urlParam.isDeeplink
    </td>

    <td>
      String(1)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      This parameter defines the type of URL to use. Set it to "<b>Y</b>" for a deeplink, or choose "<b>N</b>" if you prefer a standard URL (HTTP/HTTPS)
      <p>  Possible Value: Y, N  </p>
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
      Payment method for the transaction.\
      Possible value : GOPAY
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

      Reserved for future use case.
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
      Transaction amount that will be paid using this payment method. If it's IDR then value includes 2 decimal digits.\
      <p> e.g. IDR 10.000 will be placed as 10000.00  </p>
      <p> Minimum value: 1.00 </p>
      <p> Maximum value : 99999999999.00 </p>
    </td>
  </tr>

  <tr>
    <td>payOptionDetails.transAmount.currency </td>\
    <td>String(3) </td>\
    <td>M </td>

    <td colspan="2">
      Transaction currency that will be paid using this payment method.\
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

  <tr>
    <td>
      additionalInfo.pointOfPurchaseId
    </td>

    <td>
      String
    </td>

    <td>
      C
    </td>

    <td colspan="2">
      PoP (Point of purchase) ID. The value will be provided by GoPay team during onboarding. <br /><br /> If merchant has a GoPay mini app integration, merchant will need to pass the PoP for both the mini app integration as well as the standard GoPay integration. <br /><br /> For example: <br /> Merchant has both mini app and standard integration. <br /> - Merchant should pass mini app PoP ID when creating mini app transaction. <br /> - Merchant should pass standard PoP ID when creating standard transaction.
    </td>
  </tr>
</table>

```
{
 "partnerReferenceNo": "merchant-order-id",
 "chargeToken": "accessToken",
 "merchantId": "G169749203",
 "urlParam": [{
   "url": "merchantapp://payments/callback/12345",
   "type": "PAY_RETURN",
   "isDeeplink": "Y"
 }],
 "validUpTo": "2023-09-24T20:34:15.452305Z",
 "payOptionDetails": [
   {
     "payMethod": "gopay",
     "payOption": "gopay",
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
   "metadata": {},
   "pointOfPurchaseId":"22cc3371-4bba-4ec6-8e0d-62163e130cdc"
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
    <td>Content-type</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Media type of the resource, i.e. application/json</td>
  </tr>

  <tr>
    <td>X-TIMESTAMP</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Client's current local time in ISO-8601 format</td>
  </tr>
</table>

```
Content-type:application/json
X-TIMESTAMP:2024-03-19T14:30:00+07:00
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
      String(7)
    </td>

    <td>M</td>

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

    <td>M</td>

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

    <td>M</td>

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

    <td>M</td>

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

    <td>M</td>

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

# 3. Launch Payment

Note: This is a Frontend SDK required to trigger the payment deeplink from payment host to host. This SDK allows redirection from MiniApp to GoPay Payment Review Page and redirection back to MiniApp

This is the Frontend Payment Response

Sample Request:

```Text Javascript
const webUrl = response.webRedirectUrl;

function convertToGoPayDeepLink(url) {
    const urlObj = new URL(url);
    const params = urlObj.search;
    return `gopay://merchanttransfer${params}`;
}
const deepLink = convertToGoPayDeepLink(webUrl);

// Assign to params object
var params = {
  deeplink: deepLink
};

window.gpContainer.call(  
  "GP",  
  "launchPayment",  
  params,  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/list-of-jssdks-webview-v4/#error-codes))

```Text JSON
{
    success: true,
    data: {
        status: "success"
    },
		"ret": "GP_SUCCESS"
}
```

```Text JSON
{
    "success": false,
    "error_code": "300",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "Permission denied",
    "ret": "GP_EXCEPTION"   
}
```

| Status    | Description                                                                |
| :-------- | :------------------------------------------------------------------------- |
| success   | User have successfully paid the transaction                                |
| failed    | User cancelled the transaction                                             |
| pending   | There's an error processing the transaction                                |
| cancelled | User goes back to the miniapp without completing or cancelling the payment |

<br />

# 4. Notify

Note: This is the Backend API required to retrieve the payment response.

In the SNAP-based Core API flow, Midtrans will call Payment Notification API on the merchant side to send payment notifications. Merchant should implement this Payment Notification API as stated in the contract below.

<Callout icon="📘" theme="info">
  ###

  Midtrans will generate a pair of **private and public key** for signature generation and share the public key to merchant. Merchant will then need to give Midtrans a **partner id** that will be used in request header as **X-PARTNER-ID**.
</Callout>

<Callout icon="🚧" theme="warn">
  ###

  Please make sure to whitelist this set of IPs to be able to accept notification from Midtrans.

  ```
  <Table align={["left","left"]}>
    <thead>
      <tr>
        <th style={{ textAlign: "left" }}>
          Environment
        </th>
  ```

  ```
      <th style={{ textAlign: "left" }}>
        IPs
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        Staging
      </td>

      <td style={{ textAlign: "left" }}>
        3.1.141.98/32

        52.76.190.190/32

        13.251.192.204/32

        8.215.39.156/32

        8.215.77.79/32

        147.139.213.119/32

        8.215.56.11/32

        8.215.39.87/32

        8.215.42.0/32

        8.215.59.158/32

        149.129.222.246/32

        8.215.26.108/32

        8.215.13.84/32
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Sandbox
      </td>

      <td style={{ textAlign: "left" }}>
        34.142.147.133/32

        34.142.169.131/32

        34.142.231.22/32

        35.240.161.215/32

        34.142.227.232/32

        34.124.184.175/32

        35.197.130.2/32

        34.142.233.114/32

        8.215.26.211/32

        8.215.22.135/32

        8.215.93.92/32

        8.215.93.214/32

        8.215.93.76/32

        8.215.33.37/32

        8.215.26.148/32

        8.215.194.225/32

        8.215.12.199/32

        149.129.255.111/32
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Production
      </td>

      <td style={{ textAlign: "left" }}>
        13.228.166.126/32

        52.220.80.5/32

        3.1.123.95/32

        8.215.30.222/32

        147.139.209.49/32

        8.215.32.142/32

        147.139.163.77/32

        8.215.25.24/32

        8.215.3.193/32

        147.139.210.20/32

        149.129.238.95/32

        8.215.9.206/32

        147.139.134.22/32
      </td>
    </tr>
  </tbody>
  ```

  ```
  </Table>
  ```
</Callout>

<Callout icon="⚠️" theme="warn">
  ### **Notes on Future Compatibility and Best Practices**

  To ensure your integration remains robust and scalable, please be aware that Midtrans **may introduce additional parameters** to the payment notification payload in the future, most likely under the additionalInfo section, but not limited to it. These enhancements are designed to provide greater flexibility and support for evolving business needs.

  To prevent any issues caused by these future changes, we strongly recommend that merchants always perform **signature verification on the entire payload**, rather than validating fields individually. This practice ensures a seamless, secure, and simple implementation that can adapt to future updates without requiring significant changes on your side.
</Callout>

## Receiving payment notifications for GoPay and GoPay Tokenization (non Pre-Auth) transaction

This section will describe how merchant should implement payment notification API for GoPay and GoPay Tokenization (non-Pre Auth) transactions for Midtrans to call.

| Path              | /`{version}`/debit/notify |
| :---------------- | :------------------------ |
| HTTP Method       | POST                      |
| Version           | v1.0                      |
| SNAP Service Code | 56                        |

### Request Header

<table>
  <tr>
    <td><strong>Field Name</strong></td>
    <td><strong>Field Type</strong></td>
    <td><strong>Mandatory</strong></td>
    <td colspan="2"><strong>Field Description</strong></td>
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
      Created using asymmetric signature

      <p>
        Asymmetric-Signature format:
      </p>

      <p>
        SHA256withRSA (privateKey, stringToSign) with
      </p>

      <p>
        stringToSign = HTTPMethod +”:“+ EndpointUrl +":“+ Lowercase(HexEncode(SHA-256(minify(RequestBody)))) + ":“ + TimeStamp
      </p>
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
      Numeric string. Reference number that should be unique in the same day or 1 day idempotency key
    </td>
  </tr>
</table>

```
Content-type:application/json
X-TIMESTAMP:2024-03-19T14:30:00+07:00
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
X-PARTNER-ID: 
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

    <td>
      <strong>Field Description</strong>
    </td>
  </tr>

  <tr>
    <td>
      createdTime
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td>
      Transaction created timestamp
    </td>
  </tr>

  <tr>
    <td>
      latestTransactionStatus
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Latest transaction status

      <p>
        <strong>Possible Values: </strong>
      </p>

      <ul>
        <li>00 - Success</li>

        <li>03 - Pending</li>

        <li>04 - Refunded</li>

        <li>05 - Canceled</li>

        <li>06 - Failure</li>

        <li> 08 - Expiry </li>

        <li> 09 - Rejected</li>
      </ul>
    </td>
  </tr>

  <tr>
    <td>
      originalReferenceNo
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Transaction identifier on service provider system. For e.g: GopayOrderId<strong> </strong>
    </td>
  </tr>

  <tr>
    <td>
      finishedTime
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td>
      Transaction completed timestamp (for latestTranscationStatus = 00)
    </td>
  </tr>

  <tr>
    <td>
      originalPartnerReferenceNo
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td>
      Original transaction identifier on service consumer system. (Merchant’s orderId)
    </td>
  </tr>

  <tr>
    <td>
      originalExternalId
    </td>

    <td>
      String(36)
    </td>

    <td>
      O
    </td>

    <td>
      Original External-ID on header message when doing charge (/payment-host-to-host)
    </td>
  </tr>

  <tr>
    <td>
      merchantId
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td>
      Merchant ID
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

    <td>
      Transaction amount
    </td>
  </tr>

  <tr>
    <td>
      amount.value
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Transaction amount
    </td>
  </tr>

  <tr>
    <td>
      amount.currency
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Transaction currency
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

    <td>
      Additional info
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory
    </td>

    <td>
      Array of Object
    </td>

    <td>
      C
    </td>

    <td>
      Array of refund transactions. Only available if transaction status is <code>refund</code>
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundNo
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Unique identifier of refund transaction generated by provider.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundStatus
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Refund status. Possible values:<br />

      * 00 --> Refund success<br />
      * 06 --> Refund failed
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.partnerRefundNo
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Unique identifier of refund transaction generated by client.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundAmount
    </td>

    <td>
      Object
    </td>

    <td>
      M
    </td>

    <td>
      Refund amount
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundAmount.value
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Net amount of the refund. If it's IDR then the value includes 2 decimal digits.

      <p>
        e.g. IDR 10.000,- will be placed with 10000.00
      </p>
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundAmount.currency
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Currency
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.reason
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Refund reason
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundTime
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Refund time
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.totalRefundAmount
    </td>

    <td>
      Object
    </td>

    <td>
      C
    </td>

    <td>
      Total refund amount. Only available if transaction status is <code>refund</code> or <code>partial refund</code>.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.totalRefundAmount.value
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Total refund amount. If it's IDR then the value includes 2 decimal digits.

      <p>
        e.g. IDR 10.000,- will be placed with 10000.00
      </p>
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.totalRefundAmount.currency
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Currency
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.userPaymentDetails
    </td>

    <td>
      Array of object
    </td>

    <td>
      M
    </td>

    <td>
      Payment option used by user. This will be not available for deeplink redirection payment flow with <b>pending</b> status.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.userPaymentDetails.payMethod
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Payment method used by user. E.g: gopay
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.userPaymentDetails.payOption
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Payment option used by user. <br /> Possible value: <br /> - GoPay = `GOPAY_WALLET` <br /> - GoPay Later = `PAY_LATER` <br /> - GoPay Tabungan by Jago = `GOPAY_SAVINGS`
    </td>
  </tr>
</table>

```
{
    "createdTime": "2020-01-01T00:00:00+07:00",
    "latestTransactionStatus": "00",
    "originalReferenceNo": "gopayOrderId",
    "finishedTime": "2020-01-02T00:00:00+07:00",
    "originalPartnerReferenceNo": "merchant-order-id",
    "transactionStatusDesc": "desc",
   "originalExternalId":"merchant-order-id",
    "additionalInfo": { 
        "userPaymentDetails": [
         {
           "payMethod": "gopay",
           "payOption": "GOPAY_WALLET"
         }
        ],
         "refundHistory":[
  	{
     	     	"refundNo":"96194816941239812",
      			"refundStatus":"00",
     	     	"partnerReferenceNo":"239850918204981205970",
          		"refundAmount":{
          	   	     	"value":"12345678.00",
         	    	     	"currency":"IDR"
     	     	},
     	     	"refundDate":"2020-12-23T07:44:16+07:00",
          		"reason":"Customer Complain"
  	}
   ]
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
</table>

```
{
   "responseCode":"2005600",
   "responseMessage":"Request has been processed successfully"
}
```

# Additional APIs

1. [Refund API](https://docs.midtrans.com/reference/refund-api)
2. [Cancel API](https://docs.midtrans.com/reference/cancel-api)
3. [Get Transaction Status API](https://docs.midtrans.com/reference/get-transaction-status-api)
4. [Payment Notification API](https://docs.midtrans.com/reference/payment-notification-api)

<br />