---
updatedAt: 2025-11-11T00:21:22.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Bagaimana cara melakukan refund transaksi?

Transaksi yang dapat di *refund* melalui Midtrans adalah hanya metode pembayaran kartu kredit,  GoPay, QRIS, Shopeepay dan Akulaku. Untuk metode pembayaran lain, *refund* dana ke konsumen dapat dilakukan langsung dari *merchant* ke *customer*.

Syarat untuk sukses melakukan *refund* transaksi diantaranya:

1. Refund hanya berlaku untuk metode pembayaran kartu kredit, GoPay, QRIS, Shopeepay dan Akulaku.
2. Status transaksi telah *settlement*. Jika status transaksi masih *success / capture / pending*, pengembalian dana dapat dilakukan melalui pembatalan transaksi, detailnya dapat Anda lihat pada link [berikut ↗.](https://docs.midtrans.com/docs/bagaimana-cara-membatalkan-transaksi)
3. Terdapat dana yang siap dicairkan (*Payable Amount*) di akun Midtrans anda dengan nilai lebih besar dari nilai transaksi yang akan di [refund](https://midtrans.com/id/pricing) setelah dikenakan [biaya ↗](https://midtrans.com/id/pricing). Contoh, untuk transaksi kartu dengan nominal Rp. 100,000, pengembalian dana penuh dapat dilakukan jika Anda memiliki *payable amount* minimal Rp. 105,000.

Proses *refund* untuk transaksi dapat dilakukan dengan menggunakan tombol *refund* melalui *dashboard* Midtrans (MAP) ataupun melalui [API refund ↗](https://api-docs.midtrans.com/#direct-refund-transaction).

Untuk *refund* melalui *dashboard* Midtrans (MAP) dapat dilakukan dengan cara : 

1. *Login* ke *dashboard* Midtrans (MAP).

   ![](https://files.readme.io/35b2024-image.png)
2. Pilih menu *Transactions*.

   ![](https://files.readme.io/a383c48-image.png)
3. Pilih Transaksi yang ingin di *refund* atau bisa melakukan pencarian berdasarkan *Order ID* atau yang lainnya.

   ![](https://files.readme.io/bc7d935-image.png)
4. Pilih *button refund* yang ada pada detail transaksi yang sudah dipilih.

   ![](https://files.readme.io/0cd1f13-image.png)
5. *Input* nominal yang ingin di refund pada kolom ***Refund Amount***, sebagai informasi tambahan untuk *refund* dapat dilakukan secara sebagian dari nominal transaksi ataupun secara *full amount*.

   ![](https://files.readme.io/8601f33-image.png)
6. *Input* alasan *refund* pada kolom *Reason for Refund*. Contoh : Pembatalan Transaksi, Dobel Pemesanan, Stok Habis, dll.

   ![](https://files.readme.io/ee6250d-image.png)
7. Pilih *button* ***Refund***.

Jika tombol *refund* Anda belum aktif, Anda dapat mengaktifkan nya dengan mengisi form yang terdapat pada [link berikut ↗](https://midtrans.com/id/contact-us/transaction-information/prosedur-refund-pengembalian-dana).