---
updatedAt: 2025-11-11T12:45:58.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# JS Callback

## Transaction Result

<br />

Object representing transaction result passed to [Snap callback](/reference/snap-js).

<br />

### Card Payment

<br />

```json Success credit card result
{
   "status_code":"200",
   "status_message":"Success, Credit Card transaction is successful",
   "transaction_id":"6d9677da-45a3-40d0-a0f0-8f0b2f860a64",
   "masked_card":"481111-1114",
   "order_id":"1459499971",
   "gross_amount":"10000.00",
   "payment_type":"credit_card",
   "transaction_time":"2016-04-01 15:39:58",
   "transaction_status":"capture",
   "fraud_status":"accept",
   "approval_code":"100057",
   "bank":"bni",
   "card_type":"credit"
}
```

<br />

### e-Channel

<br />

```json Pending e-channel result
{
   "status_code":"201",
   "status_message":"Transaksi sedang diproses",
   "transaction_id":"0ae66c29-e4a6-4e7b-b223-a103564a8d29",
   "order_id":"1459500813",
   "gross_amount":"10000.00",
   "payment_type":"echannel",
   "transaction_time":"2016-04-01 15:54:07",
   "transaction_status":"pending",
   "fraud_status":"accept",
   "bill_key":"001689",
   "biller_code":"70012",
   "pdf_url": "https://app.midtrans.com/snap/v1/transactions/0ae66c29-e4a6-4e7b-b223-a103564a8d29/pdf"
}
```
```json Success e-channel result
{
   "status_code":"200",
   "status_message":"Success, transaction is found",
   "transaction_id":"d2f79099-158d-413b-8968-cc23e0b0c99e",
   "order_id":"Farah-4998f180-f11f-488a-926f-abfa86519ba9",
   "gross_amount":"10000.00",
   "payment_type":"echannel",
   "transaction_time":"2022-08-01 15:55:36",
   "transaction_status":"settlement",
   "fraud_status":"accept",
   "bill_key":"992326882473",
   "biller_code":"70012",
   "pdf_url":"https://app.midtrans.com/snap/v1/transactions/7c873142-f9db-4404-a3fd-b7dacea61c47/pdf",
   "finish_redirect_url":"http://example.com?order_id=Farah-4998f180-f11f-488a-926f-abfa86519ba9&status_code=200&transaction_status=settlement"
}
```

<br />

### BNI VA & BRI VA

<br />

```json Pending BNI VA & BRI VA result
{
   "status_code":"201",
   "status_message":"Your Transaction is being processed",
   "transaction_id":"b9b651b6-2be9-4930-83fb-3bfa3b0a2f91",
   "order_id":"Farah-dc556491-51cc-4056-a184-c6d469c3dbc6",
   "gross_amount":"10000.00",
   "payment_type":"bank_transfer",
   "transaction_time":"2022-08-01 12:56:00",
   "transaction_status":"pending",
   "va_numbers":[{
      "bank":"bni",
      "va_number":"8202684534204029"
   }],
   "fraud_status":"accept",
   "pdf_url":"https://app.midtrans.com/snap/v1/transactions/630add54-9a0f-4abd-9a9b-8ac45a42e591/pdf",
   "finish_redirect_url":"http://example.com?order_id=Farah-dc556491-51cc-4056-a184-c6d469c3dbc6&status_code=201&transaction_status=pending"
}
```
```text Success BNI VA & BRI VA result
{
   "status_code":"200",
   "status_message":"Success, transaction is found",
   "transaction_id":"5bd36ae1-d331-4ba3-9bb0-71b4f97b3350",
   "order_id":"Farah-18b11c96-d38c-4a67-8e14-b5f658ce275c",
   "gross_amount":"10000.00",
   "payment_type":"bank_transfer",
   "transaction_time":"2022-08-01 13:02:34",
   "transaction_status":"settlement",
   "va_numbers":[{
      "bank":"bni",
      "va_number":"8202243460709261"
   }],
   "fraud_status":"accept",
   "pdf_url":"https://app.midtrans.com/snap/v1/transactions/9109f1f3-c1bb-4514-8265-e219f629f8d9/pdf",
   "finish_redirect_url":"http://example.com?order_id=Farah-18b11c96-d38c-4a67-8e14-b5f658ce275c&status_code=200&transaction_status=settlement"
}
```

<br />

