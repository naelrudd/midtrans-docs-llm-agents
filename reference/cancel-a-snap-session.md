---
updatedAt: 2025-11-10T22:58:47.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Cancel a Snap Session

Cancel a Snap page session via API

In principle, a Snap page will have an expiry time (default 24 hour), which can also be customized following this guide [Expire a Snap Session](https://docs.midtrans.com/reference/expire-a-snap-session).

In a scenario where you want to cancel a Snap page before the expiry time, you can use this endpoint.

<br />

## Sample Request

```shell cURL
curl --request POST \
  --url https://app.midtrans.com/snap/v1/transactions/{token}/cancel \
  --header 'Authorization: {merchant_server_key}' \
  --header 'Content-Type: application/json' \
  --header 'Accept: application/json'
```

<br />

## Sample Response

```json Success Response
{
  "canceled_at": "2025-06-03T13:09:39.776Z"
}
```
```json Token has been canceled response
{
  "error_messages": [
    "token already canceled"
  ]
}
```
```json Transaction is in progress response
{
  "error_messages": [
    "Transaction is on progress"
  ]
}
```
```json Token not found response
{
  "error_messages": [
    "token not found"
  ]
}
```

<br />

If the user remains on the Snap page after the session has been canceled and attempts to continue the transaction, they will see an error indicating that they are not able to proceed with the transaction.

<br />

<Image align="center" width="50% " src="https://files.readme.io/9282ac7344cd711dcbd719c0218cdcc2a0e435b3be725997a665ec0c15ab9e83-image.png" />