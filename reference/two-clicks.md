---
updatedAt: 2025-11-10T22:58:39.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Card Payment - Subscription (Two Clicks)

Two clicks feature allows you to capture customer's card number, expiry date, email and phone number as a `TWO_CLICKS_TOKEN`. For successive payments by the same customer the `TWO_CLICKS_TOKEN` can be utilized to pre-fill the details. Customer just needs to fill out the CVV number to finish the payment.

To activate subscriptions/recurring for your merchant account in production, please reach out to your Midtrans PIC or [Support team](https://midtrans.com/contact-us/payment-method-and-service-addition-1/pertanyaan-lain-4).

There are two steps required to utilize two clicks feature:

<br />

***

<br />

## Initial Transaction

<br />

* Create `SNAP_TOKEN` with `credit_card.save_card` value set to `true`
* Customer will be presented with save option when they fill out the credit card details
* If customer chooses the save option, then the [Transaction Result](#example-of-http-post-payment-notification) will have two extra fields namely `saved_token_id` (referred as `TWO_CLICKS_TOKEN`) and `saved_token_id_expired_at`

<br />

### Sample Implementation

```json Request SNAP_TOKEN with credit_card.save_card value set to true
{
  "transaction_details": {
    "order_id": "ORDER-101",
    "gross_amount": 10000
  },
  "credit_card": {
    "secure": true,
    "save_card": true
  }
}
```

<br />

### Example of HTTP Post Payment Notification

```json
{
    "status_code": "200",
    "status_message": "Success, Credit Card 3D Secure transaction is successful",
    "transaction_id": "f50c0aef-b629-4a5b-957b-4c52f45e2e63",
    "order_id": "A87550",
    "payment_type": "credit_card",
    "transaction_time": "2014-08-25 11:21:48",
    "transaction_status": "capture",
    "fraud_status": "accept",
    "masked_card": "481111-1114",
    "saved_token_id": "4811117d16c884-2cc7-4624-b0a8-10273b7f6cc8",
    "saved_token_id_expired_at": "2024-08-25 11:21:48",
    "approval_code": "1408940508666",
    "gross_amount": "145000.00",
    "eci": "05"
}
```

<br />

***

## Successive Transactions

<br />

* Create `SNAP_TOKEN` with `credit_card.card_token` value set to `TWO_CLICKS_TOKEN` saved during the initial transaction
* Customer will be presented with pre-filled credit card number, expiry date, email and phone number

<br />

### Sample Implementation

```json Request SNAP_TOKEN with credit_card.card_token value is being set
{
  "transaction_details": {
    "order_id": "ORDER-101",
    "gross_amount": 10000
  },
  "credit_card": {
    "secure": true,
    "card_token": "4811117d16c884-2cc7-4624-b0a8-10273b7f6cc8"
  }
}
```