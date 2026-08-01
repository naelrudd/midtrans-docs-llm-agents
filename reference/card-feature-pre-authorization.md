---
updatedAt: 2025-11-10T23:02:13.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Feature: Pre-Authorization

Pre-authorization payment feature temporarily blocks the fund from the customer's account. Successful Pre-authorization can be settled only if the transaction has been captured. You can initiate "capture" action through [Capture API](https://docs.midtrans.com/reference/capture-transaction). By default, reserved fund will be released after seven days if there is no "capture" action for that transaction.

You need a token from [Get Card Token](/reference/get-token#getting-card-token) response to charge with Pre-authorization feature.

<br />

***

<br />

## Pre-Authorization Charge Request

<br />

```json Sample Request - Pre-Authorization Charge
{
  "payment_type": "credit_card",
  "transaction_details": {
    "order_id": "C17550",
    "gross_amount": 145000
  },
  "credit_card": {
    "token_id": "< your token ID >",
    "bank": "bni",
    "type": "authorize"
  }
}
```
```coffeescript Sample Request - Pre-Authorization Charge With Full Pan
{
  "payment_type": "credit_card",
  "transaction_details": {
    "order_id": "C17550",
    "gross_amount": 145000
  },
  "credit_card": {
    "card": {
      "number": "4811111111111114",
      "expiry_month": "03",
      "expiry_year": "2020",
      "cvv": "123"
    },
    "bank": "bni",
    "type": "authorize"
  }
}
```

The `credit_card` object in Charge request to configure Pre-authorization feature is identical with [Card Payment Charge Request](/reference/charge-transactions-on-card), with the additional attributes given below.

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
        type
      </td>

      <td>
        Flag to indicate if the transaction is pre-authorized or automatically captured. Valid value: `authorize`. 
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        token\_id
      </td>

      <td>
        Token ID represents customer's card information acquired from [Get Card Token](/reference/get-token#get-card-token-response) response.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        credit\_card
      </td>

      <td>
        The details of the payment card used for the transaction.
      </td>

      <td>
        Object]\(ref:credit-card-object)
      </td>
    </tr>

    <tr>
      <td>
        credit\_card.card
      </td>

      <td>
        The details of the payment card used for the transaction.
      </td>

      <td>
        Object
      </td>
    </tr>

    <tr>
      <td>
        credit\_card.card.number
      </td>

      <td>
        Primary Account Number (PAN) of credit card.
      </td>

      <td>
        Integer (13-19)
      </td>
    </tr>

    <tr>
      <td>
        credit\_card.card.expiry\_month
      </td>

      <td>
        The card expiry month in MM format.
      </td>

      <td>
        String (2)
      </td>
    </tr>

    <tr>
      <td>
        credit\_card.card.expiry\_year
      </td>

      <td>
        The card expiry year in YYYY format.
      </td>

      <td>
        String (4)
      </td>
    </tr>

    <tr>
      <td>
        credit\_card.card.cvv
      </td>

      <td>
        Also known as Card Verification Code (CVC) shown at the back of the credit card.\
        Note: If card.cvv is not passed, then transaction will be treated as recurring.
      </td>

      <td>
        Integer (3-4)
      </td>
    </tr>
  </tbody>
</Table>

<br />

***

<br />

## Pre-Authorization Charge Response and Notifications

<br />

```json Sample Response - Success
{
    "status_code": "200",
    "status_message": "Success, Credit Card transaction is successful",
    "transaction_id": "be4f3e44-d6ee-4355-8c64-c1d1dc7f4590",
    "order_id": "C17550",
    "gross_amount": "145000.00",
    "payment_type": "credit_card",
    "transaction_time": "2016-07-02 14:00:27",
    "transaction_status": "authorize",
    "fraud_status": "accept",
    "approval_code": "003873",
    "eci": "05",
    "masked_card": "48111111-1114",
    "bank": "bca",
    "channel_response_code": "0",
    "channel_response_message": "Approved",
    "currency": "IDR",
    "card_type": "credit",
    "on_us": true
}
```
```json Sample Response - Pre-Authorization
{
  "masked_card": "48111111-1114",
  "approval_code": "003873",
  "bank": "bca",
  "eci": "05",
  "transaction_time": "2016-07-02 14:00:27",
  "gross_amount": "145000.00",
  "order_id": "C17550",
  "payment_type": "credit_card",
  "signature_key": "7156a83f0beb052c689e3775e60049062dd84379eda494b929704955957a41949df03c7010a0ad888347828f04b9288bdf541e044569372d1ab957295a6c5a14",
  "status_code": "200",
  "transaction_id": "be4f3e44-d6ee-4355-8c64-c1d1dc7f4590",
  "transaction_status": "authorize",
  "fraud_status": "accept",
  "status_message": "midtrans payment notification",
  "channel_response_code": "0",
  "channel_response_message": "Approved",
  "card_type": "credit",
  "on_us": false
}
```

