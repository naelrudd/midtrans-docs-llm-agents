---
updatedAt: 2025-11-11T00:18:17.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Pengenalan QRIS Statis

*Quick Response Code Indonesian Standard* atau biasa disingkat QRIS (dibaca KRIS) adalah penyatuan berbagai macam QR dari berbagai Penyelenggara Jasa Sistem Pembayaran (PJSP) menggunakan kode QR. QRIS dikembangkan oleh industri sistem pembayaran bersama dengan Bank Indonesia agar proses transaksi dengan kode QR dapat lebih mudah, cepat, dan terjag​a keamanannya.

*Merchant* hanya perlu membuat akun pada salah satu penyelenggara QRIS yang sudah [berizin dari BI​ ↗](https://www.bi.go.id/PJSPQRIS/Default.aspx) yang salah satunya adalah [Midtrans ↗](https://midtrans.com/id).

Selanjutnya, ***merchant* dapat menerima pembayaran dari customer menggunakan QR dari aplikasi manapun**. Tunggu apa lagi? ayo daftar dan gunakan QRIS!​​​​

<br />

# Content List

## Apa perbedaan antara QRIS statis dan QRIS dinamis?

| **QRIS Statis**                                                                                                                                                  | **QRIS Dinamis**                                                                                                             |
| :--------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------- |
| Kode QR untuk QRIS statis akan **selalu sama**, *merchant* hanya membutuhkan **1 kode QR** untuk setiap transaksi.                                               | Kode QR untuk QRIS dinamis akan **selalu berbeda** untuk setiap transaksi.                                                   |
| Nominal pembayaran pada QRIS statis tidak ditentukan terlebih dahulu oleh *merchant*, **customer dapat melakukan input nominal** setelah scan kode QR dilakukan. | Nominal pembayaran pada QRIS dinamis **ditentukan terlebih dahulu oleh*merchant*** dan tidak bisa diubah oleh customer Anda. |
| Order ID untuk transaksi QRIS statis **ditentukan oleh sistem**, dengan format QRIS-xxx.                                                                         | Order ID untuk transaksi QRIS dinamis **dapat ditentukan oleh*merchant*** secara bebas.                                      |
| Transaksi akan terbentuk untuk QRIS statis **setelah pembayaran dilakukan**.                                                                                     | Transaksi akan terbentuk untuk QRIS dinamis **sebelum pembayaran dilakukan**.                                                |
| *Refund* untuk QRIS statis untuk saat ini **belum dapat dilakukan**.                                                                                             | Refund untuk QRIS dinamis **dapat dilakukan** lewat dashboard dan API.                                                       |

<br />

<Image
  alt="An example of a **static QRIS** that can be displayed in your offline store. The QR code will **always be the same** for every transaction.  
[Image Source](https://qris.online/homepage/qris-news-detail?page=3-7-alasan-mengapa-bisnis-anda-wajib-pakai-qris-sekarang-juga)"
  align="center"
  src="https://files.readme.io/693e486-image_14.png"
>
  Contoh **QRIS statis** yang bisa dipajang di toko *offline* Anda.\
  Kode QR akan **selalu sama** untuk setiap transaksi.\
  [Sumber Gambar](https://qris.online/homepage/qris-news-detail?page=3-7-alasan-mengapa-bisnis-anda-wajib-pakai-qris-sekarang-juga)
</Image>

<br />

<Image alt="An example of a **dynamic QRIS**. The QR code will **always be different** for each transaction." align="center" src="https://files.readme.io/1644ec3-QRIS_dinamis.png">
  Contoh **QRIS dinamis**. Kode QR akan **selalu berbeda** untuk setiap transaksi.
</Image>

***

<br />

## Untuk apa *merchant* menggunakan QRIS statis?

Pada umumnya QRIS statis dapat digunakan untuk:

* Kebutuhan menerima pembayaran melalui QRIS tanpa mesin EDC/POS di toko *offline* atau bazaar dimana diperlukan *flow* pembayaran yang sangat cepat.
* Penerimaan donasi/*open amount transaction*, kode QRIS dapat dipasang oleh *merchant* di *website* atau media sosial.
* Pembayaran transaksi melalui media sosial/*chat app*, sebagai alternatif dari *Payment Link*.
* Pembayaran untuk transaksi yang sifatnya tidak diketahui jumlahnya sebelum transaksi berakhir/dapat berubah-ubah, seperti *down payment*, pembayaran jasa, ataupun yang lainnya.

***

<br />

## How to receive payments using static QRIS

![](https://files.readme.io/363723a-image.png)

***

<br />

## Cara aktivasi QRIS statis untuk GoPay

Dengan mendaftar produk GoPay di Midtrans, *merchant* akan langsung mendapatkan produk QRIS statis sekaligus dengan QRIS dinamis.

QRIS statis akan didapatkan dalam **3-7 hari kerja** setelah menyelesaikan [proses pendaftaran ↗](https://dashboard.midtrans.com/register) dan mengisi formulir [pendaftaran QRIS GoPay ↗](https://www.tfaforms.com/5019792).

***

<br />

## Apakah *merchant* membutuhkan akun (MID) yang berbeda untuk aktivasi GoPay statis jika GoPay dinamis nya sudah aktif?

Tidak perlu, *merchant* bisa menggunakan akun (MID) yang sama.

***

<br />

## Cara *merchant* mendapatkan kode QR statis

Midtrans akan mengirimkan ***file digital image*** (gambar digital kode QR statis) ke ***email*** dan ***WhatsApp*** *merchant*.

***

<br />

## Apa yang perlu *merchant* lakukan setelah filenya dikirimkan?

* Mencetak kode QRIS statis untuk dipasang di toko/bazaar.
* Sharing secara digital (misalnya untuk transaksi via WhatsApp, atau bisa dipasang di *website* untuk donasi *open amount*, media sosial, dikirim via *newsletter*, dan lain-lain).

***

<br />

## Cara cek transaksi QRIS statis

Anda perlu menjadi *merchant* Midtrans untuk dapat menggunakan QRIS statis Midtrans.

Cek transaksi QRIS statis dapat dilakukan di [dashboard Midtrans (MAP) ↗](https://dashboard.midtrans.com/login?language=id). Mohon diperhatikan bahwa transaksi QRIS statis **tidak dapat** dicek melalui ***GoBiz app/dashboard***.

Ikuti langkah-langkah berikut untuk mengecek transaksi Anda:

1. [Login ↗](https://dashboard.midtrans.com/login?language=id) with your registered email.
2. Pilih menu **Transaksi**.

   ![](https://files.readme.io/83d1279-image.png)
3. Daftar transaksi yang berhasil dapat anda temukan pada halaman ini.
   1. Transaksi dengan status ***SETTLEMENT*** artinya dana sudah diterima dari pelanggan, dan dapat **dicairkan dalam 2 hari kerja**.
   2. Transaksi dengan status ***FAILURE, DENY, CANCEL, EXPIRE*** artinya transaksi gagal dan **uang tidak diterima**.

***

<br />

## Cara pencairan dana QRIS statis

Pencairan dana dapat dilakukan dalam **2 hari kerja** setelah pembayaran dari pelanggan diterima (berstatus **SETTLEMENT**).

Terdapat 2 metode untuk dapat mencairkan dana Anda, yaitu **Payout Manual** dan **Payout Otomatis**.

Silakan klik [di sini ↗](https://docs.midtrans.com/docs/bagaimana-cara-mencairkan-dana-saya) untuk mengetahui bagaimana cara mencairkan dana Anda dengan metode yang Anda butuhkan.

***

<br />

## Is static QRIS already available on the Payment Link?

Saat ini belum tersedia, *merchant* cukup menggunakan *file digital image* (gambar digital kode QR statis) yang dikirimkan Midtrans ke ***email*** dan ***WhatsApp merchant***.

***

<br />

## Can a static QRIS be created via the API?

Saat ini belum tersedia, *merchant* cukup menggunakan *file digital image* (gambar digital kode QR statis) yang dikirimkan Midtrans ke ***email*** dan ***WhatsApp merchant***.

***

<br />

## Transaksi berhasil namun tidak ada di dashboard Midtrans.

Apakah Anda pernah mendaftar QRIS di provider lain selain Midtrans?

**Apabila ya**, maka mohon untuk melakukan pengecekan terlebih dahulu di provider tersebut apakah transaksinya ada atau tidak.

**Apabila tidak**, maka silakan kirimkan bukti-bukti di bawah ini ke [link berikut ↗](https://midtrans.com/id/kontak-kami/transaction-information/Pertanyan-lain).

1. Bukti transaksi berhasil (foto berisikan bukti berhasil, nama *merchant* dan nominal) - Contoh [bukti transaksi ↗](https://drive.google.com/file/d/1NX4CweILhhx9yWBpcUnIRp-VA3URi5vz/view).
2. Nominal transaksi, pembayaran menggunakan *e-wallet*/bank apa dan jam transaksi (Apabila tidak ada di screenshot. Jika terdapat di *screenshot* maka Anda bisa abaikan poin nomor 2 ini).

***

<br />

## Bagaimana jika Anda pernah mendaftar QRIS di provider lain selain Midtrans?

Aturan PTEN saat ini mewajibkan konsep 1 QRIS untuk semua, dengan prioritas untuk memproses transaksi QRIS secara ***on-us* (*issuer-acquirer* sama)**. Dikarenakan konsep 1 QRIS untuk semua tersebut, maka apabila KTP/Entitas sudah pernah didaftarkan sebelumnya ke PTEN untuk produk QRIS di luar Midtrans, maka kode QRIS statis yang diberikan Midtrans otomatis berlaku juga untuk acquirer QRIS yang didaftarkan di luar Midtrans.

Dengan hal ini berarti bahwa **ada kemungkinan transaksi tertentu akan masuk ke*acquirer* lain di luar *acquirer* yang disupport oleh Midtrans**, walaupun kode QRIS ini dikirimkan oleh Midtrans ke Anda. Dalam hal ini, **silakan lakukan pengecekan di*acquirer* tersebut untuk memastikan apakah transaksinya berhasil atau tidak**.

***

> 📘 Info 💡
>
> ***Acquirer*** adalah bank atau lembaga non-bank yang berfungsi menerima dana transaksi dari bank *merchant* (*issuer*). Contoh: GoPay, ShopeePay, OVO, DANA, dan lain-lain.
>
> ***Issuer*** adalah bank atau lembaga non-bank yang berfungsi mengirim dana transaksi ke *acquirer*. Contoh: BCA, BNI, BRI, Mandiri, dan lain-lain.

> 🚧 Catatan 📝
>
> Midtrans **tidak dapat melihat transaksi yang diproses oleh*acquiring* lain**. Dalam hal ini, Midtrans berperan sebagai penyalur kode QRIS yang dibuat oleh PTEN, namun Midtrans tidak berhak untuk mengatur *acquiring* mana yang akan memproses transaksi tersebut.
>
> Apabila Anda ingin agar semua transaksi secara pasti hanya masuk/diproses oleh Midtrans, Anda dapat mengajukan permohonan ke *provider* lain untuk **mengajukan pemberhentian kerjasama dengan*provider* lain** agar provider tersebut tidak lagi terdaftar di PTEN sebagai *acquirer* Anda.