---
updatedAt: 2025-11-11T00:09:29.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Handle After Payment

## Getting Notified of Payment Status

You can get **notifications when the transaction status is updated** on Midtrans (payment success, expire, etc.), so that you can process the customer order accordingly. Once the payment process is completed by the customer, **Midtrans sends notification to you**. You can access notifications via any of the following methods:

#### [HTTP(S) Notification / Webhook](/docs/https-notification-webhooks)

You can have automated/programmatic transaction status update on your system.

* The most recommended & customizable way to receive notifications.

#### [Call API Get Status](/docs/get-status-api-requests)

Alternatively, you can also actively retrieve the transaction status from the Midtrans side.

* Enquire about the current transaction status by calling API **GET Status**.

#### [Email Notification](/docs/email-notification)

You can get notified to your email inbox at the event of a transaction.

* Simplest way to receive notifications.
* Requires no complicated set up.

#### [Merchant Administration Portal (MAP) Dashboard](/docs/midtrans-dashboard-usage)

You can view the transaction notifications on the dashboard of Midtrans Administrative Portal (MAP).

* Simple, easy and user-friendly.