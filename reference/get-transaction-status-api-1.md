---
updatedAt: 2026-09-28T12:00:08.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Get Transaction Status API

Endpoints: `/api/v1/core/{{transaction_id}}/status`

HTTP Method: `GET`

## Response Body

```json 200 - Success
{
  "status_code" : "200",
  "status_message" : "Success, Credit Card transaction is successful",
  "transaction_id" : "249fc620-6017-4540-af7c-5a1c25788f46",
  "masked_card" : "48111111-1114",
  "order_id" : "example-1424936368",
  "payment_type" : "credit_card",
  "transaction_time" : "2015-02-26 14:39:33",
  "transaction_status" : "capture",
  "fraud_status" : "accept",
  "approval_code" : "1424936374393",
  "signature_key" : "2802a264cb978fbc59f631c68d120cbda8dc853f5dfdc52301c615cf4f14e7a0b09aa...",
  "bank" : "bni",
  "gross_amount" : "30000.00",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "card_type": "credit",
  "payment_option_type": "GOPAY_WALLET",
  "shopeepay_reference_number": "103995032913255264",
  "reference_id": "DL-dduIy7XtGtvxJtNNpOfbAt"
}

```
```json 200 - Success (Refund)
{
  "status_code" : "200",
  "status_message" : "Success, refund request is approved by the bank",
  "transaction_id" : "249fc620-6017-4540-af7c-5a1c25788f46",
  "masked_card" : "48111111-1114",
  "order_id" : "example-1424936368",
  "payment_type" : "credit_card",
  "transaction_time" : "2015-02-26 14:39:33",
  "transaction_status" : "partial_refund",
  "fraud_status" : "accept",
  "approval_code" : "1424936374393",
  "signature_key" : "2802a264cb978fbc59f631c68d120cbda8dc853f5dfdc52301c615cf4f14e7a0b09aa...",
  "bank" : "bni",
  "gross_amount" : "30000.00",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "card_type": "credit",
  "payment_option_type": "GOPAY_WALLET",
  "refund_amount": "12000.00",
  "refunds": [
    {
      "refund_chargeback_id": 1,
      "refund_amount": "5000.00",
      "created_at": "2015-02-27 00:14:20",
      "reason": "some reason",
      "refund_key": "reference1"
    },
    {
      "refund_chargeback_id": 2,
      "refund_amount": "7000.00",
      "created_at": "2015-02-28 01:23:15",
      "reason": "",
      "refund_key": "reference2"
    },
  ]
}
```
```json 200 - Success (Point)
{
  "masked_card": "52412500-0127",
  "approval_code": "T12345",
  "bank": "bni",
  "eci": "02",
  "point_balance_amount": "1644.00",
  "point_redeem_amount": 80000,
  "point_redeem_quantity": 26667,
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "channel": "dragon",
  "three_ds_version": "2",
  "transaction_time": "2023-11-20 07:30:03",
  "custom_field1": "TEST1",
  "custom_field2": "TEST2",
  "gross_amount": "410400.00",
  "currency": "IDR",
  "order_id": "TKP2453912939",
  "payment_type": "credit_card",
  "signature_key": "d60dc0a9c7c3cd5c20399d99d56968c241dbaacc26444c2eebc541d3b0fad594cefb50dd866a83089ecba785bd153ee95c03d81a35ccf82689b15d8f57bdbb80",
  "status_code": "200",
  "transaction_id": "0c8b481d-8b99-4c6a-b735-aec18be92f28",
  "transaction_status": "capture",
  "fraud_status": "accept",
  "expiry_time": "2023-11-20 07:40:03",
  "status_message": "Success, Credit Card transaction is successful",
  "merchant_id": "B200000000000001005476",
  "card_type": "credit",
  "challenge_completion": true
}
```

