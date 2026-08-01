---
updatedAt: 2025-11-11T00:19:48.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Kode Respon Bank

## Ditolak oleh Bank - Kode Respon

Ketika data pembayaran untuk Kartu Kredit diterima, ada beberapa lapisan keamanan yang harus dilalui. Keamanan akhir yang harus dilalui adalah sistem otorisasi otomatis bank. Sistem otorisasi ini memperhitungkan berbagai faktor seperti perilaku konsumen dalam berbelanja, saldo rekening pelanggan, limit kartu yang digunakan, dll. 

Jika ada kasus dimana transaksi pelanggan Anda ditolak oleh bank, Midtrans akan memberikan informasi sesuai dengan apa yang Midtrans terima dari bank, **melalui notifikasi*HTTP* pada portal Midtrans (Merchant Administration Portal)**. Informasi akan diberikan dalam bentuk kode melalui API, sedangkan informasi lebih sederhana akan diberikan melalui portal Midtrans dalam bentuk yang lebih mudah dimengerti.

Dalam beberapa kasus, bank dapat memberikan penjelasan yang cukup informatif seperti "dana / limit tidak mencukupi", “nomor kartu tidak valid”, “kartu kedaluwarsa”, sayangnya beberapa penjelasan lain seperti “*do not honour*” bersifat terlalu umum dimana sangat kecil kemungkinannya untuk bisa mengetahui alasan pasti penolakan yang terjadi. Anda bisa melihat lebih rinci pengertian dari "*do not honour*" [di sini ↗](https://docs.midtrans.com/docs/apa-arti-do-not-honour-05).

Setelah berhasil masuk ke portal Midtrans, silahkan buka menu "transaksi" dan klik transaksi yang dimaksud, dan akan melihat halaman seperti dibawah ini. Klik ikon "i" untuk melihat informasi “*Invalid Card Number* (14)”.

![](https://files.readme.io/b0b3e27-image.png)

Berikut adalah contoh bagaimana respon API dikirimkan oleh Midtrans. Silahkan mengacu ke bagian “***status\_message***” seperti yang terlihat pada gambar dibawah ini.

```
{  
 "transaction_time": "2019-09-09 05:07:19",  
 "transaction_status": "deny",  
 "transaction_id": "bf9k2ba0-7hb9-88ah-o778-b1124376b3bd",  
 "status_message": "midtrans payment notification",  
 "status_code": "202",  
 "signature_key": "uu819dnk8jk880qerwlkai909018371jjhdo0129ddj89hj119fhk09134hj777jk36hy7ji89017fh77nvb123h3ef81uh73e40i8u3vhs8h1327hhhdfer89nccs9o",  
 "promo_details": {  
 "original_amount": "500007.00",  
 "code": "TEST_PROMO_UNLIMITED"  
 },  
 "payment_type": "credit_card",  
 "order_id": "ABC-889",  
 "metadata": {  
 "merchant_phone_number": "08129228011",  
 "merchant_partner_name": "ID_144",  
 "merchant_emails": [  
 "outdoor@mail.com",  
 "other@mail.com"  
 ],  
 "merchant_address": "Jl Jend Sudirman Kav 10-11 Jakarta Pusat 10220, DKI Jakarta, indonesia"  
 },  
 "masked_card": "459920-2414",  
 "gross_amount": "17000.00",  
 "fraud_status": "accept",  
 "eci": "01",  
 "custom_field3": "custom field 3 content",  
 "custom_field2": "custom field 2 content",  
 "custom_field1": "custom field 1 content",  
 "currency": "IDR",  
 "channel_response_message": "Do not honour",  
 "channel_response_code": "05",  
 "card_type": "credit",  
 "bank": "mandiri",  
 "approval_code": " "  
}
```

Dalam contoh ini, Anda dapat melihat bahwa transaksi ditolak dengan kode bank 05.\
Anda dapat mengacu ke daftar kode bank melalui link [berikut ](https://api-docs.midtrans.com/#channel-response-code.)↗ untuk mengetahui lebih rinci terkait informasi setiap kode yang ada.