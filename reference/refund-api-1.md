---
updatedAt: 2026-09-28T12:00:08.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Refund API

This API is used to reverse the money back to customers for previous successful transaction.

Refund transaction is called to reverse the money back to customers for transactions with payment status `Settlement`. If transaction's status is still `Pending` `Authorize` or `Capture` please use Cancel API instead. The same `refund_id` cannot be reused.

Refund transaction is supported only for `credit_card` , `gopay`, `shopeepay` , `QRIS` ,  and `akulaku` payment methods.

Refund request is made to Midtrans where Midtrans will then forward it to payment providers.

For QRIS with acquirers AirPay (Shopee) and ShopeePay, the maximum refund window is 24 hours. Airpay Shopee accepts refund only from 06:00 to 23:30 GMT+7.

While the maximum refund window for GoPay is as stated below:

* QRIS with acquirers GoPay: 45 days
* GoPay Tokenization and GoPay deeplink with GoPay payment option GOPAY\_COINS: 90 days
* Other GoPay transactions: 180 days

Endpoints: `/api/v1/core/{{transaction_id}}/refund/online/direct`

HTTP Method: `POST`

## Request Body

```json
{
  "refund_key": "reference1",
  "amount": 5000,
  "reason": "for some reason"
}
```

<Table align={[null,"left","left",null]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Attribute
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        refund\_key
      </td>

      <td>
        String
      </td>

      <td>
        Optional
      </td>

      <td>
        Merchant refund ID. If not passed then Midtrans creates a new one. It is recommended to use this parameter to avoid double refund attempt. Allowed characters are alphabets, numbers, dash (`-`), and underscore (`_`).
      </td>
    </tr>

    <tr>
      <td>
        amount
      </td>

      <td>
        Long
      </td>

      <td>
        Optional
      </td>

      <td>
        Amount to be refunded. By default whole transaction amount is refunded. Note :\
        `Shopeepay` does not support partial refund at the moment.
      </td>
    </tr>

    <tr>
      <td>
        reason
      </td>

      <td>
        String(255)
      </td>

      <td>
        Optional
      </td>

      <td>
        Reason justifying the refund. <br /> <hr />For GoPay & GoPay Tokenization payments, reason will be shown on customers' GoPay transaction history. <br /> <hr />Reason is mandatory for card payment with BNI as acquiring bank. If the value is not sent, Midtrans will autofill it with "refund request from merchant" to BNI.
      </td>
    </tr>
  </tbody>
</Table>

## Response Body

```json 200 - Success
{
  "status_code": "200",
  "status_message": "Success, refund request is approved",
  "transaction_id": "447e846a-403e-47db-a5da-d7f3f06375d6",
  "order_id": "vtcc05",
  "payment_type": "credit_card",
  "transaction_time": "2015-06-15 13:36:24",
  "transaction_status": "refund",
  "gross_amount": "10000.00",
  "refund_chargeback_id": 1,
  "refund_amount": "10000.00",
  "refund_key": "reference1"
}
```
```json 200 - Success (Partial Refund)
{
  "status_code": "200",
  "status_message": "Success, refund request is approved",
  "transaction_id": "447e846a-403e-47db-a5da-d7f3f06375d6",
  "order_id": "vtcc05",
  "payment_type": "credit_card",
  "transaction_time": "2015-06-15 13:36:24",
  "transaction_status": "partial_refund",
  "gross_amount": "10000.00",
  "refund_chargeback_id": 1,
  "refund_amount": "5000.00",
  "refund_key": "reference1"
}
```
```json 200 - Error (Invalid Refund)
{
  "status_code" : "412",
  "status_message" : "Merchant cannot modify the status of the transaction"
}
```
```json 200 - Error (Invalid Amount)
{
  "status_code" : "414",
  "status_message" : "Refund request is rejected due to invalid amount"
}
```
```json 200 - Error (Invalid Refund ID)
{
  "status_code" : "406",
  "status_message" : "Duplicate refund ID"
}
```

<Table align={[null,"left",null]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        status\_code
      </td>

      <td>
        String
      </td>

      <td>
        Status code of transaction refund result.
      </td>
    </tr>

    <tr>
      <td>
        status\_message
      </td>

      <td>
        String
      </td>

      <td>
        Description of transaction refund result.
      </td>
    </tr>

    <tr>
      <td>
        transaction\_id
      </td>

      <td>
        String
      </td>

      <td>
        Transaction ID given by Midtrans.
      </td>
    </tr>

    <tr>
      <td>
        order\_id
      </td>

      <td>
        String
      </td>

      <td>
        Order ID specified by you.
      </td>
    </tr>

    <tr>
      <td>
        payment\_type
      </td>

      <td>
        String
      </td>

      <td>
        The payment method used by the customer.
      </td>
    </tr>

    <tr>
      <td>
        transaction\_time
      </td>

      <td>
        String
      </td>

      <td>
        Timestamp of transaction in ISO 8601 format. Time Zone: GMT+7.
      </td>
    </tr>

    <tr>
      <td>
        transaction\_status
      </td>

      <td>
        String
      </td>

      <td>
        Transaction status after refund action. Possible values are<br/>`refund` : Transaction is fully refunded. <br/>`partial_refund`: transaction is partially refunded.
      </td>
    </tr>

    <tr>
      <td>
        gross\_amount
      </td>

      <td>
        String
      </td>

      <td>
        Total amount of transaction in IDR.
      </td>
    </tr>

    <tr>
      <td>
        refund\_chargeback\_id
      </td>

      <td>
        String
      </td>

      <td>
        Identification of the refund process.
      </td>
    </tr>

    <tr>
      <td>
        refund\_amount
      </td>

      <td>
        String
      </td>

      <td>
        Total amount to be refunded in IDR.
      </td>
    </tr>

    <tr>
      <td>
        refund\_key
      </td>

      <td>
        String
      </td>

      <td>
        Merchant refund reference key.
      </td>
    </tr>
  </tbody>
</Table>