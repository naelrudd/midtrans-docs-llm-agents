---
updatedAt: 2025-11-11T00:31:13.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Feature: Installment

You can use Midtrans Installment Payment feature so that the customers can pay their bills in small amounts over a fixed period of time. These can be Online Installment Payment or Offline Installment Payment depending on the *Acquiring Bank* and the *Card Issuing Bank*. Successful request returns `transaction_status:capture` and is ready for settlement.

<br />

> 📘 Note:
>
> Installment feature is not supported for debit cards

***

<br />

## Online Installment Charge Request

In Online Installment feature, the *Acquiring Bank* and the *Card Issuing Bank* are the same.

You need a token from [Get Card Token](/reference/get-token#getting-card-token) response to charge with Online Installment feature.

```json Sample Request - Online Installment Charge
{
  "payment_type": "credit_card",
  "transaction_details": {
    "order_id": "C17550",
    "gross_amount": 145000
  },
  "credit_card": {
    "token_id": "< your token ID >",
    "bank": "bni",
    "installment_term": 12
  }
}
```

The `credit_card` object in Charge request to configure Online Installment feature is identical with [Card Charge Request](/reference/charge-transactions-on-card), with the additional attributes given below.

| JSON Attribute    | Description                                                                                                                            | Type    |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| token\_id         | Token ID represents customer's card information acquired from [Get Card Token](/reference/get-token#get-card-token-response) response. | String  |
| bank              | The name of the *Acquiring Bank*. **Note**: For Online installment, *Acquiring Bank* and *Card Issuing Bank* are the same.             | String  |
| installment\_term | Installment tenure in months.                                                                                                          | Integer |

<br />

***

<br />

## Online Installment Charge Response and Notifications

Successful installment transaction responds with `transaction_status: capture` and is ready for settlement.

```json Sample Response - Success
{
      "status_code": "200",
      "status_message": "Success, Credit Card transaction is successful",
      "transaction_id": "c1e1cc28-5208-4965-bc99-076919dc0a26",
      "order_id": "20527106",
      "gross_amount": "1687180.00",
      "payment_type": "credit_card",
      "transaction_time": "2016-06-19 09:12:15",
      "transaction_status": "capture",
      "fraud_status": "accept",
      "approval_code": "R71372",
      "masked_card": "48111111-1114",
      "bank": "bni",
      "installment_term": "6",
      "channel_response_code": "00",
      "channel_response_message": "Approved",
      "currency": "IDR",
      "card_type": "credit",
      "on_us": true
}
```
```json Sample Response - Online Installment Capture
{
  "masked_card": "48111111-1114",
  "approval_code": "R71372",
  "bank": "bni",
  "eci": "01",
  "installment_term": 6,
  "transaction_time": "2016-06-19 09:12:15",
  "gross_amount": "1687180.00",
  "order_id": "20527106",
  "payment_type": "credit_card",
  "signature_key": "4a4e59bdc26b3c473014f8dbc1bb9faf35c1f29c473f48666ea6faaf9d8eb80bf8e47be8d79ef4cdec820c6aecad7da198a64461cdf08937f7c56688fafb8448",
  "status_code": "200",
  "transaction_id": "c1e1cc28-5208-4965-bc99-076919dc0a26",
  "transaction_status": "capture",
  "fraud_status": "accept",
  "status_message": "midtrans payment notification",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "card_type": "credit",
  "on_us": false
}
```

> 📘 Note
>
> Approve the transaction when <code>fraud\_status: challenge</code> to accept it, or the transaction will get cancelled automatically during settlement.

<br />

***

<br />

## Offline Installment Charge Request

Offline Installment feature allows merchants to do installment conversion for transactions which are not supported by MID installment.

The `credit_card` object in Charge request to configure Offline Installment feature is identical with [Card Charge Request](/reference/charge-transactions-on-card), with the additional attribute `bins`. The purpose of `bins` is to limit the use of certain cards depending on the agreement between you and the bank.

```json Sample Request - Offline Installment Charge
{
  "payment_type": "credit_card",
  "transaction_details": {
    "order_id": "C17550",
    "gross_amount": 145000
  },
  "credit_card": {
    "token_id": "< your token ID >",
    "installment_term": 12,
    "bins": ["48111111", "3111", "5"]
  }
}
```

| JSON Attribute    | Description                                                                                                                            | Type       |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| token\_id         | Token ID represents customer's card information acquired from [Get Card Token](/reference/get-token#get-card-token-response) response. | String     |
| bank              | The name of the *Acquiring Bank*. **Note**: For Offline installment, *Acquiring Bank* and *Card Issuing Bank* are different.           | String     |
| installment\_term | Installment tenure in months.                                                                                                          | Integer    |
| bins              | List of card's BIN (Bank Identification Number) that is allowed for transaction.                                                       | JSON Array |

<br />

***

<br />

## Offline Installment Charge Response and Notifications

Successful installment transaction responds with `transaction_status: capture` and is ready for settlement.

```json Sample Response - Success
{
   "status_code": "200",
   "status_message": "Success, Credit Card transaction is successful",
   "transaction_id": "b046340b-dc40-480a-828f-085fc265850c",
   "order_id": "62465770",
   "gross_amount": "1352373.00",
   "payment_type": "credit_card",
   "transaction_time": "2016-06-19 05:41:18",
   "transaction_status": "capture",
   "fraud_status": "accept",
   "approval_code": "854442",
   "eci": "05",
   "masked_card": "48111111-1114",
   "bank": "bni",
   "installment_term": "6",
   "channel_response_code": "00",
   "channel_response_message": "Approved",
   "currency": "IDR",
   "card_type": "credit",
   "on_us": true
}
```
```json Sample Response - Offline Installment Notifications
{
  "masked_card": "48111111-1114",
  "approval_code": "833736",
  "bank": "bni",
  "eci": "05",
  "installment_term": 12,
  "transaction_time": "2016-07-04 14:00:55",
  "gross_amount": "16277555.00",
  "order_id": "160288134251",
  "payment_type": "credit_card",
  "signature_key": "1742c43dbda320dfe26a0e570eb8c95f710058967a2bb45b3996b664e19feb30aec8a6458be56ee310e7941fb89e3e3da09833b0f858fc8226bfa0442af2b5b0",
  "status_code": "201",
  "transaction_id": "3c1b1f1a-bfcf-4fa1-9a93-bebf5b9cb488",
  "transaction_status": "capture",
  "fraud_status": "challenge",
  "status_message": "midtrans payment notification",
  "card_type": "credit",
  "on_us": false
}
```