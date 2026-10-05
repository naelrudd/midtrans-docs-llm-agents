---
updatedAt: 2026-09-28T12:00:08.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Expire API

Expire transaction is triggered to update the `transaction_status` to `expire`, when the customer fails to complete the payment. The expired `order_id` can be reused for the same or different payment methods.

Endpoints: `/api/v1/core/{{transaction_id}}/expire`

HTTP Method: `POST`

## Response Body

```json 200 - Success
{
  "status_code": "407",
  "status_message": "Success, transaction has expired",
  "transaction_id": "447e846a-403e-47db-a5da-d7f3f06375d6",
  "order_id": "vtmbill05",
  "payment_type": "echannel",
  "transaction_time": "2015-06-15 13:36:24",
  "transaction_status": "expire",
  "gross_amount": "10000.00"
}
```
```json 200 - Error
{
  "status_code" : "412",
  "status_message" : "Merchant cannot modify the status of the transaction"
}
```

| Field               | Type   | Description                                                    |
| ------------------- | :----- | -------------------------------------------------------------- |
| status\_code        | String | Status code of transaction expire result.                      |
| status\_message     | String | Description of transaction expire result.                      |
| transaction\_id     | String | Transaction ID given by Midtrans.                              |
| order\_id           | String | Order ID specified by you.                                     |
| payment\_type       | String | The payment method used by the customer.                       |
| transaction\_time   | String | Timestamp of transaction in ISO 8601 format. Time Zone: GMT+7. |
| transaction\_status | String | Status of the transaction.                                     |
| gross\_amount       | String | Total amount of transaction in IDR.                            |