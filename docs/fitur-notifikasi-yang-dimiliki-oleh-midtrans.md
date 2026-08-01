---
updatedAt: 2025-11-11T00:18:38.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Fitur notifikasi yang dimiliki oleh Midtrans

Midtrans memiliki 2 macam notifikasi yang digunakan untuk mengirimkan informasi kepada Anda sebagai merchant atau customer merchant, yaitu notifikasi email dan notifikasi HTTP.

# Notifikasi Email

Midtrans akan mengirimkan notifikasi secara otomatis berupa email yang berisi informasi terkait cara pembayaran, nomor *Virtual Account* (VA), order ID, dan juga status pembayarannya.

Anda dapat mengaktifkan fitur Notifikasi Email (*Email Notification*) pada *dashboard Midtrans* Anda.

* Untuk mengirimkan notifikasi kepada merchant, Anda dapat mengaktifkannya pada menu ***Settings - Email Notification - (centang) Send email to me - Save***.
* Untuk mengirimkan notifikasi kepada customer, Anda dapat mengaktifkannya pada menu ***Settings - Email Notification - (centang) Send email to customer - Save***.

> 🚧 Notes 📝
>
> *Template email* notifikasi tersebut tidak dapat dirubah.

<Image alt="Contoh notifkasi email yang dikirimkan" align="center" src="https://files.readme.io/3e238c6-image.png">
  Contoh notifkasi email yang dikirimkan
</Image>

***

# Notifikasi HTTP

Midtrans mengirimkan notifikasi melalui *HTTP format* ke *backend merchant*, di mana *merchant* dapat menggunakan notifikasi tersebut untuk *update* status transaksi di sisi *database merchant* atau keperluan internal yang lain.

Untuk mengatur halaman URL yang akan dilihat pelanggan setelah berhasil menyelesaikan transaksi, Anda dapat melakukannya melalui menu **Pengaturan -*Payment* - *Finish Redirect URL***.

![](https://files.readme.io/f4fa3d8-image.png)

![](https://files.readme.io/a9aa2df-image.png)

Silakan memastikan beberapa hal berikut pada saat setting *Finish Redirect URL*:

1. Mohon untuk tidak menggunakan *port* yang tidak biasa pada *endpoint URL* notifikasi Anda (contoh, jangan menggunakan <https://tokoecomm.com:**20070**/notification>), karena layanan notifikasi Midtrans tidak dapat mengirimkan notifikasi ke *port* yang tidak biasa.
2. URL yang Anda gunakan dapat menerima notifikasi HTTP yang dikirimkan Midtrans dan tidak ter-*redirect* ke *URL* lainnya saat diakses.
3. Tidak menggunakan format *IP Address*. (contoh: jangan menggunakan <https://172.168.111.111/notification>).\
   Untuk melakukan setting notifikasi HTTP dapat anda lakukan melalui menu **Pengaturan - Payment - URL Notifikasi**.

![](https://files.readme.io/d3390e9-image.png)

![](https://files.readme.io/34e1212-image.png)

Silahkan memastikan beberapa hal berikut pada saat setting \_Payment URL\_\_ Notifikasi:

1. Mohon untuk tidak menggunakan port yang tidak biasa pada endpoint URL notifikasi  Anda (contoh, jangan menggunakan <https://tokoecomm.com:**20070**/notification>), karena layanan notifikasi midtrans tidak dapat mengirimkan notifikasi ke port yang tidak biasa.
2. URL yang Anda gunakan dapat menerima notifikasi HTTP yang dikirimkan Midtrans dan tidak ter-*redirect* ke URL lainnya saat diakses.
3. Tidak menggunakan format *IP Address*. (contoh: jangan menggunakan <https://172.168.111.111/notification>).\
   Jika Anda menggunakan *IP Whitelist* untuk berkomunikasi dengan API Midtrans, silahkan *whitelist domain* dan *IP address* Midtrans pada [link berikut ↗](https://docs.midtrans.com/docs/ip-address).
4. Jika Anda menggunakan plugin tertentu silahkan sesuaikan setting payment notification URL pada masing - masing plugin yang Anda gunakan [di sini ↗](https://docs.midtrans.com/en/technical-reference/library-plugin).

<br />

Contoh JSON yang dikirimkan untuk masing-masing metode pembayaran dapat Anda lihat pada [link berikut ↗](https://docs.midtrans.com/en/after-payment/http-notification?id=sample-for-various-payment-methods).