### Permata VA

<br />

```json Pending Permata VA Result
{
   "status_code":"201",
   "status_message":"Your Transaction is being processed",
   "transaction_id":"b0073bad-880b-474f-bcca-80e35d06312d",
   "order_id":"Farah-0b06064b-54b3-46bf-bc33-5175283a9896",
   "gross_amount":"10000.00",
   "payment_type":"bank_transfer",
   "transaction_time":"2022-08-01 13:06:44",
   "transaction_status":"pending",
   "fraud_status":"accept",
   "permata_va_number":"491004103177391",
   "pdf_url":"https://app.midtrans.com/snap/v1/transactions/bae01323-1708-4f81-a7ad-3159bb27aad8/pdf",
   "finish_redirect_url":"http://example.com?order_id=Farah-0b06064b-54b3-46bf-bc33-5175283a9896&status_code=201&transaction_status=pending"
}
```
```json Success Permata VA Result
{
   "status_code":"200",
   "status_message":"Success, transaction is found",
   "transaction_id":"90fcd23e-7dce-4777-8234-6383bde34733",
   "order_id":"Farah-d2170e96-0939-4e97-af1a-ea0631a5281e",
   "gross_amount":"10000.00",
   "payment_type":"bank_transfer",
   "transaction_time":"2022-08-01 13:10:28",
   "transaction_status":"settlement",
   "fraud_status":"accept",
   "permata_va_number":"491007046084211",
   "pdf_url":"https://app.midtrans.com/snap/v1/transactions/19eff40c-e474-4711-bd72-c1dcaf23af6d/pdf",
   "finish_redirect_url":"http://example.com?order_id=Farah-d2170e96-0939-4e97-af1a-ea0631a5281e&status_code=200&transaction_status=settlement"
}
```

<br />

### BCA VA

<br />

```json Pending BCA VA Result
{
   "payment_type":"bank_transfer",
   "transaction_status":"pending",
   "pdf_url":"https://app.midtrans.com/snap/v1/transactions/f8eb89e6-50d7-4060-b4af-66170d9e0bf2/pdf",
   "finish_redirect_url":"http://example.com?order_id=Farah-40e5b947-9933-40c0-89f7-168f639e10d8&status_code=201&transaction_status=pending",
   "status_code":"201",
   "bca_va_number":"49112893603"
}
```
```json Success BCA VA Result
{
   "payment_type":"bank_transfer",
   "transaction_status":"settlement",
   "pdf_url":"https://app.midtrans.com/snap/v1/transactions/f8eb89e6-50d7-4060-b4af-66170d9e0bf2/pdf",
   "finish_redirect_url":"http://example.com?order_id=Farah-40e5b947-9933-40c0-89f7-168f639e10d8&status_code=200&transaction_status=settlement",
   "status_code":"200",
   "bca_va_number":"49112893603",
   "transaction_time":"2022-08-01 12:40:10",
   "gross_amount":"10000.00",
   "order_id":"Farah-40e5b947-9933-40c0-89f7-168f639e10d8",
   "transaction_id":"4f027746-7231-408a-aefa-481167b62e5e",
   "fraud_status":"accept",
   "status_message":"Success, transaction is found",
   "va_numbers":[{
      "bank":"bca",
      "va_number":"49112893603"
   }]
}
```

<br />

### GoPay

<br />

```json Pending GoPay QRIS Result
{
   "status_code":"201",
   "status_message":"Your Transaction is being processed",
   "transaction_id":"1030b91a-9cd0-4f71-b165-ec4e2e1835cc",
   "order_id":"Farah-8daaac75-9657-4b03-80ca-0cc89bab6be7",
   "gross_amount":"10000.00",
   "payment_type":"gopay",
   "transaction_time":"2022-08-01 13:36:04",
   "transaction_status":"pending",
   "fraud_status":"accept",
   "finish_redirect_url":"http://example.com?order_id=Farah-8daaac75-9657-4b03-80ca-0cc89bab6be7&status_code=201&transaction_status=pending"
}
```
```json Success GoPay QRIS Result
{
   "payment_type":"gopay",
   "transaction_status":"settlement",
   "pdf_url":null,
   "finish_redirect_url":"http://example.com?order_id=Farah-8daaac75-9657-4b03-80ca-0cc89bab6be7&status_code=200&transaction_status=settlement",
   "status_code":"200",
   "transaction_time":"2022-08-01 13:36:04",
   "gross_amount":"10000.00",
   "order_id":"Farah-8daaac75-9657-4b03-80ca-0cc89bab6be7",
   "transaction_id":"1030b91a-9cd0-4f71-b165-ec4e2e1835cc",
   "fraud_status":"accept",
   "status_message":"Success, transaction is found"
}
```
```json Pending GoPay Deeplink Result
{
   "payment_type":"gopay",
   "transaction_status":"pending",
   "pdf_url":null,
   "finish_redirect_url":"http://example.com?order_id=Farah-4acd7c82-07b0-4ed7-91df-8fb7740c078a&status_code=201&transaction_status=pending",
   "status_code":"201"
}
```

