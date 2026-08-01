---
updatedAt: 2025-11-10T22:58:14.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Other QRIS

Other QRIS is a QRIS payment method presented as generic QRIS to customer. Other QRIS works exactly like Other Bank feature which will mask either GoPay or Shopeepay QRIS acquirer, however in Snap's payment user will be shown a generic QRIS with various issuer logo.

<br />

![](https://files.readme.io/2511a74-other_qris.PNG "other qris.PNG")

<p style={{ textAlign: "center" }}> <i>Other QRIS payment list in Snap </i> </p>

<br />

To use this feature, make sure that you have at least GoPay or Shopeepay QRIS active in your merchant account. If both is active, GoPay will be set as the default acquirer - this setting cannot be changed.

Any payment made by users who choose `Other QRIS` will then be processed as regular transaction of the designated QRIS acquirer (GoPay/Shopeepay) and shown in reporting as said acquirer's transaction.

By default, Other QRIS transaction expiry is 15 minutes (min 20s, max 7 days).

<br />

Steps to integrate :

1. Send the charge API request to Midtrans.
2. Redirect your customer back to your page by configuring Finish URL in Midtrans's Dashboard > [Snap Preferences](https://dashboard.midtrans.com/settings/snap_preference) or via [API Request](/docs/snap-advanced-feature#custom-finish-url).
3. [Handle notifications](/reference/notifications-handling).

You can also show Other QRIS as a single payment method via API request (provided that you have performed the configuration in Snap Settings as shown above) - see below.

<br />

> 📘 Displaying Other QRIS
>
> If you specify Other QRIS explicitly in `enabled_payments`, Other QRIS will always show up in Snap Checkout page regardless of customer's screen size. You can take advantage of this properties if you need to show QRIS persistently.

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
  "enabled_payments": ["other_qris"]
}
```

| Parameter                                                                                                           | Description                                                                 |
| ------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| transaction *details<br />*[Transaction Details](/reference/json-objects#transaction-details) Object (required)\_   | Unique transaction ID                                                       |
| item *details<br />*[Item Details](/reference/json-objects#item-details) Object (optional)\_                        | Shopping item details will be paid by customer                              |
| customer *details<br />*[Customer Details](/reference/json-objects#json-parameter-request-body) Object (optional)\_ | Details of the customer                                                     |
| enabled*payments<br />\_Array (optional)*                                                                           | Set what payment method to show in Snap's payment list. Value: `other_qris` |

<br />

For a full list of request body parameters please refer to the [Request Body (JSON Parameter)](https://docs.midtrans.com/reference/request-body-json-parameter) section.

<br />