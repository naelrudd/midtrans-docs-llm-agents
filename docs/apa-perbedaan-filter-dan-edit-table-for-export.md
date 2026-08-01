---
updatedAt: 2026-01-28T07:09:57.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Cara Mengkonfigurasi Data dan Kolom yang Ingin Ditampilkan Laporan yang Diunduh

Pada bagian atas dari setiap halaman laporan, baik laporan transaksi maupun laporan saldo, terdapat fungsi navigasi dan operasional, berupa pencarian (search), penyaringan (filter), dan pengunduhan dalam bentuk file (export). Meskipun sering digunakan bersamaan, Filter dan Edit Table for Export memiliki fungsi yang berbeda. Artikel ini akan menjelaskan perbedaan keduanya agar Anda dapat menggunakan fitur laporan dengan lebih optimal.

<br />

Pada bagian atas dari setiap halaman laporan, baik laporan transaksi maupun laporan saldo, terdapat fungsi navigasi dan operasional, berupa pencarian (search), penyaringan (filter), dan pengunduhan dalam bentuk file (export). Meskipun sering digunakan bersamaan, Filter dan Edit Table for Export memiliki fungsi yang berbeda. Artikel ini akan menjelaskan perbedaan keduanya agar Anda dapat menggunakan fitur laporan dengan lebih optimal.

1. Filter\
   Filter digunakan untuk menyaring data transaksi yang ditampilkan di halaman laporan berdasarkan kriteria tertentu.
   Contoh penggunaan:
   a. Menampilkan hanya transaksi dengan transaction type = payment
   b. Menyaring transaksi berdasarkan tanggal, status, atau metode pembayaran tertentu

   Filter dibagi menjadi dua jenis:
   a. Quick Filter: filter yang sering digunakan dan dapat diakses langsung
   b. More Filter: filter tambahan untuk penyaringan yang lebih spesifik

   📌 Catatan:
   Filter hanya memengaruhi data transaksi yang ditampilkan di halaman laporan dan akan menjadi acuan jika laporan tersebut diekspor.
2. Export\
   Export digunakan untuk mengirim laporan dalam bentuk file (misalnya CSV atau Excel) ke email Anda. Laporan yang dikirim dapat berupa:
   a. Data tanpa filter, atau
   b. Data sesuai filter yang sedang aktif

   Sebelum laporan dikirim, Anda dapat menggunakan fitur Edit Table for Export untuk mengatur kolom apa saja yang ingin ditampilkan atau disembunyikan pada file laporan.

   <br />

   Cara Menggunakan Edit Table for Export:

   1. Klik tombol Export
   2. Pilih Edit Table for Export
   3. Centang kolom yang ingin ditampilkan pada laporan
   4. Klik Apply untuk menyimpan pengaturan kolom
   5. Klik Send to Email untuk mengirim laporan ke email Anda

   <br />

   📌 Catatan:
   Edit Table for Export tidak memengaruhi data yang ditampilkan di halaman, melainkan hanya mengatur struktur kolom pada file hasil export.

<br />

**Penyimpanan Preferensi**

Untuk memudahkan penggunaan berulang, pengaturan filter dan pilihan kolom pada Edit Table for Export akan otomatis mengikuti pengaturan terakhir yang digunakan oleh pengguna.

Rangkuman:

<br />

| Aspek                                        | Filter                                                          | Edit Table for Export                                        |
| -------------------------------------------- | --------------------------------------------------------------- | ------------------------------------------------------------ |
| Tujuan                                       | Menyaring data transaksi yang ditampilkan                       | Mengatur kolom yang ditampilkan pada file laporan            |
| Mempengaruhi data transaksi yang ditampilkan | ✅ Ya                                                            | ❌ Tidak                                                      |
| Mempengaruhi tampilan kolom laporan          | ❌ Tidak                                                         | ✅ Ya                                                         |
| Mempengaruhi hasil export                    | ✅ Ya, baris data yang dimunculkan sesuai filter yang aktif      | ✅ Ya, hanya pada struktur kolom                              |
| Contoh penggunaan                            | Menampilkan hanya transaksi dengan `transaction type = payment` | Menyembunyikan kolom fee atau menampilkan kolom reference ID |
| Waktu penggunaan                             | Sebelum melihat atau meninjau data                              | Sebelum mengirim laporan via email                           |
| Ruang lingkup                                | Data transaksi                                                  | Layout kolom pada file export                                |
| Disimpan untuk penggunaan berikutnya         | ✅ Ya                                                            | ✅ Ya                                                         |