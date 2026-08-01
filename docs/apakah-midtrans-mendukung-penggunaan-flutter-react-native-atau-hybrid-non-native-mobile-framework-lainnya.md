---
updatedAt: 2025-11-11T00:19:23.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Apakah Midtrans mendukung penggunaan Flutter, React Native atau hybrid / non-native mobile framework lainnya?

Midtrans belum secara resmi menyediakan SDK untuk *mobile hybrid framework*, karena saat ini fokus implementasi SDK dilakukan untuk membantu pengguna aplikasi Android dan iOS native. Anda dapat melihat detail informasi mengenai Midtrans Mobile SDK [di sini ↗](http://mobile-docs.midtrans.com/).

Percayalah, bahwa layanan pembayaran Midtrans sudah kompatibel untuk digunakan pada Flutter, React Native atau *hybrid / non-native mobile framework* lainnya.

Cara paling sederhana dan paling mudah yang dapat dilakukan adalah dengan menggunakan **webview** (seperti menampilkan halaman HTML), developer dapat menampilan halaman HTML (dengan webview) dari layanan [SNAP ↗ ](http://snap-docs.midtrans.com/)(HTML yang menggunakan snap.js). Sehingga *developer* dapat membuat halaman website yang terintegrasi dengan snap.js untuk menampilkan halaman pembayaran dan menggunakan *webview* di dalam aplikasi untuk menampilkan halaman pembayaran tersebut.

Cara lainnya, *developer* juga dapat menggunakan layanan [CORE API ↗](http://api-docs.midtrans.com/), yang merupakan API berbasis objek JSON, tentunya dapat diintegrasikan pada berbagai bentuk *framework/platform*.