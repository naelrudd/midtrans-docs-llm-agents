---
updatedAt: 2025-11-11T00:22:05.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Mengapa status transaksi customer Saya Pending/Failure sedangkan dana sudah berkurang?

Dalam beberapa kasus yang jarang terjadi, ketika dana konsumen berhasil terdebet tetapi dari sisi bank/payment provider gagal memproses transaksi karena hal-hal seperti masalah jaringan, maka transaksi dianggap gagal di sisi Midtrans. Pada umumnya, dana konsumen tidak akan terdebet. Jika dana terdebet, maka akan dikembalikan (*refund*) secara otomatis oleh pihak payment provider dalam 1-5 hari kerja setelah transaksi.

Sebagian besar bank atau payment provider memberi tahu konsumen (melalui SMS, email, *push notification*, dan sebagainya) hanya ketika dana berhasil terdebet. Terkadang konsumen tidak mendapatkan informasi saat transaksi dikembalikan atau dibatalkan oleh bank/*payment provider*. Hal ini dapat membingungkan konsumen.

Merchant dapat menyarankan konsumen untuk memeriksa laporan tagihan atau transaksi mereka secara berkala atau dapat menghubungi bank/*payment provider* mereka untuk memastikan bahwa tidak ada dana yang dipotong. Anda juga dapat memeriksa detail transaksi di *Dashboard* Midtrans untuk melihat apakah transaksi tersebut mendapatkan status *cancel*.

Jika diperlukan pengecekan status dana lebih lanjut, Anda dapat menghubungi kami dengan akses halaman [Contact Us ↗](https://midtrans.com/id/kontak-kami/transaction-information/dana-konsumen-saya-terdebet-namun-status-di-midtrans-failurepending), pilih kategori **Informasi Transaksi** dan pilih pertanyaan **Dana konsumen saya terdebet namun status di Midtrans*Failure/Pending***, klik **"Ya"** pada pilihan **"Apakah Anda masih membutuhkan informasi lebih lanjut?"** isi dan *submit form* nya.