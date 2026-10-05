---
updatedAt: 2026-09-28T12:00:08.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Get merchant API

Get merchant API is an API call that can be used to search merchants within the system based on various criteria. This API provides several parameters to filter data and perform pagination.

<br />

#### Request Header

| Field         | Type   | Attribute | Description                                          |
| :------------ | :----- | :-------- | :--------------------------------------------------- |
| Authorization | String | Mandatory | Basic Base64Encode(partnerServerKey:)                |
| X-PARTNER-ID  | String | Mandatory | Unique identifier for partner. Provided by Midtrans. |

#### Request Params

| Field     | Type   | Attribute | Description                                                   |
| :-------- | :----- | :-------- | :------------------------------------------------------------ |
| page      | Int    | Optional  | Maximum number of data returned in one pagination. Default: 1 |
| per\_page | Int    | Optional  | Current page numberDefault: 10                               |
| keyword   | String | Optional  | Query search by merchant ID or merchant name                  |

#### Example

`GET api/v1/merchants?page=1&per_page=10`

```http
Authorization: Basic cGFydG5lci1hcGkta2V5Og==
X-PARTNER-ID: 82150823919040624621823174737537
```

#### Response

##### Body

| Field                       | Type   | Description                                           |
| :-------------------------- | :----- | :---------------------------------------------------- |
| status\_code                | String | Merchant identifier that is unique per each merchant  |
| status\_message             | String | The name of the merchant                              |
| merchants                   | Array  | List of merchants                                     |
| \[].merchant\_id            | String | Merchant identifier that is unique per each merchant  |
| \[].merchant\_name          | String | The name of the merchant                              |
| \[].merchant\_phone\_number | String | The phone number of the merchant without country code |
| \[].email                   | String | The email of the merchant registered with Midtrans.   |

##### Successful Response

```json
{
  "status_code": "200",
  "status_message": "Merchants have been successfully retrieved.",
  "merchants": [
    {
      "merchant_id": "M123456",
      "merchant_name": "HQ Midtrans Merchant",
      "merchant_phone_number": "81211111111",
      "email": "merchant@midtrans.com"
    }
  ]
}
```

##### Error Response 200 Data doesn’t exist

```json
{
  "status_code": "200",
  "status_message": "Merchants have been successfully retrieved.",
  "merchants": []
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

```json JSON
{
  "status_code": "500",
  "status_message": "Internal Server Error"
}
```