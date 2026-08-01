---
updatedAt: 2025-11-11T00:22:02.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Mengapa saya tidak menerima notifikasi HTTP dari sistem Midtrans?

Terdapat beberapa alasan mengapa merchant tidak dapat menerima HTTP notifikasi dari Midtrans; beberapa di antaranya adalah masalah *network*, atau *endpoint URL* yang tidak dapat menerima notifikasi. Jika Anda melakukan *whitelist* untuk *incoming message*, silakan *whitelist* blok IP berikut:

***Production Environment:***

**103.208.23.0/24\
103.208.23.6/32\
103.127.16.0/23\
103.127.17.6/32**

***Sandbox Environment:***

**103.58.103.177**

Untuk detil lebih lengkap silahkan [klik disini ↗](https://docs.midtrans.com/en/technical-reference/ip-address).