---
updatedAt: 2025-11-11T00:24:30.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Response

## Response Success

<br />

```json
{
  "token": "d379aa71-99eb-4dd1-b9bb-eefe813746e9",
  "redirect_url": "https://app.sandbox.midtrans.com/snap/v3/redirection/071e0c3d-dade-4148-a1b5-296ee8735b79"
}
```

HTTP status code: `201`

| Field                             | Description                                          |
| --------------------------------- | ---------------------------------------------------- |
| token <br /> *String(36)*         | Snap token for [opening the Snap popup](https://docs.midtrans.com/reference/snap-js) |
| redirect\_url <br /> *String(75)* | URL for [redirection](https://docs.midtrans.com/reference/window-redirection)        |

<br />

***

<br />

## Response Failed

<br />

### Authentication Failed

<br />

```json
{
  "error_messages": [
    "Access denied due to unauthorized transaction, please check client or server key",
    "Visit https://snap-docs.midtrans.com/#request-headers for more details"
  ]
}
```

HTTP status code: `401`

| Field                          | Description    |
| ------------------------------ | -------------- |
| error\_messages <br /> *Array* | Error messages |

<br />

### Validation Error

<br />

```json
{
  "error_messages": [
    "transaction_details.gross_amount is not equal to the sum of item_details"
  ]
}
```

HTTP status code: `400`

| Field                         | Description    |
| ----------------------------- | -------------- |
| error*messages<br /> \_Array* | Error messages |

<br />

### Order ID Already Paid and Utilized

<br />

```json
{
  "error_messages": [
    "transaction_details.order_id has been paid and utilized, please use another order ID"
  ]
}
```

HTTP status code: `400`

| Field                         | Description    |
| ----------------------------- | -------------- |
| error*messages<br /> \_Array* | Error messages |

<br />

### Internal System Error

<br />

```json
{
  "error_messages": [
    "Sorry, we encountered internal server error. We will fix this soon."
  ]
}
```

HTTP status code: `500`

| Field                         | Description    |
| ----------------------------- | -------------- |
| error*messages<br /> \_Array* | Error messages |