---
updatedAt: 2025-11-11T00:16:23.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Why one-time-password (3D secure) page can't be open from my mobile application ?

Did you encounter problem like below picture ?

![](https://files.readme.io/0718709-image.png)

It happen because you are using web view on your application, and there is possibility that your application is preventing 3D secure redirect URL being opened. Please make sure you are using Midtrans' SDK (you can refer to our technical documentation here to find the SDK).

If you can't use Midtrans' SDK for your application, Midtrans can help to give you some steps to investigate the problem :

Please try pressing the  **"Tap to Continue"** button, it should be work,\
Please make sure Javascript is active for the web view,\
Please make sure your application allow opening (white list) website domain / URL for each bank one-time-password (3D secure) pages, which might means white list every website  domain / URL using `*`