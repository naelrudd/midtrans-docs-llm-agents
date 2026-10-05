---
updatedAt: 2026-09-28T12:00:08.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Unbind Pay Account (GoPay Tokenizations)

Unbind Pay Account is triggered to remove the linked customer account. This method is only applicable for GoPay Tokenizations.

Endpoints: `/api/v1/core/pay/account/{{account_id}}/unbind`

HTTP Method: `POST`

## Response Body

```json Sample Response - Success
{
  "status_code": "204",
  "payment_type": "gopay",
  "account_id": "00000269-7836-49e5-bc65-e592afafec14",
  "account_status": "DISABLED",
  "channel_response_code": "0",
  "channel_response_message": "Process service request successfully."
}
```
```json Sample Response - Denied
{
  "status_code": "202",
  "payment_type": "gopay",
  "account_id": "00000269-7836-49e5-bc65-e592afafec14",
  "channel_response_code": "1001",
  "channel_response_message": "Caller authentication error."
}
```

| JSON Attribute             | Description                                                                                   | Type   |
| -------------------------- | --------------------------------------------------------------------------------------------- | ------ |
| status\_code               | Status code of the API result.                                                                | String |
| payment\_type              | Payment channel associated with the account.                                                  | String |
| account\_id                | Customer account id to be used for payment.                                                   | String |
| account\_status            | Status of the account. <br />Possible values are `PENDING`, `EXPIRED`, `ENABLED`, `DISABLED`. | String |
| channel\_response\_code    | Response code from payment channel provider.                                                  | String |
| channel\_response\_message | Response message from payment channel provider.                                               | String |

<br />

## Pay Account Unbind Notification

```json Sample Notification - Pay Account Unbind Notification
{
  "account_id": "00000269-7836-49e5-bc65-e592afafec14",
  "merchant_id": "M099098",
  "payment_type": "gopay",
  "signature_key": "ad7ccda03d8ec6f2f415661fb511d47fcd17dcc7d7e1ade96a305dd5d3bc2bea5438a8bdfe1aeedabdefb226000338ac169fc18d5ae73788fd5e78dbac945ce4",
  "status_code": "204",
  "account_status": "DISABLED",
  "status_message": "Midtrans account_unlinked notification"
}
```

Pay Account unbind notification will be sent to merchant when user unlinked the account from merchant services/payment provider service (ex: Gojek App). This notification sample can be seen on the side, and you can see [Handle notifications](https://docs.midtrans.com/reference/notifications-handling) section to know how to handle the notifications.

Specifically for GoPay Tokenization, user account will be automatically unlinked if user change GoPay PIN and phone number in Gojek app. Unbind notification will also be sent to merchant.