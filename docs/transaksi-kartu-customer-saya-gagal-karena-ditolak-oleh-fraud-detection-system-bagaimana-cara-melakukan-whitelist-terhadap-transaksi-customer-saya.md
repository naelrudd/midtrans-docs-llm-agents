---
updatedAt: 2025-11-11T00:21:36.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Transaksi kartu customer saya gagal karena ditolak oleh Fraud Detection System, bagaimana cara melakukan whitelist terhadap transaksi customer saya?

Memasukkan *customer* ke daftar *whitelist* adalah proses memberikan pengecualian kepada *customer* di *Fraud Detection System (FDS)* Midtrans untuk melonggarkan *filtering FDS* pada transaksi *customer* tersebut kedepannya. *Merchant* dapat menginformasikan email *customer* yang ingin di*whitelist* yang digunakan untuk bertransaksi di merchant ke kami - setelah whitelist dilakukan, *FDS* akan melonggarkan *filtering fraud* ke *customer* tersebut selama *customer* bertransaksi menggunakan email tersebut di bisnis *merchant*.

Kami mewajibkan *merchant* untuk melakukan *verifikasi customer* terlebih dahulu dan memastikan bahwa customer adalah *customer valid* sebelum melakukan *request whitelist*. Hal tersebut dilakukan untuk mengurangi kemungkinan *dispute* dari pemegang kartu di kemudian hari. Kesalahan *request whitelist* dapat menyebabkan kerugian di merchant yang diakibatkan oleh *chargeback* atas transaksi *fraud* yang dilakukan oleh customer tersebut.

Verifikasi yang pada umumnya dapat dilakukan oleh *merchant* terhadap *customer* adalah verifikasi kepemilikan kartu dengan meminta foto / scan KTP / paspor beserta foto / scan kartu yang digunakan untuk bertransaksi dengan menutupi sebagian nomor kartu. Hasil verifikasi tersebut dapat disimpan oleh merchant sebagai bukti kepada bank jika terjadi dispute atas transaksi customer.

Permintaan whitelist dapat dikirimkan ke email kami di <operations.fraud@midtrans.com>.

> 🚧 Catatan
>
> Whitelist hanya dapat dilakukan pada transaksi kartu dan tidak berlaku untuk metode pembayaran lainnya.