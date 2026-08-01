---
updatedAt: 2025-11-11T00:21:38.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Mengapa transaksi kartu kredit pelanggan saya tidak berhasil?

Anda dapat melihat alasan penolakan transaksi di *dashboard* dengan cara:

1. Buka *Merchant* Administration Portal (MAP).
2. Cari transaksi yang ditolak.
3. Klik *OrderID* nya untuk masuk ke halaman detail transaksi.
4. Klik Tombol **"*See Why*"** di notifikasi pada detail transaksi tersebut.

   ![](https://files.readme.io/3e35272-image.png)

Penolakan transaksi dapat terjadi karena alasan berikut:

1. **Transaksi ditolak oleh Bank**\
   Transaksi ditolak oleh Bank terjadi karena bank penerbit tidak menyetujui transaksi tersebut.\
   Kami menyarankan pemegang kartu menghubungi bank penerbit untuk dapat melakukan klarifikasi terhadap alasan penolakannya.\
   Note : Kami sarankan agar customer menanyakan ke banknya alasan transaksinya ditolak, bukan apakah kartu customer bermasalah atau tidak agar pihak bank dapat melakukan pengecekan dengan tepat.

2. **Transaksi ditolak oleh Fraud Detection System (FDS)**\
   Transaksi ditolak oleh *FDS* berarti transaksi menunjukkan pola parameter yang tidak wajar sehingga transaksi tersebut ditolak demi keamanan transaksi Anda.\
   Jika transaksi tersebut dilakukan oleh pelanggan valid dan sudah diverifikasikan oleh pihak merchant, kami dapat memasukkan email ke daftar [whitelist ↗](https://docs.midtrans.com/docs/transaksi-customer-saya-gagal-dengan-alasan-blacklist-apa-yang-dimaksud-dengan-blacklist) untuk mencegah penolakan lebih lanjut oleh *Fraud Detection System* kami. Namun, kami menyarankan agar permintaan *whitelist* hanya diberikan kepada pelanggan terverifikasi untuk mencegah munculnya dispute di masa mendatang dari pemegang kartu yang sah.

3. **Transaksi dilakukan oleh blacklisted customer.**\
   Customer masuk kedalam daftar *blacklisted user* oleh Midtrans dikarenakan beberapa alasan, seperti laporan penipuan dari Prinsipal atau bank.