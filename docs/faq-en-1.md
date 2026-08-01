---
updatedAt: 2026-06-23T12:19:31.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# FAQ (EN)

<br />

# Frequently Asked Questions

## Initialization

**Q: Can I call `GoPayEnterpriseFactory.createEnterpriseSdk` more than once?**

A: Yes, but retain and reuse the returned `GoPayEnterpriseSdk` instance for the lifetime of the user session. Only call `createEnterpriseSdk` again after `logout()` or when a new configuration is required (e.g. switching environments).

***

**Q: What is `clientID` and where do I get it?**

A: `clientID` is a unique identifier assigned to your integration by GoPay. It is provided alongside the SDK artifact via email. Use the Staging `clientID` for development and testing; use the Production `clientID` before going live.

***

**Q: Should I set `enableDebugLogs = true` in production?**

A: No. Always set `enableDebugLogs: false` in production builds. Debug logs may expose sensitive request/response payloads.

***

**Q: What does `additionalData` in `GoPayEnterpriseConfiguration` do?**

A: `additionalData` is an optional `[String: String]` dictionary forwarded to the backend for security validations or feature-flag purposes. Pass `nil` or omit the parameter if not required.

***

**Q: The delegate I passed to `createEnterpriseSdk` is not receiving callbacks. Why?**

A: The SDK holds the delegate **weakly**. Ensure the object conforming to `GoPayEnterpriseCallbackDelegate` is retained strongly by your view controller, coordinator, or another owner for the duration of the session.

***

**Q: What thread should I call `createEnterpriseSdk` and other SDK methods on?**

A: Call all SDK methods on the **main thread** unless stated otherwise. The KYC completion closures are also delivered on the main thread.

***

## Verify Flow

**Q: Does `FeatureRequest.Builder.build()` throw if required fields are missing?**

A: No. `build()` performs no validation — it constructs the object regardless. Validation runs inside `verify()`. If `requestId` or `userCorrelationId` is blank, `callback.onError` is called with `GPE-2206`. No exception is thrown.

***

**Q: What is a `requestId` and how should I generate one?**

A: `requestId` is a client-generated unique identifier used to correlate a specific verify call with its callback and handshake. Generate a fresh value for every `verify` call:

```swift
let requestId = UUID().uuidString
```

***

**Q: When should I use `.exchange` vs `.none` for `CredentialReceiver`?**

A: Use `.exchange` when the user has a **short-term linking token**. The SDK invokes your handler with an auth code, which you exchange on your backend to obtain the `userCorrelationId`. Use `.none` when the user already has a **long-term token** that is still valid and no exchange is required.

***

**Q: What do I call inside the `CredentialExchangeHandler` if my backend call fails?**

A: Call `completion(.failure(reason: "description"))`. Never throw from inside the handler. The SDK stops the flow and delivers `callback.onError` with code `GPE-2208`, with `error.message` set to the `reason` you provided.

***

**Q: What thread is the `CredentialExchangeHandler.handle` closure called on?**

A: It may be called on a background thread. Do not update UI directly inside the handler closure.

***

**Q: My `FeatureCallback` stopped receiving `onComplete`/`onError`. What happened?**

A: `AnyFeatureCallback` holds a **weak** reference to the wrapped callback. If your `FeatureCallback` instance is released before the flow completes, the callbacks will be silently dropped. Keep a strong reference (e.g. a property on your view controller):

```swift
private var verifyCallback: VerifyFeatureCallback?

// ...
let callback = VerifyFeatureCallback(...)
self.verifyCallback = callback

try sdk.getFeatureManager().verify(
    viewController: self,
    request: request,
    credentialReceiver: credentialReceiver,
    callback: AnyFeatureCallback(wrapping: callback)
)
```

***

**Q: Should I pass `featureId` for the verify flow?**

A: No. Do not set `featureId` when calling `verify()`. Leave it unset on the `FeatureRequest.Builder`.

***

**Q: `verify()` is marked `throws` — what does it throw?**

A: Currently, `verify()` does not throw for validation errors — those are reported via `callback.onError`. The `throws` annotation is present for future extensibility. Wrap the call in `do-catch` to be safe.

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

***

