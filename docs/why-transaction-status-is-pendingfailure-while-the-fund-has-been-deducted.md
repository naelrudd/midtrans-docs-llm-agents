---
updatedAt: 2025-11-11T00:16:27.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Why transaction status is Pending/Failure, while the fund has been deducted?

In some rare cases, when the customer fund is deducted but the acquiring bank/payment provider is having issues such as network timeout or Acquiring Bank failure to respond to a transaction charge request, the transaction is considered a failure. By default, the customer funds will not be deducted. If the fund is deducted, it will be automatically refunded.

Most banks or payment providers notify the customer (through SMS, email, push notifications, and so on) only when a fund deduction happens. Sometimes the customer is not notified when a transaction is refunded or reversed. This may confuse the customer. Unfortunately, this is directly under the bank's or the payment provider's control, which neither you nor Midtrans is able to control.

The customer should check their transaction history or contact their bank/payment provider to ensure that no fund has been deducted. You can also check the transaction details within Midtrans Dashboard. Such transactions will have a reversal event.

If further fund status check is required, you can send email to **<support@midtrans.com>** with at least the following information: Order ID, Transaction date, Transaction amount.