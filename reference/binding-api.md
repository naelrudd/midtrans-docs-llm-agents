---
updatedAt: 2026-02-25T05:07:19.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Bind Account API

| Path              | /\{version}/registration-account-binding |
| :---------------- | :--------------------------------------- |
| HTTP Method       | POST                                     |
| Version           | v1.0                                     |
| SNAP service code | 07                                       |

<br />

## Request Header

| Field Name    | Field Type | Mandatory | Field Description                                                                                                                                                                                                         |
| :------------ | :--------- | :-------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Content-type  | String     | M         | Media type of the resource, i.e. application/json.                                                                                                                                                                        |
| X-TIMESTAMP   | String     | M         | Client’s current local time in ISO-8601 format.                                                                                                                                                                           |
| X-SIGNATURE   | String     | M         | Created using symmetric signature HMAC\_SHA512 algorithm.                                                                                                                                                                 |
| Authorization | String     | M         | Represents access\_token of a request; string starts with keyword “Bearer ” followed by access\_token. Can get this token from [Access Token B2B API](https://docs.midtrans.com/reference/signature-generation) response. |
| X-PARTNER-ID  | String     | M         | Unique identifier for merchant. Provided by Midtrans.                                                                                                                                                                     |
| X-EXTERNAL-ID | String     | M         | Alphanumeric string. We suggest merchant to use UUID format. Reference number that should be unique in the same day or 1 day idempotency key.                                                                             |
| CHANNEL-ID    | String     | M         | Mandatory field from Bank Indonesia that can take any value with correct format 5 digits numeric string.                                                                                                                  |

```
Content-type:application/json
X-TIMESTAMP:2024-03-19T14:30:00+07:00
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
Authorization: Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
X-PARTNER-ID: G123456
X-EXTERNAL-ID:12345678901234567890
CHANNEL-ID:12345
```

<br />

## Request Body

| Field Name | Field Type  | Mandatory | Field Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| :--------- | :---------- | :-------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| merchantId | String (64) | M         | Merchant ID (use the same value with merchantId in get-auth-code endpoint) <br /><br /> Merchant payment handle, merchant identifier in UUID format. Provided by Midtrans. <br /> Note: this value is not Midtrans Merchant ID, but a different value, here's the sample format: 303b4f89-xxxx-xxxx-xxxx-62a8ffaefaf3 <br /><br /> The value on staging and production is different. Please make sure that you are sending the correct value based on the environment that you are using. |
| authCode   | String(256) | M         | Auth code to exchange with access token. Can get this code from [Get Auth Code API](https://docs.midtrans.com/reference/get-auth-code-api) response.                                                                                                                                                                                                                                                                                                                                      |
| grantType  | String (64) | M         | Auth code grant type, possible value = `AUTHORIZATION_CODE`.                                                                                                                                                                                                                                                                                                                                                                                                                              |

```
{  
   "authCode":"eyqwwewiasdawwesdwa",
   "merchantId":"550e8400-e29b-41d4-a716-446655440000",
   "grantType":"AUTHORIZATION_CODE"
}
```

<br />

## Response Header

| Field Name   | Field Type | Mandatory | Field Description                                  |
| :----------- | :--------- | :-------- | :------------------------------------------------- |
| Content-type | String     | M         | Media type of the resource, i.e. application/json. |
| X-TIMESTAMP  | String     | M         | Client’s current local time in ISO-8601 format.    |

```
Content-type: application/json
X-TIMESTAMP: 2024-03-19T14:30:00+07:00
```

<br />

## Response Body

| Field Name                                                                 | Field Type    | Mandatory | Field Description                                                           |
| :------------------------------------------------------------------------- | :------------ | :-------- | :-------------------------------------------------------------------------- |
| responseCode                                                               | String(7)     | M         | Error code to specify the error returned.                                   |
| responseMessage                                                            | String (150)  | M         | Debug message to provide more information.                                  |
| referenceNo                                                                | String (64)   | M         | Debug ID to provide more information.                                       |
| accessTokenInfo <br /> *Only returned on successful response*              | Object        | C         | Access token object that contain access token data.                         |
| accessTokenInfo.accessToken  <br /> *Only returned on successful response* | String (2048) | C         | Access token used for transaction (used for Authorization-Customer header). |

```Text Successful Response
{
   "responseCode":"2000700",
   "responseMessage":"Request has been processed successfully",
   "referenceNo":"19352694-0ef6-4439-8ad1-b1dfb8bbb85f",
   "accessTokenInfo":{
      "accessToken":"MjAyMjEwMTM2NjE1OGRiMS00NmM1LTQxMWQtYmU4NC01ODk1ZTdhMjg2NmY6OGNmM2U4NWUtZTc3Mi00NTJmLWFkYmEtNDcyNjRiOWZiZWIw"
   }
}
```
```Text Error Response
{
   "responseCode":"5000700",
   "responseMessage":"Timeout",
   "referenceNo":"19352694-0ef6-4439-8ad1-b1dfb8bbb85f"
}
```

<br />

### List of Response Code

| Response Code | HTTP Status Code | Response Message                                          |
| :------------ | :--------------- | :-------------------------------------------------------- |
| 2000700       | 200              | Success                                                   |
| 4000702       | 400              | Invalid Mandatory Field                                   |
| 4010700       | 401              | Unauthorized. Auth token required                         |
| 4010701       | 401              | Invalid Token (B2B)                                       |
| 4040705       | 404              | Merchant Is Not Registered For Card Registration Services |
| 4040711       | 404              | Invalid Customer AuthCode                                 |
| 5000701       | 500              | Internal Server Error                                     |
| 5040700       | 504              | Timeout                                                   |