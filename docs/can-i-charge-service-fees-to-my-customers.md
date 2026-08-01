---
updatedAt: 2025-11-11T00:12:23.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Can I charge service fees to my customers?

Standard Midtrans procedure, transaction fees will be charged to merchants who carry out the collaboration process to use Midtrans services.\ <br />\
If you want the transaction fee to be charged to your customer, then please add the transaction fee to the final value (gross\_amount parameter) that you want to send to Midtrans API.\ <br />\
An example of the API can be seen below:

```Text sample JSON body request
{
    "transaction_details": {
       "order_id": "CustOrder-102",
       "gross_amount": 8000
},
"item_details": [
    {
      "id": "a01",
      "price": 7000,
      "quantity": 1,
      "name": "Apple"
    },
    {
     "id": "b02",
     "price": 1000,
     "quantity": 1,
     "name": "Biaya Transaksi"
     }
  ]
{
```

<br />

Make sure the total amount in **item\_details** is the same as the **gross\_amount** to avoid errors.

For the details, you can see our technical documentation [here ↗](https://docs.midtrans.com/docs/technical-faq?id=how-should-i-include-internal-fee-tax-discount-in-item_details-api-params).