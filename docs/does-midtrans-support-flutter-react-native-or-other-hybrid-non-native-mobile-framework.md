---
updatedAt: 2025-11-11T00:13:11.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Does Midtrans support Flutter, React Native, or other hybrid / non-native mobile framework?

Midtrans does not directly provide official SDK for a hybrid mobile framework, because currently we focus on supporting native Android & iOS experience via our Mobile SDK. You can check the details of our Mobile SDK information [here](http://mobile-docs.midtrans.com).

Rest assured, our payment products are compatible to be used on Flutter, React Native, or other hybrid mobile framework platforms.

The simplest and easiest method is to utilize **webview** (or similar method to display HTML page), the developer can display (via webview) the HTML page of [SNAP payment](http://snap-docs.midtrans.com) (HTML which utilizes snap.js). So the developer needs to set up a web page that integrated with snap.js to display payment and use webview within the app to display it as a payment page.

Alternatively, the developer can also utilize [Core API](http://api-docs.midtrans.com), which is JSON-based REST API, that should be able to be integrated on virtually any framework/platform.