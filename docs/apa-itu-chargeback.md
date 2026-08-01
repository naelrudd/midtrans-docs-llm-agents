---
updatedAt: 2025-11-11T00:21:35.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Apa itu Chargeback?

Chargeback merupakan permintaan pengembalian sejumlah dana pemilik kartu kredit (*cardholder*) yang dilakukan melalui bank kepada merchant atas nominal transaksi yang telah ditagihkan sebelumnya untuk dikembalikan ke cardholder. Bank akan meneruskan permintaan *chargeback* ke merchant via *Payment Gateway* dan meminta bukti-bukti pendukung, sebelum melakukan pendebetan apabila bukti dinilai tidak mencukupi.

Chargeback biasanya dilakukan oleh cardholder karena berbagai alasan, seperti *cardholder* tidak merasa melakukan transaksi tersebut karena alasan fraud, tidak menerima barang/jasa, barang/jasa yang diterima tidak sesuai dengan deskripsi, customer ingin mengajukan refund, dan sebagainya.

Proses chargeback dimulai dengan pengajuan sanggahan oleh cardholder kepada pihak bank atas transaksi yang mengalami perselisihan (*dispute*).

Setelah bank menerima permintaan *chargeback*, sanggahan akan diteruskan oleh bank penerbit kartu ke bank acquiring merchant, untuk diinformasikan ke merchant melalui Midtrans sebagai *payment gateway* atau langsung ke merchant.

Bank kemudian akan meminta dokumen pendukung dan bukti terkait transaksi ke merchant untuk menjawab permintaan *chargeback customer*, seperti:

1. *Invoice* transaksi.
2. Resi pengiriman, jika ada.
3. Detail customer, jika ada.
4. *Transcript* komunikasi dengan pihak penyanggah/customer apabila ada

Dokumen pendukung tersebut harus dikirimkan oleh merchant sebelum batas waktu yang ditentukan oleh bank, biasanya bank akan memberkan batas waktu 7 hari kalender. Acquiring bank akan memproses dokumen pendukung ini untuk menyanggah balik permintaan *chargeback* dari pemegang kartu.

Perlu diperhatikan bahwa bank memiliki batas maksimal chargeback yang dapat diterima oleh setiap merchant, sehingga walaupun merchant sudah menggunakan 3DS, merchant tetap memiliki kewajiban untuk menjaga jumlah *chargeback* yang terjadi di merchant. Midtrans menyediakan [sistem deteksi anomali ↗](https://midtrans.com/id/features/fraud-detection) yang sudah termasuk dari bagian *service* layanan pembayaran kami untuk membantu merchant mengurangi potensi *chargeback* di bisnis merchant.