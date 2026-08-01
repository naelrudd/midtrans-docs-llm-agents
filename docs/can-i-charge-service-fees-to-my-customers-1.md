---
updatedAt: 2025-11-11T00:12:53.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Can I charge service fees to my customers?

Standard Midtrans procedure, transaction fees will be charged to merchants who carry out the collaboration process to use Midtrans services.

If you want the transaction fee to be charged to your customer, then please add the transaction fee to the final value (gross\_amount parameter) that you want to send to Midtrans API.\
An example of the API can be seen below:

```
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

Make sure the total amount in **item\_details** is the same as the **gross\_amount** to avoid errors.

For the details, you can see in our technical documentation [here ↗](https://docs.midtrans.com/en/other/faq/technical?id=how-should-i-include-internal-fee-tax-discount-in-item_details-api-params).