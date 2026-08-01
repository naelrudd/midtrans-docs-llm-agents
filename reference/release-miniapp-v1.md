---
updatedAt: 2026-03-16T07:33:47.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Release MiniApp V1

This guide explains how to submit your MiniApp version for release, apply for approval, and officially launch it through the GoPay MiniApp Portal

**Quick Start**: Follow the **bold actions** to quickly release your MiniApp version. You can do this automatically in VS Code or manually in the portal. The manual steps are optional, skip them if you’ve already released via VS Code.

# 1. Submit your MiniApp for Release

There are two ways to release:

* **Release via VSCode**\
  If you've followed the previous steps and click "**release**" you may **skip this steps** or [click here for next steps](https://docs.midtrans.com/reference/release-miniapp-v1/#2-apply-for-release-your-miniapp)

  <Image border={false} src="https://files.readme.io/ea8a17549c0c4d86adc50201d2232f17f7c800122c823a7020a292cdeab32bb3-image.png" />
* **Release via GoPay MiniApp Portal**\
  Login to the GoPay MiniApp Portal,

  1. Select your MiniApp

     <Image align="center" border={false} src="https://files.readme.io/2562d7ca8b9ca9cd96916dcdd22a9cab2f8efa24b1d4c1276652a142b170353a-p541935.png" />
  2. Open the Versions tab, and click "Release

     <Image align="center" border={false} src="https://files.readme.io/a091b3331e0393ff089f14020d0319771680c72ec568dfb7be9e710a95926029-img_v3_02q7_3990ee0f-96fc-4e6b-9096-6199bc4d77hu.png" />
  3. Click "All No

     <Image border={false} src="https://files.readme.io/75069df60b5e5d99a08797166e4e9f58835ad46f91347e8087b8e2ac79182830-img_v3_02q7_cd67e13b-246e-469f-9e30-4c52efe0d0hu.png" />
  4. Choose the target app for release

     <Image border={false} src="https://files.readme.io/f4d04fe351e3800f62f56158ca4d4580d6b5fba5e6d69e48c30a80447a0b80ae-img_v3_02q7_1ba01828-add0-43bb-86ee-10517fdcc1hu.png" />
  5. The figure below shows the MiniApp in the Version Creation phase

     <Image border={false} src="https://files.readme.io/dee977defbc77240ffd542a4561f68dc9c4618eb7f151fd2134f37a1b504e147-img_v3_02q7_36a73e5d-eff3-4a75-ae58-6bc30ba63fhu.png" />

# 2. Apply for Release your MiniApp

**Prerequisite**: You can request a release only after **Submit your MiniApp for Release** is completed.

1. Login to the GoPay MiniApp Portal, select your MiniApp, go to the Versions tab, and click "**Detail**"

   <Image align="center" border={false} src="https://files.readme.io/a091b3331e0393ff089f14020d0319771680c72ec568dfb7be9e710a95926029-img_v3_02q7_3990ee0f-96fc-4e6b-9096-6199bc4d77hu.png" />
2. In Version Creation, please follow the steps below\
   Note: This **QR will not work**, to test your miniapp please refer [here](https://docs.midtrans.com/reference/preview-and-test-your-miniapp-internal-only)

   * Click "**Apply Release**"

     <Image border={false} src="https://files.readme.io/dee977defbc77240ffd542a4561f68dc9c4618eb7f151fd2134f37a1b504e147-img_v3_02q7_36a73e5d-eff3-4a75-ae58-6bc30ba63fhu.png" />
   * Review the Confirm Release Information and click "**OK**"

     <Image align="center" border={false} src="https://files.readme.io/1bc75aa961726bceb6561f76aa213dfb32058a231ea3be1a7589fc5899024547-p540469.png" />
   * Review the Submit for Release panel and click "**OK**"

     <Image align="center" border={false} src="https://files.readme.io/a195367fb38ac5cf32ff1558a442920030efecdd174b0c06cbb815abdd2425aa-p540472.png" />
3. In Submit for Review, wait for approval from the target app administrator. You may contact [support team](https://docs.midtrans.com/reference/miniapp-v1/#technical-assistant-and-support) if needed.

<br />

# 3. Officially Release your MiniApp

**Prerequisite**: You can release a version only after **Request Release of your MiniApp** is approved.

1. **Release for the first time**\
   For the first release, you may only do **official release**.

   1. In Pilot test, Click "**Officially Release**

      <Image align="center" border={false} src="https://files.readme.io/763fde11c4c7fbdc799f0d12e52160d3408e4133e81d56366e055656d9ed8f27-p609030.png" />
   2. In the pop-up, click "**OK**" to complete
2. **Release after the first time**\
   For Subsequent releases, you can do a whitelist test, a canary release, then official release (or go straight to official release).

* **(Optional) Whitelisting test**

  1. On the Release tab, click Setting Whitelist

     <Image align="center" border={false} src="https://files.readme.io/4238dd0d6fcef776354a04ccb0eb50dd1ba293db8dc794edb197a1e370a3ebd0-p609194.png" />
  2. Add user IDs

  <Image align="center" border={false} src="https://files.readme.io/2f8d73cdf1dda73e1291ad38561237b7f438dce07be12864dd248a970ed7ca10-p609195.png" />

  3. Click Start Testing
* **(Optional) Canary release**\
  After the canary release is started, the official release can be started when user feedback and actual business operation results meet expectations.

  1. On the Release tab, click Set Grayscale

     <Image align="center" border={false} src="https://files.readme.io/41c1c10bda4d217f1d4b746de82a573fe9b7e40d8dc662a39d9a249db25a63ee-p540608.png" />
  2. In set Grayscale, specify the canary release ratio

     <Image align="left" border={false} src="https://files.readme.io/c4ad8642dc037ccaf766fdce1cd88943fbd3e348e4018f960b8a777b3df45e9c-p540611.png" />
  3. Click Start Grayscale
* **Official Release**\
  After the canary release is started, the official release can be started when user feedback and actual business operation results meet expectations.\
  Note: Releasing a new version automatically archives the previous version.

  1. In Pilot test, Click "Officially Release"

     <Image align="center" border={false} src="https://files.readme.io/763fde11c4c7fbdc799f0d12e52160d3408e4133e81d56366e055656d9ed8f27-p609030.png" />
  2. In the pop-up, click "OK" to complete