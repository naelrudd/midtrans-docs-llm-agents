---
updatedAt: 2025-11-11T00:21:39.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# FDS and 3DS

Dengan transaksi tanpa menunjukkan kartu, merchant dihadapkan pada risiko menerima transaksi penipuan. Dalam ranah kartu kredit, transaksi dianggap sebagai penipuan jika transaksi tidak dilakukan oleh pemilik sah kartu kredit, atau pemegang kartu tidak mengotorisasi transaksi. Ketika transaksi penipuan terjadi, Tagihan Balik (*chargeback*) dan Sengketa (*dispute*) akan menyusul - yang biasanya ketika merchant mengalami kasus tolak bayar atau sengketa, merchant berkewajiban untuk mengembalikan jumlah nilai transaksi kembali kepada pemegang kartu, terlepas dari apakah produk telah dikirim atau belum.

Salah satu langkah pengamanan yang kami berikan kepada merchant kami adalah perlindungan *3DSecure*, dimana ketika merchant mengaktifkan fitur ini, selama syarat penyelesaian sengketa terpenuhi (dalam hal pemenuhan dokumen), merchant akan terlindungi dari kewajiban di atas. Lalu, mengapa pedagang memerlukan penyaringan tambahan dari *FDS* ketika *3DSecure* cukup untuk melindungi mereka dari sengketa? Belum lagi, *3DSecure* memaksa semua pelanggan untuk memasukkan kata sandi terlebih dahulu untuk mengotorisasi transaksi, bukankah seharusnya cukup aman?

Jawabannya adalah bahwa Bank dan *Principal* benar-benar melacak rasio penipuan masing-masing merchant. Bank dan *Principal* mungkin menganggap penipuan berlebihan yang terjadi di *merchant* sebagai sinyal bahwa pedagang mungkin lalai dalam menyaring transaksinya, atau bahkan menyalahgunakan perlindungan *3DSecure*. Oleh karena itu, pedagang dengan rasio penipuan yang tinggi dapat menyebabkan pedagang tersebut dimasukkan ke dalam program pemantauan *Principal* dan Bank, atau bahkan berbagai bentuk hukuman.

*3DSecure* tidak menjamin bahwa suatu transaksi mungkin 100% asli karena terdapat berbagai perbedaan dalam penerapan di seluruh bank dan negara, dan juga celah yang dapat dieksploitasi seperti skema rekayasa sosial, tingkat proses otentikasi keamanan yang lebih rendah (seperti penggunaan kata sandi statis untuk otorisasi kode alih-alih kata sandi satu kali (*OTP*)), dan banyak kemungkinan lainnya. Namun, *FDS* mengevaluasi transaksi berdasarkan berbagai kondisi, seperti norma perilaku transaksi dalam suatu industri, tren penipuan terkini, basis data penipuan yang terkait dengan lingkaran kejahatan online yang sedang aktif, dan banyak lagi lainnya.

Dengan semua pertimbangan di atas, kami tidak menganggap setiap ukuran sebagai pengganti satu sama lain. Sebaliknya, *FDS* dan *3DSecure* digunakan bersama-sama untuk menciptakan mekanisme penyaringan penipuan yang kuat untuk semua transaksi yang diproses oleh Midtrans.