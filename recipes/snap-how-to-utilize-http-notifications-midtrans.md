---
updatedAt: 2025-11-11T00:24:06.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# [SNAP] How to utilize HTTP Notifications Midtrans

```javascript JavaScript
curl -X POST \
  https://tokoecommerc.com/payment-notification-handler/ \
  -H 'User-Agent: Veritrans' \
  -H 'Accept: application/json'\
  -H 'Content-Type: application/json' \
  -d '{
  "transaction_time": "2020-01-09 18:27:19",
  "transaction_status": "capture",
  "transaction_id": "57d5293c-e65f-4a29-95e4-5959c3fa335b",
  "status_message": "midtrans payment notification",
  "status_code": "200",
  "signature_key": "16d6f84b2fb0468e2a9cf99a8ac4e5d803d42180347aaa70cb2a7abb13b5c6130458ca9c71956a962c0827637cd3bc7d40b21a8ae9fab12c7c3efe351b18d00a",
  "payment_type": "credit_card",
  "order_id": "Postman-1578568851",
  "merchant_id": "G141532850",
  "masked_card": "48111111-1114",
  "gross_amount": "10000.00",
  "fraud_status": "accept",
  "eci": "05",
  "currency": "IDR",
  "channel_response_message": "Approved",
  "channel_response_code": "00",
  "card_type": "credit",
  "bank": "bni",
  "approval_code": "1578569243927"
}'
```

# Handle Pending Transaction



There's a slight possibility that the transaction is still waiting for the card's 3DS provider to process/verify it, which then Snap will trigger redirection with `?transaction_status=pending` instead of `capture` or `settlement`.

# HTTP notification from Midtrans



When the transaction status changes, the customer is redirected to the Redirect URL and Midtrans sends HTTP notification to the merchant backend. This ensures that you are updated on the transaction status securely.

# Configure Payment Notification URL

<!-- javascript@2 -->

To configure the Payment Notification URL, follow the steps given below.

- Login to your MAP account.
- On the Home page, go to SETTINGS > CONFIGURATION.
- Configuration page is displayed.
- Enter Payment Notification URL.
- Click Update.

Please refer to [this docs](/docs/https-notification-webhooks#b-configuring-http-notifications-on-mapb) for more information.

# Sample HTTP Notifications Sent From Midtrans

<!-- javascript@6-26 -->

Some examples of how the HTTP notification will be sent from Midtrans side.

Please refer to [this docs](/docs/https-notification-webhooks#sample-for-various-payment-methods) for more different payment methods.