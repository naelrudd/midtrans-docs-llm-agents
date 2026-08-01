---
updatedAt: 2025-11-11T00:19:24.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Bagaimana cara untuk menampilkan log dari SDK dengan menggunakan code ?

Ada metode yang harus di inisialisasi terlebih dahulu pada SDK Anda.\
Silahkan menggunakan potongan code berikut.

Berikut adalah tampilan dalam bentuk code :

```
...............................

SdkUIFlowBuilder.init(CONTEXT, BuildConfig.CLIENT_KEY, BuildConfig.BASE_URL, new TransactionFinishedCallback()  
{  
@Override  
public void onTransactionFinished(TransactionResult result) {  
// Handle finished transaction here.  
}  
})  
.enableLog(true)  
.buildSDK();

................................
```

> 🚧 Catatan:
>
> hal ini bisa dilakukan hanya jika Anda melakukan integrasi dengan Android.