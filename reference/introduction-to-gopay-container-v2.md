---
updatedAt: 2026-03-16T07:30:58.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Introduction to GoPay Container

This guide introduces GoPay Container, the runtime environment for MiniApps inside the GoPay app. It explains the differences between Container V1 and V2, their features, deployment models, and how they enable seamless login, payments, and native-like experiences for users.

# What is GoPay Container V2

GoPay Container V2 (formerly known as WebKit Container) is a WebKit-based runtime environment where MiniApps are hosted externally by merchants and loaded into the GoPay app through a configured entrypoint URL.

Instead of uploading bundled builds into a portal, merchants deploy updates directly on their own infrastructure. This enables faster iteration, simplified deployment workflows, and better alignment with modern web development practices.

Key characteristics:

* Merchant-hosted MiniApp
* Faster loading performance
* Smaller application size
* Growing set of JSAPIs
* Recommended for new MiniApp integrations

GoPay Container V2 represents the evolution of the MiniApp platform, providing a lightweight and flexible architecture while still maintaining secure communication with GoPay services. The container acts as a secure runtime layer inside the GoPay app, allowing MiniApps to integrate authentication, payments, deeplinking, and frontend JSAPIs without requiring packaged uploads.

This approach reduces operational overhead for merchants while improving scalability, deployment flexibility, and long-term maintainability.

## Key Features of the GoPay Container V2

Below are the features & capabilities you or your dev team can expect when using GoPay Container V2:

| Feature                           | What it does / why it matters                                                                                                                                      |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Hosted Web Entrypoint**         | MiniApps are hosted on your own public domain instead of uploading builds. This gives merchants full control over deployments, infrastructure, and release cycles. |
| **Seamless GoPay Login**          | Supports integrated GoPay authentication flows, allowing users to access MiniApps without separate login steps, improving conversion and reducing friction.        |
| **Integrated Payment Support**    | MiniApps can trigger GoPay payment flows securely through standardized APIs and container capabilities without building native payment UI.                         |
| **Frontend JSAPI Access**         | Provides access to native capabilities such as deeplinks, device interactions, and container communication through standardized frontend APIs.                     |
| **Cross-Platform Runtime**        | Runs consistently inside the GoPay app on both iOS and Android, allowing teams to build once using web technologies.                                               |
| **Faster Iteration & Deployment** | Since MiniApps are externally hosted, updates can be deployed instantly without uploading new builds through the portal.                                           |
| **Deeplink & Parameter Support**  | Supports MiniApp deeplinks with parameters, enabling content segmentation, campaigns, and dynamic user journeys.                                                   |
| **Improved Scalability**          | Public domain hosting allows merchants to scale infrastructure independently while still leveraging GoPay’s container ecosystem.                                   |
| **Standardized Security Model**   | Maintains secure communication between the MiniApp and GoPay through predefined authentication and container protocols.                                            |
| **Analytics Integration**         | Merchants can define and trigger events in their miniapps, while we automatically track default events for GoPay analytics insights.                               |

<br />

# What is GoPay Container V1

<Image align="center" border={false} src="https://files.readme.io/4ee0136ee1063164ee21c442f70d0b8291216f4a7d5d5e70c814c635f22e6a0d-ano.drawio.png" />

GoPay Container V1 (formerly known as GoPay Container SDK) is a bundled WebView-based environment where MiniApps are uploaded, versioned, and released through the MiniApp Portal.

Unlike Container V2, this approach relies on packaged MiniApp builds that are managed through portal workflows. It provides a large set of legacy SDK capabilities and deeper native integrations that support existing MiniApp implementations.

Key characteristics:

* Bundled MiniApp upload & versioning
* Large set of JSAPIs
* Portal-based release workflow
* Legacy support for existing integrations

This container acts as a secure shell inside the GoPay app, providing merchants with tooling to manage versions, release updates, and integrate GoPay login, payments, and native device features. While still supported for existing integrations, Container V1 is primarily maintained for legacy compatibility as newer MiniApps adopt the Container V2 architecture.

## Key Features of the GoPay Container V1

Below are the features & capabilities you or your dev team can expect when using the GoPay Container SDK

| Feature                                  | What it does / why it matters                                                                                                                                                                 |
| ---------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Seamless GoPay Login**                 | Uses GoPay SDK / auth flows so users who already have a GoPay account are recognized. No need for separate registration/login in your MiniApp. Better for conversion.                         |
| **Integrated Payment Handling**          | You can accept payments via GoPay wallet or other methods supported, handling payment flows securely using GoPay’s infrastructure. You don’t need to build or manage payment UI from scratch. |
| **Access to Native Device Capabilities** | Via Frontend JSAPIs: access things like camera use, location services, file uploads, biometrics, sensors etc. Better UX similar to native apps.                                               |
| **Cross-Platform (iOS & Android)**       | Build once using web tech (HTML/CSS/JavaScript) and it runs inside the container on both major mobile platforms. Saves time & cost.                                                           |
| **Instant / Faster Updates**             | Since your MiniApp is inside GoPay’s container, you can push updates or new versions via the Portal without waiting for App Store / Play Store approvals.                                     |
| **Version / Build Management**           | Upload different versions, test builds, manage release workflow (e.g. staging / release). Merchant can see status, coordinate with GoPay for approvals if needed.                             |
| **Deeplink & Test Access**               | The GoPay Portal provides QR codes and deeplinks so you can easily test and open your MiniApp inside the GoPay app during development.                                                        |
| **Standardized Flows & Security**        | You follow GoPay’s standard flows for login, payments etc. This means less handling of sensitive data on your side, more consistent user experience, better security.                         |
| **Discovery & Visibility**               | MiniApps are listed within the GoPay app’s MiniApp section, giving merchants exposure to GoPay’s user base and potential growth opportunities.                                                |
| **Analytics / Monitoring**               | Tools in the Portal let you see usage data: how many users opened your MiniApp, payment stats, performance metrics, error rates etc. Helps you maintain quality and improve.                  |

<br />