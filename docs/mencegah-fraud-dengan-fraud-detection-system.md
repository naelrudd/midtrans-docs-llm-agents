---
updatedAt: 2025-11-11T00:21:39.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Mencegah Fraud dengan Fraud Detection System

Setelah merchant online mulai menerima pembayaran kartu kredit online, tolak bayar dan perselisihan tidak bisa dihindari. Sebagai *gateway* pembayaran, Midtrans menawarkan *3DSecure* sebagai bentuk perlindungan, namun *3DSecure* tidak menjamin 100% transaksi bebas penipuan. Bank dan Principal (mis. VISA, MasterCard, JCB, AMEX, dll) mewajibkan pedagang untuk menjaga rasio penipuan mereka sendiri agar berada di bawah ambang batas yang dapat diterima Bank dan Prinsipal.

*FDS* Midtrans terintegrasi langsung ke dalam sistem pembayaran, mencegah kemungkinan transaksi yang mencurigakan sebagai perlindungan lapis kedua sebelum transaksi dibebankan ke bank. FDS menggunakan kombinasi mesin aturan dan algoritma pembelajaran mesin. Skema aturan kami dikembangkan berdasarkan pola penipuan yang berlaku di setiap industri, diperbarui terus menerus berdasarkan tren penipuan. Di area di mana mesin aturan kami gagal, algoritma pembelajaran mesin kami - mesin 'pintar' yang belajar sendiri dari perilaku transaksi historis - akan mencakupnya. *FDS* Midtrans juga dibuat dengan database daftar hitam (*blacklist*) yang komprehensif di atas mesin aturan dan algoritma pembelajaran mesin kami, yang kami kumpulkan dari berbagai sumber (laporan penipuan bank dan *Principal*, kasus sengketa yang diketahui, dan aktivitas pemantauan kami sendiri) selama bertahun-tahun. Setiap transaksi yang melalui Midtrans disaring dengan semua mekanisme ini - yang menciptakan proses penyaringan penipuan yang kuat.

Untuk dapat menangkap pola penipuan tanpa menolak transaksi yang valid, *FDS* mengandalkan data yang dikirimkan *merchant* kepada kami - semakin banyak area data yang kami terima, semakin canggih skema aturan yang dapat diterapkan. Karenanya, kami mendorong merchant untuk mengirimkan data sebanyak mungkin kepada kami (data Anda hanya akan digunakan untuk tujuan ini saja - kami menjaga keamanan dan privasi data *merchant* kami dengan serius).