---
updatedAt: 2026-07-07T05:06:05.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Enable GoPayLater for MiniApp

This section describes the additional metadata fields required to enable GoPay Later as a payment option in the Mini App.

> ### To enable GoPay Later as a payment option in your MiniApp, include the following fields under additionalInfo.metadata in the request body.

## Additional Request Body

| Field Params                                                        | Field Type | Mandatory | Field Description                                                                                               | Sample                                                                                                                  |
| ------------------------------------------------------------------- | ---------- | --------- | --------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| additionalInfo.metadata.order\_info.shipping\_info                  | object     | M         | Shipping information for the order. Required for physical goods only.                                           |                                                                                                                         |
| additionalInfo.metadata.order\_info.shipping\_info.address1         | string     | O         | Street address of the shipping destination.                                                                     | jl. beringin 1 no. 2 sumor bor (belakang pom bensin sumor bor) RT 001 RW 002 cengkareng barat (ada iklan rumah dijual.) |
| additionalInfo.metadata.order\_info.shipping\_info.city             | string     | O         | City of the shipping destination.                                                                               | Jakarta Barat                                                                                                           |
| additionalInfo.metadata.order\_info.shipping\_info.mobile           | string     | O         | Recipient's mobile phone number.                                                                                | 6282211867085                                                                                                           |
| additionalInfo.metadata.order\_info.shipping\_info.shipping\_name   | string     | O         | Recipient's name for the shipment.                                                                              | Alex                                                                                                                    |
| additionalInfo.metadata.order\_info.shipping\_info.state            | string     | O         | State or province of the shipping destination.                                                                  | DKI Jakarta                                                                                                             |
| additionalInfo.metadata.order\_info.sub\_orders                     | object     | M         | List of sub-order information for each purchased item.                                                          |                                                                                                                         |
| additionalInfo.metadata.order\_info.sub\_orders.merchant\_id        | string     | M         | The sub merchant id of a single item (ecommerce platform only)                                                  | 74285213                                                                                                                |
| additionalInfo.metadata.order\_info.sub\_orders.category\_id        | string     | M         | The category id of a single item (ecommerce platform only)                                                      | 1624                                                                                                                    |
| additionalInfo.metadata.order\_info.sub\_orders.category\_one\_name | string     | M         | The category one name of a single item (ecommerce platform only)                                                | fashion-anak-bayi                                                                                                       |
| additionalInfo.metadata.order\_info.sub\_orders.category\_two\_name | string     | O         | The category two name of a single item (ecommerce platform only)                                                | pakaian-anak-laki-laki                                                                                                  |
| additionalInfo.metadata.order\_info.sub\_orders.sku\_id             | string     | M         | The sku id of a single item                                                                                     | d4a4fe146c6bfbf7b7986f1a6293572a0e81154a854ae75e355be9d1ba562381                                                        |
| additionalInfo.metadata.order\_info.sub\_orders.sku\_name           | string     | M         | The sku name of a single item                                                                                   | celana pendek anak laki laki SS S M L XL bawahan cowok motif sport39                                                    |
| additionalInfo.metadata.order\_info.sub\_orders.quantity            | string     | M         | The quantity of a single item                                                                                   | 2                                                                                                                       |
| additionalInfo.metadata.order\_info.sub\_orders.amount              | string     | M         | The amount of a single item                                                                                     | 20000                                                                                                                   |
| additionalInfo.metadata.order\_info.sub\_orders.user\_id            | string     | M         | The identification of the user of a service provided, like game user id, biller id, etc.                        | 12345678                                                                                                                |
| additionalInfo.metadata.user\_info                                  | Object     | M         | Information about the user on the partner platform.                                                             |                                                                                                                         |
| additionalInfo.metadata.user\_info.id                               | string     | M         | Unique identifier of the user on the partner platform.                                                          | 9760c1e583b05a07be861f58ad41ea1ae4bdefc45c54527dbba0f3894d683abc                                                        |
| additionalInfo.metadata.user\_info.registration\_date               | string     | M         | The registration date of this user on the partner platform (or could be the days/days group since registration) | 2023/2/5                                                                                                                |

## Sample Response

```javascript
{
  "partnerReferenceNo": "merchant-order-id",
  "chargeToken": "accessToken",
  "payOptionDetails": [
    {
      "payMethod": "Gopay",
      "payOption": "Coins",
      "transAmount": {
        "value": "12345678.00",
        "currency": "IDR"
      },
      "additionalInfo": {
        "accountId": "midTransAccountId",
        "paymentOptionToken": "aGoPayWalletToken / aPayLaterToken / aGoPayCoinsToken",
        "challengeId": "aChallengeID",
        "paymentToken": "aPaymentToken",
        "callbackUrl": "www.tokopedia.com"
      }
    }
  ],
  "additionalInfo": {
    "metadata": {
      "order_info": {
        "shipping_info": [
          {
            "address1": "jl. beringin 1 no. 2 sumor bor ( belakang pom bensin sumor bor) RT 001 RW 002 cengkareng barat (ada iklan rumah dijual.)",
            "city": "Jakarta Barat",
            "mobile": "6282211867085",
            "shipping_name": "",
            "state": "DKI Jakarta"
          }
        ],
        "sub_orders": [
          {
            "merchant_id": "1234434",
            "category_id": "1624",
            "category_one_name": "fashion-anak-bayi",
            "category_two_name": "pakaian-anak-laki-laki",
            "sku_id": "d4a4fe146c6bfbf7b7986f1a6293572a0e81154a854ae75e355be9d1ba562381",
            "sku_name": "celana pendek anak laki laki SS S M L XL bawahan cowok motif sport39",
            "quantity": "2.0",
            "amount": "78269.0",
            "user_id": "123445"
          }
        ]
      },
      "user_info": {
        "id": "9760c1e583b05a07be861f58ad41ea1ae4bdefc45c54527dbba0f3894d683abc",
        "registration_date": "2023/2/5"
      }
    }
  }
}
```

<br />