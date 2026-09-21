---
updatedAt: 2026-09-17T07:51:47.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# MiniApp Performance Guidelines

This guide explains performance best practices for building GoPay MiniApps and highlights common practices developers should follow to ensure fast loading, responsive interactions, and a smooth user experience. ⚡

Performance is important to ensure MiniApps provide a fast, responsive, and stable experience within the host app.

## Performance Targets

| Metric                    |     Target |
| ------------------------- | ---------: |
| JavaScript on first visit | `< 300 KB` |
| Total page size           | `< 1.5 MB` |
| LCP                       |   `< 2.5s` |
| INP                       |  `< 200ms` |
| CLS                       |    `< 0.1` |
| API response time         |  `< 500ms` |
| First meaningful content  |     `< 2s` |

## 1. Page Loading

* Load only what is required for the first screen.
* Defer non-critical scripts and styles.
* Inline critical CSS where appropriate.
* Preload key fonts and use `font-display: swap`.
* Use a CDN for static files.

## 2. JavaScript

* Keep the initial JavaScript bundle below **300 KB**.
* Remove unused libraries and dependencies.
* Use code splitting by route.
* Lazy-load components that are not required on the first screen.
* Enable tree-shaking.
* Check npm package size before adding new dependencies.

## 3. Image Optimisation

* Compress all images before uploading.
* Target **< 200 KB per image**.
* Prefer **WebP or AVIF** formats.
* Set explicit width and height for images.
* Lazy-load images below the fold.
* Use `srcset` to serve appropriate image sizes.
* Optimise SVG files before use.

## 4. Network & API

* API responses should complete within **500ms**.
* Do not block page rendering while waiting for an API response.
* Show a skeleton or loading state instead.
* Enable **Brotli or gzip** compression.
* Set appropriate `Cache-Control` headers for static assets.
* Combine API calls where possible to reduce network round trips.

> **Note:** Do not use Service Workers for caching. They are not supported in the iOS MiniApp container. Use HTTP caching and server-side caching instead.

## 5. Third-Party Scripts

Third-party scripts can significantly affect MiniApp loading performance.

* Remove scripts that are not actively used.
* Do not load analytics or trackers synchronously.
* Use `async` or `defer` for third-party scripts.
* Run Lighthouse after adding new third-party scripts.

Keep the number of third-party scripts as low as possible.

## 6. Layout & Mobile Optimisation

* Keep animations short and simple, preferably **under 300ms**.
* Avoid animating `box-shadow` and `filter`.
* Set explicit dimensions for images and videos.
* Reserve space for dynamic content.
* Do not inject content above existing page elements.
* Use CSS `aspect-ratio` for embeds and iframes.
* Test the layout at **360px width**.
* Avoid heavy animations and particle effects.

## 7. MiniApp Runtime

MiniApps run inside the **MiniApp Container (MAC)** rather than a regular browser, so always test in the actual container before launch.

* Keep pages lightweight to avoid memory issues.
* Do not rely on `localStorage` for critical data because the OS may clear it.
* Store important state on the server where appropriate.
* Test on mobile devices and realistic network conditions.

## 8. Performance Testing

Before every major release:

1. **Measure** — Run PageSpeed Insights or Lighthouse in Mobile mode.
2. **Identify** — Find the biggest performance issues.
3. **Optimise** — Prioritise images and JavaScript.
4. **Monitor** — Track real-user performance where RUM is available.

Always test under simulated **3G and 4G** conditions, not only office Wi-Fi.

## Recommended Tools

| Tool                                             | Use For                                   |
| ------------------------------------------------ | ----------------------------------------- |
| [PageSpeed Insights](https://pagespeed.web.dev/) | Core Web Vitals and performance audit     |
| Lighthouse                                       | Performance audit through Chrome DevTools |
| [WebPageTest](https://www.webpagetest.org/)      | Real-device and network simulation        |
| [Bundlephobia](https://bundlephobia.com/)        | Check npm package size                    |
| [TinyPNG](https://tinypng.com/)                  | Image compression                         |
| [Squoosh](https://squoosh.app/)                  | Image compression and format conversion   |
| SVGO                                             | SVG optimisation                          |

## Launch Checklist

Before submitting a MiniApp for review:

* [ ] Initial JavaScript is below **300 KB**
* [ ] Total page size is below **1.5 MB**
* [ ] LCP is below **2.5s**
* [ ] INP is below **200ms**
* [ ] CLS is below **0.1**
* [ ] API responses are below **500ms**
* [ ] Images are compressed and optimised
* [ ] Unused third-party scripts are removed
* [ ] MiniApp has been tested in the actual MiniApp Container
* [ ] Mobile and throttled network testing has been completed