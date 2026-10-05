---
updatedAt: 2026-09-28T12:00:08.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Get Transaction Status B2B API

Get Transaction Status B2B is triggered to obtain the transaction status for all B2B transactions related to an `order_id`. B2B here refers to bank transfer or virtual account transaction which can be paid multiple times by customer or open amount virtual account.

Endpoints: `/api/v1/core/{{transaction_id}}/status/b2b?page=1&per_page=10`

HTTP Method: `GET`

## Request Query Parameter

| Query Parameter | Attribute | Description                                                 |
| --------------- | --------- | ----------------------------------------------------------- |
| page            | Optional  | Index of the search. Default is `0`.                        |
| per\_page       | Optional  | Number of transactions displayed per page. Default is `10`. |

Say merchant has five transactions created under a certain order\_id **A**. The transactions are **B**, **C**, **D**, **E**, **F** (ordered to the latest). Below are the examples on how merchant can use `page` and `per_page` parameters.

1. `per_page` is not set, `page` is not set: Merchant gets **F**, **E**, **D**, **C**, **B**, **A**
2. `per_page` is set 2, `page` is not set: Merchant gets **F**, **E**
3. `per_page` is set 2, `page` is set 1: Merchant gets **D**, **C**
4. `per_page` is set 3, `page` is set 1: Merchant gets **C**, **B**, **A**

## Response Body

```json 200 - Success
{
  "status_code": "200",
  "status_message": "Success, transactions are retrieved",
  "transactions": [
    {
      "payment_type": "echannel",
      "bill_key": "990568881594",
      "transaction_time": "2016-09-17 06:36:31",
      "gross_amount": "6000.00",
      "order_id": "vttesta73fb08ebd1-160916233631561",
      "signature_key": "ae85d0ade1bcdfdce4400b63918a8250b3ce45056621c743f71c02197e851accae43787190ee343b18f665d811a4e4d372bddbd347bda588a90d89c1b1c4ed53",
      "status_code": "200",
      "transaction_id": "647c9366-596a-4ba2-b20f-77baaa1e6647",
      "transaction_status": "settlement",
      "fraud_status": "accept",
      "status_message": "Success, transaction is found"
    },
    {
      "payment_type": "echannel",
      "bill_key": "990568881594",
      "transaction_time": "2016-09-17 06:34:52",
      "gross_amount": "6000.00",
      "order_id": "vttesta73fb08ebd1",
      "signature_key": "e8ae2f8cba40fe505c3c0f8bfec8dbc748ee5c8d04ad0699f33d17b7fc6aba5b1218f518226b4ea2ff095cb60125a5e6e1cb345608446378d29cb10ad687f560",
      "status_code": "200",
      "transaction_id": "f9a6684f-e3b4-46dd-8b6c-b61d805b3c6f",
      "transaction_status": "settlement",
      "fraud_status": "accept",
      "status_message": "Success, transaction is found"
    }
  ]
}
```

<HTMLBlock>{`
<table>
<tr><th colspan="2">Field</th><th>Description</th><th>Type</th></tr>
<tr><td colspan="2">status_code</td><td>Status code of transaction charge result</td><td>String</td></tr>
<tr><td colspan="2">status_message</td><td>Description of transaction charge result.</td><td>String</td></tr>
<tr><td colspan="2">transactions</td><td>Details of transaction</td><td>JSON Array</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;payment_type</td><td>The payment method used by the customer.</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;bill_key</td><td></td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;transaction_time</td><td>Timestamp of transaction in ISO 8601 format. Time Zone: GMT+7.</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;gross_amount</td><td>Total amount of transaction in IDR.</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;order_id</td><td>Order ID specified by you.</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;signature_key</td><td>Signature key to validate if the notification is originated from Midtrans.</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;status_code</td><td>Status code of transaction charge result.</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;transaction_id</td><td>Transaction ID given by Midtrans.</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;transaction_status</td><td>Transaction status after charge credit card transaction. Possible values are<br/><code>capture</code> : Transaction is accepted by the bank and ready for settlement. <br/><code>deny</code>: transaction is denied by the bank or FDS.<br/><code>authorize</code>: Credit card is authorized in pre-authorization feature.</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;fraud_status</td><td>Detection result by Fraud Detection System (FDS). Possible values are<br/><code>accept</code> : Approved by FDS.<br/><code>deny</code>: Denied by FDS. Transaction automatically failed.</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;status_message</td><td>Description of transaction charge result.</td><td>String</td></tr>
</table>
`}</HTMLBlock>