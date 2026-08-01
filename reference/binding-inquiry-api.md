---
updatedAt: 2025-11-25T08:22:37.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Account Binding Inquiry API

| Path              | /\{version}/registration-account-inquiry |
| :---------------- | :--------------------------------------- |
| HTTP Method       | POST                                     |
| Version           | v1.0                                     |
| SNAP service code | 08                                       |

<Callout icon="📘" theme="info">
  **Merchants are encouraged to always call this API before payment to make sure the merchant uses the updated token when creating payment** as the payment option token may change from time to time due to various reasons (example: customer upgrade their GoPay account to GoPay Tabungan).
</Callout>

## Request Header

| Field Name             | Field Type | Mandatory | Field Description                                                                                                                                                                                                                                                                                                                                                                                                                                |
| :--------------------- | :--------- | :-------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Content-type           | String     | M         | Media type of the resource, i.e. application/json                                                                                                                                                                                                                                                                                                                                                                                                |
| X-TIMESTAMP            | String     | M         | Client’s current local time in ISO-8601 format                                                                                                                                                                                                                                                                                                                                                                                                   |
| X-SIGNATURE            | String     | M         | Created using symmetric signature HMAC\_SHA512 algorithm                                                                                                                                                                                                                                                                                                                                                                                         |
| Authorization          | String     | M         | Represents access\_token of a request; string starts with keyword “Bearer ” followed by access\_token. Can get this token from Access Token B2B API response.                                                                                                                                                                                                                                                                                    |
| Authorization-Customer | String     | C         | Represents access\_token of a request; string starts with keyword “Bearer ” followed by access\_token from Binding API response <br /><br /> - If merchant intent to make a brand new binding, merchant needs to pass Authorization-Customer in the request header. <br /> - If merchant intent to swap Midtrans account ID from legacy API to Authorization-Customer from BI-SNAP API, merchant is not required to pass Authorization-Customer. |
| X-PARTNER-ID           | String     | M         | Unique identifier for merchant. Merchant can send any value.                                                                                                                                                                                                                                                                                                                                                                                     |
| X-EXTERNAL-ID          | String     | M         | Alphanumeric string. We suggest merchant to use UUID format. Reference number that should be unique in the same day or 1 day idempotency key.                                                                                                                                                                                                                                                                                                    |
| X-DEVICE-ID            | String     | M         | Device identification on which the API services is currently being accessed by the end user (customer)                                                                                                                                                                                                                                                                                                                                           |
| CHANNEL-ID             | String     | M         | Mandatory field from Bank Indonesia that can take any value with correct format 5 digits numeric string                                                                                                                                                                                                                                                                                                                                          |

```Text Creating new binding in BI-SNAP
Content-type:application/json
Authorization: Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
Authorization-Customer : Bearer MjAyMjEwMTM2NjE1OGRiMS00NmM1LTQxMWQtYmU4NC01ODk1ZTdhMjg2NmY6OGNmM2U4NWUtZTc3Mi00NTJmLWFkYmEtNDcyNjRiOWZiZWIw
X-TIMESTAMP:2024-03-19T14:30:00+07:00
X-PARTNER-ID: BMRI
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
X-DEVICE-ID: 0987ADCASA
X-EXTERNAL-ID:1234567890123456789
CHANNEL-ID:12345
```
```Text Swapping Midtrans account ID (legacy API) with Authorization-Customer (BI-SNAP API)
Content-type:application/json
Authorization: Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
X-TIMESTAMP:2024-03-19T14:30:00+07:00
X-PARTNER-ID: BMRI
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
X-DEVICE-ID: 0987ADCASA
X-EXTERNAL-ID:1234567890123456789
CHANNEL-ID:12345
```

<br />

## Request Body

| Field Name               | Field Type | Mandatory | Field Description                                                                                                                                                                               |
| :----------------------- | :--------- | :-------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| additionalInfo           | Object     | O         | Some additional info                                                                                                                                                                            |
| additionalInfo.accountId | String     | O         | Account ID from legacy Core API flow. <br /><br /> Merchant needs to pass accountId if merchant wants to swap Midtrans account ID from legacy API with Authorization-Customer from BI-SNAP API. |

```text
{
    "additionalInfo":{
      “accountId” : “acd52694-0ef6-4439-8ad1-b1dfb8bb111“
     } 
}
```

<br />

<Callout icon="📘" theme="info">
  **Swapping Midtrans Account ID (from Legacy API) to Authorization-Customer (from BI-SNAP API)**

  Merchants who already has existing account binding on legacy API doesn't need to do rebinding when migrating to BI-SNAP flow. Merchant can swap the existing Midtrans Account ID from legacy API to the Authorization-Customer token that is needed in BI-SNAP API by calling the Account Binding Inquiry.

  Merchant can pass the request with the detail below:

  * Merchant doesn't need to pass the Authorization-Customer parameter in request header
  * Merchant need to pass Midtrans account ID in additionalInfo.accountId parameter in request body

  Midtrans will return  accessToken parameter in the response body. Merchant can then use this value for Authorization-Customer when calling BI-SNAP API.
</Callout>

## Response Header

