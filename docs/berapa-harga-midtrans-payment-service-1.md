---
updatedAt: 2025-11-11T00:19:02.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Berapa harga Midtrans payment service?

Struktur harga Midtrans sangat sederhana, Anda hanya perlu membayar per transaksi yang sukses. Tidak ada biaya untuk implementasi atau *maintenance*. Untuk detil harga per metode pembayaran, silakan lihat [di sini ↗](https://midtrans.com/id/biaya). Semua biaya belum termasuk pajak pertambahan nilai (PPN).

PPN diambil dari nilai biaya tiap metode pembayaran, dimana contoh simulasinya seperti ini:

Jika harga barang adalah **Rp. 100,000** dan customer membayar menggunakan **Bank Transfer** dimana biaya Midtrans nya adalah **Rp. 4,000, PPN** (11%) diambil dari nilai tersebut sehingga total biaya nya adalah **Rp. 4,440.** Anda sebagai merchant mendapatkan nilai bersih bersih sebesar **Rp. 100,000 - Rp. 4,440 = Rp. 95,560** ketika melakukan pencairan dana (Midtrans secara otomatis memotong biaya pada saat merchant melakukan pencairan dana).

Untuk payment channel yang menggunakan sistem MDR seperti *Credit Card*, terdapat tambahan potongan biaya MDR dari total harga barang disetiap transaksinya. MDR (*Merchant Discount Rate*) adalah biaya yg dihitung dalam bentuk *percentage* (%) dan hanya berlaku untuk beberapa metode pembayaran. (contoh: *Credit Card* MDR nya 2.9%)

Midtrans juga tidak membebankan biaya tambahan untuk penggunaan *service* CoreAPI.

Untuk biaya metode pembayaran BCA dan Indomaret, terdapat proses kerjasama yang perlu dilakukan dengan pihak BCA dan Indomaret untuk mengetahui detail nilainya. Jika Anda tetap tertarik untuk menggunakan metode pembayaran tersebut atau ingin melakukan negosiasi nilai biaya yang diterapkan, Anda dapat menghubungi kami melalui halaman [Hubungi Kami ↗](https://midtrans.com/id/contact-us/informasi-transaksi/berapa-biaya-penggunaan-layanan-midtrans) isi dan submit form nya.