---
updatedAt: 2026-09-28T12:00:08.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Cancel Checkout Page Session

In principle, a checkout page will have an expiry time (default 24 hour), which can also be customized following this guide [Expire a Snap Checkout Session](https://docs.midtrans.com/reference/expire-a-snap-session).

In a scenario where you want to cancel a checkout page before the expiry time, you can use this endpoint.

<br />

Endpoints: `/api/v1/checkout/transactions/{{token}}/cancel`

HTTP Method: `POST`

## Response Body

```json Success response
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
    "Transaction is in progress"
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

| JSON Attribute | Description                               | Type   |
| -------------- | ----------------------------------------- | ------ |
| canceled\_at   | Timestamp when the page has been canceled | String |

<br />

If the user remains on the checkout page after the session has been cancelled and attempts to continue the transaction, they will see an error indicating that they are not able to proceed with the transaction.

<br />

<Image align="center" width="50% " src="https://files.readme.io/da00d0e6c7fd899ef2e8fec3a29ef545b6c2b6a83ba9a011e2150434e0afc364-image.png" />