<br />

### Shopeepay

<br />

```json Pending Shopeepay QRIS Result
{
   "status_code":"201",
   "status_message":"Your Transaction is being processed",
   "transaction_id":"cfe7aee8-774b-45a9-a81b-29de33aed349",
   "order_id":"Farah-9ca61c03-51ab-43b1-b788-fa4a5a9259ce",
   "gross_amount":"10000.00",
   "payment_type":"qris",
   "transaction_time":"2022-08-01 13:48:34",
   "transaction_status":"pending",
   "fraud_status":"accept",
   "finish_redirect_url":"http://example.com?order_id=Farah-9ca61c03-51ab-43b1-b788-fa4a5a9259ce&status_code=201&transaction_status=pending"
}
```

<br />

### Indomaret

<br />

```json Pending Indomaret Trx Result
{
   "status_code":"201",
   "status_message":"Your Transaction is being processed",
   "transaction_id":"06160057-7f70-47aa-8edb-b17ea129d675",
   "order_id":"Farah-d3a87270-8b96-406a-910b-bfcf87f210d9",
   "gross_amount":"10000.00",
   "payment_type":"cstore",
   "transaction_time":"2022-08-01 13:52:07",
   "transaction_status":"pending",
   "payment_code":"G7723491121852129730",
   "pdf_url":"https://app.midtrans.com/snap/v1/transactions/f9c65342-d7d8-4e8c-bff6-90cdc9fd9573/pdf",
   "finish_redirect_url":"http://example.com?order_id=Farah-d3a87270-8b96-406a-910b-bfcf87f210d9&status_code=201&transaction_status=pending"
}
```
```json Success Indomaret Trx Result
{
   "status_code":"200",
   "status_message":"Success, transaction is found",
   "transaction_id":"3afd0454-4ebf-4167-9088-01708743ad9f",
   "order_id":"Farah-41d629bc-2ff3-490d-b695-f21d403cc972",
   "gross_amount":"10000.00",
   "payment_type":"cstore",
   "transaction_time":"2022-08-01 15:29:57",
   "transaction_status":"settlement",
   "payment_code":"G7723491122452129730",
   "pdf_url":"https://app.midtrans.com/snap/v1/transactions/fe4246a2-cff3-4971-88a8-b5de58505876/pdf",
   "finish_redirect_url":"http://example.com?order_id=Farah-41d629bc-2ff3-490d-b695-f21d403cc972&status_code=200&transaction_status=settlement"
}
```

<br />

### Alfamart

<br />

```json Pending Alfamart Trx Result
{
   "status_code":"201",
   "status_message":"Your Transaction is being processed",
   "transaction_id":"42d4cd59-b51a-4ad7-9a0d-14392f68fe53",
   "order_id":"Farah-014d66ae-0968-4a75-802f-e75da350aecb",
   "gross_amount":"10000.00",
   "payment_type":"cstore",
   "transaction_time":"2022-08-01 15:22:08",
   "transaction_status":"pending",
   "fraud_status":"accept",
   "payment_code":"9909743975002416",
   "pdf_url":"https://app.midtrans.com/snap/v1/transactions/2d42293b-1b76-495d-81da-07d5e30ba103/pdf",
   "finish_redirect_url":"http://example.com?order_id=Farah-014d66ae-0968-4a75-802f-e75da350aecb&status_code=201&transaction_status=pending"
}
```
```json Success Alfamart Trx Result
{
   "status_code":"200",
   "status_message":"Success, transaction is found",
   "transaction_id":"dc6cb612-276f-4a16-a4a2-a9a23fccd18e",
   "order_id":"Farah-250c1613-75d8-4cf9-ac82-2a73cc5142b3",
   "gross_amount":"10000.00",
   "payment_type":"cstore",
   "transaction_time":"2022-08-01 15:45:07",
   "transaction_status":"settlement",
   "fraud_status":"accept",
   "payment_code":"9909736722245808",
   "pdf_url":"https://app.midtrans.com/snap/v1/transactions/c63c3afa-f416-4558-9d70-2538f38491e2/pdf",
   "finish_redirect_url":"http://example.com?order_id=Farah-250c1613-75d8-4cf9-ac82-2a73cc5142b3&status_code=200&transaction_status=settlement"
   }
```

