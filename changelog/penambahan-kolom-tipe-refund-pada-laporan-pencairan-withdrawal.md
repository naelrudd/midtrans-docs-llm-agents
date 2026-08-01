Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Penambahan Kolom Tipe Refund Pada Laporan Pencairan (Withdrawal)

Dengan  ini kami ingin menyampaikan adanya pembaruan pada Laporan Withdrawal yang nantinya akan mempengaruhi kolom laporan untuk bisnis Anda.

**Apa yang Ditambahkan, dan Apa Kelebihannya?**

* Penambahan kolom baru pada laporan ekspor dan laporan pencairan otomatis untuk menunjukkan Tipe Refund, apakah itu berupa Chargeback atau Normal Refund.
* Hal ini akan memberikan visibilitas yang lebih bagi merchant saat meninjau transaksi.

**Mengapa Hal Ini Penting?**

* Merchant kini dapat dengan mudah membedakan antara chargeback dan normal refund langsung dari laporan.
* Hal ini membantu meningkatkan pelacakan operasional dan proses rekonsiliasi.
* Jika Anda memiliki automasi atau skrip yang memproses laporan yang melakukan pengecekan exact match kepada keseluruhan kolom, harap diperhatikan bahwa pembaruan ini dapat menggaggu logic reporting Anda.
* Perubahan ini tidak akan mengganggu urutan nomor kolom dan nama kolom, melainkan menambahkan informasi dan kolom baru di **akhir kolom**. Sehingga jika automasi atau skrip Anda menggunakan nomor indeks atau nama kolom tidak akan terganggu.
* Selain itu, kami tetap menyarankan untuk **menggunakan nama kolom**, bukan posisi/urutan/nomor kolom sebagai pengenal agar tabel laporan Anda tidak mengalami crash. Karena kolom laporan dapat diperbarui dari waktu ke waktu sesuai kebutuhan bisnis yang terus berkembang.

**Hal yang Perlu Anda Lakukan**

* Tinjau dan perbarui automation logic Anda jika masih bergantung pada nomor kolom.
* Tidak perlu ada perubahan jika sistem Anda sudah menggunakan nama kolom.