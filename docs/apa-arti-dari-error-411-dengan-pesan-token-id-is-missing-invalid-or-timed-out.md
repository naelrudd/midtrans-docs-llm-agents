---
updatedAt: 2025-11-11T00:21:59.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Apa arti dari error 411 dengan pesan “Token id is missing, invalid, or timed out”?

*Error* ini berkaitan dengan token untuk transaksi kartu kredit. Berikut hal yang bisa Anda lakukan jika Anda menerima pesan tersebut:

* Pastikan bahwa perbedaan waktu antara get/*generate token* dan charge token tidak terlalu panjang (sebaiknya kurang dari 10 menit);\
  Pastikan *servey key* dan *client key* yang digunakan berasal dari **MID dan*environment* yang sama** untuk kedua proses diatas.
* Pastikan bahwa tidak ada **'token\_id'** yang digunakan lagi untuk transaksi lainnya; kecuali untuk transaksi *One Click* atau *Two Clicks*.