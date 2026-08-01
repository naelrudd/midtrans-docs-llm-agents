---
updatedAt: 2025-11-11T00:19:52.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Apa Midtrans dapat memproses transaksi yang menggunakan desimal?

Tidak. Standar fomat penulisan dalam Rupiah tidak memiliki desimal. Silakan lakukan pembulatan desimal menjadi ke atas atau ke bawah pada parameter *amount* sebelum mengirimkan request ke Midtrans. Sistem Midtrans akan melakukan validasi jika menemukan *amount* dengan desimal.