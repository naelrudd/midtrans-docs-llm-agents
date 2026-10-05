---
updatedAt: 2026-09-28T12:00:08.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Cancel API

Cancel transaction is triggered to void the transaction. If transaction is already settled (status : `settlement`) you should perform `refund` instead if the payment method supports it.

## Card Payment

Card payment can be voided with Cancel method if the transaction has not been settled. The time interval during which the pre-authorized transaction can be cancelled depends on the Acquiring Bank.

| Acquiring Bank                | Trigger Cancel Method                                         |
| ----------------------------- | ------------------------------------------------------------- |
| **BNI**                       | After pre-authorization payment has been captured.            |
| **Mandiri**                   | After the initial charge of the pre-authorized payment.       |
| **BCA**, **BRI**, **MAYBANK** | Before and after pre-authorization payment has been captured. |

***

## Pending Payment

Payment with `transaction_status:pending` can be voided with cancel method if the transaction has not expired or has not been completed. The list of payment methods with `transaction_status:pending` are given below.

* Bank Transfer: [Permata Virtual Account](https://docs.midtrans.com/reference/permata-virtual-account), [BCA Virtual Account](https://docs.midtrans.com/reference/bca-virtual-account), [Mandiri Bill Payment](https://docs.midtrans.com/reference/mandiri-bill-payment), [BNI Virtual Account](https://docs.midtrans.com/reference/bni-virtual-account), [BRI Virtual Account](https://docs.midtrans.com/reference/bri-virtual-account)
* Direct Debit: [BCA KlikPay](https://docs.midtrans.com/reference/bca-klikpay), [KlikBCA](https://docs.midtrans.com/reference/klikbca), [BRImo](/reference/brimo-1), [CIMB Clicks](https://docs.midtrans.com/reference/cimb-clicks), [Danamon Online Banking](https://docs.midtrans.com/reference/danamon-online-banking), [UOB Ezpay](https://docs.midtrans.com/reference/uob-ez-pay)
* E-money: [QRIS](https://docs.midtrans.com/reference/qris), [GoPay](https://docs.midtrans.com/reference/gopay), [ShopeePay](https://docs.midtrans.com/reference/shopeepay)
* Over the Counter: [Indomaret](https://docs.midtrans.com/reference/indomaret), [Alfamart](https://docs.midtrans.com/reference/alfamart)
* Cardless Credit: [Akulaku](https://docs.midtrans.com/reference/akulaku), [Kredivo](https://docs.midtrans.com/reference/kredivo)

Endpoints: `/api/v1/core/{{transaction_id}}/cancel`

HTTP Method: `POST`

## Response Body

```json 200 - Success
{
  "status_code" : "200",
  "status_message" : "Success, transaction is canceled",
  "transaction_id" : "249fc620-6017-4540-af7c-5a1c25788f46",
  "masked_card" : "48111111-1114",
  "order_id" : "example-1424936368",
  "payment_type" : "credit_card",
  "transaction_time" : "2015-02-26 14:39:33",
  "transaction_status" : "cancel",
  "fraud_status" : "accept",
  "bank" : "bni",
  "gross_amount" : "30000.00"
}
```
```json 200 - Error
{
  "status_code" : "412",
  "status_message" : "Merchant cannot modify the status of the transaction"
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
        Status code of transaction cancel result.
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
        Description of transaction cancel result.
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
        masked\_card
      </td>

      <td>
        String
      </td>

      <td>
        First 8-digits and last 4-digits of customer's credit card number.
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
        Transaction status after charge credit card transaction. Possible values are<br/>`capture` : Transaction is accepted by the bank and ready for settlement. <br /> **Note**: Cancel transaction to deny / cancel it. Otherwise, transaction is settled automatically. <br/>`deny`: transaction is denied by the bank or FDS.<br/>`authorize`: Credit card is authorized in pre-authorization feature.
      </td>
    </tr>

    <tr>
      <td>
        fraud\_status
      </td>

      <td>
        String
      </td>

      <td>
        Detection result by Fraud Detection System (FDS). Possible values are<br/>`accept` : Approved by FDS.<br/>`deny`: Denied by FDS. Transaction automatically failed.
      </td>
    </tr>

    <tr>
      <td>
        bank
      </td>

      <td>
        String
      </td>

      <td>
        The acquiring bank of the transaction.
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
  </tbody>
</Table>