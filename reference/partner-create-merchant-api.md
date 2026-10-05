---
updatedAt: 2026-09-28T12:00:08.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Create merchant API

Create merchant API is an API call that can be used to register a new merchant under a Partner

### Request Header

| Field         | Type   | Attribute | Description                                          |
| :------------ | :----- | :-------- | :--------------------------------------------------- |
| Authorization | String | Mandatory | Basic Base64Encode(partnerServerKey:)                |
| X-PARTNER-ID  | String | Mandatory | Unique identifier for partner. Provided by Midtrans. |

<br />

### Request Body

| Field             | Type   | Attribute | Description                                                                                                                                                                                                                                                                                                                                            |
| :---------------- | :----- | :-------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| email             | String | Mandatory | Email to be registered as Midtrans merchant                                                                                                                                                                                                                                                                                                            |
| merchant\_name    | String | Mandatory | Name of the merchant.                                                                                                                                                                                                                                                                                                                                  |
| callback\_url     | String | Optional  | Merchant’s endpoint URL where Midtrans sends a response after completing a particular request.                                                                                                                                                                                                                                                         |
| notification\_url | String | Optional  | Merchant’s endpoint URL where Midtrans’ Payment Gateway sends HTTP callbacks for payment success or failure events. This is only for payment notifications and does not apply to disbursement or transfer. For disbursement notifications, see [Disbursement HTTP Notification setup](https://docs.midtrans.com/reference/partner-http-notification-1) |
| pay\_account\_url | String | Optional  | Merchant’s endpoint URL where Midtrans' notification engine will send HTTP notification related with pay account (linking & unlinking).                                                                                                                                                                                                                |
| owner\_name       | String | Optional  | The name of the merchant’s owner.                                                                                                                                                                                                                                                                                                                      |
| phone\_number     | String | Optional  | The phone number of the merchant without country code                                                                                                                                                                                                                                                                                                  |
| mcc               | String | Mandatory | Pass the expected value as specified here [Possible values of industry category - Partner Onboarding API](https://docs.google.com/spreadsheets/d/1Wj2XdtMXPMyW2-ia5hAyNw4G5eE6ZBG-nvTYusR9QsY/edit?gid=0#gid=0).                                                                                                                                       |
| entity\_type      | string | Optional  | Pass either ‘individual’ or ‘corporate’ as the values.                                                                                                                                                                                                                                                                                                 |
| business\_name    | String | Optional  | The name of the legal entity representing said merchant.                                                                                                                                                                                                                                                                                               |

<br />

### Example

`POST api/v1/merchants`

```http
Authorization: Basic cGFydG5lci1hcGkta2V5Og==
X-PARTNER-ID: 82150823919040624621823174737537
{
  "email": "merchant@midtrans.com",
  "merchant_name": "HQ Midtrans Merchant",
  "callback_url": "https://merchant.com/midtrans-callback",
  "notification_url": "https://merchant.com/midtrans-notification",
  "pay_account_url": "https://merchant.com/pay-account-notification",
  "owner_name": "Owner Midtrans",
  "phone_number": "81211111111",
  "mcc": "Event",
  "entity_type": "corporate",
  "business_name": "PT Business Name"
}
```

<br />

#### Response

##### Header

| Field                            | Type   | Description                                                                 |
| :------------------------------- | :----- | :-------------------------------------------------------------------------- |
| x-rate-limit-limit               | String | Maximum number of requests that can be sent in the current period of time   |
| x-rate-limit-remaining           | String | Remaining number of requests that can be sent in the current period of time |
| x-rate-limit-reset               | String | Rate limit reset time (in Unix epoch seconds)                               |
| x-rate-limit-retry-after-seconds | String | Number of seconds until the next rate limit reset                           |

##### Body

| Field             | Type      | Description                                                                                                                                                                                                       |
| :---------------- | :-------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| status\_code      | String    | Status code                                                                                                                                                                                                       |
| status\_message   | String    | Status message                                                                                                                                                                                                    |
| error\_messages   | String\[] | Error messages                                                                                                                                                                                                    |
| merchant\_id      | String    | Merchant identifier that is unique per each merchant                                                                                                                                                              |
| merchant\_name    | String    | The name of the merchant                                                                                                                                                                                          |
| phone\_number     | String    | The phone number of the merchant without country code                                                                                                                                                             |
| callback\_url     | String    | Merchant’s endpoint URL where Midtrans sends a response after completing a particular request.                                                                                                                    |
| notification\_url | String    | Merchant’s endpoint URL where Midtrans’ notification engine will send a success or failure HTTP notification.                                                                                                     |
| pay\_account\_url | String    | Merchant’s endpoint URL where Midtrans' notification engine will send HTTP notification related with pay account (linking & unlinking).                                                                           |
| mcc               | String    | Pass the expected value as specified here [Possible values of industry category - Partner Onboarding API](https://docs.google.com/spreadsheets/d/1Wj2XdtMXPMyW2-ia5hAyNw4G5eE6ZBG-nvTYusR9QsY/edit?gid=0#gid=0) . |
| entity\_type      | String    | Pass either ‘individual’ or ‘corporate’ as the values.                                                                                                                                                            |
| business\_name    | String    | The name of the legal entity representing said merchant.                                                                                                                                                          |

<br />

##### Successful Response

```json
{
  "status_code": "200",
  "status_message": "Merchants have been successfully created.",
  "merchant_id": "M123456",
  "merchant_name": "HQ Midtrans Merchant",
  "phone_number": "81211111111",
  "callback_url": "https://merchant.com/midtrans-callback",
  "notification_url": "https://merchant.com/midtrans-notification",
  "pay_account_url": "https://merchant.com/pay-account-notification",
  "owner_name": "Owner Midtrans",
  "mcc": "Event",
  "entity_type": "corporate",
  "business_name": "business name"
}
```

##### Error Response 400

```json
{
  "error_messages": [   
      "merchant_name cannot be empty",
      "email cannot be empty",
  ]
}
```

##### Error Response 401

```json JSON
{
    "status_code": "401",
    "status_message": "Partner is unauthorized"
}
```

##### Error Response 500

```json
{
  "status_code": "500",
  "status_message": "Internal Server Error"
}
```