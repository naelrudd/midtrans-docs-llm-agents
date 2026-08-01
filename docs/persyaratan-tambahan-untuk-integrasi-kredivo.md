---
updatedAt: 2025-11-11T00:19:16.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Persyaratan Tambahan untuk Integrasi Kredivo

Kredivo mensyaratkan ***item\_details*** ([klik di sini ↗](https://docs.midtrans.com/reference/json-objects#item-details-object)) dan ***customer\_details*** ([klik di sini ↗](https://docs.midtrans.com/reference/json-objects#customer-details-object)) selain ***payment\_type*** dan ***transaction\_details*** untuk dikirimkan oleh merchant sebagai **PARAMETER WAJIB**.

Untuk memastikan merchant memenuhi persyaratan dari Kredivo, semua merchant perlu melakukan **pengujian transaksi** dengan tim Kredivo sebelum menerima transaksi Kredivo yang sesungguhnya (real transactions) dari customer. Kredivo akan mengecek kelengkapan parameter selama proses pengujian berlangsung.