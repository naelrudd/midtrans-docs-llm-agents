---
updatedAt: 2025-11-11T00:18:52.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Pengenalan alur pembayaran Kartu Kredit

**Alur Pembayaran Kartu Kredit**

Pembayaran *online* menggunakan kartu kredit / debit adalah salah satu metode pembayaran yang paling nyaman dan umum digunakan; ini bekerja secara instan - Anda akan mendapatkan status pembayaran segera setelah Anda mengkonfirmasi pembayaran. Tetaplah di kursi Anda, keluarkan kartu dari dompet Anda untuk mengisi detail kartu - dan Anda langsung mendapatkan status pembayaran. Bayangkan Anda perlu melakukan perjalanan bisnis hari ini; Anda cukup duduk dan mencari-cari opsi penerbangan yang paling nyaman untuk Anda, membeli dan membayar segera, menerima tiket, lalu pergi ke bandara. Ini sangat berbeda dengan jenis pembayaran asinkron lainnya seperti transfer bank atau pembayaran toko swalayan, di mana Anda harus pergi ke ATM (atau toko swalayan) setelah Anda mengonfirmasi pembayaran di situs web *eCommerce*.

Meski terasa instan, ada banyak langkah dan proses di bawah pembayaran kartu; mari kita pahami lebih baik dengan membaca penjelasan di bawah ini.

**Pelanggan mengisi kartu dan detail pelanggan di**

