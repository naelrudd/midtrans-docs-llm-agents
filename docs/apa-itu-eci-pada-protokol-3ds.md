---
updatedAt: 2025-11-11T00:21:41.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Apa itu ECI pada protokol 3DS?

*Electronic Commerce Indicator (ECI)* adalah kode yang dikirimkan oleh *Directory Servers* (seperti  Visa, MasterCard, JCB, and American Express) sebagai *output* terhadap suatu transaksi *3DS*.

Berikut adalah daftar kode yang akan dikirimkan dari [VISA ↗](https://usa.visa.com/dam/VCOM/download/merchants/verified-by-visa-acquirer-merchant-implementation-guide.pdf), **American Express**, dan **JCB** dan artinya:

* **ECI 05:** Sukses melakukan transaksi *3DS* – kartu memiliki sistem *3DS* dan berhasil mengisi *OTP* yang sesuai.
* **ECI 06:** Sistem *3DS* telah dicoba untuk dilakukan namun tidak terjadi; biasanya terjadi karena kartu tidak memiliki sistem *3DS*.
* **ECI 07:** Sistem 3DS tidak berhasil dilakukan; biasanya terjadi karena kartu tidak memiliki sistem *3DS*, terdapat masalah teknis/koneksi, atau kesalahan setting/konfigurasi.

Berikut adalah daftar kode yang akan dikirimkan dari [MasterCard ↗](https://www.mastercard.us/content/dam/mccom/en-us/documents/SMI_Manual.pdf) dan artinya:

* **ECI 02:** Sukses melakukan transaksi *3DS* – kartu memiliki sistem *3DS* dan berhasil mengisi *OTP* yang sesuai.
* **ECI 01:** Sistem *3DS* telah dicoba untuk dilakukan namun tidak terjadi; biasanya terjadi karena kartu tidak memiliki sistem *3DS*.
* **ECI 00:** Sistem *3DS* tidak berhasil dilakukan; biasanya terjadi karena kartu tidak memiliki sistem *3DS*, terdapat masalah teknis/koneksi, atau kesalahan setting/konfigurasi.