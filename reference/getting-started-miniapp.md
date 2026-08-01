---
updatedAt: 2026-03-16T07:30:53.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Best Practices for Building a MiniApp

This guide outlines recommended practices for developing, integrating, testing, and launching a MiniApp within the GoPay ecosystem, helping developers and merchants deliver secure, scalable, and user-friendly experiences.

# What are the common practices to build a MiniApp?

When building a MiniApp for the GoPay ecosystem, it is important to follow industry-proven practices to ensure scalability, security, and seamless integration. The goal of a MiniApp is to provide a lightweight, fast, and reliable application that runs inside the GoPay Super App while leveraging GoPay APIs and SDKs for payments, authentication, and user services.

## Below are the recommended practices for building and launching your MiniApp:

| Area                             | Best Practice                                                                                                                                                                                  | Why It Matters                                                                           |
| -------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| **Plan Your MiniApp**            | Define your MiniApp’s purpose (e.g., ordering, loyalty, booking), and what is the required APIs (login, payments, device features), and expected user traffic.                                 | Helps GoPay allocate the right permissions and ensures smooth scaling.                   |
| **Submit & Onboard**             | Fill in the [MiniApp submission form](https://gotocompany.sg.larksuite.com/share/base/form/shrlgnBkuAhMEnphzmFxhlDFUtU) and join as a GoPay MiniApp.                                           | Grants your team access to the tools and credentials needed for development.             |
| **Use GoPay Container SDK**      | Integrate login, payments, and native device features (camera, location, biometrics) through the SDK. We will provide MiniApp Integration Guide with openlinks once you've submitted the form. | Delivers a native-like user experience and reduces development complexity.               |
| **Authentication Flow**          | Implement `getAuthCode` on FE and `getAuthToken` on BE using provided credentials.                                                                                                             | Ensures secure and seamless login via GoPay account id without handling sensitive data.  |
| **Payments Integration**         | Use BI-SNAP one-time checkout: redirect to GoPay for payment, then back to MiniApp.                                                                                                            | Provides a trusted, seamless payment experience while keeping security managed by GoPay. |
| **Consistent UI/UX**             | Merchants can design their own UI while optionally using GoPay’s design patterns for login, payments, and navigation to keep user experiences consistent.                                      | Builds user trust and makes the MiniApp feel native inside GoPay.                        |
| **Test in Container**            | Validate login, payments, and error flows inside the GoPay container using MiniApp Deeplink before publishing.                                                                                 | Prevents production issues and ensures a smooth experience.                              |
| **Publish & Submit for Release** | Upload and Release your MiniApp                                                                                                                                                                | Keeps releases fast and avoids lengthy app store reviews.                                |
| **Monitor & Improve**            | Track performance, payments, and user behavior via the GoPay platform analytics.                                                                                                               | Enables continuous optimization and better business insights.                            |

<br />