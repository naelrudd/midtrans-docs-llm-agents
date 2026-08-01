---
updatedAt: 2025-12-10T07:19:34.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Cara download laporan transaksi (transaction reports) dari MAP?

Untuk mengunduh laporan transaksi (*transaction reports*).

1. [Login ↗](https://dashboard.midtrans.com/login?language=id) ke *Merchant Administration Portal* (MAP) dashboard Anda.

2. Pilih ***Environment*** yang Anda butuhkan (***Production*** atau ***Sandbox***).

   <Image border={false} src="https://files.readme.io/058c4d04820183feb2163dd8b03a458567a09aebc0736f9da69233685365d582-Screenshot_2025-12-03_at_10.13.28.png" />

3. Klik menu ***Transactions***.

4. Klik ***Filter*** untuk menyaring daftar transaksi yang ingin ditampilkan. Saat ini filter menggunakan rentang tanggal berfungsi untuk menyaring tanggal transaksi terjadi hingga 30 hari ke belakang. Jika Anda ingin menyaring berdasarkan tanggal settlement, gunakan tombol **"*more filter*"** . Pahami tipe filter-filter Midtrans di artikel berikut ini: <Anchor label="Filtering Guide ↗" target="_blank" href="https://docs.midtrans.com/docs/transactions-page-reporting-operations">Filtering Guide ↗</Anchor>.

5. Klik **Apply** untuk menerapkan filter yang sudah dipilih.

   <Image border={false} src="https://files.readme.io/7697d824b3a8fb2b136842df591d506c10d60a7402b437c25204b46bb8a5bc89-Screenshot_2025-12-03_at_10.33.23.png" />

6. Untuk mendapatkan file laporan tersebut, klik ***Export***.

7. Pilih tanggal transaksi untuk mencantumkan transaksi-transaksi yang ingin di-*export*. Export dibatasi hingga rentang waktu 31 hari per file terkirim.

8. Pilih format file yang ingin diexport: CSV atau Excel. Klik  ***edit table for export*** jika Anda ingin mengatur kolom apa saja yang ingin dimunculkan dalam file yang akan dikirimkan.

<Image border={false} src="https://files.readme.io/0355bb57a8f06f86d2994562e5082c10c9df22f58384295bdeaf4a8a535c9882-Screenshot_2025-12-03_at_10.41.36.png" />

<br />

9. Pilih field yang ingin ditampilkan dengan mencentang checkbox (seperti yang dilingkari pada gambar di bawah ini). Untuk membuka masing-masing bagian (contoh: General Info), klik "^" dan "v" (seperti gambar yang dilingkari di bawah ini).  Klik ***Apply***.

   <Image border={false} src="https://files.readme.io/45a975e28736ca5b198f8a2133d25a0b16149de8c7b1dfdca62f2cd7d4ce44a2-Screenshot_2025-12-03_at_10.42.17.png" />
10. Klik **Send to Email**.

***

> 🚧 Catatan 📝
>
> Link untuk *download report file* akan diterima di inbox Anda dalam waktu 30 menit dan akan kedaluwarsa dalam waktu 48 jam.

> ❗️ Penting ❗️
>
> Anda hanya dapat mengunduh transaksi**dalam 6 bulan terakhir** dari *dashboard*.
>
> Anda **tidak dapat mengunduh transaksi yang lebih lama dari 6 bulan** (misalnya, jika Anda masuk ke *dashboard* pada Juli 2023 dan ingin *download* transaksi dari Januari 2023 ke belakang).
>
> Jika Anda ingin *request* transaksi yang lebih dari 6 bulan. Anda dapat menghubungi tim *support* kami melalui [link berikut ↗](https://midtrans.com/id/kontak-kami/transaction-information/bagaimana-cara-mengunduh-laporan-transaksi).