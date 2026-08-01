---
updatedAt: 2025-11-11T00:19:56.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Apakah saya dapat menerima pembayaran dalam kurensi selain Rupiah (IDR)?

Anda dapat menjual produk menggunakan mata uang asing, namun Anda harus melakukan konversi ke Rupiah sebelum mengirimkan *payment/charge request* ke sistem Midtrans. Mengikuti regulasi Bank Indonesia, Midtrans hanya memproses transaksi dengan Rupiah.

Proses konversi perlu dilakukan pada saat *customer checkout* pada website/aplikasi Anda - disarankan Anda menampilkan konversi kurs ke pelanggan untuk menghindari dispute akibat selisih ekspektasi konversi kurs di kemudian hari. Pastikan nilai transaksi yang Anda kirimkan pada *charge request* di Midtrans sudah merupakan nominal dalam IDR.

Untuk pembayaran kartu jika *card issuer* dari luar Indonesia, dari sisi bank *principal* (VISA/MasterCard) sudah support kurensi asing (contoh: *card issuer* USD, *card acquiring* IDR).