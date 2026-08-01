---
updatedAt: 2026-07-27T07:51:26.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Get Auth Code API

| Path              | /\{version}/get-auth-code |
| :---------------- | :------------------------ |
| HTTP Method       | GET                       |
| Version           | v1.0                      |
| SNAP service code | 10                        |

<Callout icon="📘" theme="info">
  To simplify the integration, **we highly recommends merchant to call this Get Auth Code API directly from merchant's front end**.
</Callout>

<Callout icon="📘" theme="info">
  **We are deprecating request and respone header from the Get Auth Code API**. Moving forward merchant is not required to pass request header as part of the Get Auth Code API call.

  For merchant that has already passed the headers, we will maintain the backward compatibality and process the API call as is.
</Callout>

## Request Header

| Field Name    | Field Type | Mandatory | Field Description                                                                                                                                                                                                          |
| :------------ | :--------- | :-------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Content-type  | String     | M         | Media type of the resource, i.e. application/json.                                                                                                                                                                         |
| X-TIMESTAMP   | String     | M         | Client’s current local time in ISO-8601 format.                                                                                                                                                                            |
| X-SIGNATURE   | String     | M         | Created using symmetric signature HMAC\_SHA512 algorithm.                                                                                                                                                                  |
| Authorization | String     | M         | Represents access\_token of a request; string starts with keyword “Bearer ” followed by access\_token. Can get this token from [Access Token B2B API](https://docs.midtrans.com/reference/signature-generation)  response. |
| X-PARTNER-ID  | String     | M         | Unique identifier for merchant. Provided by Midtrans.                                                                                                                                                                      |
| X-EXTERNAL-ID | String     | M         | Alphanumeric string. We suggest merchant to use UUID format. Reference number that should be unique in the same day or 1 day idempotency key.                                                                              |
| CHANNEL-ID    | String     | M         | Mandatory field from Bank Indonesia that can take any value with correct format 5 digits numeric string                                                                                                                    |

```
Content-type:application/json
X-TIMESTAMP:2024-03-19T14:30:00+07:00
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
Authorization: Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
X-PARTNER-ID: G123456
X-EXTERNAL-ID:12345678901234567890
CHANNEL-ID:12345
```

## Query Parameter

| Field Name                | Field Type           | Mandatory | Field Description                                                                                                                                                                                                                                                                                                                                                                                 |
| :------------------------ | :------------------- | :-------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| redirectURL               | String (256)         | M         | Merchant callback URL after success get auth code. Need to be whitelisted from GoPay side (part of GoPay Tokenization onboarding process).                                                                                                                                                                                                                                                        |
| scopes                    | List of String (256) | M         | Access scope from authorization. Possible value = `DEFAULT`.                                                                                                                                                                                                                                                                                                                                      |
| state                     | String (32)          | M         | Random string for CSRF.                                                                                                                                                                                                                                                                                                                                                                           |
| merchantId                | String (64)          | M         | Merchant payment handle, merchant identifier in UUID format. Provided by Midtrans. <br /> Note: this value is not Midtrans Merchant ID, but a different value, here's the sample format: 303b4f89-xxxx-xxxx-xxxx-62a8ffaefaf3 <br /><br /> The value on staging and production is different. Please make sure that you are sending the correct value based on the environment that you are using. |
| lang                      | String(2)            | M         | Language code for service<br />Possible values: `en`,` id`.                                                                                                                                                                                                                                                                                                                                       |
| seamlessData              | String (512)         | M         | Data to speed up the validation and verification process.                                                                                                                                                                                                                                                                                                                                         |
| seamlessData.mobileNumber | String               | M         | Mobile number to be linked (format should be country code (without "+") + phone number. Example: 62812345678).                                                                                                                                                                                                                                                                                    |
| seamlessData.paymentType  | String               | M         | Payment type to be linked. Possible value: `gopay`.                                                                                                                                                                                                                                                                                                                                               |
| seamlessSign              | String (512)         | M         | Signature from seamlessData.                                                                                                                                                                                                                                                                                                                                                                      |

```
/get-auth-code?state=<RANDOM_UNIQUE>&merchantId=<merchant-id>&lang=id&scopes=DEFAULT&redirectUrl=<MERCHANT_OAUTH_CALLBACK_URL>&seamlessData=<SEAMLESS_DATA>&seamlessSign=<SIGNATURE>
```

| Seamless Data Format                                                    |
| :---------------------------------------------------------------------- |
| seamlessData = URLEncode("mobileNumber=62822999999\&paymentType=gopay") |

| Seamless Sign Format                                                     |
| :----------------------------------------------------------------------- |
| seamlessSign = URLEncode(Base64(SHA256withRSA(privateKey, seamlessData)) |

Note: Merchant need to use their private key to encrypt seamless sign

## Response Header

| Field Name   | Field Type | Mandatory | Field Description                                 |
| :----------- | :--------- | :-------- | :------------------------------------------------ |
| Content-type | String     | M         | Media type of the resource, i.e. application/json |
| X-TIMESTAMP  | String     | M         | Client’s current local time in ISO-8601 format    |

```text
Content-type: application/json
X-TIMESTAMP: 2024-03-19T14:30:00+07:00
```

## Redirection Response Header

| Field Name | Field Type | Mandatory | Field Description                                                                                                                                                                                                                                                                                                                                                                     |
| :--------- | :--------- | :-------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Location   | String     | M         | GoPay PIN/OTP page URL <br /><br /> - Webview: Redirect user to GoPay PIN/OTP page in webview <br /> - App redirection: Redirect user to GoPay PIN page in Gojek/GoPay app. <br /><br /> GoPay may add/change GoPay redirection URL from time to time. To ensure merchant can always support GoPay flow at all times, we highly suggest merchant to not do explicit URL whitelisting. |
| Origin     | String     | O         | Only will be returned if merchant is using App redrection flow. Will contains linking QR flow. User will need to scan QR using Gojek/GoPay app to continue linking. <br /><br /> GoPay may add/change GoPay URL from time to time. To ensure merchant can always support GoPay flow at all times, we highly suggest merchant to not do explicit URL whitelisting.                     |

```Text Success
HTTP/1.1 302 Found
Location: https://www.integration-gws-app.gopayapi.com/app/authorize?referenceId=19352694-0ef6-4439-8ad1-b1dfb8bbb85f
```
```Text Error
HTTP/1.1 302
Location:merchantRedirectURL?responseCode=4001002&responseMessage=Invalid Mandatory Field mobileNumber
```

In case of a successful API request call (merchant successfully calls the Get Auth Code API), Midtrans will return `Location` in header with the GoPay PIN/OTP page URL. But if the call fails, Midtrans will return `Location` in header with the merchant's redirect URL and the error responseCode and responseMessage.

## Response Query Parameter (After redirection)

| Field Name | Field Type   | Mandatory | Field Description                                                                                                                                      |
| :--------- | :----------- | :-------- | :----------------------------------------------------------------------------------------------------------------------------------------------------- |
| authCode   | String (256) | C         | Auth code used to exchange with access token.  <br /> *Please refer to the section below for the detailed explanation on authCode*                     |
| state      | String (32)  | C         | Random string for CSRF<br />(Merchant can validate to check if this is the same as `state` sent on request).                                           |
| success    | String       | C         | Indicating whether user has successfully completed linking on GoPay page <br /> *Will be returned if merchant is onboarded on webview flow*            |
| result     | String       | C         | Indicating whether user has successfully completed linking on GoPay page <br /> *Will be returned if merchant is onboarded on app redirection flow*    |
| errCode    | String       | C         | Indicating the error code in case user fails to successfully linked on GoPay page <br /> *Will be returned if merchant is onboarded on webview flow*   |
| errDesc    | String       | C         | Indicating the error mesage in case user fails to successfully linked on GoPay page <br /> *Will be returned if merchant is onboarded on webview flow* |

<Callout icon="📘" theme="info">
  ### Response query parameter (after redirection) behavior

  **(will be live in prod on August 26, 2024)**

  Please refer to the table below for the redirect url format for each of the Tokenization flow.

  | Tokenization flow | App type/version    | Success scenario                                    | Failure scenario                                           |
  | :---------------- | :------------------ | :-------------------------------------------------- | :--------------------------------------------------------- |
  | Webview           | -                   | redirectUrl?authCode=xxx\&state=yyy\&success=true   | redirectUrl?errorCode=xxx\&errorDesc=yyy                   |
  | App redirection   | GoPay (all version) | redirectUrl?authCode=xxx\&state=yyy\&result=success | redirectUrl?authCode=null\&state=yyy\&result=abort/failure |
  |                   | Gojek \< 4.95       | redirectUrl?authCode=xxx\&state=yyy\&result=success | redirectUrl?authCode=xxx\&state=yyy\&result=abort/failure  |
  |                   | Gojek >= 4.95       | redirectUrl?authCode=xxx\&state=yyy\&result=success | redirectUrl?authCode=null\&state=yyy\&result=abort/failure |

  <br /> **Things to note**

  - In the case where user is using Gojek app \< 4.95 and they have failed to complete linking on the app, Midtrans will still return authCode value on redirect url query parameters.
  - When merchant call the [Bind Account API](https://docs.midtrans.com/reference/binding-api) with that authCode, Midtrans will return an error and linking cannot be confirmed/successful.
  - It is highly recommended that merchant reads the `result` value to know whether linking is successful from the user side (on Gojek app) before calling the Bind Account API.
</Callout>

<br />

## Response Body

| Field Name      | Field Type   | Mandatory | Field Description                          |
| :-------------- | :----------- | :-------- | :----------------------------------------- |
| responseCode    | String(7)    | M         | Code to specify the response returned.     |
| responseMessage | String (150) | M         | Debug message to provide more information. |
| referenceNo     | String (256) | C         | Debug id to provide more information       |

```Text Successful Response
{
   "responseCode":"2001001",
   "responseMessage":"Successful"
}
```
```Text Error Response
{
   "responseCode":"5001001",
   "responseMessage":"Internal Server Error",
   "referenceNo":"19352694-0ef6-4439-8ad1-b1dfb8bbb85f"
}
```

### List of Response Code

| Response Code | Response Message                                                                                           |
| :------------ | :--------------------------------------------------------------------------------------------------------- |
| 4001001       | Invalid Field Format {field name} (example: Invalid Field Format seamlessData)                             |
| 4001002       | Invalid Mandatory Field mobileNumber                                                                       |
| 4011000       | Unauthorized. Auth token required                                                                          |
| 4011001       | Invalid Token (B2B)                                                                                        |
| 4041012       | Invalid Bill/Virtual Account Not Found <br /> This error is due to phone number is not registered on GoPay |
| 5001001       | Internal Server Error                                                                                      |
| 5041000       | Timeout                                                                                                    |

<br />