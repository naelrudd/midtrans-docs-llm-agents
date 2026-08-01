---
updatedAt: 2025-11-11T00:18:39.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Apakah ada batasan format untuk parameter email yang dikirim ke Midtrans?

Ya, Midtrans melakukan validasi untuk format email pelanggan pada metode pembayaran tertentu seperti Permata VA, CIMB Clicks, Telkomsel Cash, KlikBCA, Mandiri Ecash, dan Indomaret

Kami menggunakan *regex*untuk proses validasi ini. Harap fokus pada nilai yang dihasilkan dari* regex* ini, dengan merujuk ke penjelasan di bawah berikut:

```
interface Constants {
String ATOM = "[a-z0-9!#$%&'*+/=?^_`{|}~-]";
String DOMAIN = "(" + ATOM + "+(\\." + ATOM + "+)+";
String IP_DOMAIN = "\\[[0-9]{1,3}\\.[0-9]{1,3}\\.[0-9]{1,3}\\.[0-9]{1,3}\\]";

String PATTERN =
"^$|^" + ATOM + "+(\\." + ATOM + "+)*@"
+ DOMAIN
+ "|"
+ IP_DOMAIN
+ ")$";
}
```

**ATOM** adalah kombinasi alfanumerik.\
**DOMAIN** adalah kombinasi DOT (".") dan ATOM.\
**IP\_DOMAIN** adalah kombinasi DOT (".") dan angka dengan panjang maksimum adalah 3.

Contoh:\
*PATTERN* yang benar <midtrans@midtrans.com>\
*PATTERN* yang salah midtrans..@ midtrans.com