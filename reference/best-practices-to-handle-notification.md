---
updatedAt: 2025-11-10T22:59:26.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Best Practices to Handle Notification

The guidelines to handle the notifications are given below.

<br />

* **Use HTTPS Endpoint**\
  It is secure and there cannot be MITM attacks because Midtrans verifies that the name on the server certificate matches with the host name. In addition to this, do not use self-signed certificates.

<br />

* **Use Notification Callback URL**\
  Use standard port (80/443) for Notification Callback URL.

<br />

* **Implement Notification in an Idempotent Way**\
  In extremely rare cases, Midtrans may send multiple notifications for the same transaction event. It should not cause double entries at the merchant's end. To prevent this, `order_id` or `account_id` can be used as the key to track the entries.

<br />

* **Use Signature Key**\
  Check the signature key of the notification. It confirms that the notification is actually sent by Midtrans. We encode the shared secret (server) key. Nobody else can build this signature hash.

<br />

* **Check the Status**\
  Check some fields given below, to ensure that the process is successful.
  * Transaction notification can check this 3 fields:
    * `status_code`: Should be 200 for successful transactions.
    * `fraud_status`: ACCEPT.
    * `transaction_status`: settlement/capture.
  * Pay Account notification can check this 2 fields:
    * `status_code`: Should be 200 for `ENABLED` or 204 for `DISABLED`
    * `account_status`: ENABLED / DISABLED.

<br />

* **Check Current Status**\
  We strive to send the notification immediately after the transaction has occurred. However, in extremely rare cases, it may be delayed due to issues (e.g. high load, incidents, network latency, etc.). If you think you have not receive notification in time, you should use the [GET Status API](/docs/get-status-api-requests) to check for current status of the transaction. In general, below is the SLA that you can expect:
  * Settlement notification : up to 20s
  * Expiry notification : up to 90s\ <br />
* **Use Status API**\
  Use Status API to get latest status.
  * Transaction notification can call [Status API](https://docs.midtrans.com/reference/get-transaction-status)
  * Pay Account notification can call [Account Status API](https://docs.midtrans.com/reference/get-pay-account) to get the latest account status

<br />

* **Reduce the Response Time**\
  We set the HTTP timeout to fifteen seconds. Please strive to keep the response time of the the HTTP notifications under five seconds.

<br />

* **Ignore delayed status notifications**\
  In extremely rare cases Midtrans may send the HTTP notifications out of order. For example, it may send `transaction_status:"settlement"` before sending a `transaction status:"pending"`. It is important that such later notifications are ignored. But again, use Midtrans status API to confirm the actual status.

<br />

* **Use JSON Parser**\
  We send the notification body as JSON. Therefore, please parse the JSON with a JSON parser. New fields get added to the notification body. Parse the JSON in a non-strict format, so that when the parser sees new fields, it should not throw exception. It should gracefully ignore the new fields. This allows Midtrans to extend its notification system for newer use cases without breaking old clients.

<br />

* **Use the right[HTTP Status code](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**\
  Always use the right HTTP Status code for responding to the notification. Midtrans handles retry for error cases differently based on the status code.
  * for `2xx`: No retries, it is considered success.
  * for `500`: Retry only once.
  * for `503`: Retry four times.
  * for `400/404`: Retry two times.
  * for `301/302/303`: No retries. We suggest to update the Notification endpoint in *Settings* instead of replying to these status code.
  * for `307/308`: Follow the new URL with POST method and same notification body. Max redirect is five times.
  * for all other failures: Retry five times.

<br />

* **Retry at the most five times**\
  Midtrans enables retry at most five times with following policy.
  * Different retry intervals from 1st time to 5th time (2m, 10m, 30m, 1.5hour, 3.5hour).
  * Put a time shift for each retry based on the above interval. For example, for the first time, retry might be two minutes after the job failed. The second retry might be ten minutes after the first retry is failed and so on.