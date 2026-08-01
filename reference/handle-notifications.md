---
updatedAt: 2025-11-10T22:58:38.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Handle Notifications

> 📘 Getting notifications of payment status
>
> See [here](/docs/https-notification-webhooks) for an in-depth guide of HTTP notification, or [here](/docs/handle-after-payment) for other types of notifications channel available for use.
>
> Ensure that email notification in General Settings is set to ensure various operations work as expected (e.g. save card / one click payments).

<br />

In order to increase security aspect, there are several ways to ensure notification received from Midtrans.

***

<br />

## Challenge Response

<br />

An additional mechanism we provide to verify the content and the origin of the notification is to challenge. This can be achieved by calling the [GET Status API](/reference/get-transaction-status). The response is the same as the notification status.

<br />

***

<br />

## Signature Key

<br />

![](https://files.readme.io/76e26b8-signaturekey1.png "signaturekey1.png")

<br />

We add signature key information in our notification. The purpose of this signature key is to validate whether the notification is originated from Midtrans or not. Should the notification is not genuine, merchants can disregard the notification. Please find on the side, the logic of the signature key and the sample code to generate signature key.

<br />

```javascript Signature key logic
SHA512(order_id + status_code + gross_amount + serverkey)
```

```php Sample code generate signature key
<?php
$orderId = "1111";
$statusCode = "200";
$grossAmount = "100000.00";
$serverKey = "askvnoibnosifnboseofinbofinfgbiufglnbfg";
$input = $orderId.$statusCode.$grossAmount.$serverKey;
$signature = openssl_digest($input, 'sha512');
echo "INPUT: " , $input."<br/>";
echo "SIGNATURE: " , $signature;
?>
```

<br />

***

<br />

## Best Practice to Handle Notification

<br />

* Always use an HTTPS endpoint. It is secure and there cannot be MITM attacks because we validate the certificates match the hosts. Do not use self signed certificates.
* Always implement notification in an idempotent way. In extremely rare cases, we may send multiple notifications for the same transaction event twice. It should not cause double entries in the merchant end; the simple way of achieving this is to use Order ID as the key to track the entries.
* Always check the signature hash of the notification. This will confirm that the notification was actually sent by Midtrans, because we encode the shared secret (server key). Nobody else can build this signature hash.
* Always check all the following three fields for confirming success transaction :
  * Status code: Should be 200 for successful transactions
  * Fraud status: ACCEPT
  * Transaction status : Settlement/Capture
* We strive to send the notification immediately after the transaction has occurred. However, in extremely rare cases, it may be delayed due to issues (e.g. high load, incidents, network latency, etc.). If you think you have not receive notification in time, you should use the [GET Status API](/docs/get-status-api-requests) to check for current status of the transaction. In general, below is the SLA that you can expect:
  * Settlement notification : up to 20s
  * Expiry notification : up to 90s
* We set the HTTP timeout to 30 seconds. In general, it is recommended to keep your HTTP notifications' response time to be under 5 seconds.
* In extremely rare cases we may send the HTTP notifications out of order, ie. a "Settlement" status for a notification before the notification for "Pending" status. It's important that such later notifications are ignored (see [Transaction Status Cycle](/docs/transaction-status-cycle) for more details). Use our Get Status API to confirm the actual status.
* We send the notification body as JSON, please parse the JSON with a JSON parser. Always expect new fields will be added to the notification body, so parse it in a non strict format, so if the parser sees new fields, it should not throw exception. It should gracefully ignore the new fields. This allows us to extend our notification system for newer use cases without breaking old clients.
* Always use the right [HTTP Status code](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) for responding to the notification. We handle retry for error cases differently based on the status code :
  * for `2xx` : No retries, it is considered success
  * for `500` : We will retry 1 times in the 1 minute interval
  * for `503` : Retry 4 times
  * for `400/404` : retry 2 times in 1 minute interval
  * for all other failures : Retry 5 times at 1 minute interval
* Redirection :
  * for `307/308`: The request will be repeated with the new URL using POST method and the same notification body. A maximum of 5 redirections are allowed.
  * for `301/301/303`: The job will be marked as failed without further retries, and merchant will be notified via email. We suggest either to use `307/308` or update the notification endpoint settings in merchant portal.

<br />

***

<br />

## Override Notification URL

<br />

Merchant can opt to change or add custom notification URLs on every transaction. It can be achieved by adding additional HTTP headers into charge request.

There are two headers we provide:

<br />

* `X-Append-Notification`: to add new notification URLs alongside the settings on dashboard
* `X-Override-Notification`: to use new notification URLs disregarding the settings on dashboard

<br />

Both header can only receive up to **maximum of 2 URLs**.

<br />

### Sample Case

<br />

```curl Append Notification Sample
curl -X POST \
  https://app.midtrans.com/snap/v1/transactions \
  -H 'Accept: application/json' \
  -H 'Authorization: Basic NjJiMTVhN2QtZTVmOC00YjNjLTllYWItY2E4MjdjYTM3ZjU1Og==' \
  -H 'Content-Type: application/json' \
  -H 'X-Append-Notification: https://example.com/test1,https://example.com/test2' \
  -H 'cache-control: no-cache' \
  -d '{
    "transaction_details": {
        "order_id": "1553229166",
        "gross_amount": 10000
    }
}'
```

```curl Override Notification Sample
curl -X POST \
  https://app.midtrans.com/snap/v1/transactions \
  -H 'Accept: application/json' \
  -H 'Authorization: Basic NjJiMTVhN2QtZTVmOC00YjNjLTllYWItY2E4MjdjYTM3ZjU1Og==' \
  -H 'Content-Type: application/json' \
  -H 'X-Override-Notification: https://example.com/test1,https://example.com/test2' \
  -H 'cache-control: no-cache' \
  -d '{
    "transaction_details": {
        "order_id": "1553229166",
        "gross_amount": 10000
    }
}
```

Assuming merchant has set <https://example.com> as their notification url on the dashboard.

If merchant set `X-Append-Notification` with values `https://example.com/test1,https://example.com/test2`, every HTTP notification for that specific transaction will be sent to:

* <https://example.com>,
* <https://example.com/test1>, and
* <https://example.com/test2>

Else if merchant set `X-Override-Notification` with values `https://example.com/test1,https://example.com/test2`, every HTTP notification for that specific transaction will be sent to:

* <https://example.com/test1> and
* <https://example.com/test2>

<br />

> 🚧
>
> When both `X-Append-Notification` and `X-Override-Notification` are used together, then only override will be used.