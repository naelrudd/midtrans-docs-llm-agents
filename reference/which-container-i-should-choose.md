---
updatedAt: 2026-03-16T07:31:04.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Choosing your GoPay Container

This guide helps you decide between GoPay Container V1 (Legacy) and V2 (Recommended) for your MiniApp integration, explaining their differences, advantages, limitations, and which option is best suited for new or existing projects.

Before building your MiniApp, you need to choose which GoPay Container your integration will run on. Currently, GoPay supports two container types:

* [GoPay Container V2](https://docs.midtrans.com/reference/miniapp-v2) (Recommended) — WebKit-based container where you host your MiniApp externally.
* [GoPay Container V1](https://docs.midtrans.com/reference/miniapp-v1) (Legacy) — Bundled WebView container where the MiniApp package is uploaded and hosted within GoPay.

If you are starting a new integration, we strongly recommend using GoPay Container V2, as future feature development will focus on this container.

<br />

# GoPay Container V2 (Recommended)

GoPay Container V2 works similarly to a WebKit-based web environment. Merchants host their MiniApp on their own infrastructure, and GoPay maps the hosted entrypoint URL into the GoPay app.

## Key Characteristics

* Uses a public MiniApp URL as the entrypoint.
* Merchants manage hosting, updates, and deployments.
* Supports custom JSAPI integrations for device features.
* Changes deployed on your server are reflected immediately in production.

## Advantages

* Easier and faster integration.
* Faster loading time and smaller application size.
* No packaging or publishing flow required.
* Ideal for teams already familiar with modern web development.

## Considerations

* Functionalities are currently more limited compared to V1 (subset of FE SDKs available).
* No versioning or staged release — updates go live instantly.
* Data is passed through URLs, requiring careful security implementation.

👉 Suitable for most new MiniApps and recommended for future integrations.

<br />

# GoPay Container V1 (Legacy)

GoPay Container V1 uses a bundled WebView approach. Merchants upload their MiniApp package, which is then hosted and managed within the GoPay environment.

## Key Characteristics

* MiniApp is packaged and uploaded to GoPay.
* Supports a large number of native JSAPIs
* Supports version publishing and controlled release flows.

## Advantages

* More native-like behavior.
* Advanced SDK capabilities.
* Versioning allows testing before production release.
* Stronger data security since assets are bundled.

## Considerations

* Higher integration effort.
* Larger application size.
* Longer initial loading time.
* Only supports SPA architecture (e.g., Next.js SSR requires conversion).
* Considered legacy — new features will prioritize V2.

👉 Recommended only for existing MiniApps that already rely on legacy SDK capabilities.

Comparison Overview

| Feature            | GoPay Container V2 (WebKit)  | GoPay Container V1 (Legacy) |
| ------------------ | ---------------------------- | --------------------------- |
| Hosting Model      | Merchant-hosted URL          | Bundled & hosted by GoPay   |
| Integration Effort | Easier                       | More complex                |
| SDK Features       | Many common JSAPIs available | Extensive                   |
| Versioning         | ❌ No versioning              | ✅ Publish & release flow    |
| Loading Time       | Faster                       | Slower first load (Preload) |
| App Size           | Smaller                      | Larger                      |
| Security Model     | URL-based                    | Bundled & secured           |
| Future Support     | ⭐ Primary focus              | Legacy support              |

<br />

# Which Container Should You Choose?

👉 New MiniApps: Use GoPay Container V2 (Recommended).\
👉 Existing integrations using advanced legacy SDKs: Continue with GoPay Container V1 until migration planning is complete.

GoPay’s roadmap focuses on expanding capabilities within Container V2, and future enhancements will be developed primarily on this platform.