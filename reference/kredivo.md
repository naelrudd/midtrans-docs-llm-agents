---
updatedAt: 2025-11-11T00:26:43.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Kredivo

Buy Now Pay Later payment method by Kredivo. Upon making purchase, customer will be redirected to the Kredivo website to complete payment.

Steps to integrate :

1. Send the charge API request to Midtrans.
2. Redirect your customer back to your page by configuring Finish URL in Midtrans's Dashboard > [Settings > Payments](https://dashboard.midtrans.com/settings/payment).
3. [Handle notifications](/reference/notifications-handling).

By default, Kredivo's transaction expiry is 24 hours (min 20s, max 180 days).

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
    "category": "Toys",
    "url": "http://toko/toko1?item=abc"
  }],
  "customer_details": {
    "first_name": "TEST",
    "last_name": "MIDTRANSER",
    "email": "test@midtrans.com",
    "phone": "+628123456",
    "shipping_address": {
      "first_name": "TEST",
      "last_name": "MIDTRANSER",
      "email": "test@midtrans.com",
      "phone": "0 8128-75 7-9338",
      "address": "Sudirman",
      "city": "Jakarta",
      "postal_code": "12190",
      "country_code": "IDN"
    }
  },
  "enabled_payments": ["kredivo"],
  "seller_details": [
    {
      "id": "sellerId-01",
      "name": "John Seller",
      "email": "seller@email.com",
      "url": "https://tokojohn.com",
      "address": {
        "first_name": "John",
        "last_name": "Seller",
        "phone": "081234567890",
        "address": "Kemanggisan",
        "city": "Jakarta",
        "postal_code": "12190",
        "country_code": "IDN"
      }
    }
  ]
}
```

| Parameter                                                                                                                | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| transaction *details<br />*[Transaction Details](/reference/json-objects#transaction-details-object) Object (required)\_ | Unique transaction ID                                                                                                                                                          |
| item *details<br />*[Item Details](/reference/json-objects#item-details-object) Object (required)\_                      | Shopping item details will be paid by customer. All field in the given sample are **(required)**                                                                               |
| customer *details<br />*[Customer Details](/reference/json-objects#customer-details-object) Object (required)\_          | Details of the customer. All field in the given sample are **(required)**                                                                                                      |
| enabled*payments<br />\_Array (optional)*                                                                                | Set what payment method to show in Snap's payment list. Value: `kredivo`                                                                                                       |
| seller*details<br />\_Array (optional)*                                                                                  | Details of the seller(s) where the customer purchased from. All field in the given sample are **(required)**. **Note:** This field is only mandatory for marketplace merchant. |

***

<br />

## Redirecting Back to Finish Page

<br />

The redirection back from Kredivo to your Finish Redirect URL will be using straight-forward HTTP GET. **Please make sure the Finish Redirect URL endpoint can receive HTTP GET request.**

Also, ensure that that the specified URL is a URL of a webpage that you own.