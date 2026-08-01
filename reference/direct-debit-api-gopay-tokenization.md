---
updatedAt: 2026-04-21T06:33:29.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Payment Method: GoPay Tokenization (non Pre-Auth)

<Callout icon="📘" theme="info">
  Merchant can now test CoreAPI BI-SNAP flow on Sandbox!

  For more details, go [here](https://docs.midtrans.com/reference/testing-bi-snap-on-sandbox-environment).

  This new sandbox will be rolled out to all merchant from **October 22nd, 2024**. Please contact your sales representative for early access.
</Callout>

<br />

> 📘 GoPay Media Kit
>
> To have a consistent and standardized GoPay branding across platform, we highly recommend merchants to refer to our media kit. Please refer to this page <https://gopay.co.id/media-kit> to access our brand guideline and image bank.

This section will explain how merchant can initiate GoPay Tokenization (non Pre-Auth) transactions using SNAP-based CoreAPI specification.

1. In order to do GoPay Tokenization transaction, merchant should link the customer's GoPay account first by initiating the [Account Linking API](https://docs.midtrans.com/reference/account-linking-api).
2. Once linked, merchant can create a transaction by calling Direct Debit Payment API.
3. Merchant can also do other subsequent actions such as Cancel, Refund, and Get Status.
4. To receive payment notification from Midtrans, merchant will need to also implement Payment Notification API.

<Callout icon="📘" theme="info">
  GoPay Tokenization in BI-SNAP flow can also support both GoPay & GoPay Later payment. Merchant should pass the corresponding payment option token as **payOptionDetails.additionalInfo.paymentoptiontoken** in the request body. The payment option token can be retrieved from [Binding Inquiry API](https://docs.midtrans.com/reference/binding-inquiry-api).
</Callout>

# Creating GoPay Tokenization transaction

<Image align="center" src="https://files.readme.io/b5860ab-SNAP_based_account_linking_flow-Copy_of_Page-1.png" />

<br />

> 📘 Redirecting to GoPay page during payment
>
> To learn more on GoPay Tokenization redirection, please refer to these API documentations:
>
> * GoPay Tokenization web flow: <https://docs.midtrans.com/reference/faq-redirection-to-gopay-web-page>
>
> * GoPay Tokenization app redirection flow: <https://docs.midtrans.com/reference/faq-redirection-to-gojek-gopay-app>
>
> > ❗️ GoPay may add/change GoPay redirection URL from time to time.
> >
> > To ensure merchant can always support GoPay flow at all times, we highly suggest merchant to not do explicit URL whitelisting.

<br />

## GoPay Tokenization - Direct Debit Payment API

| Path              | /\{version}/debit/payment-host-to-host |
| :---------------- | :------------------------------------- |
| HTTP Method       | POST                                   |
| Version           | v1.0                                   |
| SNAP service code | 54                                     |

### Request Header

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field Name
      </th>

      <th>
        Field Type
      </th>

      <th>
        Mandatory
      </th>

      <th>
        Field Description
      </th>
    </tr>
  </thead>

  <tbody>
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

      <td>
        Media type of the resource, i.e. application/json.
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

      <td>
        Client’s current local time in ISO-8601 format.
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

      <td>
        Created using symmetric signature HMAC_SHA512 algorithm.
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

      <td>
        Represents access_token of a request; string starts with keyword “Bearer ” followed by access_token. Can get this token from [Access Token B2B API](https://docs.midtrans.com/reference/signature-generation)   response.
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

      <td>
        Represents access_token of a request; string starts with keyword “Bearer ” followed by access_token from [Binding API](https://docs.midtrans.com/reference/binding-api) response.
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

      <td>
        Unique identifier for merchant. Provided by Midtrans.
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

      <td>
        Alphanumeric string. We suggest merchant to use UUID format. The value should be unique. Maximum string length is 36 characters. <br /><br /> In case of timeout, merchant can do:

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

      <td>
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

      <td>
        Device identification on which the API services are currently being accessed by the end user (customer).

        Sample:  
        Web Application:  
        Mozilla / 5.0(Windows NT 10.0; Win64; x64)AppleWebKit / 537.36(KHTML, like Gecko)Chrome / 75.0.3770.100 Safari / 537.36 OPR / 62.0.3331.99

        Mobile Application:  
        Android: android-20013adf6cdd8123f  
        iOS: 72635bdfd223yvjm7246nsdj34hd4559393kjh42
      </td>
    </tr>
  </tbody>
</Table>

```
Content-type:application/json
X-TIMESTAMP:2024-03-19T14:30:00+07:00
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
Authorization: Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
Authorization-Customer: Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
X-PARTNER-ID: G123456
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
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      The account token used to represent the account binding between merchant and GoPay.

      <p>
        We are not sharing accountToken/accessToken with Merchant. Merchant needs to call the Bind Account API to fetch the accountToken/accessToken.
      </p>
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
      M
    </td>

    <td colspan="2">
      Merchant redirect URL.

      <p>
        After completing payment, user will be redirected back to this URL
      </p>
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
      URL value (need to be whitelisted as part of GoPay Tokenization onboarding process)
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
      validUpTo
    </td>

    <td>
      String(25)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      The time when the payment will be automatically expired. Using ISO 8601 format.

      <p>
        (Maximum value: 180 days from transaction time, minimum value: 20 seconds, default value: 15 minutes)
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
      Payment option that will be used for this payment

      <p>
        Currently only accept 1 payOptions
      </p>
    </td>
  </tr>

  <tr>
    <td>
      payOptionDetails.payMethod
    </td>

    <td>
      String (64)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Payment method. Possible value: `GOPAY`
    </td>
  </tr>

  <tr>
    <td>
      payOptionDetails.payOption
    </td>

    <td>
      String (64)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Payment option which shows the provider of this payment

      <p>
        Possible value: `GOPAY_WALLET`, `PAY_LATER`
      </p>

      <p>
        (Value can be acquired from additionalInfo.paymentOptions.name in Account Binding Inquiry API response)
      </p>
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
      O
    </td>

    <td colspan="2">
      Payment transaction amount
    </td>
  </tr>

  <tr>
    <td>
      payOptionDetails.transAmount.value
    </td>

    <td>
      String (16,2)
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

      <p>
        (item price \* item quantity should be the same amount as transAmount)
      </p>
    </td>
  </tr>

  <tr>
    <td>
      payOptionDetails.transAmount.currency
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
      payOptionDetails.additionalInfo
    </td>

    <td>
      Object
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Additional information field which merchants need to pass to support current API contracts.
    </td>
  </tr>

  <tr>
    <td>
      payOptionDetails.additionalInfo.recurring
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Recurring flag

      <p>
        Possible value : Y/N
      </p>

      <p>
        If recurring: Y then we will treat this transaction as recurring transaction and bypass PIN challenge. Only applies if recurring feature has already been enabled, please talk to your Midtrans sales representative to have this feature enabled.
      </p>
    </td>
  </tr>

  <tr>
    <td>
      payOptionDetails.additionalInfo.promotionIds
    </td>

    <td>
      Array of String
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      List of promotion ID

      <p>
        Promotion ID can be obtained from Get Promotion API.
      </p>
    </td>
  </tr>

  <tr>
    <td>
      payOptionDetails.additionalInfo.paymentOptionToken
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Can get this from Account Binding Inquriy API response.
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
      O
    </td>

    <td colspan="2">
      Merchant cross reference id (payment flow identifier)
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.lang
    </td>

    <td>
      String (2)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Language code for service <br />
      Possible values: en, id. <br />

      Default value : id.
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

    <td colspan="2" />
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

    <td colspan="2" />
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
      additionalInfo.items
    </td>

    <td>
      Array Of Object
    </td>

    <td>
      O
    </td>

    <td colspan="2" />
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

      <p>
        Shall merchant intent to apply SKU based promotion, merchant should pass the agreed item ID value for promotion.
      </p>
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

    <td colspan="2" />
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
      Item price value (item price \* item quantity should be the same amount as transAmount)
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.items.price.currency
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
      additionalInfo.items.quantity
    </td>

    <td>
      String(16)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Item quantity (item price \* item quantity should be the same amount as transAmount)
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
      M
    </td>

    <td colspan="2">
      Item name
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
      Name of the merchant selling the item
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
      Brand name of the item
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
      Category of the item
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
      Merchant's metadata
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.paymentProviderMetadata
    </td>

    <td>
      Object
    </td>

    <td>
      C
    </td>

    <td colspan="2">
      Object containing the payment provider’s metadata parameter. This is used whenever merchant needs to pass additional information to payment provider.

      In the case of GoPay Later Multi Month transaction, merchant needs to pass the required risk data information as agreed with GoPay Later team.
    </td>
  </tr>
</table>

```text Sample Request - Direct Debit Payment
{
    "partnerReferenceNo": "merchant-order-id",
    "chargeToken": "accessToken",
    "validUpTo": "2023-07-03T10:36:17+07:00",
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
    "urlParams":[ {
        "url": "https://www.merchant.com/",
        "type": "PAY_RETURN",
        "isDeeplink": "N"
    }],
    "additionalInfo": {
    		"merchantCrossReferenceId": "303b4f89-xxxx-xxxx-xxxx-62a8ffaefaf3",
    		"lang": "en",
        "customerDetails": {
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
        },
        "items": [
            {
                "id": "8za1ieleavwusxn6u5re60ri",
                "price": {
                    "value": "12345678.00",
                    "currency": "IDR"
                },
                "quantity": “1”,
                "name": "Video A",
                "brand": "Some Brand",
                "category": "Subsciption",
                "merchantName": "Amazon Prime"
            }
        ],
        "metadata": {},
        "paymentProviderMetadata": {
            "subOrders": [
                {
                    "subOrderId": "subOrderId001",
                    "periodType": 3,
                    "mainOrderId": <string>,
                    "skuId": "sku2",
                    "skuName": "rice",
                    "categoryId": "categoryId2",
                    "categoryOneName": "mock1",
                    "categoryTwoName": "mock2",
                    "categoryCodes": [],
                    "quantity": 2,
                    "amount": 100000,
                    "discounts": {
                        "funder": <string>,
                        "totalTenor": <int>,
                        "discountDetails": [
	                        "tenor": <int>
	                        "discountType": <string> [DISCOUNT_INTEREST_AMOUNT / DISCOUNT_INTEREST_PERCENTAGE]
	                        "discountAmount": <int>,
	                        "discountRate": <float>,
	                        "extendInfo": {}
                        ]
                    },
                    "merchantId": <string>,
                    "merchantRegisterTime": <long>,
                    "merchantGrade": <string>,
                    "transactionTimestamp": <long>,
                    "merchantName": <string>,
                    "externalMerchantId": <string>,
                    "transactionId": <string>,
                    "serviceType" <int>,
                    "extendInfo": {},
                    "platformInformation": {
                        "merchantUserId": <string>,
                        "firstTransactionDate": "2024/4/12",
                        "latestTransactionDate": "2024/4/12",
                        "successTransactionCount": 30,
                        "successTransactionAmount": 30000000,
                        "successTransactionCountMonthly": 30,
                        "successTransactionAmountMonthly": 30000000,
                        "successCodTransactionCountMonthly": 15,
                        "successCodTransactionAmountMonthly": 30000000,
                        "paidByCreditCard": true/false,
                        "paidByOther": true/false,
                        "paidByEWallet": true/false,
                        "inPayLaterWhitelist": true/false,
                        "inPayLaterBlacklist": true/false,
                        "creditApplicationScore": 501.58,
                        "trxnBehaviorScore: 684.29
                    },
                    "itemInformation": {
                        "itemName": <string>,
                        "categoryName": <string>
                    }
                }
            ],
            "extendInfo": {
                "address": {
                    "address": <string>,
                    "addressId": <string>,
                    "state": <string>,
                    "city": <string>,
                    "shippingName": <string>
                    "shippingPhoneNo": <string>
                },
                "ecommerceOrder": {
                    "orderAmount": 100000,
                    "ecommerceSubOrders": [
                        {
                            "periodType": 3,
                            "subOrderId": "GTF_MOCK",
                            "skuId": "GTF_MOCK",
                            "skuName": "GTF_MOCK",
                            "categoryId": "GTF_MOCK",
                            "categoryOneName": "GTF_MOCK",
                            "categoryTwoName": "GTF_MOCK",
                            "categoryCodes": [
                                "GTF_MOCK"
                            ],
                            "quantity": 1,
                            "amount": 100000,
                            "merchantId": "BLIBLI",
                            "merchantRegisterTime": 0,
                            "merchantGrade": "GTF_MOCK",
                            "transactionTimeStamp": 1674703781574,
                            "extendInfo": {}
                        }
                    ]
                },
                "deviceInfo": {
                    "platform": "string",
                    "gps": {
                        "longitudeHashed": "string",
                        "latitudeHashed": "string",
                        "longitude": "string",
                        "latitude": "string",
                        "time": null
                    },
                    "device": {
                        "deviceId": "string",
                        "isRoot": true,
                        "androidId": "string",
                        "build": {
                            "board": "string",
                            "brand": "string",
                            "cpuAbi": "string",
                            "device": "string",
                            "manufacturer": "string",
                            "model": "string",
                            "product": "string"
                        },
                        "isTampered": true,
                        "isHooked": true,
                        "isEmulators": true
                    },
                    "wifiList": [
                        {
                            "ssid": "string"
                        }
                    ],
                    "ipAddress": {
                        "ethIp": "string",
                        "trueIp": "string"
                    },
                    "appVersion": "string",
                    "advertisingId": "string",
                    "usedByStreamingApps": "string",
                    "widevineId": "string",
                    "dexguardId": "string",
                    "uuid": "string",
                    "deviceIdInUuid": "string"
                }
            }
        }
    }
}
```

### Response Header

| Field Name   | Field Type | Mandatory | Field Description                                  |
| :----------- | :--------- | :-------- | :------------------------------------------------- |
| Content-type | String     | M         | Media type of the resource, i.e. application/json. |
| X-TIMESTAMP  | String     | M         | Client’s current local time in ISO-8601 format.    |

```
Content-type: application/json
X-TIMESTAMP: 2020-01-01T00:00:00+07:00
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
      M
    </td>

    <td colspan="2">
      Unique transaction identifier from payment provider system e.g : <strong>Gopay order ID. </strong>

      <p>
        (Only filled if transaction created successfully)
      </p>
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
      webRedirectUrl
    </td>

    <td>
      String (2048)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      <ul>
        <li>
          If merchant is onboarded to Tokenization webview flow: This will return a GoPay PIN webpage. Merchant should open this link to redirect user to GoPay PIN page to complete payment. <strong>Merchant should refer to this field if merchant is onboarded to Tokenization webview flow.</strong>
        </li>

        <li>
          If merchant is onboarded to Tokenization app redirection flow: This will return a GoPay webpage with a timer as well as payment instructions. User will receive a push notification on their Gojek app to complete payment. Once the customer verifies the transaction on the app, it will be automatically redirected to the merchant page.
        </li>

        <li>
          GoPay may add/change GoPay redirection URL from time to time.To ensure merchant can always support GoPay flow at all times, we highly suggest merchant to not do explicit URL whitelisting.
        </li>
      </ul>
    </td>
  </tr>

  <tr>
    <td>
      appRedirectUrl
    </td>

    <td>
      String (2048)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      This will return a universal link to the Gojek/GoPay app. Use this link to redirect user to GoPay PIN page on Gojek/GoPay app for them to complete payment. <strong>Merchant should refer to this field if merchant is onboarded to Tokenization app redirection flow.</strong> GoPay may add/change GoPay redirection URL from time to time.To ensure merchant can always support GoPay flow at all times, we highly suggest merchant to not do explicit URL whitelisting.
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
      String (ISO4217)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Amount value
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.currency
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Amount currency
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.status
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Midtrans legacy transaction status
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.expiryTime
    </td>

    <td>
      String (ISO8601)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Midtrans legacy expiry transaction time
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.paymentType
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Payment type used
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
      M
    </td>

    <td colspan="2" />
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
      String
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
      additionalInfo.payOptionDetails
    </td>

    <td>
      Array of Object.
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Payment option detail. This parameter will be deprecated soon. We encourage merchant to not consume this parameter and instead consume the parameter `additionalInfo.userPaymentDetails` instead.
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
      Possible value: `gopay`
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.payOptionDetails.payOption
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      GoPay payment option used. <br /> Possible value:  <br /> - GoPay =`GOPAY_WALLET` <br /> -GoPay Later =`PAY_LATER` <br /> - GoPay Tabungan by Jago = `GOPAY_SAVINGS`
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.userPaymentDetails
    </td>

    <td>
      Array of Object
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Payment used by user
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

    <td colspan="2">
      Possible value: `gopay`
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

    <td colspan="2">
      GoPay payment option used. <br /> Possible value:  <br /> - GoPay =`GOPAY_WALLET` <br /> -GoPay Later =`PAY_LATER` <br /> - GoPay Tabungan by Jago = `GOPAY_SAVINGS`
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
      Transaction status

      <p>
        <strong>Possible Values: </strong>
      </p>

      <ul>
        <li>00 - Success</li>

        <li> 03 - Pending</li>

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
      Fraud status from Midtrans. Possible values: <br /> - accept --> Transaction is safe to proceed. It is not considered as a fraud. <br /> - deny --> Transaction is considered as fraud. It is rejected by Midtrans.
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
      The time when the payment will be automatically expired. Using ISO 8601 format.
    </td>
  </tr>
</table>

```Text Successful response
{
   "responseCode":"20054000",
   "responseMessage":"Request has been processed successfully",
   "referenceNo":"gopay-order-id",
   "partnerReferenceNo":"merchant-order-id",
   "webRedirectUrl":"https://pjsp.com/universal?bizNo=REF993883&...",
   "appRedirectUrl":"https://pjsp.com/universal?bizNo=REF993883&...",
   "additionalInfo":{
      "grossAmount":{
              "value": "12345678.00",
              "currency": "IDR"
       },
      "currency":"IDR",
      "amount": "12345678.00",
      "status": "PENDING",
      "expiryTime": "2024-03-28T07:49:09.00Z"
      "paymentType": "GOPAY",
      "payOptionDetails" : [{
          "payMethod":"gopay",
          "payOption": "GOPAY_WALLET"
       }], 
       "userPaymentDetails" : [{
          "payMethod":"gopay",
          "payOption": "GOPAY_WALLET"
       }], 
      "transactionTime":"2024-03-19T14:30:00+07:00",
      "transactionStatus":"03",  
      "fraudStatus":"accept"  ,
    	"validUpTo":"2023-07-03T10:36:17+07:00"
   }
}
```
```Text Error respnse
{
   "responseCode":"4001001",
   "responseMessage":"There is some issue with the transaction request",
   "originalExternalId": "merchant-order-id",
}
```

### List of response code

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
      2005400
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
      Suspected Fraud.
    </td>
  </tr>

  <tr>
    <td>
      4035405
    </td>

    <td>
      403
    </td>

    <td>Inactive Account </td>
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

> 📘 Redirecting to GoPay page during payment
>
> To learn more on GoPay Tokenization redirection, please refer to these API documentations:
>
> * GoPay Tokenization web flow: <https://docs.midtrans.com/reference/faq-redirection-to-gopay-web-page>
> * GoPay Tokenization app redirection flow: <https://docs.midtrans.com/reference/faq-redirection-to-gojek-gopay-app>

# Additional APIs

1. [Refund API](https://docs.midtrans.com/reference/refund-api)
2. [Cancel API](https://docs.midtrans.com/reference/cancel-api)
3. [Get Transaction Status API](https://docs.midtrans.com/reference/get-transaction-status-api)
4. [Payment Notification API](https://docs.midtrans.com/reference/payment-notification-api)