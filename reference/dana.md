---
updatedAt: 2025-11-11T00:26:46.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# DANA

# DANA Payment Integration

DANA is an e-Wallet payment method that serves as an alternative payment option for DANA users. This API reference describes the implementation of regular payment flow with DANA.

By default, DANA's transaction expiry is set to 15 minutes (minimum 15 minutes, maximum 1 days).

<br />

> 📘 Payment Flow
>
> DANA offers two primary payment flows based on whether the user has the DANA app installed on their device or not. The appropriate flow will be automatically determined and presented to the user.

<br />

## When users make a purchase using DANA

<br />

1. Users initiate a payment using DANA on Snap page.

2. Snap redirects the user to the DANA app or DANA Webview.

3. DANA determines if the user has the DANA app installed or not
   * If the DANA app is installed, users are redirected directly to the DANA app.
   * If the DANA app is not installed, users are redirected to the DANA Webview.

4. Users complete the payment process in either the DANA app or Webview.

5. The transaction is completed, and the users' DANA balance is deducted.

6. Users are redirected back to the merchant's platform to see the transaction result.

7. Midtrans sends an HTTP notification (webhook) to the merchant's server with the final transaction status.

<br />

## Sample JSON Request Body

```json
{
  "transaction_details": {
    "order_id": "ORDER-101",
    "gross_amount": 10000
  },
  "item_details": [{
    "id": "ITEM1",
    "price": 10000,
    "quantity": 1,
    "name": "Midtrans Bear",
    "brand": "Midtrans",
    "category": "Toys",
    "merchant_name": "Midtrans"
  }],
  "customer_details": {
    "first_name": "TEST",
    "last_name": "MIDTRANSER",
    "email": "test@midtrans.com",
    "phone": "+628123456"
  },
  "enabled_payments": ["dana"],
  "dana": {
    "callback_url": "https://yourwebsite.com/dana-callback"
  }
}
```

| Parameter                                                                                                       | Description                                                        |
| --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| transaction\_details <br />[Transaction Details](/reference/json-objects#transaction-details) Object (required) | Unique transaction ID                                              |
| item\_details <br />[Item Details](/reference/json-objects#item-details) Object (optional)                      | Item details to be paid by customer                                |
| customer\_details <br />[Customer Details](/reference/json-objects#customer-details) Object (optional)          | Details of the customer                                            |
| enabled\_payments <br />Array (optional)                                                                        | Set what payment method to show in the payment list. Value: `dana` |
| dana <br />[Dana](/reference/json-objects#dana-object) (optional)                                               | DANA payment options                                               |

<br />

## Implementing DANA Callback

<br />

To handle the return flow from DANA to your platform, you need to implement a callback mechanism.

<br />

> 📘 Prerequisites
>
> Prepare a callback URL that can accept two query parameters.

Steps to integrate with DANA callback:

1. Set the `callback_url` parameter in the API request with the URL that will handle the redirection back to the merchant's platform.
2. If you need additional information when redirection to your platform, you can pass into callback\_url when creating Snap token, `https://yourwebsite.com/dana-callback?order_id=example`
3. If `callback_url` is not present in the API request, Snap will read the URL from the URL provided in Dashboard > Snap Preference > Finish URL. Only Finish URL `callback_url` will be used.

For a full list of request body parameters, please refer to the [Request Body (JSON Parameter)](/reference/request-body-json-parameter) section.

<br />

## API Operations for DANA

DANA supports only three API operations: **Get Status**, **Refund**, and **Cancel**. These operations use the **transaction\_id** as the identifier to process the payment. The **transaction\_id** can be obtained from the HTTP notification (Webhook).

<br />

### Get Status API

<br />

Use this API to check the current status of a transaction.

```curl cURL
curl --location 'https://api.sandbox.midtrans.com/v2/{transaction_id}/status' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--header 'transaction-source: SNAP_API' \
--header 'Authorization: Key'
```
```Text Response
{
    "status_code": "200",
    "transaction_id": "A120240830074017NP16XMU4JTID",
    "gross_amount": "20000.00",
    "currency": "IDR",
    "order_id": "sample-store-1725003597",
    "payment_type": "dana",
    "signature_key": "1b1f71e1b1b525e6c58c09f845c8b6b6d911ddfce34820bc52a9e6e5cf654a5f40639d6e33e510a2e9095c234b122becbe1ad919da2dedea3a4343f7905656d2",
    "transaction_status": "settlement",
    "fraud_status": "accept",
    "status_message": "Success, transaction is found",
    "merchant_id": "M007743",
    "transaction_time": "2024-08-30 14:40:17",
    "settlement_time": "2024-08-30 14:40:21",
    "expiry_time": "2024-08-30 14:55:17"
}
```

<br />

### Refund API

<br />

Use this API to process a refund for a transaction.

```curl cURL
curl --location 'https://api.sandbox.midtrans.com/v2/{transaction_id}/refund' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--header 'transaction-source: SNAP_API' \
--header 'Authorization: Key' \
--data '{
  "refund_key": "reference1",
  "amount": 20000,
  "reason": "for some reason"
}'
```
```json Response
{
    "status_code": "200",
    "status_message": "Success, refund request is approved",
    "order_id": "A120240830074017NP16XMU4JTID",
    "merchant_id": "M007743",
    "gross_amount": "20000.00",
    "currency": "IDR",
    "payment_type": "dana",
    "transaction_time": "2024-08-30 14:40:17",
    "transaction_status": "refund",
    "fraud_status": "accept",
    "refund_amount": "20000.00",
    "settlement_time": "2024-08-30 14:40:21",
    "refund_key": "reference1"
}
```

<br />

### Cancel API

<br />

Use this API to cancel a transaction.

```curl cURL
curl --location --request POST 'https://api.sandbox.midtrans.com/v2/{transaction_id}/cancel' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--header 'transaction-source: SNAP_API' \
--header 'Authorization: Key'
```
```json Response
{
    "status_code": "200",
    "status_message": "Success, transaction is canceled",
    "merchant_id": "G379181825",
    "gross_amount": "20000.00",
    "currency": "IDR",
    "payment_type": "dana",
    "transaction_status": "cancel",
    "fraud_status": "accept",
    "transaction_time": "2024-08-30 14:55:45"
}
```

<br />

> 🚧 API Usage Notes
>
> * The **transaction\_id** is the key identifier for all API operations with DANA. Ensure you retrieve and store this ID from the HTTP notification.
> * Replace \{**transaction\_id**} in the API endpoints with the actual transaction ID received from the HTTP notification.
> * Always check the `status_code` and `status_message` in the response to confirm the success of your API call.