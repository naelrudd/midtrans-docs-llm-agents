---
updatedAt: 2025-11-11T00:21:56.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Mengapa Saya mendapatkan pesan `javax.net.ssl.SSLHandshakeException: Menerima peringatan fatal: handshake_failure` ketika mencoba untuk terhubung ke API Midtrans?

Ini biasanya disebabkan oleh Java client yang sudah tidak update.\
Silakan pastikan kembali **versi Java, versi web framework**, dan **versi OS** yang digunakan dalam proses integrasi. Harap pastikan Anda tidak menggunakan versi lama, dan selalu memperbaharui dengan versi yang paling update.

Misalnya, jika yang Anda gunakan adalah Java versi 7, web framework Spring versi 3.1, dan OS windowa versi 7.\
Harap perbaharui versi Java Anda, karena versi 7 tidak lagi secara resmi didukung oleh Oracle (<https://java.com/en/download/faq/java_7.xml>). Selain itu, versi web framework dan OS yang digunakan juga bukan yang paling baru. Menggunakan *platform* lama dapat membuat sistem Anda rentan terhadap ancaman keamanan, dimana sangat tidak disarankan untuk digunakan dalam penanganan sistem pembayaran.