| Field Name   | Field Type | Mandatory | Field Description                                 |
| :----------- | :--------- | :-------- | :------------------------------------------------ |
| Content-type | String     | M         | Media type of the resource, i.e. application/json |
| X-TIMESTAMP  | String     | M         | Client’s current local time in ISO-8601 format    |

```
Content-type: application/json
X-TIMESTAMP: 2024-03-19T14:30:00+07:00
```

<br />

## Response Body

| Field Name                                                                                    | Field Type   | Mandatory | Field Description                                                          |
| :-------------------------------------------------------------------------------------------- | :----------- | :-------- | :------------------------------------------------------------------------- |
| responseCode                                                                                  | String (7)   | M         | Error code to specify the error returned.                                  |
| responseMessage                                                                               | String (150) | M         | Debug message to provide more information.                                 |
| referenceNo                                                                                   | String       | M         | Debug id to provide more information.                                      |
| additionalInfo <br /> *Only returned in successful response*                                  | Object       | C         | Some additional info                                                       |
| additionalInfo.accessToken  <br /> *Only returned in successful response*                     | String       | C         | Access token used for transaction (used for Authorization-Customer header) |
| additionalInfo.paymentType <br /> *Only returned in successful response*                      |              | C         | Some payment type                                                          |
| additionalInfo.paymentOptions <br /> *Only returned in successful response*                   | Object       | C         | List of payment options                                                    |
| additionalInfo.paymentOptions.name <br /> *Only returned in successful response*              | String       | C         | Account balance name for each payment options.                             |
| additionalInfo.paymentOptions.active <br /> *Only returned in successful response*            | Boolean      | C         | Flag to mark if payment option is active.                                  |
| additionalInfo.paymentOptions.balance <br /> *Only returned in successful response*           | Object       | C         | Linked account balance for each payment options.                           |
| additionalInfo.paymentOptions.balance.value <br /> *Only returned in successful response*     | Long         | C         | Account balance value for each payment options.                            |
| additionalInfo.paymentOptions..balance.currency <br /> *Only returned in successful response* | String       | C         | Account balance currency for each payment options.                         |
| additionalInfo.paymentOptions.token <br /> *Only returned in successful response*             | String       | C         | Token that need to be use on Gopay Tokenization charge request.            |

```Text Successful Response
{
    "responseCode": "2000800",
    "responseMessage": "Successful",
    "referenceNo": "19352694-0ef6-4439-8ad1-b1dfb8bbb85f",
    "additionalInfo": {
        "accessToken": "MjAyMjEwMTM2NjE1OGRiMS00NmM1LTQxMWQtYmU4NC01ODk1ZTdhMjg2NmY6OGNmM2U4NWUtZTc3Mi00NTJmLWFkYmEtNDcyNjRiOWZiZWIw",
        "paymentType": "gopay",
        "paymentOptions": [
            {
                "name": "GOPAY_WALLET",
                "active": true,
                "balance": {
                    "value": 7985000,
                    "currency": "IDR"
                },
                "token": "f527bf45-1612-4ec0-bec0-5c407e33adef"
            },
            {
                "name": "PAY_LATER",
                "active": true,
                "balance": {
                    "value": 350000,
                    "currency": "IDR"
                },
                "token": "eyJ0eXBlIjogIlBBWV9MQVRFUiIsICJpZCI6ICIifQ=="
            },
            {
                "name": "GO_CICIL_MAB",
                "active": true,
                "balance": {
                    "value": 5000000,
                    "currency": "IDR"
                },
                "token": "eyJ0eXBlIjogIlBBWV9MQVRFUiIsICJpZ7shdj12345f"
                },
            {
                "name": "GOPAY_SAVINGS",
                "active": true,
                "balance": {
                    "value": 250000,
                    "currency": "IDR"
                },
                "token": "eyJ0eXBlIjogIlBBWV9MQVRFUiIsICJpZ7389rujowd"
            }
        ]
    }
}
```
```Text Error Response
{
   "responseCode":"5000800",
   "responseMessage":"Timeout",
   "referenceNo":"19352694-0ef6-4439-8ad1-b1dfb8bbb85f"
}
```

<br />

### List of Response Code

| Response Code | HTTP Status Code | Response Message                                                                                                                                                                              |
| :------------ | :--------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2000800       | 200              | Successful                                                                                                                                                                                    |
| 4000802       | 400              | Invalid Mandatory Field                                                                                                                                                                       |
| 4010800       | 401              | Unauthorized                                                                                                                                                                                  |
| 4010801       | 401              | Invalid Token (B2B)                                                                                                                                                                           |
| 4010802       | 401              | Invalid Customer Token                                                                                                                                                                        |
| 4040805       | 404              | Merchant Is Not Registered For Card Registration Services                                                                                                                                     |
| 4010802       | 401              | Invalid Customer Token <br /><br /> Note: we will return this when the account linking is already INACTIVE. Applies if merchant passes Authorization-Customer on request header.              |
| 4030818       | 403              | Inactive Card/Account/Customer <br /><br /> Note: we will return this when the account linking is already INACTIVE. Applies if merchant passes AccountID (from legacy API) on request header. |
| 5000801       | 500              | Internal Server Error                                                                                                                                                                         |
| 5040800       | 504              | Timeout                                                                                                                                                                                       |