---
updatedAt: 2026-04-01T04:00:51.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# OVO

# OVO Payment Integration

OVO is an e-Wallet payment method that serves as an alternative payment option for OVO users. This API reference describes the implementation of regular payment flow with OVO.

OVO's transaction expiry is set to 65 seconds, and customers have 55 seconds to complete purchase.

## When users make a purchase using OVO

1. Users initiate a payment using OVO on Snap page.

2. OVO user got notification from their OVO app

3. Users complete the payment process in the OVO app.

4. The transaction is completed, and the users' OVO balance is deducted.

5. After payment, user could go back to the snap page, and it will automatically check transaction status.

6. Midtrans sends an HTTP notification (webhook) to the merchant's server with the final transaction status.

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
  "enabled_payments": ["ovo"]
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
        transaction_details <br />[Transaction Details](/reference/json-objects#transaction-details) Object (required)
      </td>

      <td>
        Unique transaction ID.
      </td>
    </tr>

    <tr>
      <td>
        item_details <br />[Item Details](/reference/json-objects#item-details) Object (optional)
      </td>

      <td>
        Item details to be paid by customer
      </td>
    </tr>

    <tr>
      <td>
        customer_details <br />[Customer Details](/reference/json-objects#customer-details) Object (optional)
      </td>

      <td>
        Details of the customer.  
        `customer_details.phone` will be used to pre-fill phone number in OVO payment page
      </td>
    </tr>

    <tr>
      <td>
        enabled_payments <br />Array (optional)
      </td>

      <td>
        Set what payment method to show in the payment list. Value: `ovo`
      </td>
    </tr>
  </tbody>
</Table>

<br />