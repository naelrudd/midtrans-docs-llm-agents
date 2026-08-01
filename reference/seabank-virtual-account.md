---
updatedAt: 2026-01-20T08:32:51.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# SeaBank Virtual Account

SeaBank Virtual Account is a bank transfer method facilitated by Bank SeaBank. Payment can be made through ATM, mobile banking, internet banking, and Indonesian bank channels that supports paying virtual accounts.

Steps to integrate :

1. Send the charge API request to Midtrans.
2. Redirect your customer back to your page by configuring Finish URL in Midtrans's Dashboard > [Snap Preferences](https://dashboard.midtrans.com/settings/snap_preference) or via [API Request](/docs/snap-advanced-feature#custom-finish-url).
3. [Handle notifications](/reference/notifications-handling).

Open amount and close amount VA has the exact same API contract - by default close amount VA type is activated for you. If you want to activate open amount VA, contact Midtrans support or your sales PIC for further assistance.

By default, default expiry time for bank transfer is 24 hours unless specified by merchant (min 20s, max 180 days).

<br />

***

<br />

## Sample JSON Request Body

<br />

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
  "enabled_payments": ["seabank_va"],
  "seabank_va": {
    "va_number": "12345678"
  }
}
```

<Table>
  <thead>
    <tr>
      <th>
        Parameter
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        transaction_details
        [Transaction Details](/reference/json-objects#transaction-details) Object (required)
      </td>

      <td>
        Unique transaction ID
      </td>
    </tr>

    <tr>
      <td>
        item_details  
        [Item Details](/reference/json-objects#item-details) Object (optional)
      </td>

      <td>
        Shopping item details will be paid by customer
      </td>
    </tr>

    <tr>
      <td>
        customer_details  
        [Customer Details](/reference/json-objects#customer-details) Object (optional)
      </td>

      <td>
        Details of the customer
      </td>
    </tr>

    <tr>
      <td>
        enabled_payments  
        Array (optional)
      </td>

      <td>
        Set what payment method to show in Snap's payment list. Value: `seabank_va`
      </td>
    </tr>

    <tr>
      <td>
        `seabank_va`  
        [SeaBank Virtual Account](/reference/json-objects#seabank-virtual-account-object) (optional)
      </td>

      <td>
        SeaBank Virtual Account payment options
      </td>
    </tr>
  </tbody>
</Table>

<br />

For a full list of request body parameters please refer to the [Request Body (JSON Parameter)](https://docs.midtrans.com/reference/request-body-json-parameter) section

<br />

**Note:** Please also refer to the [Custom VA Number](https://docs.midtrans.com/reference/custom-virtual-account-number) section if you're looking to define your own VA number for your customers.

***

## API Operations for SeaBank VA

SeaBank VA supports two API operations: **Get Status**, and **Cancel**. These operations use the **transaction\_id** as the identifier to process the payment. The **transaction\_id** can be obtained from the HTTP notification (Webhook).

### Get Status API

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

### Cancel API

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

> 🚧 API Usage Notes
>
> * The **transaction\_id** is the key identifier for all API operations with SeaBank VA. Ensure you retrieve and store this ID from the HTTP notification.
> * Replace \{**transaction\_id**} in the API endpoints with the actual transaction ID received from the HTTP notification.
> * Always check the `status_code` and `status_message` in the response to confirm the success of your API call.