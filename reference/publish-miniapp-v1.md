---
updatedAt: 2026-03-16T07:33:35.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Publish MiniApp V1

This guide explains how to bind your project to the GoPay MiniApp Portal and build, upload, and publish your MiniApp version using VS Code or the MiniApp Portal.

**Quick Start**: Follow the **bold actions** to publish your MiniApp version. You can do this automatically in VS Code or manually in the portal. The manual steps are optional, skip them if you’ve already released via VS Code.

# 1. Bind your Project to GoPay MiniApp Portal

1. In VS Code, open the GoPay plugin sidebar and select the “**Login**” button.

   * Make sure you change the host and add your username and password in the [settings screen](https://docs.midtrans.com/reference/project-setup-v1/#3-project-initial-setup)

   <Image border={false} src="https://files.readme.io/62216e49a38f21362e682815eeba77e064d90681d097f026541c55827b27a3c7-image.png" />

   * If the binding is successful, a confirmation message will appear and click "**OK**".

     <Image border={false} src="https://files.readme.io/88943fc96d964d3d76fd70ea48306f0e72e4a733062ef8b2ed1ccc56a8a699f7-image.png" />
2. Click “**Select Space & Bind Miniapp**” to select the GoPay application you want to link to your MiniApp project.

   <Image align="center" border={false} src="https://files.readme.io/53134a827ffc06c85abf7bbd4df8a85d8a603a62771447446f466308f8d45cfd-Screenshot_2025-07-14_at_09.25.43.png" />

   * If your MiniApp is already bound, you’ll be prompted to rebind.

     <Image border={false} src="https://files.readme.io/3d765f33499c491b4d089f27c563db0d5b18203696ae93b4ae9a51364e070ed5-image.png" />
   * Select Yes to choose a different app, or No to keep the current one.

<br />

# 2. Build and Publish your MiniApp

There are two ways to build and upload a version:

* **Publish via VSCode (Automatically)**\
  We're recommending to follow this to simplify the process steps

  1. In VS Code, click “**Publish MiniApp**”\
     The extension fetches the latest version, updates it in package.json, and prepares it for release.\
     It then runs npm run build, compresses the build output, and uploads it automatically.

     <Image align="center" border={false} src="https://files.readme.io/b2c36901905de298d67190f96291e64d616a9e53a2ae8c8506c97a6fec0041e9-Screenshot_2025-07-14_at_09.42.07.png" />
  2. Click the **latest version**.

     <Image border={false} src="https://files.readme.io/21b27054fa30b3466729386cab5d3f74225bef0908095fed779a9503a9d8cee8-image.png" />
  3. Click "**Release**".

     <Image border={false} src="https://files.readme.io/ea8a17549c0c4d86adc50201d2232f17f7c800122c823a7020a292cdeab32bb3-image.png" />
  4. Choose the **target app** for release and click "**OK**"

     <Image align="center" border={false} src="https://files.readme.io/4c1b0702864d429488bca342294671915872c5481cad3be8b241003768886015-image.png" />
  5. Optionally, click Show Temporary Code to generate a QR code for testing your MiniApp.\
     Note: This **QR will not work**, to test your miniapp please refer [here](https://docs.midtrans.com/reference/testing-miniapp-v1)

     <Image border={false} src="https://files.readme.io/4a60b56ee8430fefae0e935b030473a8fee86cc1ac5e4154aac7d9344c57fd7d-image.png" />
  6. If the publish is successful, a confirmation message will appear

     <Image border={false} src="https://files.readme.io/ac60db11b511e48eaa6cfd4282dd5f9e78d5f585b1dacb8fb23681c0b6765551-image.png" />
* **Publish via GoPay MiniApp Portal (Manual)**\
  If you’ve already published the MiniApp in VS Code, you may **skip these steps**

  1. Login to the GoPay MiniApp Portal, select your MiniApp, go to the Versions tab, and click "Add Version" and select "Upload by Files"

     <Image border={false} src="https://files.readme.io/f04480621c9106f78d17b3fc7114e21098608d725b9db5b13f2ef7eaf84321b0-img_v3_02q7_1701f17e-fb2a-4db2-a424-bf89ee1ee7hu.png" />
  2. Upload your app package (ZIP) and click "OK"

     <Image align="center" border={false} src="https://files.readme.io/2aeb75273786a9db5066bfad437f960c2b4637fac60cab906770b7c465770090-p539769.png" />

<br />