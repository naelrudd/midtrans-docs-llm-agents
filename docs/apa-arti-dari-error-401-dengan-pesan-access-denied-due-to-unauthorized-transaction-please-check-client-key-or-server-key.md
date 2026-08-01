---
updatedAt: 2025-11-11T00:22:01.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Apa arti dari error 401 dengan pesan “Access denied due to unauthorized transaction, please check client key or server key”?

Terdapat beberapa kemungkinan:

* Anda menggunakan credential dari Production untuk digunakan di Sandbox, atau sebaliknya;
* Server Key  **belum diubah**ke dalam format base64;
* Anda memiliki **karakter spasi** ( ) saat melakukan konversi.

Silahkan menghubungi kami di **[Contact Us ↗](https://midtrans.com/id/kontak-kami/technical-integration-development/i-get-error-code-401-when-doing-integration)** jika kendala tetap berlanjut atau Anda dapat menemukan informasi detail pada [link berikut ↗](https://docs.midtrans.com/en/technical-reference/api-header?id=authorization-header).