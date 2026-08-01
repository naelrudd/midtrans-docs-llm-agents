---
updatedAt: 2026-04-09T08:34:17.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# GoPay Container V2: Getting Started

This guide helps you get started with onboarding and integrating your MiniApp using GoPay Container V2.

# Introduction

Get a quick understanding of GoPay Container V2 MiniApp and related resources:

1. [MiniApp Overview](https://docs.midtrans.com/reference/overview-miniapp)
2. [Introduction to GoPay Container V2](https://docs.midtrans.com/reference/introduction-to-gopay-container-v2/#what-is-gopay-container-v2)
3. [MiniApp Security Guidelines](https://docs.midtrans.com/reference/miniapp-security-guidelines)
4. [Version History](https://docs.midtrans.com/reference/version-history)

***

# Quick Start

To start integrating your GoPay Mini App, follow the steps below.

1. **Complete the Mini App Onboarding Submission and select Create New MiniApp to begin.**\
   This form is the single entry point for all MiniApp requests, including Create, Update, Rollout, Migration, and Deactivation.
   1. The **submission form** will be provided by GoPay.
   2. [Onboard as Merchant](https://docs.midtrans.com/reference/onboarding-v2) and input MID
   3. Select "GoPay Container V2"
2. **Receive Integration Guide & Credentials**\
   After submission (\~5 working days), the GoPay team will provide these details via Email:

   1. 📘 MiniApp Integration Guide\
      A curated technical guide with **Miniapp deeplink**, **pointOfPurchaseId**, and direct links to required SDKs and APIs.
   2. 🔐 MiniApp AuthCredentials\
      Required for backend authentication using authToken

   👉 Follow the Integration Guide shared via email to continue development.
3. **Start Development**

   1. Build your MiniApp based on the Integration Guide.
      1. [How to Test MiniApp](https://docs.midtrans.com/reference/testing-miniapp-v2)
   2. Review the MiniApp <Anchor label="UI/UX Guidelines" target="_blank" href="https://docs.midtrans.com/reference/miniapp-uiux-guidelines">UI/UX Guidelines</Anchor> to ensure compliance before submitting for UAT
4. **Submit for UAT**

   1. Once you've completed development, submit MiniApp Completed using the same **onboarding form.**
   2. QA team conducts UAT and provides final sign-off
5. **Rollout & Go Live**

   1. After QA sign-off, the rollout team will deploy the MiniApp
   2. You will be notified once the MiniApp is live in GoPay

***

# Technical Specification

Detailed documentation for building your MiniApp, including core flows, frontend SDKs, and backend APIs.

* [MiniApp Core Flows](https://docs.midtrans.com/reference/coreflow-v2)
* [Frontend SDKs](https://docs.midtrans.com/reference/frontend-v2)
* [Backend APIs](https://docs.midtrans.com/reference/backend-v2)

***

# Technical Assistant and Support

For any technical queries or clarifications,

* Please contact the GoPay integration team via email: <Anchor label="GoPay-mini-app-integrations@gojek.com" target="_blank" href="mailto:GoPay-mini-app-integrations@gojek.com"><GoPay-mini-app-integrations@gojek.com></Anchor> or
* MiniApp Technical Support Team
  * @Janson
  * @Raihan

<br />

**Need help?**\
Refer to the FAQ for common questions:

* [Seamless Login and Payment FAQ](https://docs.midtrans.com/reference/miniapp-faq/#seamless-login-and-payment-faq)
* [Backend API FAQ](https://docs.midtrans.com/reference/miniapp-faq/#backend-api-faq)
* [V2 Integration FAQ](https://docs.midtrans.com/reference/miniapp-faq/#v2-integration-faq)
* [General FAQ](https://docs.midtrans.com/reference/miniapp-faq/#general-faq)

<br />