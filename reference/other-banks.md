---
updatedAt: 2025-11-10T22:57:54.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Other Banks

Other Banks is a bank transfer payment method to support payment from any banks in Indonesia. How this works is Snap will be masking the designated open loop (support payment from any bank) virtual account and present it in SNAP as Other Bank. This feature is handy for users who are not familiar on how Virtual Account works, hence might not understand which Virtual Account can support payment from their bank of choice (e.g. Permata Virtual Account, despite the name, can actually accept payments from all banks in Indonesia).

To use this feature, make sure that you have at least BNI or Permata VA active in your merchant account.

To configure which bank you will set as Other Banks, go to you [Snap Preference Setting](https://dashboard.midtrans.com/settings/snap_preference) in Midtrans's dashboard, go to `Bank List`, and set your desired Virtual Account as Other Banks in the `Other Bank/ATM Bank Processor` menu.

Steps to integrate :

1. Send the charge API request to Midtrans.
2. Redirect your customer back to your page by configuring Finish URL in Midtrans's Dashboard > [Snap Preferences](https://dashboard.midtrans.com/settings/snap_preference) or via [API Request](/docs/snap-advanced-feature#custom-finish-url) .
3. [Handle notifications](/reference/notifications-handling).

By default, default expiry time for bank transfer is 24 hours unless specified by merchant (min 20s, max 180 days).

<br />

<Image title="Other Banks.PNG" alt={939} align="center" className="border" width="80%" border={true} src="https://files.readme.io/42beeaa-Other_Banks.PNG" />

<br />

Once set, your customer will see your Snap payment list as shown below :

<br />

<Image title="Other Banks 2.PNG" alt={677} align="center" className="border" width="80%" border={true} src="https://files.readme.io/a89ab2c-Other_Banks_2.PNG" />

<br />

Any payment made by users who choose 'Other Bank' will then be processed as regular transaction of the designated open loop virtual account.

You can also show Other Bank as a single payment method via API request (provided that you have performed the configuration in Snap Settings as shown above) - see below.

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
  "enabled_payments": ["other_va"]
}'
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
        transaction\_details
        [Transaction Details](/reference/json-objects#transaction-details) Object (required)
      </td>

      <td>
        Unique transaction ID
      </td>
    </tr>

    <tr>
      <td>
        item\_details\
        [Item Details](/reference/json-objects#item-details) Object (optional)
      </td>

      <td>
        Shopping item details will be paid by customer
      </td>
    </tr>

    <tr>
      <td>
        customer\_details\
        [Customer Details](/reference/json-objects#json-parameter-request-body) Object (optional)
      </td>

      <td>
        Details of the customer
      </td>
    </tr>

    <tr>
      <td>
        enabled\_payments\
        Array (optional)
      </td>

      <td>
        Set what payment method to show in Snap's payment list. Value: `other_va`
      </td>
    </tr>
  </tbody>
</Table>

<br />

For a full list of request body parameters please refer to the [Request Body (JSON Parameter)](https://docs.midtrans.com/reference/request-body-json-parameter) section.