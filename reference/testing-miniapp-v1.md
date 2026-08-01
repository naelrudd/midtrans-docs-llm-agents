---
updatedAt: 2026-03-16T07:33:41.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Testing MiniApp V1

This guide explains how to preview, test, and debug your MiniApp using GoPay, Visual Studio Code, and Android or iOS simulators, including the supported capabilities and limitations of each method.

There are four ways to Preview and Test your MiniApp:

* [In GoPay](https://docs.midtrans.com/reference/testing-miniapp-v1/#test-in-gopay)
  No limitation, you need to publish and release miniapp first. This will not appear in GoPay page until it's officially release so you may safely test this.
* [In Visual Studio Code](https://docs.midtrans.com/reference/testing-miniapp-v1/#visual-studio-code)\
  Limitation: does not support certain SDKs (e.g., motion).
* [In Android Simulator](https://docs.midtrans.com/reference/testing-miniapp-v1/#android-simulator)
  Limitation: does not support GoPay JSAPIs (getAuthCode, launchDeeplink, launchUri, and launchPayment)
* [In IOS Simulator](https://docs.midtrans.com/reference/testing-miniapp-v1/#ios-simulator)
  Limitation: does not support GoPay JSAPIs (getAuthCode, launchDeeplink, launchUri, and launchPayment)

Note: If you see errors while testing in a browser, it’s because the APIs are only supported within the GoPay app and are not available in browsers.

<br />

# Test in GoPay

1. Login to GoPay MiniApp Portal, Click your MiniApp, Open the Versions tab, and click "**Release**"

   <Image align="center" src="https://files.readme.io/a091b3331e0393ff089f14020d0319771680c72ec568dfb7be9e710a95926029-img_v3_02q7_3990ee0f-96fc-4e6b-9096-6199bc4d77hu.png" />
2. In the Release tab, Click the **QR Code for testing** button, a QR code will appear.

   ![](https://files.readme.io/c6d3165edd9a1b0e243828ff81a0810de4ad3330e7167340db9aba22476f5cf0-image.png)

   <br />
3. Scan the QR code and note the **redirect URL**. (**QR will not work**)
4. Use the noted values to generate the deeplink using the template below:\
   `gopay://mini-app/windvane?app_id=<appId>&publish_id=<publishId>`

**Common mistakes**:

* Scanning the QR code only opens a page with extra information.
* Ignore that page: instead, copy the URL link directly.
* The useful values are in the URL. Copy appid and publishid to construct the deeplink.

<br />

| Deeplink Params | Mandatory | Description                                                                                                                 | Where this is being used                                                                           |
| :-------------- | :-------- | :-------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------- |
| app\_id         | M         | This is your **miniappid**, you may get this from the portal                                                                | To open your latest miniapp version                                                                |
| publish\_id     | O         | This is your **unreleased version id**, you can get this when you try to publish the miniapp and get from the QR code note. | To open your unreleased version of your miniapp (you need to include both app\_id and publish\_id) |
| mini\_app\_path | O         | This is to specify your subpath of your miniapp where you want the user to land on, you can get this when.                  | To redirect to a specific page inside your miniapp (the value of path has to be URL encoded)       |

<br />

# Visual Studio Code

1. **Open VS Code and Render application.**
2. **Click Preview Miniapp in the plugin sidebar.**

   ![](https://files.readme.io/abff84150909bdfade013e938f0f344213ec07bbdd04669230bdfd3b2fcbfdc4-image.png)

   * Yes: Manually input your MiniApp preview URL.
   * No: The plugin will run your start script and show the preview input afterward.
3. **Paste your MiniApp URL in the top input field.**.

   ![](https://files.readme.io/112ef2e25f59c2424faad7753ffd1ad1a1cf023af051cf6016420de29d8086ba-image.png)
4. **The preview will appear inside VS Code.**.

   <Image align="center" src="https://files.readme.io/9b7db703dd4ab2cef2247b049090288576e250673516b0616c317a2ce1be45aa-Screenshot_2025-07-14_at_09.30.34.png" />
5. **To debug, run Developer: Toggle Developer Tools from the command palette.**.

   <Image align="center" src="https://files.readme.io/d0d9acbc5cd700383325cb2d4bd777a489f8ee53475bf2653f2e7ec6c4442c2d-Screenshot_2025-07-14_at_09.38.37.png" />

## Android Simulator

1. **Click Preview Miniapp in Android Emulator.**.

   <Image align="center" src="https://files.readme.io/e1e33496233764ac81c181898708da140d0f146cd1bce073c5089a5cb252815f-Screenshot_2025-07-11_at_10.10.41.png" />
2. **Enter the preview URL in the field that appears.**.

   ![](https://files.readme.io/c8c581c094c68407d67344b9ee03d3f7dbb3c6df881cef31e8e53b2a458c6e35-image.png)
3. **Open Chrome → go to`chrome://inspect/#devices` → find the WebView and click Inspect.**.

   ![](https://files.readme.io/d0618f250e799b4a99b9d265c949e814d4dd7260e2a6e69f46ed9e07d25a966d-image.png)

   ![](https://files.readme.io/ba1003b5437c0e246026b881358ea31725c706359b8a93e578c71b990ce62720-image.png)

   <br />

## IOS Simulator

1. **In Safari: Enable Develop menu in Preferences > Advanced.**

   ![](https://files.readme.io/ac0a624ecb53b98f3bf4f07cc6477066be70fcacf6d44b7804796b9bf5be9e74-image.png)
2. **Click Preview Miniapp in iOS Emulator, then select a simulator.**

   <Image align="center" src="https://files.readme.io/e3f9c59636adca283c43d25b3072d199b818fea08a8aa470d232caca449deffd-Screenshot_2025-07-11_at_10.10.41.png" />

   ![](https://files.readme.io/eb512eea94d635f2aa582663095bd496ecc08b17001e4afee9dff9a37a17caad-image.png)

   <br />
3. **Enter the MiniApp preview URL.**

   <Image align="center" src="https://files.readme.io/9acd8e1f80d4320a6de2b75a3aa683bc2e45a8abdeecfe2ff69a4b7eed9bf12a-Screenshot_2025-07-14_at_09.40.54.png" />
4. **In Safari: Go to Develop > Simulator, then click the WebView to inspect it.**

   ![](https://files.readme.io/5d109b1b73b167387c5ce8962b337d28769af0604d7fb71e1b4a00939cca421f-image.png)
5. **Click the WebView object that you want to inspect, and then debug the miniapp in Web Inspector.**

   ![](https://files.readme.io/64c93a7a28014561ed74f562d2dfa411fdcea2f5e4294bd816f88500c6854365-image.png)