---
updatedAt: 2025-11-11T00:28:07.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Item Details Object

```json Item Details
"item_details": [{
    "id": "a1",
    "price": 50000,
    "quantity": 2,
    "name": "Apel",
    "brand": "Fuji Apple",
    "category": "Fruit",
    "merchant_name": "Fruit-store",
    "tenor": "12",
    "code_plan": "000",
    "mid": "123456",
    "url": "https://tokobuah.com/apple-fuji"
  }]
```

| JSON Attribute | Description                                                                                                                          | Type       | Required    |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------ | ---------- | ----------- |
| id             | Item ID.                                                                                                                             | String     | Optional    |
| price          | Price of the item in IDR. <br /> **Note**: Do not add decimal.                                                                       | Integer    | Required    |
| quantity       | Quantity of the item purchased by the customer.                                                                                      | Integer    | Required    |
| name           | Name of the item.                                                                                                                    | String     | Required    |
| brand          | Brand name of the item.                                                                                                              | String     | Optional    |
| category       | Category of the item.                                                                                                                | String     | Optional    |
| merchant\_name | Name of the merchant selling the item.                                                                                               | String     | Optional    |
| tenor          | Installment term, use two digits numeric. For example, 03, 06, 09, 12, 24. <br /> **Note**: This is a *BCA KlikPay* exclusive field. | Integer(2) | Conditional |
| code\_plan     | Installment code, use **000** for default. <br /> **Note**: This is a *BCA KlikPay* exclusive field.                                 | Integer(3) | Conditional |
| mid            | Installment Merchant ID. <br /> **Note**: This is a *BCA KlikPay* exclusive field.                                                   | Integer(9) | Conditional |
| url            | HTTP URL of the item in the merchant site                                                                                            | String     | Optional    |

<br />

> 📘 Note
>
> * Please avoid using vertical line (`|`) for Alfamart payment type
>   * **item\_details** is required for Akulaku payment type.
>   * Subtotal (item price multiplied by quantity) of all the item details needs to be exactly same as the gross\_amount inside the transaction\_details object.
>   * Akulaku payment type doesn't allow duplicate item ID (item\_details.id) in one request.