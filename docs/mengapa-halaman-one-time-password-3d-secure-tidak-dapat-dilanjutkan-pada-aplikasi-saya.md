---
updatedAt: 2025-11-11T00:21:57.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Mengapa halaman one time password (3D secure) tidak dapat dilanjutkan pada aplikasi Saya ?

Apakah masalah yang Anda temukan seperti gambar di bawah ini ?

![](https://files.readme.io/3e3b53a-image.png)

Hal ini terjadi dikarenakan Anda menggunakan tampilan web (*web view*) pada aplikasi Anda, dan ada kemungkinan aplikasi Anda mencegah untuk *URL* halaman *one time password* (*3D secure*) dibuka. Silahkan pastikan Anda menggunakan SDK Midtrans (Anda dapat merngacu ke dokumentasi teknis kami [di sini ↗](http://mobile-docs.midtrans.com/#getting-started) untuk mendapatkan SDK tersebut).

Jika Anda tidak dapat menggunakan SDK Midtrans pada aplikasi Anda, Midtrans dapat membantu memberi Anda beberapa langkah untuk melakukan investigasi terhadap masalah tersebut :

1. Silakan coba menekan tombol  **"*Tap to Continue*"**, seharusnya ini bisa menyelesaikan masalah yang ada
2. Pastikan Javascript aktif untuk tampilan web (web view)
3. Pastikan aplikasi Anda mengizinkan pembukaan domain / *URL website* (*white list*) untuk setiap halaman *one time password* (*3D secure*) bank, yang mungkin berarti Anda perlu melakukan *white list* pada setiap *domain* / *URL website* menggunakan `*`