<HTMLBlock>{`
<table>
<tr><th colspan="2">Field</th><th>Description</th><th>Type</th></tr>
<tr><td colspan="2">status_code</td><td>Status code of transaction. See this <a href="https://docs.midtrans.com/reference/transaction-status">section</a> for full list of transaction status.</td><td>String</td></tr>
<tr><td colspan="2">status_message</td><td>Description of transaction status.</td><td>String</td></tr>
<tr><td colspan="2">transaction_id</td><td>Transaction ID given by Midtrans.</td><td>String</td></tr>
<tr><td colspan="2">masked_card</td><td>First 8-digit and last 4-digit of customer's credit card number.</td><td>String</td></tr>
<tr><td colspan="2">order_id</td><td>Order ID specified by you.</td><td>String</td></tr>
<tr><td colspan="2">payment_type</td><td>The payment method used by the customer.</td><td>String</td></tr>
<tr><td colspan="2">transaction_time</td><td>Timestamp of transaction in ISO 8601 format. Time Zone: GMT+7.</td><td>String</td></tr>
<tr><td colspan="2">transaction_status</td><td>Transaction status after charge credit card transaction. Possible values are<br/><code>capture</code>: Transaction is accepted by the bank and ready for settlement. <br/><code>deny</code>: transaction is denied by the bank or FDS.<br/><code>authorize</code>: Credit card is authorized in pre-authorization feature.</td><td>String</td></tr>
<tr><td colspan="2">fraud_status</td><td>Detection result by Fraud Detection System (FDS). Possible values are<br/><code>accept</code>: Approved by FDS.<br/><code>deny</code>: Denied by FDS. Transaction automatically failed.</td><td>String</td></tr>
<tr><td colspan="2">approval_code</td><td>Approval code from payment provider for successful transaction. It can be used for refund.</td><td>String</td></tr>
<tr><td colspan="2">signature_key</td><td>Signature key to validate if the notification is originated from Midtrans. This field is used to validate notification to merchant, not to partner (multi-outlet).</td><td>String</td></tr>
<tr><td colspan="2">bank</td><td>The acquiring bank of the transaction.</td><td>String</td></tr>
<tr><td colspan="2">gross_amount</td><td>Total amount of transaction in IDR. </td><td>String</td></tr>
<tr><td colspan="2">channel_response_code</td><td>Response code from payment channel provider.</td><td>String</td></tr>
<tr><td colspan="2">channel_response_message</td><td>Response message from payment channel provider</td><td>String</td></tr>
<tr><td colspan="2">card_type</td><td>Type of card used. Possible values are <code>credit</code>, <code>debit</code>.</td><td>String</td></tr>
<tr><td colspan="2">payment_option_type</td><td>Type of payment that is being used, possible values are <code>GOPAY_WALLET</code>, <code>PAY_LATER</code>, <code>GO_CICIL</code>, <code>GOPAY_COINS</code> (more possible values will be added once we launch more payment option on Gopay). Only available for Gopay payment type.</td><td>String</td></tr>
<tr><td colspan="2">shopeepay_reference_number</td><td>Reference number given by ShopeePay. Only available for ShopeePay payment type and QRIS payment type with acquirer <code>airpay shopee</code>.</td><td>String</td></tr>
<tr><td colspan="2">reference_id</td><td>Reference ID given by payment provider. Only available for ShopeePay payment type and QRIS payment type with acquirer <code>airpay shopee</code>.</td><td>String</td></tr>
<tr><td colspan="2">refund_amount</td><td>Cumulative refund amount in \`IDR\`.</td><td>String</td></tr>
<tr><td colspan="2">refunds</td><td>List of refund details related to the transaction. Only available on transaction status <code>partial_refund</code> or <code>refund</code>.</td><td>JSON Array</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;refund_chargeback_id</td><td>Midtrans refund ID.</td><td>Long</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;refund_amount</td><td>Amount of the specific refund.</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;created_at</td><td>Timestamp of the refund creation.</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;reason</td><td>Reason the refund is created.</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;refund_key</td><td>Merchant refund reference.</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;refund_method</td><td>Refund confirmation method. The value is applied after Midtrans confirm the refund request (1 day after request is made). Possible values are <code>online</code>, <code>offline</code>.</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;bank_confirmed_at</td><td>Timestamp of receipt of refund request confirmation from acquiring bank.</td><td>String</td></tr>
<tr><td colspan="2">point_redeem_amount</td><td>Amount redeemed in IDR.</td><td>Long</td></tr>
<tr><td colspan="2">point_redeem_quantity</td><td>Point representation of point_redeem_amount.</td><td>Long</td></tr>
<tr><td colspan="2">point_balance_amount</td><td>Balance amount in IDR.</td><td>String</td></tr>
</table>
`}</HTMLBlock>