<br />

## Error Result

<br />

```json
{
  "status_code": "406",
  "status_message": ["transaction has been processed"]
}
```

<br />

## Definition

<br />

| Name                                        | Description                                                                                                                                                                                                                                                                                            |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| status\_code <br /> String                  | Transaction status code. Possible values: `200`, `201`, `202`, `400`, `404`, `406`, `500`                                                                                                                                                                                                              |
| status\_message <br /> String               | Transaction status message                                                                                                                                                                                                                                                                             |
| order\_id <br /> String                     | Merchant's unique payment ID or order ID                                                                                                                                                                                                                                                               |
| gross\_amount <br /> String                 | Processed gross amount                                                                                                                                                                                                                                                                                 |
| payment\_type <br /> Array (optional)       | Selected payment type for transaction. Possible values: <br />**Credit Cards**:<br /> `credit_card`. <br />**Banks**:<br /> `echannel` (mandiri va/bill), `bank_transfer`, `bca_klikpay`, `bca_klikbca`, `bri_epay`. <br />**E-wallets**:<br />  `gopay`, `qris`. <br />**Merchants**:<br /> `cstore`. |
| transaction\_id <br /> String               | Transaction ID                                                                                                                                                                                                                                                                                         |
| transaction\_time <br /> String             | Timestamp in `yyyy-MM-dd hh:mm:ss` format                                                                                                                                                                                                                                                              |
| transaction\_status <br /> String           | Transaction status. Possible values: `capture`, `settlement`, `pending`, `cancel`, `expired`                                                                                                                                                                                                           |
| fraud\_status <br /> String                 | Fraud status. Possible values: `accept`, `deny`                                                                                                                                                                                                                                                        |
| approval\_code <br /> String                | Bank approval code                                                                                                                                                                                                                                                                                     |
| masked\_card <br /> String                  | Customer's masked card (only in `credit_card`)                                                                                                                                                                                                                                                         |
| bank <br /> String                          | Acquiring Bank                                                                                                                                                                                                                                                                                         |
| permata\_va\_number <br /> String           | Permata VA Number (only in `bank_transfer` using `permata_va`)                                                                                                                                                                                                                                         |
| bca\_va\_number <br /> String               | Bca VA Number (only in `bank_transfer` using `bca_va`)                                                                                                                                                                                                                                                 |
| bill\_key <br /> String                     | Customer bill key (only in `echannel`)                                                                                                                                                                                                                                                                 |
| biller\_code <br /> String                  | Customer biller code (only in `echannel`)                                                                                                                                                                                                                                                              |
| saved\_token\_id <br /> String              | `TWO_CLICKS_TOKEN` value. Only available in `credit_card` payment type                                                                                                                                                                                                                                 |
| saved\_token\_id\_expired\_at <br /> String | Specifies the expiration time of the `TWO_CLICKS_TOKEN`                                                                                                                                                                                                                                                |
| card\_type <br /> String                    | Type of card used. Possible values: `credit`, `debit`                                                                                                                                                                                                                                                  |
| pdf\_url <br /> String                      | Link to show the payment instructions. Used for most asynchronous payment channels.                                                                                                                                                                                                                    |
| va\_numbers <br /> Array object             | Virtual Account informations that only appear in `bank_transfer` using va except `echanel`, `permata va`. Possible values: `[{ bank: <bank>, va_number: <va_number> }]`                                                                                                                                |

<br />

> 🚧
>
> For security reason, results from JS callback should only be used for UI feedback to user and should NOT be used to alter transaction status on your database. We provide HTTP Notification for that purpose. You can set your payment HTTP Notification URL in [Settings - Configuration](https://dashboard.sandbox.midtrans.com/settings/vtweb_preference).

<br />