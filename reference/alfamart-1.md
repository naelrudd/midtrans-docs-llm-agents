---
updatedAt: 2025-11-10T23:04:27.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Alfamart

Using *Over the Counter* payment feature provided by Alfamart, the customer can perform online shopping and complete the payment at various stores under Alfa group. The supported stores are: Alfamart, Alfamidi, and DAN+DAN. Midtrans will send a real-time notification to you for every incoming payment.

The steps to integrate with Alfamart stores are given below.

1. Send the charge API request to Midtrans with the selected acquirer.
2. Display the payment code to customers.
3. [Handle notifications](/reference/notifications-handling).

Send a Charge API request with payment details, transaction details, convenience store details, customer details, and item details. Successful response returns `status_code:201`.

By default, default expiry time for Alfamart is 24 hours unless specified by merchant (min 20s, max 180 days).

<br />

***

<br />

## Alfamart Charge API Request

<br />

```json Sample Request - Charge API
{
  "payment_type": "cstore",
  "transaction_details": {
    "gross_amount": 162500,
    "order_id": "order05"
  },
  "cstore": {
    "store": "alfamart",
    "alfamart_free_text_1": "Thanks for shopping with us!,",
    "alfamart_free_text_2": "Like us on our Facebook page,",
    "alfamart_free_text_3": "and get 10% discount on your next purchase."
  },
  "customer_details": {
    "first_name": "Budi",
    "last_name": "Utomo",
    "email": "budi.utomo@midtrans.com",
    "phone": "0811223344"
  },
  "item_details": [
    {
      "id": "id1",
      "price": 162500,
      "quantity": 1,
      "name": "tiket2"
    }
  ]
}
```

| JSON Attribute       | Description                                                                    | Type                                     |
| -------------------- | ------------------------------------------------------------------------------ | ---------------------------------------- |
| payment\_type        | The payment method used by the customer. Value: `cstore`.                      | String                                   |
| transaction\_details | The details of the specific transaction such as `order_id` and `gross_amount`. | [Object](https://docs.midtrans.com/reference/transaction-details-object) |
| cstore               | Details of the convenience store.                                              | [Object](https://docs.midtrans.com/reference/convenience-store-object)   |
| customer\_details    | Details of the customer.                                                       | [Object](https://docs.midtrans.com/reference/customer-details-object)    |
| item\_details        | Details of the item(s) purchased by the customer.                              | [Object](https://docs.midtrans.com/reference/item-details-object)        |

<br />

***

<br />

## Alfamart Charge Response and Notifications

<br />

```json Success
{
    "status_code": "201",
    "status_message": "Success, cstore transaction is successful",
    "transaction_id": "f1d381f8-7519-4139-b28f-81c6b3dc38ea",
    "order_id": "order05",
    "gross_amount": "10500.00",
    "payment_type": "cstore",
    "transaction_time": "2016-06-28 16:22:49",
    "transaction_status": "pending",
    "fraud_status": "accept",
    "payment_code": "010811223344",
    "store": "alfamart"
}
```
```json Pending
{
  "status_code": "201",
  "status_message": "midtrans payment notification",
  "transaction_id": "e3f0b1b5-1941-4ffb-9083-4ee5a96d878a",
  "order_id": "order04",
  "gross_amount": "162500.00",
  "payment_type": "cstore",
  "transaction_time": "2016-06-19 17:18:07",
  "transaction_status": "pending",
  "signature_key": "2d488c1ff0adc2396ee9b9765807b6d53182a0aa17cd9bb251b99879099d4f727903a75440b1814539f565774f7a80de0a7336c81d2071b4d3efe92f15400e41",
  "payment_code": "25709650945026",
  "store": "alfamart"
}
```
```json Settlement
{
  "status_code": "200",
  "status_message": "midtrans payment notification",
  "transaction_id": "991af93c-1049-4973-b38f-d6052c72e367",
  "order_id": "order04",
  "gross_amount": "162500.00",
  "payment_type": "cstore",
  "transaction_time": "2016-06-20 11:44:07",
  "transaction_status": "settlement",
  "signature_key": "a198f93ac43cf98171dcb4bd0323c7e3afbee77a162a09e2381f0a218c761a4ef0254d7650602971735c486fea2e8e9c6d41ee65d6a53d65a12fb1c824e86f9f",
  "payment_code": "25709650945026",
  "store": "alfamart"
}
```
```json Expired
{
  "status_code": "202",
  "status_message": "midtrans payment notification",
  "transaction_id": "fd70880f-3458-4b16-9f09-289924185977",
  "order_id": "order04",
  "gross_amount": "162500.00",
  "payment_type": "cstore",
  "transaction_time": "2016-06-20 17:18:08",
  "transaction_status": "expire",
  "signature_key": "c260504a448018b4c4831b381f8a8c5088c37f2706dcc60b4d7d99a16e0ae3c22bc8945cb5177742386bab1ddb12e7c175e1f57686b488e215406fa40fc75481",
  "payment_code": "25709650945026",
  "store": "alfamart"
}
```

<Table>
  <thead>
    <tr>
      <th>
        JSON Attribute
      </th>

      <th>
        Description
      </th>

      <th>
        Type
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        status\_code
      </td>

      <td>
        Status code of transaction charge result.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        status\_message
      </td>

      <td>
        Message describing the status of the result of API request.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        transaction\_id
      </td>

      <td>
        Transaction ID given by Midtrans.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        order\_id
      </td>

      <td>
        Order ID specified by merchant.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        gross\_amount
      </td>

      <td>
        Total amount of transaction in IDR.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        payment\_type
      </td>

      <td>
        The payment method used by the customer. Value: `cstore`.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        transaction\_time
      </td>

      <td>
        Timestamp of transaction in ISO 8601 format. Time Zone (GMT+7).
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        transaction\_status
      </td>

      <td>
        Transaction status of Indomaret transaction. Possible values are `pending`, `settlement`, and `expire`.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        fraud\_status
      </td>

      <td>
        Detection result by Fraud Detection System (FDS). Possible values are<br/>`accept` : Approved by FDS.<br/>`challenge`: Questioned by FDS.<br />**Note**: [Approve transaction](/#approve-transaction) to accept it or transaction will auto cancel during settlement.<br/>`deny`: Denied by FDS. Transaction automatically failed.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        payment\_code
      </td>

      <td>
        Unique payment code for customer to complete the payment in Alfamart.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        store
      </td>

      <td>
        Convenience store identifier.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        signature\_key
      </td>

      <td>
        Special string to verify the integrity of the response. For more details refer [Verifying Notification Authenticity](/docs/https-notification-webhooks#verifying-notification-authenticity).
      </td>

      <td>
        String
      </td>
    </tr>
  </tbody>
</Table>

<br />

> 📘 Note
>
> Possible error codes are **400**, **401**, **402**, **406**, **410**