---
updatedAt: 2025-11-11T00:21:21.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Pengenalan Refund

## Tentang Refund (Pengembalian Dana)

Pengembalian dana berarti mengembalikan dana tersebut kembali ke pelanggan. Ini disebabkan oleh pesanan ganda, produk / layanan tidak tersedia, penerbangan dibatalkan, dll.

Untuk memproses pengembalian dana, atau mengembalikan dana kepada pelanggan, kami perlu memastikan bahwa uang telah berhasil ditransfer dari pelanggan ke *merchant*; atau secara operasional, status pembayaran telah diubah menjadi “*Settlement*”. Di Midtrans, permintaan pengembalian dana sebagian besar berlaku dalam transaksi Pembayaran Kartu Kredit, dan ini bekerja dengan mengembalikan limit Kartu. Pengembalian dana untuk metode pembayaran lain dapat diproses oleh pedagang itu sendiri, biasanya dengan mentransfer uang kembali.

Proses pengembalian dana untuk Kartu Kredit biasanya memakan waktu 7-14 hari kerja. Pengembalian dana untuk Kartu Debit bisa memakan waktu lebih lama, hingga dua bulan; dan pelanggan juga perlu menghubungi *Issuing* Bank mereka.

Pengajuan refund memakan waktu beberapa hari karena perlu dikoordinasikan dengan berbagai pihak, seperti bank yang mengakuisisi dan penerbit. Jika pelanggan mengeluh bahwa limit mereka belum dikembalikan, *merchant* harus bertanya kepada *Acquiring* Bank dan pelanggan juga harus bertanya kepada Issuing Bank. Biasanya membutuhkan data: *orderID*, *detail merchant*, detail pelanggan, dan kode persetujuan.

## Kartu Kredit - Agregator

Jika Anda adalah merchant yang menggunakan perjanjian aggregator Midtrans untuk pembayaran Kartu Kredit, permintaan refund harus dilakukan melalui Midtrans. Anda dapat membuka *Merchant Administration Portal (MAP)*, mencari *orderID* spesifik yang Anda butuhkan untuk pengembalian dana, dan klik tombol *Refund*. Setelah menekan tombol, mohon isi jumlah pengembalian dana dan alasan pengembalian dana kemudian tekan *Send*. Kami akan memproses permintaan Anda ke bank pada hari kerja berikutnya. Anda masih akan mendapatkan dana, tetapi kami akan memotong dana dari permintaan pembayaran Anda (*payout*) berikutnya.

Jika tombol refund Anda belum aktif, Anda dapat mengaktifkan nya dengan mengisi form yang terdapat pada [link berikut ↗](https://midtrans.com/id/contact-us/transaction-information/prosedur-refund-pengembalian-dana).

## Kartu Kredit - Fasilitator

Jika Anda adalah merchant yang menggunakan perjanjian *fasilitator* Midtrans untuk pembayaran Kartu Kredit, permintaan *refund* harus dilakukan langsung melalui Bank. Silakan hubungi kami melalui [link berikut ↗](https://midtrans.com/id/contact-us/transaction-information/prosedur-refund-pengembalian-dana) untuk memberi Anda *template* permintaan *refund*.