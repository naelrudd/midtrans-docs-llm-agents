---
updatedAt: 2025-11-11T00:22:09.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Mengapa pelanggan Saya tidak menerima notifikasi email dari sistem Midtrans?

Notifikasi email dari Midtrans biasanya gagal diterima dikarenakan beberapa faktor, yang paling sering terjadi dikarenakan adanya gangguan *network* dan/atau penuhnya inbox dari email terkait. Faktor tersebut bisa menjadi acuan, jika masalah ini terjadi pada satu atau beberapa dari pelanggan Anda. Tidak ada batasan terhadap domain email yang ada, untuk bisa **menerima** notifikasi email Midtrans.

Jika masalah ini terjadi merata pada semua pelanggan Anda, mohon pastikan Anda sudah mengaktifkan fitur **"*send email to customer*"** pada portal Midtrans yang dimiliki.\
Ada faktor lain yang memungkinkan masih terjadinya masalah ini, mohon pastikan email alias ("***email support***") yang dikonfigurasi pada portal Midtrans tidak menggunakan **domain yahoo**. Email support akan digunakan sebagai ***email sender*** pada notifikasi email yang dikirimkan ke pelanggan Anda, dan ada kebijakan DMARC dari pihak yahoo yang akan menolak email tersebut jika menggunakan domain mereka.

Informasi lebih detail silakan [klik disini ↗.](https://help.yahoo.com/kb/account?redirect=true)