---
updatedAt: 2025-11-11T00:19:50.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Bagaimana cara membatalkan transaksi?

Membatalkan transaksi hanya dapat dilakukan untuk transaksi kartu kredit dengan status ***CAPTURE / SUCCESS***, dan juga metode pembayaran lain dengan status ***PENDING***. Anda dapat melakukannya melalui [Merchant Administration Portal (MAP) ↗](https://dashboard.midtrans.com/transactions) pada menu **transaksi**, atau melalui [API ↗ ](https://api-docs.midtrans.com/#cancel-transaction)kami. Untuk membatalkan transaksi melalui MAP, Anda dapat mencari transaksi yang ingin Anda batalkan, masuk ke dalam halaman detilnya, lalu klik tombol ***CANCEL***.

Untuk transaksi kartu kredit jika statusnya sudah *Capture/Success* dan dilakukan cancel, maka *limit customer* akan otomatis kembali maksimal dalam H+1 hari kerja.

Untuk metode pembayaran lain, tidak ada proses pengembalian dana dari sisi Midtrans kepada *merchant* atau konsumen *merchant*, dikarenakan status transaksi belum sampai *Settlement*.

> 🚧 Catatan
>
> transaksi yang statusnya sudah *Settlement* tidak dapat dibatalkan dan dapat dilakukan [Refund ↗](https://support.midtrans.com/hc/id/articles/900000326046-Bagaimana-cara-melakukan-refund-transaksi-) namun hanya untuk transaksi kartu kredit, GoPay, QRIS, Shopeepay dan Akulaku.