---
updatedAt: 2026-09-28T12:00:08.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Unlink Account

Merchant can provide the capability for users to unlink the account outside of checkout page by sending DELETE request for a specific `user_id`.

Endpoints: `/api/v1/checkout/users/{{user_id}}/gopay`

HTTP Method: `DELETE`

## Response Body

```json Sample Response - Success
{
  "account_status": "DISABLED",
  "phone_number": "****3424"
}
```
```json Sample Response - Account Not Found
{
  "error_messages": [
    "account not found"
  ],
  "locale": "en"
}
```

| JSON Attribute  | Description                                                   | Type   |
| --------------- | ------------------------------------------------------------- | ------ |
| account\_status | Status of the account. <br />Possible values are  `DISABLED`. | String |
| phone\_number   | The masked phone number that is linked to the user\_id.       | String |