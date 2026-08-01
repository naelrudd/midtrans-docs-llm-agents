---
updatedAt: 2026-03-16T07:33:28.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Project Setup V1

This guide covers the initial steps required to access the portal, create your MiniApp project, and prepare your local setup.

# 1. Onboard to GoPay Mini App Portal

Please follow the steps below to gain access:

1. Complete the <Anchor label="GoPay Mini App Portal Submission" target="_blank" href="https://gotocompany.sg.larksuite.com/share/base/form/shrlglFV3Rigwk9X8b09VhPaEGb">GoPay Mini App Portal Submission</Anchor> to request login access.\
   Kindly check your email after 1-2 days.
2. Log in <Anchor label="Gopay Mini App Portal" target="_blank" href="https://miniapp.midtrans.com">Gopay Mini App Portal</Anchor> and fill out required details and submit.\
   Kindly check the portal again 1-2 days after approval from GoPay.

You may contact [support team](https://docs.midtrans.com/reference/miniapp-v1/#technical-assistant-and-support) if needed.

<br />

# 2. Create New MiniApp Project

1. **Log in to the <Anchor label="Gopay Mini App Portal" target="_blank" href="https://miniapp.midtrans.com">Gopay Mini App Portal</Anchor>.**
2. **Create a Miniapp**

   * If you don’t have one yet, go to the MiniApp page and click “Create Miniapp.”

     <Image border={false} src="https://files.readme.io/10fecca87fe7bf5decb6a55c04cf39deb5cd6d46d3420c26531f5b7fcb8f4006-image.png" />
   * Fill in the required info: name, type (only windvane), permissions, description, logo, contact info, etc. Click “**Create**” to finish

     <Image border={false} src="https://files.readme.io/b66ac1222f154a24e505a4ba1c235769d9f76bd0e6490afb1adda4726179dfbd-image.png" />
3. **If a MiniApp already exists, you can skip creation and proceed to edit or publish it.**

   <Image border={false} src="https://files.readme.io/deb2fee9135a502ab50dc1ee5f90bad6a49386884e4bb76979d78a27abc24103-image.png" />
4. Took note of the **Miniapp ID**

   <Image border={false} src="https://files.readme.io/c9150990a9dbeb58a5bb12ae253bf7915362b6640568125b6b0f706f957a567e-image.png" />
5. Continue to <Anchor label="submit form" target="_blank" href="https://gotocompany.sg.larksuite.com/share/base/form/shrlgnBkuAhMEnphzmFxhlDFUtU">submit form</Anchor> and select "Create new MiniApp" and input Miniapp ID as mentioned in [quick start section](https://docs.midtrans.com/reference/miniapp-v1)

<br />

# 3. Project Initial Setup

## Install the Visual Studio Code Extension

1. **Install the GoPay Mini App Plugin in VS Code**

   * Download Gopay VS Code Extension from [here](https://superapp-sg-public-new.oss-ap-southeast-1.aliyuncs.com/plugins/vscode/gopay-mini-app-plugin-0.0.7.vsix)
   * Open VS Code.
   * Click the Extensions icon in the sidebar and click (...) symbol.
   * Install from ViX using the downloaded build.

     <Image border={false} src="https://files.readme.io/2579c8448f69a74a02d9f146156aceca714ed1af2970f562f395e887097a38ee-image.png" />
   * Search for “gopay miniapp”.
   * Find the installed plugin named Gopay Miniapp Develop Tool by searching in the extension search bar.
   * If your VS Code supports auto-updates, enable Auto Update after installing

     <Image border={false} src="https://files.readme.io/a055aa085ba910506b29b57db541d3414de6adbea0b1f86993ecf8f5f8c1f121-image.png" />
2. **Open plugin settings**

   * Once installed, click the plugin’s sidebar icon (it appears under the VS Code icon bar).

     <Image border={false} src="https://files.readme.io/8811e7212756c21cdb2a6ec55d44179a78a0baec09ebf1b3c5d5b04f08f9c5dd-image.png" />
   * In the Gopay Miniapp Develop Tool panel, select Extension Settings

     <Image border={false} src="https://files.readme.io/ef16e75c5ca58c10f85bd5579442809de94635a99cce68ac89d569dd42478949-image.png" />
3. **Configure required settings**\
   Fill in these parameters in the settings:

   * Make sure you change these information as follows and restart the VSCode

     * Go Pay: Env to **\[[https://miniapp.midtrans.com](https://miniapp.stg.midtrans.com)]**
     * Go Pay: Username to **\[Portal username]**
     * Go Pay: Password to **\[Portal password]**
     * **Restart VSCode** to apply the changes

     <Image border={false} src="https://files.readme.io/1994acb01ff1dfd1fa2c70a16cefdeab58369007c9ab222d3e08daedeaf9ebf5-image.png" />

| Parameter           | Description                                                                                                                                                                                                                                            | Mandatory  |
| :------------------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------- |
| Build Path          | The directory where the build artifact is stored. Default value: dist.                                                                                                                                                                                 | M          |
| Env                 | The development environment = <https://miniapp.midtrans.com>                                                                                                                                                                                           | M          |
| Need Auth From App  | If enabled, invoking client capabilities within the mini-program will prompt for authorization; otherwise, no authorization prompt will be shown.                                                                                                      | O          |
| Password            | The account password used to log on to GoPay MiniApp Portal.                                                                                                                                                                                           | M          |
| Username            | The account username used to log on to GoPay MiniApp Portal.                                                                                                                                                                                           | M          |
| Npm                 | The storage path of npm commands.                                                                                                                                                                                                                      | M          |
| Start Command       | The command for starting the miniapp. Default value: npm start.                                                                                                                                                                                        | M          |
| Adb Linux           | The storage path of Android adb commands in the macOS system. Default value: \~/Library/Android/sdk/platform-tools.                                                                                                                                    | By Default |
| Adb Mac             | The storage path of Android adb commands in the macOS system. Default value: \~/Library/Android/sdk/platform-tools.                                                                                                                                    | By Default |
| Adb Windows         | The storage path of Android adb commands in the Windows system. Example: D:\sdk\platform-tools. If your computer runs Windows, you must specify this parameter. If you do not specify this parameter, the Android emulator cannot start as expected.   | By Default |
| Emulator Linux      | The storage path of Android emulator commands in the Linux system. Default value: \~/Library/Android/sdk/emulator.                                                                                                                                     | By Default |
| Emulator Mac        | The storage path of Android emulator commands in the macOS system. Default value: \~/Library/Android/sdk/emulator.                                                                                                                                     | By Default |
| Emulator Windows    | The storage path of Android emulator commands in the Windows system. Example: D:\sdk\emulator. If your computer runs Windows, you must specify this parameter. If you do not specify this parameter, the Android emulator cannot start as expected.    | By Default |
| Sdk Manager Linux   | The storage path of Android sdkmanager commands in the Linux system. Default value: \~/Library/Android/sdk/tools/bin.                                                                                                                                  | By Default |
| Sdk Manager Mac     | The storage path of Android sdkmanager commands in the macOS system. Default value: \~/Library/Android/sdk/tools/bin.                                                                                                                                  | By Default |
| Sdk Manager Windows | The storage path of Android sdkmanager commands in the Windows system. Example: D:\sdk\tools\bin. If your computer runs Windows, you must specify this parameter. If you do not specify this parameter, the Android emulator cannot start as expected. | By Default |
| Avd Manager Linux   | The storage path of Android avdmanager commands in the Linux system. Default value: \~/Library/Android/sdk/tools/bin.                                                                                                                                  | By Default |
| Avd Manager Mac     | The storage path of Android avdmanager commands in the macOS system. Default value: \~/Library/Android/sdk/tools/bin.                                                                                                                                  | By Default |
| Avd Manager Windows | The storage path of Android sdkmanager commands in the Windows system. Example: D:\sdk\tools\bin. If your computer runs Windows, you must specify this parameter. If you do not specify this parameter, an Android emulator cannot be created.         | By Default |

<br />

## Create project scaffold for MiniApp

1. **Prepare your environment**
   * Ensure Visual Studio Code and Node.js (latest) are installed.
2. **Initialize the scaffolding**

   * In VS Code, click the GoPay  icon in the sidebar and choose Create Miniapp.

     <Image border={false} src="https://files.readme.io/505dee2ab43ae12183210d275b9b5f9afd609591842558ef8bf85e28a7e6cd3c-image.png" />
   * Pick a template (React, Vue, Angular, or plain JS).

     <Image border={false} src="https://files.readme.io/51102cf6e24d56c87e7221efded25e4e80d06c681f545884b2959ccb843be728-image.png" />
   * In the dialog, name your miniapp and select the project folder, then click Create. This opens the new project in VS Code automatically

     <Image border={false} src="https://files.readme.io/174b20d957728113e872be95ec4e5b3adf7fdf4802ee71e5062935acde1710e3-image.png" />

     <br />
3. **Install dependencies**

   * Open the integrated terminal and run: `npm install`
   * <Image border={false} src="https://files.readme.io/91324e7e578d9feddbdcbdbefeadb8d387f4fb87370cbb7d5e194aab65c86822-image.png" />

     Your project file

     <Image border={false} src="https://files.readme.io/ffbd116a475cc391091171c9c1e7dc0f4dd77de71b4e5e45be0973a7a6d9abd2-image.png" />
4. **Explore project structure**\
   After `npm install`, your project will include:
   * public/ – static assets
   * scripts/ – build scripts
   * src/ – source code (assets/, components/, index.js)
   * package.json – project metadata & scripts
   * node\_modules/ – installed dependencies
   * dist/ – build output (after packaging)
5. **Integrate JavaScript APIs**

   * In .js or .ts files, type GP to trigger IntelliSense suggestions for GoPay Container SDK JS APIs(available on Visual Studio Code).

     <Image border={false} src="https://files.readme.io/133b1c777e6525bd6ce9412af5add217608bf96bd5800e5e766df32833fd4521-image.png" />
   * Select an API snippet to auto-insert usage code.

     <Image border={false} src="https://files.readme.io/c0166ec3edacf0df035cdbf6f324952831a2cdb3d34e67fd269f5967af57677a-image.png" />

<br />

<br />