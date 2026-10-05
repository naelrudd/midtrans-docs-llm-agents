---
updatedAt: 2026-09-28T12:00:08.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Unregister Merchant API

Unregister merchant API is an API call that can be used to remove a merchant from a partner based on the provided Merchant ID.

#### Request Header

| Field         | Type   | Description                                          |
| :------------ | :----- | :--------------------------------------------------- |
| Authorization | String | Basic Base64Encode(partnerServerKey:)                |
| X-PARTNER-ID  | String | Unique identifier for partner. Provided by Midtrans. |

#### Example

`PUT api/v1/merchants/M123456/unregister`

```text HTTP
Authorization: Basic  
X-PARTNER-ID: 82150823919040624621823174737537
```

<br />

#### Response

##### Body

| Field           | Type   | Description                                          |
| :-------------- | :----- | :--------------------------------------------------- |
| status\_code    | String | Merchant identifier that is unique per each merchant |
| status\_message | String | The name of the merchant                             |

##### Successful Response

```json JSON
{
  "status_code": "204",
  "status_message": "Merchants have been successfully removed from partners."
}
```

##### Error Response 404 Data doesn’t exist

```json
{
  "status_code": "404",
  "status_message": "Merchant doesn't exist."
}
```

##### Error Response 500

```json
{
  "error_messages": [
    "Internal server error"
  ]
}
```