![](https://files.readme.io/de8bc9e-image.png)

Sebelum proses kartu kredit bekerja, ada beberapa tindakan yang perlu dilakukan oleh pelanggan setelah dia memutuskan untuk membayar menggunakan kartu kredit: mengisi data kartu dan pelanggan. Selain alamat email atau nomor telepon, pelanggan akan diminta untuk mengisi nomor kartu, tanggal kedaluwarsa, dan CVV. Selain itu, informasi alamat penagihan dan pengiriman mungkin juga diperlukan untuk beberapa situs web eCommerce.

Setelah semua informasi terisi dan pelanggan memutuskan untuk membayar dengan mengklik tombol **bayar**, pedagang/merchant akan mengirimkan permintaan pembayaran ke gateway pembayaran (Jika pedagang menggunakan Core API Midtrans, merchant harus melakukan [Get Token ↗](https://api-docs.midtrans.com/#get-token) dan [Charge ↗](https://api-docs.midtrans.com/#authorization)).

**Pelanggan mengautentikasi pembayaran (3D Secure System)**

<Image alt="Source: <http://bnicardcenter.co.id/Promo/Info-Promo/3D-Secure.aspx>" align="center" src="https://files.readme.io/662c93e-image.png">
  Source: [http://bnicardcenter.co.id/Promo/Info-Promo/3D-Secure.aspx](http://bnicardcenter.co.id/Promo/Info-Promo/3D-Secure.aspx)
</Image>

Sebagian besar merchant menggunakan sistem 3D Secure, lapisan keamanan tambahan di mana jaringan utama (VISA / MasterCard / JCB / Amex) akan berkoordinasi dengan Bank nasabah untuk mengotentikasi nasabahnya menggunakan OTP (One Time Password). Setelah pelanggan mengklik bayar, pelanggan akan menerima kode melalui SMS atau USSD atau email; saat dia dialihkan ke halaman otentikasi Issuing Bank. Kemudian pelanggan harus memasukkan kode untuk mengautentikasi pembayaran.

Namun, jika Bank pelanggan atau merchant tidak mendukung sistem 3DS, maka pelanggan tidak perlu melakukan autentikasi (halaman autentikasi akan dilewati).

**Fraud Detection System memfilter transaksi**

Jika merchant menggunakan payment gateway, biasanya ada Fraud Detection System (FDS) yang bekerja di belakang. Sistem Deteksi Penipuan bekerja dengan memperhatikan perilaku atau pola pembayaran online yang tidak umum dan / atau mengidentifikasi basis data Penipuan dan / atau pembelajaran mesin. FDS sangat efektif dalam mencegah penipuan online, namun ini bukan jaminan bahwa upaya penipuan dapat sepenuhnya diisolasi.

**Bank mengotorisasi pembayaran**

Sementara nasabah menunggu status transaksinya, Bank melakukan dua proses berturut-turut - Authorize dan Capture. Di Otorisasi, Bank meninjau kartu pelanggan dan melihat apakah ada cukup dana untuk menutupi nilai barang / jasa yang dibeli oleh pelanggan. Setelah selesai, dana akan dikunci (booked) - ini disebut Capture. Proses ini bekerja di belakang tanpa diketahui pelanggan; dan bekerja dalam milidetik.

**Pelanggan menerima status transaksi**

Pelanggan akan memiliki status transaksinya dalam hitungan detik setelah permintaan pembayaran. Ini bisa menjadi Success atau Deny. Perlu diketahui bahwa tingkat keberhasilan pembayaran kartu kredit kira-kira sekitar 70% - 80%, artinya mungkin ada 2-3 dari 10 pembayaran kartu kredit yang ditolak karena berbagai alasan.

Berikut contoh notifikasi http pada transaksi Sukses yang diterima merchant:

```
{  
"status_code" : "200",  
"status_message" : "Success, Credit Card capture transaction is successful",  
"transaction_id" : "ca297170-be4c-45ed-9dc9-be5ba99d30ee",  
"masked_card" : "451111-1117",  
"order_id" : "testing-0.4555-1414741517",  
"payment_type" : "credit_card",  
"transaction_time" : "2014-10-31 14:46:44",  
"transaction_status" : "capture",  
"fraud_status" : "accept",  
"bank"" : "bni",  
"gross_amount" : "30000.00"  
}
```

**Tindakan yang harus diambil setelah pembayaran**

Setelah status transaksi diubah menjadi Success, merchant bisa langsung mengirimkan barang / jasa. Harap diperhatikan bahwa transaksi Success akan tetap Success dan akan diubah menjadi Settlement pada saat Settlement.

Namun, merchant juga dapat membatalkan transaksi Success jika pelanggan melakukan pemesanan ganda atau permintaan pengembalian dana lainnya. Sebelum waktu Settlement, merchant dapat mengirimkan permintaan pembatalan (biasa disebut Cancel / Void), kemudian limit akan kembali ke kartu kredit pelanggan (sebagian besar langsung tapi bisa sampai paling lambat 1-2 hari). Namun, jika permintaan pembatalan dikirim setelah waktu Settlement - biasa disebut Refund, limit akan kembali ke kartu kredit pelanggan selambat-lambatnya 14 hari kerja.

**Sistem mengunci transaksi: Settlement**

Settlement adalah ketika sistem terkunci dan memicu transfer dana dari Issuer ke Acquirer; dalam hal ini dari kartu kredit pelanggan ke Bank merchant. Di toko offline, Settlement biasanya dilakukan di akhir penjualan - saat toko tutup.

Anda dapat melakukan apapun pada transaksi tersebut (termasuk Cancel transaksi Success) tetapi tidak setelah waktu Settlement.

[Klik disini ↗](https://docs.midtrans.com/reference/credit-card-object) untuk detailnya.

Berikut contoh notifikasi http pada transaksi Settlement:

```
{  
"masked_card": "518828-5606",  
"approval_code": "A12345",  
"bank": "bni",  
"eci": "02",  
"transaction_time" : "2014-10-31 14:46:44",  
"gross_amount": "59378.00",  
"order_id" : "testing-0.4555-1414741517",  
"payment_type": "credit_card",  
"status_code": "200",  
"transaction_id": "123456789abcdefghijklmnopqrstuvwxyz",  
"transaction_status": "settlement",  
"fraud_status": "accept",  
"status_message": "Midtrans payment notification"  
}
```