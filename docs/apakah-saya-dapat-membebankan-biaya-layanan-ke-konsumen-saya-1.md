---
updatedAt: 2025-11-11T00:18:59.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Apakah saya dapat membebankan biaya layanan ke konsumen saya?

Standar prosedur Midtrans, biaya transaksi akan dibebankan kepada pihak merchant yang melakukan proses kerja sama untuk menggunakan layanan Midtrans.

Jika biaya transaksi ingin dibebankan kepada pelanggan Anda, maka silahkan biaya transaksi ditambahkan pada nilai akhir (parameter **gross\_amount**) yang ingin dikirimkan ke Midtrans API.\
Contoh API nya dapat dilihat dibawah ini:

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

Pastikan nilai total amount pada **item\_details** sama dengan nilai *amount***gross\_amount** untuk menghindari *error*.

Untuk detail lebih lanjut dapat Anda lihat pada dokumentasi teknis kami [di sini ↗](https://docs.midtrans.com/en/other/faq/technical?id=how-should-i-include-internal-fee-tax-discount-in-item_details-api-params).