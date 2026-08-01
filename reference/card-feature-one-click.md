---
updatedAt: 2025-11-10T23:02:15.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Feature: One Click

One Click feature allows your customers to make purchases with just *one click* using previously saved payment information.\
The additional attributes in `credit-card` object required to configure One Click feature are `token_id`, `saved_token_id`. Successful request returns `transaction_status:capture` and is ready for settlement.

You need a token from [Get Card Token](/reference/get-token#getting-card-token) response to charge with One Click feature.

<br />

***

<br />

## One Click Initial Charge Request

<br />

```json Sample Request - Initial One Click Charge
{
    "payment_type": "credit_card",
    "credit_card": {
        "token_id": "4811117d16c884-2cc7-4624-b0a8-10273b7f6cc8",
        "save_token_id": true     // <-- To flag that token is saved during initial charge
    },
    "transaction_details": {
        "order_id": "A87550",
        "gross_amount": 145000
    }
}
```

The `credit_card` object in Charge request to configure the initial One Click feature is identical with [Card Charge Request](/reference/charge-transactions-on-card#card-charge-request), with the additional attributes given below.

| JSON Attribute  | Description                                                                                                                       | Type    |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------- | ------- |
| token\_id       | Token ID represents customer's card information acquired from [Get Card Token](/reference/get-token#getting-card-token) response. | String  |
| save\_token\_id | A flag to indicate whether the `token_id` is saved for future transactions.                                                       | Boolean |

<br />

***

<br />

## One Click Initial Charge Response and Notifications

<br />

```json Sample Response - Card Payment Initial One Click
{
    "status_code": "200",
    "status_message": "Success, Credit Card 3D Secure transaction is successful",
    "transaction_id": "f50c0aef-b629-4a5b-957b-4c52f45e2e63",
    "order_id": "A87550",
    "payment_type": "credit_card",
    "transaction_time": "2014-08-25 11:21:48",
    "transaction_status": "capture",
    "fraud_status": "accept",
    "masked_card": "48111111-1114",
    "saved_token_id": "4811117d16c884-2cc7-4624-b0a8-10273b7f6cc8",
    "saved_token_id_expired_at": "2024-08-25 11:21:48",
    "approval_code": "1408940508666",
    "gross_amount": "145000.00",
    "bank": "bni",
    "channel_response_code": "00",
    "channel_response_message": "Approved",
    "currency": "IDR",
    "card_type": "credit",
    "on_us": true
}
```
```json Sample Response - Initial One Click Notification
{
  "masked_card": "48111111-1114",
  "approval_code": "1408940508666",
  "bank": "bni",
  "eci": "05",
  "saved_token_id": "4811117d16c884-2cc7-4624-b0a8-10273b7f6cc8",
  "saved_token_id_expired_at": "2024-08-25 11:21:48",
  "transaction_time": "2014-08-25 11:21:48",
  "gross_amount": "145000.00",
  "order_id": "A87550",
  "payment_type": "credit_card",
  "signature_key": "c77f17bf6a8dee35c19f02f2c33f9e4a2ee61b4bad15370a9f0f149a96909c8d887a0e0cddeb47bd02e88f369422aee6e323aaf938bb7bc5c55228459babbdb1",
  "status_code": "200",
  "transaction_id": "f50c0aef-b629-4a5b-957b-4c52f45e2e63",
  "transaction_status": "capture",
  "fraud_status": "accept",
  "status_message": "midtrans payment notification",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "card_type": "credit",
  "on_us": false
}
```

One Click Initial Charge response and notifications are identical with [Card Payment Charge](/reference/charge-transactions-on-card#card-charge-request) response and notifications, with additional attributes given below.

| JSON Attribute                | Description                                                   | Type   |
| ----------------------------- | ------------------------------------------------------------- | ------ |
| saved\_token\_id              | Token ID of a card to be charged for the future transactions. | String |
| saved\_token\_id\_expired\_at | Expiry date of the Token ID.                                  | String |

<br />

***

<br />

## One Click Subsequent Charge

<br />

```json Sample Request - Subsequent One Click Charge
{
    "payment_type": "credit_card",
    "credit_card": {
        "token_id": "44811117d16c884-2cc7-4624-b0a8-10273b7f6cc8"
    },
    "transaction_details": {
        "order_id": "A87551",
        "gross_amount": 145000
    }
}
```

You need `saved_token_id` from initial Charge response in order to charge future One Click transactions.

| JSON Attribute | Description                                                                                              | Type   |
| -------------- | -------------------------------------------------------------------------------------------------------- | ------ |
| token\_id      | `saved_token_id` represents customer's card information acquired from One Click initial Charge response. | String |

<br />

***

<br />

## One Click Subsequent Charge Response and Notifications

<br />

Subsequent One Click Charge response is identical with [Card Payment Charge Response](/reference/charge-transactions-on-card#card-charge-response-and-notifications).\
Successful One Click transaction is described as `capture` and is ready for settlement.

<br />

***

<br />

## One Click with CIT and MIT

To increase payment acceptance rate during **one click recurring payment**, the customer participant can be defined in the charge request. The types are CIT (Customer-Inititated Transactions) and MIT (Merchant-Initiated Transaction).

## CIT (Customer-Initiated Transactions)

Customer-Initiated Transactions (CIT) are payments actively initiated by the cardholder, typically through an online checkout or point-of-sale interaction. These transactions involve real-time authorization as the cardholder provides payment details, such as card number and CVV, to complete the purchase. CITs are commonly used for recurring payment with saved card triggered by customer / card holder. They prioritize security and cardholder consent, ensuring compliance with card network standards for a seamless payment experience.

```Text sample CIT request
{
    "payment_type": "credit_card",
    "credit_card": {
        "token_id": "41111111ugjzrxeHHXXmCMhhCVXbJ8888", 
        "authentication": false,
        "initiated_by": "customer"
 },
    "transaction_details": {
        "order_id": "A87550",
        "gross_amount": 145000
    }
}
```

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        JSON Attribute
      </th>

      <th>
        Description
      </th>

      <th>
        Mandatory
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        credit\_card.token\_id
      </td>

      <td>
        Contain temporary token that merchant get from GET Token or contain saved card that was previously stored on midtrans vault.
      </td>

      <td>
        yes
      </td>
    </tr>

    <tr>
      <td>
        credit\_card.authentication
      </td>

      <td>
        "true": if merchant willing to enable 3DS for transaction\
        Default: "false"
      </td>

      <td>
        optional
      </td>
    </tr>

    <tr>
      <td>
        credit\_card.initiated\_by
      </td>

      <td>
        Filled with value "customer" by default
      </td>

      <td>
        optional
      </td>
    </tr>
  </tbody>
</Table>

## MIT (Merchant Initiated Transactions)

Merchant Initiated Transactions (MIT) enable merchants to process payments using saved credit card information without requiring the cardholder's direct involvement at the time of the transaction. This feature is commonly used for recurring payments, subscriptions, or post-purchase charges. Payments are securely initiated by the merchant, leveraging tokenized card data to ensure compliance with PCI-DSS standards. MIT simplifies customer experience, enhances transaction efficiency, and is supported by card networks with appropriate authentication and agreement from the cardholder.

> 📘 Note
>
> To enable MIT feature merchants need to send attribute "initiated\_by":"merchant" under "credit\_card object".

```Text sample MIT request
{
    "payment_type": "credit_card",
    "credit_card": {
        "token_id": "41111111ugjzrxeHHXXmCMhhCVXbJ8888", 
        "initiated_by":"merchant"
    },
    "transaction_details": {
        "order_id": "A87550",
        "gross_amount": 145000
    }
}
```

| JSON Attribute             | Description                                                                                                                  | Mandatory |
| :------------------------- | :--------------------------------------------------------------------------------------------------------------------------- | :-------- |
| credit\_card.token\_id     | Contain temporary token that merchant get from GET Token or contain saved card that was previously stored on midtrans vault. | yes       |
| credit\_card.initiated\_by | Filled with value "merchant"                                                                                                 | yes       |