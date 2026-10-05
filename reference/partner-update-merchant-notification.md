---
updatedAt: 2026-09-28T12:00:08.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Update Notification API

Update merchant notification API is an API call that can be used to update the notification URL for a particular merchant under a Partner

#### Request Header

| Field         | Type   | Description                                           |
| :------------ | :----- | :---------------------------------------------------- |
| Authorization | String | Basic Base64Encode(partnerServerKey:)                 |
| X-PARTNER-ID  | String | Unique identifier for partner. Provided by Midtrans.  |
| X-MERCHANT-ID | String | Unique identifier for merchant. Provided by Midtrans. |

#### Request Body

| Field                           | Type   | Attribute | Description                                                         |
| :------------------------------ | :----- | :-------- | :------------------------------------------------------------------ |
| payment\_notification\_url      | String | Optional  | Notification URL for successful, failed, and more payment statuses. |
| iris\_notification\_url         | String | Optional  | Notification URL for payout and top up notifications                |
| recurring\_notification\_url    | String | Optional  | Notification URL for successful/failed recurring payment.           |
| pay\_account\_notification\_url | String | Optional  | Notification URL for successful/failed GoPay account linking        |
| finish\_payment\_redirect\_url  | String | Optional  | Redirect URL on payment completion                                  |

#### Example

`PATCH /api/v1/merchants/notifications`

```http
Authorization: Basic cGFydG5lci1hcGkta2V5Og==
X-PARTNER-ID: 82150823919040624621823174737537
X-MERCHANT-ID: 77788612106050785053951792116179
{
  "payment_notification_url": "https://merchant.com/midtrans-payment-notification",
  "iris_notification_url": "https://merchant.com/midtrans-payout-notification",
  "recurring_notification_url": "https://merchant.com/midtrans-recurring-notification",
  "pay_account_notification_url": "https://merchant.com/midtrans-pay-account-notification",
  "finish_payment_redirect_url": "https://merchant.com/midtrans-finish-payment-redirect"
}
```

#### Response

##### Body

| Field                           | Type      | Description                                                         |
| :------------------------------ | :-------- | :------------------------------------------------------------------ |
| status\_code                    | String    | Status code                                                         |
| status\_message                 | String    | Status message                                                      |
| error\_message                  | String    | Error message                                                       |
| errors                          | String    | Errors                                                              |
| error\_messages                 | String\[] | Error messages for partial success response                         |
| payment\_notification\_url      | String    | Notification URL for successful, failed, and more payment statuses. |
| iris\_notification\_url         | String    | Notification URL for payout and top up notifications                |
| recurring\_notification\_url    | String    | Notification URL for successful/failed recurring payment.           |
| pay\_account\_notification\_url | String    | Notification URL for successful/failed GoPay account linking        |
| finish\_payment\_redirect\_url  | String    | Redirect URL on payment completion                                  |

##### Successful Response

```json
{
  "status_code": "200",
  "status_message": "Success",
  "payment_notification_url": "https://merchant.com/midtrans-payment-notification",
  "iris_notification_url": "https://merchant.com/midtrans-payout-notification",
  "recurring_notification_url": "https://merchant.com/midtrans-recurring-notification",
  "pay_account_notification_url": "https://merchant.com/midtrans-pay-account-notification",
  "finish_payment_redirect_url": "https://merchant.com/midtrans-finish-payment-redirect"
}
```

##### Partial Success Response

In this case only iris\_notification\_url has failed to be updated due to internal server error. It can be safely retried independently of the other 3 URLs.

```json
{
  "status_code": "200",
  "status_message": "Partial Success",
  "payment_notification_url": "https://merchant.com/midtrans-payment-notification",
  "recurring_notification_url": "https://merchant.com/midtrans-recurring-notification",
  "pay_account_notification_url": "https://merchant.com/midtrans-pay-account-notification",
  "finish_payment_redirect_url": "https://merchant.com/midtrans-finish-payment-redirect",
  "error_messages": [
      "iris_notification_url: Internal server error"
  ]
}
```

##### Error Response 401

```json
{
    "status_code": "401",
    "status_message": "Partner is unauthorized"
}
```

##### Error Response 500

```json
{
    "error_message": "Internal server error",
    "errors": "Internal server error"
}
```