---
updatedAt: 2025-11-11T00:25:30.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# CIMB Virtual Account

CIMB Virtual Account is a bank transfer method facilitated by Bank CIMB Niaga. Despite the name, customers can pay using any Indonesian Bank account to complete payment. Payment can be made through ATM, mobile banking, internet banking, and Indonesian bank channels that supports paying virtual accounts.

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
  "enabled_payments": ["cimb_va"],
  "cimb_va": {
    "va_number": "12345678"
  }
}
```

| Parameter                                                                                                                    | Description                                                              |
| ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| transaction\_details     <br /> [Transaction Details](/reference/json-objects#transaction-details) Object (required)         | Unique transaction ID                                                    |
| item\_details                <br /> [Item Details](/reference/json-objects#item-details) Object (optional)                   | Shopping item details will be paid by customer                           |
| customer\_details   <br /> [Customer Details](/reference/json-objects#customer-details) Object (optional)                    | Details of the customer                                                  |
| enabled\_payments <br /> Array (optional)                                                                                    | Set what payment method to show in Snap's payment list. Value: `cimb_va` |
| `cimb_va`                      <br /> [CIMB Virtual Account](/reference/json-objects#cimb-virtual-account-object) (optional) | CIMB Virtual Account payment options                                     |

<br />

For a full list of request body parameters please refer to the [Request Body (JSON Parameter)](https://docs.midtrans.com/reference/request-body-json-parameter) section

<br />

**Note:** Please also refer to the [Custom VA Number](https://docs.midtrans.com/reference/custom-virtual-account-number) section if you're looking to define your own VA number for your customers.