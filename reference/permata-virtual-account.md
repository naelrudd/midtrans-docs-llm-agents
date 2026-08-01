---
updatedAt: 2025-11-11T00:25:22.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Permata Virtual Account

Permata Virtual Account is a bank transfer payment method facilitated by Bank Permata. Despite the name, customers can pay using any Indonesian Bank account to complete payment. Payment can be made trough ATM Bersama, Prima, or Alto ATM networks.

Steps to integrate :

1. Send the charge API request to Midtrans.
2. Redirect your customer back to your page by configuring Finish URL in Midtrans's Dashboard > [Snap Preferences](https://dashboard.midtrans.com/settings/snap_preference) or via \[API Request] (/docs/snap-advanced-feature#custom-finish-url).
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
  "enabled_payments": ["permata_va"],
  "permata_va": {
    "va_number": "1234567890",
    "recipient_name": "SUDARSONO"
  }
}
```

| Parameter                                                                                                         | Description                                                                 |
| ----------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| transaction *details<br />*[Transaction Details](/reference/json-objects#transaction-details) Object (required)\_ | Unique transaction ID                                                       |
| item *details<br />*[Item Details](/reference/json-objects#item-details) Object (optional)\_                      | Shopping item details will be paid by customer                              |
| customer *details<br />*[Customer Details](/reference/json-objects#custom-details) Object (optional)\_            | Details of the customer                                                     |
| enabled*payments<br />\_Array (optional)*                                                                         | Set what payment method to show in Snap's payment list. Value: `permata_va` |
| permata *va<br />*[Permata Virtual Account](/reference/json-objects#permata-virtual-account-object) (optional)\_  | Permata Virtual Account payment options                                     |

<br />

For a full list of request body parameters please refer to the [Request Body (JSON Parameter)](https://docs.midtrans.com/reference/request-body-json-parameter) section

<br />

**Note:** Please also refer to the [Custom VA Number](/reference/custom-virtual-account-number) section if you're looking to define your own VA number for your customers.