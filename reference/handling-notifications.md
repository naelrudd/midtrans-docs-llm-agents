---
updatedAt: 2025-11-11T00:41:59.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Handling Notifications

> 📘 Getting notifications of payment status
>
> See [here](/docs/https-notification-webhooks) for an in-depth guide of HTTP notification, or [here](/docs/handle-after-payment) for other types of notifications channel available for use.
>
> Ensure that email notification in General Settings is set to ensure various operations work as expected (e.g. save card / one click payments).

<br />

In order to receive payment status update for invoice, merchant can subscribe to Transaction notification. Subscribing to Transaction notification can be done by configuring `Payment Notification URL` on merchant dashboard.

Currently merchant will receive HTTP notification when

1. Invoice is paid by the user
2. Invoice is expired

Here's the sample of HTTP notification body for invoice transaction

```json JSON
{
  "va_numbers": [
    {
      "va_number": "333333333333333",
      "bank": "bca"
    }
  ],
  "transaction_time": "2021-06-23 11:27:20",
  "transaction_status": "settlement",
  "transaction_id": "9aed5972-5b6a-401e-894b-a32c91ed1a3a",
  "status_message": "midtrans payment notification",
  "status_code": "200",
  "signature_key": "fe5f725ea770c451017e9d6300af72b830a668d2f7d5da9b778ec2c4f9177efe5127d492d9ddfbcf6806ea5cd7dc1a7337c674d6139026b28f49ad0ea1ce5107",
  "settlement_time": "2021-06-23 11:27:50",
  "payment_type": "bank_transfer",
  "payment_amounts": [],
  "order_id": "bca-va-01",
  "merchant_id": "G141532850",
  "gross_amount": "100000.00",
  "fraud_status": "accept",
  "currency": "IDR",
  "metadata": {
    "midtrans_invoice_id": "65f295f869aa5a30f8fc0e1c"
  }
}
```

HTTP notification for invoice transaction will have `midtrans_invoice_id` inside metadata object. Merchant can use this field to know which invoice this transaction belongs to.