Pre-authorization Charge response is different from the Card Payment Charge response.\
Successful Pre-authorization transaction is described as `authorize` and can be settled only if the transaction has been captured. To charge the customer after Pre-authorization, [Capture Transaction](https://docs.midtrans.com/reference/capture-transaction) method is used with `transaction_status` set to `authorize`.\
If the transaction is captured, the transaction status is updated to `capture` and is ready for settlement.

<br />

> 📘 Note
>
> Charge method in a Pre-authorized transaction checks and places a temporary hold on a customer’s card, and reserves funds.
>
> For settling the Pre-authorized transaction, use below Capture Transaction's method within seven days. After that, the Pre-authorized funds will be released back to the cardholder.
>
> Approve the transaction when <code>fraud\_status: challenge</code> to accept it or, the transaction will get cancelled automatically during settlement.

<br />

***

<br />

## Capture Transaction Method

<br />

| Endpoint          | HTTP Method | Definition                            |
| ----------------- | ----------- | ------------------------------------- |
| BASE\_URL/capture | POST        | Capture a Pre-authorized transaction. |

<br />

***

<br />

## Capture Transaction Request

<br />

```json Sample Request - Capture transaction
{
    "transaction_id" : "1ac1a089d-a587-40f1-a936-a7770667d6dd",
    "gross_amount" : 55000 // <--- Value should not exceed the Charge Value on Pre-Authorization
}
```

| JSON Attribute  | Description                                                                                                                                                                                                                                      | Type   |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------ |
| transaction\_id | Transaction ID from Charge Pre-Authorization Response.                                                                                                                                                                                           | String |
| gross\_amount   | Total amount of transaction in IDR. <br />**Note**: This value should not exceed `gross_amount` specified in Pre-Authorization Charge request. If left undefined, capture full transaction amount specified in Pre-Authorization Charge request. | Long   |

<br />

***

<br />

## Capture Transaction Response and Notification

<br />

```json Sample Response - Success
{
    "status_code": "200",
    "status_message": "Success, Credit Card capture transaction is successful",
    "transaction_id": "1ac1a089d-a587-40f1-a936-a7770667d6dd",
    "order_id": "A27550",
    "payment_type": "credit_card",
    "transaction_time": "2014-08-25 10:20:54",
    "transaction_status": "capture",
    "fraud_status": "accept",
    "masked_card": "48111111-1114",
    "bank": "bca",
    "eci": "05",
    "gross_amount": "55000.00",
    "channel_response_code": "0",
    "channel_response_message": "Approved",
    "currency": "IDR",
    "card_type": "credit"
}
```
```json Sample Response - Deny
{
  "status_code": "202",
  "status_message": "Deny by Bank [MANDIRI] with code [01] and message [Refer to card issuer]",
  "channel_response_code": "01",
  "channel_response_message": "Refer to card issuer",
  "bank": "mandiri",
  "transaction_id": "79e92a1c-01b4-4383-bfb5-e00af4bdf05f",
  "order_id": "order-11236345131993942",
  "merchant_id": "G479619422",
  "gross_amount": "7.00",
  "currency": "IDR",
  "payment_type": "credit_card",
  "transaction_time": "2023-02-15 17:28:12",
  "transaction_status": "deny",
  "fraud_status": "accept",
  "approval_code": "001122",
  "masked_card": "43650203-6407"
}
```
```json Sample Response - Capture Notification
{
  "masked_card": "48111111-1114",
  "approval_code": "T67700",
  "bank": "bca",
  "eci": "05",
  "transaction_time": "2014-08-25 10:20:54",
  "gross_amount": "55000.00",
  "order_id": "A27550",
  "payment_type": "credit_card",
  "signature_key": "23a7036edb8171b926e5292c7729c6bd26ed3250e22aead55110e34086dbc8fb393e7d3b7f764428a27c76e77d0a3bb6a7ba867066b2fbf5dae9e0f8a6c0dc0d",
  "status_code": "200",
  "transaction_id": "1ac1a089d-a587-40f1-a936-a7770667d6dd",
  "transaction_status": "capture",
  "fraud_status": "accept",
  "status_message": "midtrans payment notification",
  "channel_response_code": "0",
  "channel_response_message": "Approved",
  "card_type": "credit"
}
```

> 📘 Note
>
> Capture transaction is triggered to capture the transaction balance when `transaction_status:authorize`.
>
> The transaction status is updated to capture and is ready for settlement if bank response is successfully captured.
>
> If bank response with unsuccessfully captured, Midtrans will respond with `transaction_status:deny` on capture response and keep `transaction_status:authorize` as the latest status on Midtrans [Get Transaction Status](/reference/get-transaction-status-card). Merchant can try to re-capture or cancel the transaction. if there is no action for up to 8 days, the transaction will expire.

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
        Description of transaction charge result.
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
        The payment method used by the customer. Value: `credit_card`. <br />**Note**: For any transactions using payment card (credit or debit), `payment_type` is `credit_card`.
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
        Timestamp of transaction in ISO 8601 format. Time Zone: GMT+7.
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
        Transaction status after charge card transaction. Possible values are<br/>`capture`: Transaction is accepted by the bank and ready for settlement. <br/>`deny`: Transaction is denied by the bank or FDS.<br/>`authorize`: Card is authorized in Pre-authorization feature.
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
        Detection result by Fraud Detection System (FDS). Possible values are<br/>`accept`: Approved by FDS.<br/>`deny`: Denied by FDS. Transaction automatically failed.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        approval\_code
      </td>

      <td>
        Approval code from payment provider for successful transaction. It can be used for refund.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        eci
      </td>

      <td>
        The 3D secure ECI Code indicating the result of the 3DS process.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        masked\_card
      </td>

      <td>
        First 8-digits and last 4-digits of customer's card number.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        bank
      </td>

      <td>
        The name of the *Acquiring Bank*.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        channel\_response\_code
      </td>

      <td>
        Response code from payment channel provider.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        channel\_response\_message
      </td>

      <td>
        Response message from payment channel provider.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        card\_type
      </td>

      <td>
        Type of payment card used for the transaction. Possible values are `credit`, `debit`.
      </td>

      <td>
        String
      </td>
    </tr>
  </tbody>
</Table>