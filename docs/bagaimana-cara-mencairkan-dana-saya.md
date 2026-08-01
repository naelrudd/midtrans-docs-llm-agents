---
updatedAt: 2025-11-10T22:49:04.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Bagaimana cara menarik dana (withdrawal) yang ada di akun merchant Midtrans saya?

Catatan: sebelumnya aktivitas ini disebut juga sebagai **"Pencairan Dana /*Payout*"**, agar lebih jelas sekarang disebut sebagai **"Tarik Dana /*Withdrawal*"**.

Jika Anda memiliki akun Merchant Midtrans, anda dapat melakukan Tarik Dana (*withdraw*) setidaknya tiga hari kerja setelah transaksi berhasil diterima via Midtrans. Anda dapat memilih kapan saja setelah tiga hari tersebut untuk proses penarikan dananya. Tidak terdapat biaya tambahan pada saat proses penarikan dana.

Untuk dapat melakukan penarikan dana **pertama kali**, mohon perhatikan kebutuhan berikut:

* Anda harus mengatur informasi rekening bank Anda pada Detail Bank, di menu *Withdrawal*.
* Anda telah melengkapi seluruh data/dokumen yang dibutuhkan saat registrasi
* Memiliki setidaknya 1 transaksi dengan status sukses/settlement.

Apabila data/dokumen kurang lengkap pada saat proses registrasi, Tim Midtrans akan menghubungi Anda melalui email dan/atau Whatsapp secara berkala dalam 3 hari kerja setelah Anda menyelesaikan proses registrasi.

***

Untuk mempelajari lebih lanjut proses Tarik Dana (*withdrawal*) secara umum bisa [dari dokumentasi berikut ini](https://docs.midtrans.com/docs/balance-page-manage-withdraw-your-funds#withdrawing-funds). Atau lanjutkan ke bagian bawah berikut untuk contoh langkahnya.

Umumnya terdapat 2 metode untuk dapat tarik dana yaitu Withdrawal Manual dan Withdrawal Otomatis, dibawah ini dijelaskan cara melakukan masing-masing metode tersebut.

### *WITHDRAWAL* MANUAL

Berikut adalah langkah-langkah yang harus Anda lakukan:

1. Klik menu SALDO pada bagian navigasi.

   ![](https://files.readme.io/2e2b727-image.png)
2. Klik tombol **Tarik dana**.
3. Klik **Konfirmasi**.

   ![](https://files.readme.io/b05863b-image.png)

### *WITHDRAWAL* OTOMATIS

Berikut adalah langkah-langkah yang harus Anda lakukan:

1. Masuk ke Midtrans portal Anda,
2. Klik menu *SETTINGS* > *WITHDRAWAL*
3. Klik menu Penarikan Dana Otomatis, untuk masuk ke halaman pengaturan payout otomatis. 
4. Pilih jangka waktu *withrawal* yang Anda inginkan. Pilih jadwal hari (untuk *withdrawal* harian) atau nama hari (untuk *withdrawal* mingguan) atau tanggal (untuk *withdrawal* bulanan) yang Anda inginkan.\
   ***Disabled***: Fitur *withdrawal* otomatis dinonaktifkan.\
   ***Enabled***: Fitur *withdrawal* otomatis diaktifkan.\
   **Harian**: Proses *withdrawal* otomatis akan dilakukan sesuai jumlah hari yang dipilih (hari kerja).\
   **Mingguan**: Proses *withdrawal* otomatis akan dilakukan setiap satu minggu sekali (hari kerja).\
   **Bulanan**: Proses *withdrawal* otomatis akan dilakukan setiap satu bulan sekali (hari kerja).
5. Klik **Simpan**.

Untuk *Withdrawal* Otomatis, pastikan dana yang dapat ditarik **lebih dari sama dengan Rp. 50,000**. Jika pada saat jadwal *withdrawal* otomatis berjalan namun dana kurang, maka proses *withdrawal* tidak dapat dilakukan hingga menunggu dana minimun tercukupi. Dan juga jika dalam 8 hari sebelum jadwal *withdrawal* otomatis, merchant Anda tidak memiliki transaksi yang sukses maka proses *withdrawal* otomatis tidak akan berjalan dan Anda dapat melakukan *withdrawal* manual untuk dapat melakukan penarikan dana.

![](https://files.readme.io/4afd02fd72d0c6c426029468d5c8d1ba628b4bcd59ce55f82b5cd404e37610c4-img_v3_02rm_5230dc89-559f-41f9-be5c-0bd2334fa1hu.jpg)

![](https://files.readme.io/f0f5643d6f8b9c20aae90a57249b6d4abb2d8ef0d1660ae202498da65b420b33-image.png)

Setelah Anda melakukan penarikan dana, maka sistem Midtrans secara otomatis akan mengirimkan email payout receipt request ke email yang Anda masukkan di dashboard **Midtrans (MAP) menu Settings > Email Notification > Email Payout Report.**

![](https://files.readme.io/c175703-image.png)

### Catatan dan Limitasi

Mohon dicatat limitasi berikut terkait proses Tarik Dana:

* Anda akan mendapatkan uang di hari yang sama jika proses penarikan dana dilakukan **SEBELUM** pukul **11.00 WIB**. Jika proses penarikan dana dilakukan **pada pukul 11.00 WIB** atau **SETELAHNYA**, Anda akan memperoleh dana keesokan harinya.
* Mungkin akan ada penundaan ketika hari libur (seperti akibat dari libur operasional bank), namun Anda dapat menghubungi kami jika belum mendapatkan uang Anda dalam jangka waktu tiga hari setelah proses penarikan dana dilakukan.
* Tarik dana **tidak tersedia pada jam 00:00 sampai 01:00** setiap hari, dikarenakan adanya proses internal *transaction summary* harian.
* Hanya bisa dilakukan jika jumlah dana yang dapat ditransfer (*Payable* (*Nett*)) pada akun Anda **paling sedikit sejumlah Rp. 10,000**.
* Dalam mengatur informasi rekening bank (baik untuk **pertama kali** atau **perubahan**), pastikan  pada **Detail Bank** untuk memilih **Nama Bank** yang sesuai dengan tipe rekening bank, khususnya terkait **perbedaan antara rekening bank reguler dan rekening bank*virtual account***. Contohnya: "Bank Permata", berbeda dengan "Bank Permata - Virtual Account".