**Q: What is the difference between `EnterpriseSelfieConfig` and `EnterpriseKYCVerificationConfig`?**

A: Both have the same fields. `EnterpriseSelfieConfig` is used for standalone Selfie Liveness and Selfie Verification flows. `EnterpriseKYCVerificationConfig` is used for the full KYC Verification flow which combines document and selfie checks.

***

**Q: Can I customise the visual appearance of KYC flows?**

A: Yes. Each config type accepts an optional `theme` parameter:

* `EnterpriseKTPScanConfig` → `theme: DigitalIdentityKTPScanFlowTheme?`
* `EnterpriseSelfieConfig` → `theme: DigitalIdentitySelfieFlowTheme?`
* `EnterpriseKYCVerificationConfig` → `theme: DigitalIdentityKYCVerificationFlowTheme?`

Pass `nil` (the default) to use the standard GoPay theme. To apply custom branding, import the `DigitalIdentity` framework, construct the appropriate theme object, and pass it to the config initialiser. Refer to the `DigitalIdentity` framework documentation for available theming properties.

***

**Q: What does `correlationId` in the KYC config correspond to?**

A: It is the `userCorrelationId` obtained from `ExchangeResult.success` during the verify flow. It uniquely links the device session to the user's GoPay identity.

***

**Q: What `language` values are accepted?**

A: Use BCP-47 locale tags. Currently supported: `"en_ID"` (English) and `"id_ID"` (Bahasa Indonesia).

***

**Q: What do the `EnterpriseDocumentVerificationResultStatus` values mean?**

A:

* `.completed` — The flow finished successfully. Use `result.submissionId` for backend tracking.
* `.notCompleted` — The user dropped out or the flow was interrupted. Check `result.extra?.errorCode` for the reason.
* `.error` — An unrecoverable error occurred. Check `result.extra` for the error code and message.

***

**Q: Where do I get `baseUrl` and `token` for KYC config objects?**

A: `baseUrl` is provided by the GoPay team as part of your integration credentials. `token` is a short-lived JWT issued by your backend for the current user session.

***

## Session & Logout

**Q: How do I call `logout()`?**

A: Call it directly on the SDK instance:

```swift
sdk.logout()
```

***

**Q: After calling `logout()`, do I need to reinitialise the SDK?**

A: Yes. After `logout()`, call `GoPayEnterpriseFactory.createEnterpriseSdk` again before making any further SDK calls.

***

**Q: Should I set the SDK reference to `nil` after logout?**

A: It is recommended to discard and nil out the old SDK instance after `logout()` to avoid accidental use:

```swift
sdk.logout()
sdk = nil
```

***

## Errors

**Q: I received `GPE-2206` — what fields are missing?**

A: Check that both `requestId` and `userCorrelationId` on your `FeatureRequest` are non-empty strings. The `error.message` field indicates which specific field failed validation.

***

**Q: I received `GPE-2202` — what should I do?**

A: The token passed to `verify()` is expired or unauthorized. Refresh the linking token on your backend and call `verify()` again with the updated token.

***

**Q: I received `GPE-2208` — what should I do?**

A: Your `CredentialExchangeHandler` returned a `.failure`. Check `error.message` for the reason string you passed, and investigate why your backend exchange call failed.

***

## Build & Integration

**Q: I see a Sandbox / rsync error during archive or build.**

A: In your target's **Build Settings → Build Options**, set **User Script Sandboxing** to **No**.

***

**Q: The SDK builds in the simulator but fails on device.**

A: Ensure the `.xcframework` is set to **Embed & Sign** (not **Do Not Embed**) in your target's **Frameworks, Libraries, and Embedded Content** section.

***

**Q: I see "module not found" or ABI-related linker errors for a dependency.**

A: Set `BUILD_LIBRARY_FOR_DISTRIBUTION = YES` on all dependency pods. Add the `post_install` block to your `Podfile` as described in [Getting Started](getting-started.md).

***

**Q: The app crashes on launch with "No KycAdapter registered".**

A: This is an internal assertion that fires if `getKycManager()` is called before the SDK's initialization completes. Ensure `GoPayEnterpriseFactory.createEnterpriseSdk` has returned successfully before calling `getKycManager()`.