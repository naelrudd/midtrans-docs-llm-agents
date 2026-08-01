---
updatedAt: 2026-03-16T07:31:24.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Migration Guides

This guide explains the step-by-step instructions for migrating miniapp to a JSAPI new version or container.

# Introduction

There is [two types of container](https://docs.midtrans.com/update/reference/which-container-i-should-choose) available which is being used to integrate to GoPay as a MiniApp

1. **GoPay Container V2** (formerly known as WebKit Container) is a WebKit-based runtime environment where MiniApps are hosted externally by merchants and loaded into the GoPay app through a configured entrypoint URL.
2. **GoPay Container V1** (formerly known as GoPay Container SDK) is a bundled WebView-based environment where MiniApps are uploaded, versioned, and released through the MiniApp Portal.

<br />

# Migration Paths

* **Webview (Deprecated) → GoPay Container V2**
* **GoPay Container V1 → GoPay Container V2**
* **GoPay Container V2 → GoPay Container V1**

<br />

Note: Before planning for migration please check the list of existing frontend sdk and make sure it's available since not all handler are presents.

* [Webview (Deprecated) → GoPay Container V2](https://docs.midtrans.com/reference/migration-guides#webview-to-gopay-container-v2-adjustments)
* [GoPay Container V2 Frontend SDK](https://docs.midtrans.com/reference/frontend-v2)
* [GoPay Container V1 Frontend SDK](https://docs.midtrans.com/reference/frontend-v1)

<br />

***

# Quick Start

1. **Complete the <Anchor label="Mini App Onboarding Submission" target="_blank" href="https://gotocompany.sg.larksuite.com/share/base/form/shrlgnBkuAhMEnphzmFxhlDFUtU">Mini App Onboarding Submission</Anchor> and select Migration to Another Platform to begin.**
   1. Webview (Deprecated) → GoPay Container V2
   2. GoPay Container V1 → GoPay Container V2
   3. GoPay Container V2 → GoPay Container V1\
      Prerequisite: [Onboard to GoPay MiniApp Portal](https://docs.midtrans.com/reference/project-setup-v1/#1-access-to-gopay-mini-app-portal) to [Create New MiniApp Project ](https://docs.midtrans.com/reference/project-setup-v1/#2-create-new-miniapp-project) and input your Miniapp ID
2. **If the MiniApp is Live**, GoPay team will temporarily remove the MiniApp.
3. Tech support will inform the merchants regarding the migration completion and the updated deeplink
4. Merchants to do adjustments using the updated deeplink
   1. [Webview (Deprecated) → GoPay Container V2](https://docs.midtrans.com/reference/migration-guides#webview-to-gopay-container-v2-adjustments)
   2. [GoPay Container V1 → GoPay Container V2](https://docs.midtrans.com/reference/migration-guides/#gopay-container-v1-to-gopay-container-v2-adjustments)
   3. [GoPay Container V2 → GoPay Container V1](https://docs.midtrans.com/reference/migration-guides/#gopay-container-v2-to-gopay-container-v1-adjustments)
5. **If the MiniApp is Live**, QA to validate once development are completed and our rollout team will update the deeplink and rollout back the MiniApp

<br />

***

# Webview to GoPay Container V2 adjustments

1. Update FE JSBridge from `npm` to `script`
2. Adjust the handler request and response to use the updated [GoPay Container V2 Frontend SDK](https://docs.midtrans.com/reference/frontend-v2)
   1. Update response from snake\_case to camelCase
3. For more information please check the [V2 getting started page](https://docs.midtrans.com/reference/miniapp-v2)

***

# GoPay Container V1 to GoPay Container V2 adjustments

1. Remove the extension and use SDK Script
2. Adjust the handler request and response to use the updated [GoPay Container V2 Frontend SDK](https://docs.midtrans.com/reference/frontend-v2)
3. For more information please check the [V2 getting started page](https://docs.midtrans.com/reference/miniapp-v2)

***

# GoPay Container V2 to GoPay Container V1 adjustments

1. Remove the SDK Script and use extension
2. Adjust the handler request and response to use the updated [GoPay Container V1 Frontend SDK](https://docs.midtrans.com/reference/frontend-v1)
3. Additional setup:
   1. [Project Initial Setup](https://docs.midtrans.com/reference/project-setup-v1/#3-project-initial-setup)
   2. [Publish your MiniApp](https://docs.midtrans.com/reference/publish-miniapp-v1)
   3. [How to Test MiniApp](https://docs.midtrans.com/reference/testing-miniapp-v1)
4. For more information please check the [V1 getting started page](https://docs.midtrans.com/reference/miniapp-v1)