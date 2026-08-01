---
updatedAt: 2025-11-11T17:33:32.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Charge Transactions on Card

Charge method is triggered every time a transaction is performed. Send a Charge API request with payment details, transaction details, card details, customer details, item details, and shipping address. Successful request returns `status_code:200`.\
The attribute that is used is dependent on the payment method desired.

<br />

***

## Card Charge Request

```json Sample Request - Card Charge
{
  "payment_type": "credit_card",
  "transaction_details": {
    "order_id": "C17550",
    "gross_amount": 145000
  },
  "credit_card": {
    "token_id": "< your token ID >"
  },
  "item_details": [{
      "id": "a1",
      "price": 145000,
      "quantity": 2,
      "name": "Apel",
      "brand": "Fuji Apple",
      "category": "Fruit",
      "merchant_name": "Fruit-store"
    }],
    "customer_details": {
      "first_name": "BUDI",
      "last_name": "UTOMO",
      "email": "test@midtrans.com",
      "phone": "+628123456",
      "billing_address": {
        "first_name": "BUDI",
        "last_name": "UTOMO",
        "email": "test@midtrans.com",
        "phone": "081 2233 44-55",
        "address": "Sudirman",
        "city": "Jakarta",
        "postal_code": "12190",
        "country_code": "IDN"
      },
      "shipping_address": {
        "first_name": "BUDI",
        "last_name": "UTOMO",
        "email": "test@midtrans.com",
        "phone": "0 8128-75 7-9338",
        "address": "Sudirman",
        "city": "Jakarta",
        "postal_code": "12190",
        "country_code": "IDN"
      }
    }
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

      <th>
        Required
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        payment\_type
      </td>

      <td>
        The payment method used by the customer. <br /> Value: `credit_card`. <br />**Note**: For any transactions using payment card (credit or debit), `payment_type` is `credit_card`.
      </td>

      <td>
        String (255)
      </td>

      <td>
        Required
      </td>
    </tr>

    <tr>
      <td>
        transaction\_details
      </td>

      <td>
        The details of the specific transaction such as `order_id` and `gross_amount`.
      </td>

      <td>
        [Object](https://docs.midtrans.com/reference/transaction-details-object)
      </td>

      <td>
        Required
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
        [Object](https://docs.midtrans.com/reference/credit-card-object)
      </td>

      <td>
        Required
      </td>
    </tr>

    <tr>
      <td>
        item\_details
      </td>

      <td>
        Details of the item(s) purchased by the customer.
      </td>

      <td>
        [Object](https://docs.midtrans.com/reference/item-details-object)
      </td>

      <td>
        Optional
      </td>
    </tr>

    <tr>
      <td>
        customer\_details
      </td>

      <td>
        Details of the customer.
      </td>

      <td>
        [Object](https://docs.midtrans.com/reference/customer-details-object)
      </td>

      <td>
        Optional
      </td>
    </tr>
  </tbody>
</Table>

<br />

***

## Card Charge Response and Notifications

### Sample Response

```json Success
{
  "transaction_id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
  "order_id": "C17550",
  "gross_amount": "145000.00",
  "payment_type": "credit_card",
  "transaction_time": "2014-08-01 15:39:22",
  "transaction_status": "capture",
  "fraud_status": "accept",
  "masked_card": "48111111-1114",
  "status_code": "200",
  "bank": "bni",
  "status_message": "Success, Credit Card 3D Secure transaction is successful",
  "approval_code": "1408869563148",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "currency": "IDR",
  "card_type": "credit",
  "on_us": true,
  "channel": "dragon",
  "expiry_time":"2014-08-09 15:39:22",
  "settlement_time":"2014-08-09 19:00:00"
}
```
```json Error
{
    "status_code": "411",
    "status_message": "Token id is missing, invalid, or timed out"
}
```
```json Capture Notif
{
  "masked_card": "48111111-1114",
  "approval_code": "T58755",
  "bank": "bni",
  "transaction_time": "2014-08-01 15:39:22",
  "gross_amount": "145000.00",
  "order_id": "C17550",
  "payment_type": "credit_card",
  "signature_key": "8d22a6b625f395a1a2cf0e62497e20be433cbad3e8a8ff36bf6b40dbd47308125ccda93546eab8a3acd91390155082658ac25b10a6294c6660642e43a5edc8bb",
  "status_code": "200",
  "transaction_id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
  "transaction_status": "capture",
  "fraud_status": "accept",
  "status_message": "midtrans payment notification",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "card_type": "credit",
  "on_us": false
}
```
```json Deny Notif
{
  "masked_card": "48111111-1114",
  "approval_code": "338016",
  "bank": "bni",
  "transaction_time": "2014-08-01 15:39:22",
  "gross_amount": "145000.00",
  "order_id": "C17550",
  "payment_type": "credit_card",
  "signature_key": "763713b31cf59c886d3cc4a0c654a060a8e990080fe29fca75ae9e4ff9de804809c4e20977829844dac01a7ac1464a4eb095ad32482048398918987295dc5022",
  "status_code": "202",
  "transaction_id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
  "transaction_status": "deny",
  "fraud_status": "accept",
  "status_message": "midtrans payment notification",
  "channel_response_code": "05",
  "channel_response_message": "Do not honor",
  "card_type": "credit",
  "on_us": true
}
```
```json Challenge Notif
{
  "masked_card": "48111111-1114",
  "approval_code": "315762",
  "bank": "bni",
  "transaction_time": "2014-08-01 15:39:22",
  "gross_amount": "145000.00",
  "order_id": "C17550",
  "payment_type": "credit_card",
  "signature_key": "393f8b6b27f9f6385d8391642942e9534fd20dad20c0631b75b0746bfc314482af4411c93e958b691a63e9154676905b906234d1f12fca031f5be5593f7ec2c6",
  "status_code": "201",
  "transaction_id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
  "transaction_status": "capture",
  "fraud_status": "challenge",
  "status_message": "midtrans payment notification",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "card_type": "credit",
  "on_us": false
}
```
```json Settlement Notif
{
  "masked_card": "48111111-1114",
  "approval_code": "131755",
  "bank": "bni",
  "transaction_time": "2014-08-01 15:39:22",
  "gross_amount": "145000.00",
  "order_id": "C17550",
  "payment_type": "credit_card",
  "signature_key": "49e158a0c3f1913eae0902875324075c562daa39b2824b865db2242adea247a228960d2f1002392fdbc29c3271c2bc78ba72e588db9047a82932d0615ddc811f",
  "status_code": "200",
  "transaction_id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
  "transaction_status": "settlement",
  "fraud_status": "accept",
  "status_message": "midtrans payment notification",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "card_type": "credit"
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
        Order ID specified by you.
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
        The payment method used by the customer. <br /> Value: `credit_card`. <br />**Note**: For any transactions using payment card (credit or debit), `payment_type` is `credit_card`.
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
        Transaction status after charge card transaction. Possible values are <br/>`capture`: Transaction is accepted by the bank and ready for settlement. <br/>`deny`: Transaction is denied by the bank or FDS.<br/>`authorize`: Card is authorized in Pre-authorization feature.
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
        Detection result by Fraud Detection System (FDS). Possible values are <br/>`accept`: Approved by FDS.<br/>`deny`: Denied by FDS. Transaction automatically failed.
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
        status\_message
      </td>

      <td>
        Status message describing the result of the API request.
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
        Approval code. It can be used for refund. This does not exist on denied transaction.
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

    <tr>
      <td>
        on\_us
      </td>

      <td>
        Indicate whether issuing and acquiring bank is the same
      </td>

      <td>
        Boolean
      </td>
    </tr>

    <tr>
      <td>
        channel
      </td>

      <td>
        The name of the payment channel provider. More details on request and possible values are available on [Card Feature: Specific Channel](https://docs.midtrans.com/reference/feature-route-to-specific-channel).
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        expiry\_time
      </td>

      <td>
        For regular card transactions (non-recurring, non-one-click, non-two-click token) and the 3DS redirect\_url expires in 10 minutes. For authorized transaction expires in 8 days.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        settlement\_time
      </td>

      <td>
        Credit card settlement time refers to the duration it takes for a credit card transaction to be processed and transaction\_status change to settlement.
      </td>

      <td>
        String
      </td>
    </tr>
  </tbody>
</Table>

<br />

The `transaction_status` and `fraud_status` attributes are the two most important details received in the JSON response.

* Transaction status `capture` and fraud status `accept`: Transaction successful.
* Transaction status `deny` and fraud status `accept`,or `deny` : Transaction rejected by bank or by Fraud Detection System (FDS).
* Transaction status `capture` and fraud status `accept`: Customer’s card has been charged and the amount is credited to your account. At this point, the payment process of a transaction is complete.\
  Send the transaction status to the customer and also update the respective database. For example, you can mark if the respective order\_id has been paid for.\
  [Login to MAP](https://account.midtrans.com/login) to see the detail of the transaction and the transaction status. Alternatively, check the transaction status using [Get Transaction Status](https://docs.midtrans.com/reference/get-transaction-status).\ <br />By default, all card transactions from 00:00 until 23:59 are settled on the next day at 16:00. The transaction status is updated from `capture` to `settlement`.  Midtrans also sends HTTP POST notification to the Notification URL configured on MAP.