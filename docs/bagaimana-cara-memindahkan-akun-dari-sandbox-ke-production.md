---
updatedAt: 2025-11-11T00:18:35.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Bagaimana cara memindahkan akun dari Sandbox ke Production?

Sebelum memindahkan akun ke *Production*, Anda perlu menyelesaikan proses *[onboarding ↗](https://passport.midtrans.com/)* untuk mengajukan aplikasi legal dokumen, memastikan bahwa aplikasi Anda diterima, dan memiliki kredensial *Production* (*Merchant ID* atau *Merchant Key*). Pastikan bahwa Anda sudah melakukan integrasi seperti yang terdapat di dalam [langkah-langkah berikut ↗](https://docs.midtrans.com/).

Setelah selesai, berikut adalah beberapa langkah tambahan untuk memindahkan akun Anda:

* Pada *Merchant Administration Portal* Anda, pastikan bahwa fields pada menu [Pengaturan Umum ↗](https://dashboard.midtrans.com/settings/general_info) sudah terisi semua;
* Konsultasi dengan tim *developer* Anda untuk memastikan bahwa menu [Konfigurasi ↗](https://dashboard.midtrans.com/settings/vtweb_configuration) terisi semua, dan saat melakukan testing pada *Payment Notification URL* sudah mengirimkan kode status '200';
* Lakukan pergantian pada mode menjadi '*Production*';
* Anda akan menemukan *Access Keys* yang berbeda dengan sebelumnya. Ganti konfigurasi di sistem Anda menjadi [*Access Keys Production ↗*](https://dashboard.midtrans.com/settings/config_info) (sangat penting untuk menghindari [*error* ini ↗](https://docs.midtrans.com/docs/apa-arti-dari-error-401-dengan-pesan-access-denied-due-to-unauthorized-transaction-please-check-client-key-or-server-key));
* Lakukan transaksi *testing* dengan pembayaran sebenarnya dengan harga Rp. 10,000.

Jika transaksi *testing* sudah berhasil, Anda siap untuk *live* dan menerima transaksi melalui Midtrans.