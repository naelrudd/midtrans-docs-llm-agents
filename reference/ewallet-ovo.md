---
updatedAt: 2026-04-01T04:07:14.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# OVO

OVO is an *E-Money* payment method by OVO. Customers will need to open OVO app after payment request is created via merchant app.

The steps to integrate with OVO are given below.

1. Provide phone number input page for OVO payment method on merchant app/website.
2. Send the charge API request to Midtrans.
3. [Handle notifications](/reference/notifications-handling).

Send a Charge API request with the details of the transaction such as `payment_type`, `ovo`, `transaction_details`, `item_details`, and `customer_details`.

OVO does not support custom expiry, as payments are expected to be completed immediately.

<br />

<Callout icon="👍" theme="okay">
  **OVO Integration Best Practices**

  OVO does not support custom transaction expiry settings. All **OVO orders have fixed expiry of 65 seconds,** while **customers have 55 seconds to complete the payment.**

  To ensure a smooth payment experience, we strongly recommend merchants to:

  1. Clearly inform customers about the 55-second payment window on the checkout page.
  2. Call **Get Transaction Status** 10 seconds after the expiry window, this needed to ensure the final transaction state is accurately captured even when there's some lag between OVO x Midtrans x Merchant.
</Callout>

***

## OVO Charge API Request

```json ShopeePay Charge Request
{
    "payment_type": "ovo",
    "transaction_details": {
        "order_id": "test-order-ovo-001",
        "gross_amount": 15000
    },
    "item_details": [
        {
            "id": "id1",
            "price": 15000,
            "quantity": 1,
            "name": "Brown sugar boba milk tea"
        }
    ],
    "customer_details": {
        "first_name": "John",
        "last_name": "Brandon",
        "email": "john.brandon@go-jek.com",
        "phone": "081111111111"
    },
    "ovo": {
        "payer_phone_number": "081111111111"
    }
}
```

| JSON Attribute       | Description                                                                    | Type                                     | Required |
| -------------------- | ------------------------------------------------------------------------------ | ---------------------------------------- | -------- |
| payment\_type        | Set OVO payment method. Value: `ovo`                                           | String                                   | Required |
| transaction\_details | The details of the specific transaction such as `order_id` and `gross_amount`. | [Object](https://docs.midtrans.com/reference/transaction-details-object) | Required |
| item\_details        | Details of the item(s) purchased by the customer.                              | [Object](https://docs.midtrans.com/reference/item-details-object)        | Optional |
| customer\_details    | Details of the customer.                                                       | [Object](https://docs.midtrans.com/reference/customer-details-object)    | Optional |
| ovo                  | Charge details using OVO.                                                      | [Object](https://docs.midtrans.com/reference/ovo-object)                 | Required |

***

## OVO Charge Response

For OVO payments, a `pending` transaction status indicates that the transaction has been successfully created. After the transaction is initiated, Midtrans forwards the payment request to OVO. The customer then completes the payment in the OVO application. Once the payment is successful, Midtrans will send a payment notification to the Merchant’s server.

```json Pending
{
    "status_code": "201",
    "status_message": "Ovo transaction is created",
    "transaction_id": "{{midtrans_transaction_id}}",
    "order_id": "{{merchant_order_id}}",
    "merchant_id": "{{midtrans_merchant_id}}",
    "gross_amount": "30000.00",
    "currency": "IDR",
    "payment_type": "ovo",
    "transaction_time": "2025-11-12 14:26:53",
    "transaction_status": "pending",
    "fraud_status": "accept",
    "expiry_time": "2025-11-12 14:27:58",
    "payer_phone_number": "08111111111"
}
```
```json Failure
{
    "status_code": "404",
    "status_message": "User with requested phone number doesn't exist",
    "id": "781ea7c4-3fa3-41a3-a27f-a6ac1efc6c7e"
}
```

| JSON Attribute       | Description                                                                                    | Type   |
| :------------------- | :--------------------------------------------------------------------------------------------- | :----- |
| status\_code         | Status code of transaction charge result.                                                      | String |
| status\_message      | Description of transaction charge result.                                                      | String |
| transaction\_id      | Transaction ID given by Midtrans.                                                              | String |
| order\_id            | Order ID specified by you.                                                                     | String |
| merchant\_id         | Midtrans merchant ID                                                                           | String |
| gross\_amount        | Total amount of transaction in IDR.                                                            | String |
| currency             | Currency used for payment                                                                      | String |
| payment\_type        | Transaction payment method.                                                                    | String |
| transaction\_time    | Timestamp of transaction in ISO 8601 format. Time Zone: GMT+7.                                 | String |
| transaction\_status  | Status of OVO transaction. Possible values are<br />`pending`, `settlement`, `expire`, `deny`. | String |
| fraud\_status        | Midtrans fraud engine rule result. Possible values are `accept` or `denied`                    | String |
| expiry\_time         | Expiration time of the related transactions.                                                   | String |
| payer\_phone\_number | Customer's phone number that will be used to create payment request to OVO.                    | String |
| merchant\_invoice    | Unique identifier for payment provider specific request.                                       | String |

<br />

> 📘 Note
>
> Possible error codes are **400**, **401**, **402**, **406**, **410**