---
updatedAt: 2026-04-10T10:31:06.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# FAQ (EN)

# Frequently Asked Questions

## Initialization

**Q: Can I call `GoPayEnterpriseFactory.createEnterpriseSdk` more than once?**

A: Yes, but retain and reuse the returned `GoPayEnterpriseSdk` instance for the lifetime of the user session. Only call `createEnterpriseSdk` again after `logout()` or when a new configuration is required.

***

**Q: What is `clientID` and where do I get it?**

A: `clientID` is a unique identifier assigned to your integration by GoPay. It is provided alongside the SDK artifact via email. Use the Staging `clientID` for testing and the Production `clientID` before going live.

***

**Q: Should I set `enableDebugLogs = true` in production?**

A: No. Always set `enableDebugLogs = false` in production builds. Debug logs may expose sensitive request/response payloads.

***

**Q: What does `additionalData` in `GoPayEnterpriseConfiguration` do?**

A: `additionalData` is an optional map of key-value pairs forwarded to the backend for security validations or feature-flag purposes. Pass `null` or an empty map if not required.

***

## Verify Flow

**Q: Does `FeatureRequest.build()` throw if required fields are missing?**

A: No. `build()` performs no validation — it constructs the object regardless. Validation runs inside `verify()`. If `requestId` or `userCorrelationId` is blank, `FeatureCallback.onError` is called with `GPE-2206`. There is no exception thrown.

***

**Q: What is a `requestId` and how should I generate one?**

A: `requestId` is a client-generated unique identifier used to correlate a specific verify call with its callback and handshake. Generate a fresh value for every `verify` call:

```kotlin
val requestId = "REQ-${System.currentTimeMillis()}-${(1000..9999).random()}"
```

***

**Q: When should I use `CredentialReceiver.Exchange` vs `CredentialReceiver.None`?**

A: Use `CredentialReceiver.Exchange` when the user has a **short-term linking token**. The SDK will invoke your handler with an auth code, which you exchange on your backend to obtain the `userCorrelationId`. Use `CredentialReceiver.None` when the user has a **long-term token** that is still valid and no exchange is required.

***

**Q: What do I return from the `CredentialReceiver.Exchange` handler if my backend call fails?**

A: Return `ExchangeResult.Failure(reason = "description")`. Never throw from inside the handler. The SDK stops the flow and delivers `FeatureCallback.onError` with code `GPE-2208`, with `error.message` set to the `reason` you provided.

***

**Q: What thread is `CredentialReceiver.Exchange.handler` called on?**

A: The handler is invoked on a background coroutine dispatcher. Do not update UI directly inside it.

***

**Q: What is the `token` field on `FeatureRequest`?**

A: `token` is the linking token for the user. Pass a **short-term linking token** when using `CredentialReceiver.Exchange` (the SDK will perform a credential exchange). Pass a **long-term token** when using `CredentialReceiver.None` (no exchange required).

***

**Q: Should I pass `featureId` for the verify flow?**

A: No. Do not set `featureId` when calling `verify()`. Leave it unset on the `FeatureRequest.Builder`.

***

**Q: Can I call `verify` multiple times concurrently?**

A: Each `verify` call is independent and keyed by `requestId`. Use a distinct `requestId` per call; do not reuse the same value across concurrent calls.

***

## KYC Manager

**Q: Does `getKycManager()` require any parameters?**

A: No. Call `sdk.getKycManager()` with no arguments.

***

**Q: What KYC flows are available?**

A: Four flows are available:

* **KTP Scan** — OCR capture of a KTP (Indonesian ID card).
* **Selfie Liveness** — Detects a live selfie to prevent spoofing.
* **Selfie Verification** — Matches a selfie against a reference document.
* **KYC Verification** — Full KYC combining document and selfie checks.

Each flow has a corresponding `launch*` and `observe*` function.

***

**Q: When should I register `observe*` callbacks?**

A: Register all `observe*` callbacks **before** calling the corresponding `launch*` function, typically in `onViewCreated`. The callbacks are tied to the `LifecycleOwner` you provide and are automatically cleared when it is destroyed.

***

**Q: Is `EnterpriseHelpCenter` required on every launch call?**

A: Yes. Every `launch*` function requires an `EnterpriseHelpCenter` implementation. If you do not need help functionality, return `false` from both `isHelpCTAVisible` and `onHelpCTAClicked`.

***

**Q: What do the `EnterpriseDocumentVerificationResultStatus` values mean?**

A:

* `COMPLETED` — The flow finished successfully. Use `result.submissionId` for backend tracking.
* `NOT_COMPLETED` — The user dropped out or was redirected (e.g. to help). Check `result.extra?.errorCode` for the reason.
* `ERROR` — An unrecoverable error occurred. Check `result.extra` for the error code and message.

***

**Q: Where do I get `baseUrl`, `token`, and `correlationId` for KYC config objects?**

A: `baseUrl` is provided by the GoPay team as part of your integration. `correlationId` is the `userCorrelationId` from `ExchangeResult.Success` during the verify flow. `token` is the short-lived JWT your backend issues for the current user session.

***

**Q: Can I provide custom theming for KYC flows?**

A: Yes. Each config object has an optional `theme` field (e.g. `DigitalIdentityKTPScanFlowTheme`). It defaults to the standard GoPay theme if not set.

***

## Session & Logout

**Q: How do I call `logout()`?**

A: Call it directly — it is a regular function:

```kotlin
sdk.logout()
```

***

**Q: After calling `logout()`, do I need to reinitialise the SDK?**

A: Yes. After `logout()`, call `GoPayEnterpriseFactory.createEnterpriseSdk` again before making any further SDK calls.

***

## Errors

**Q: I received `GPE-2206` — what fields are missing?**

A: Check that both `requestId` and `userCorrelationId` on your `FeatureRequest` are non-null and non-blank. The `error.title` field will indicate which specific field failed validation.

***

**Q: I received `GPE-2202` (token expired) — what should I do?**

A: Refresh the token on your backend and retry `verify()` with an updated `token` in the `FeatureRequest`.

***

**Q: I received `GPE-2204` (feature not whitelisted) — what should I do?**

A: The `featureId` passed is not enabled for your `clientID`. Contact the GoPay team to verify your feature entitlements.

***

**Q: I received `GPE-2208` (credential exchange failed) — what should I do?**

A: Your `CredentialReceiver.Exchange` handler returned `ExchangeResult.Failure`. Check `error.message` for the `reason` string you returned and investigate the backend exchange call.

***

**Q: I received an error code not in the documentation — what should I do?**

A: Report the full `GoPayEnterpriseError` (`code`, `title`, `message`) to the GoPay integration team for investigation.