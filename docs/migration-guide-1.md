---
updatedAt: 2026-04-10T10:28:50.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Migration Guide

This is a guide for existing oneKYC SDK partners who needs to migrate to Enterprise SDK.

# OneKyc White Label flow - Migration Guide: DigitalIdentity SDK → GoPayEnterprise SDK

This guide covers the breaking changes and updated APIs when migrating from the `DigitalIdentitySdk` to `GoPayEnterpriseSdk`.

## Overview of Changes

| Area                                | Old                                               | New                                               |
| ----------------------------------- | ------------------------------------------------- | ------------------------------------------------- |
| SDK initialization                  | `DigitalIdentitySdk.shared.initialise(...)`       | `GoPayEnterpriseFactory.createEnterpriseSdk(...)` |
| KYC entry point                     | Direct on shared instance                         | Via `KycManager` obtained from SDK instance       |
| Config type — KTP Scan              | `DigitalIdentityKTPScanConfig`                    | `EnterpriseKTPScanConfig`                         |
| Config type — Selfie Liveness       | `DigitalIdentitySelfieLivenessConfig`             | `EnterpriseSelfieConfig`                          |
| Config type — Face Verification     | `DigitalIdentitySelfieVerificationConfig`         | `EnterpriseSelfieConfig`                          |
| Config type — Identity Verification | `DigitalIdentityKYCVerificationConfig`            | `EnterpriseKYCVerificationConfig`                 |
| Language type                       | `DigitalIdentityUserLanguage`                     | `GoPayEnterpriseLocale`                           |
| Helpcenter Delegate                 | `DigitalIdentityHelpCenterDelegate`               | `EnterpriseHelpCenterDelegate`                    |
| Result callback data                | `DigitalIdentityDocumentVerificationResult`       | `EnterpriseDocumentVerificationResult`            |
| Result status                       | `DigitalIdentityDocumentVerificationResultStatus` | `EnterpriseDocumentVerificationResultStatus`      |
| Result Extra data                   | `DigitalIdentityResultExtraData`                  | `EnterpriseResultExtraData`                       |
| Result Error code                   | `DigitalIdentityFlowErrorCode`                    | `EnterpriseFlowErrorCode`                         |

***

## 1. SDK Initialization

### Before

```swift
let userProfile = DigitalIdentityUserProfile(userId: <User id>)

let configuration = DigitalIdentityConfiguration(
    environment: <DigitalIdentityEnvironment>,
    analyticsManager: IDigitalIdentityAnalyticsManager,
    userProfile: userProfile
)

DigitalIdentitySdk.shared.initialise(configuration: configuration) {
    // Completion handler
}
```

### After

```swift
let configuration = GoPayEnterpriseConfiguration(
    clientID: "YOUR_CLIENT_ID",
    environment: .STAGING, // or .PRODUCTION
    enableDebugLogs: true,  // or false
    additionalData: nil,
    locale: .en             // or .id
)

let sdk = GoPayEnterpriseFactory.createEnterpriseSdk(
    configuration: configuration,
    callbackDelegate: <GoPayEnterpriseCallbackDelegate>
)

// Obtain KycManager from the initialized SDK instance
let kycManager = sdk.getKycManager()
```

**Key changes:**

* The singleton `DigitalIdentitySdk.shared` is replaced with the Enterprise sdk instance. `GoPayEnterpriseFactory.createEnterpriseSdk(...)` returns an SDK instance you own.
* All Whitelabel flows are now accessed through a `KycManager` instance retrieved via`sdk.getKycManager()`.

***

## 2. KTP Scan

### Before

```swift
let config = DigitalIdentityKTPScanConfig(
    baseUrl: <DigitalIdentity BE Base Url>,
    token: <DigitalIdentity Token>,
    correlationId: <Correlation Id>,
    language: <DigitalIdentityUserLanguage>,
    theme: <DigitalIdentityKTPScanFlowTheme>
)

DigitalIdentitySdk.shared.launchKTPScan(
    config: config,
    viewcontroller: <viewcontroller instance>
) { result in
    // Completion handler
}
```

### After

```swift
let config = EnterpriseKTPScanConfig(
    baseUrl: <DigitalIdentity BE Base Url>,
    token: <DigitalIdentity Token>,
    correlationId: <Correlation Id>,
    language: <GoPayEnterpriseLocale>,
    theme: <DigitalIdentityKTPScanFlowTheme>
)

kycManager.launchKTPScan(config: config, from: <viewcontroller instance>) { result in
    // Completion handler
}
```

**Key changes:**

* Config type renamed from `DigitalIdentityKTPScanConfig` → `EnterpriseKTPScanConfig`.
* `language` parameter type renamed from`DigitalIdentityUserLanguage`→ `GoPayEnterpriseLocale`
* Call site moved from `DigitalIdentitySdk.shared` → `kycManager`.
* Presenter parameter label changed from `viewcontroller:` → `from:`.
* Completion closure:
  * `DigitalIdentityDocumentVerificationResult`→`EnterpriseDocumentVerificationResult`
  * `DigitalIdentityDocumentVerificationResultStatus`→ `EnterpriseDocumentVerificationResultStatus`
  * `DigitalIdentityResultExtraData`→ `EnterpriseResultExtraData`
  * `DigitalIdentityFlowErrorCode` → `EnterpriseFlowErrorCode`

**No changes:**.

* baseUrl
* token
* correlationId
* theme

***

## 3. Selfie Liveness

### Before

```swift
let config = DigitalIdentitySelfieLivenessConfig(
    baseUrl: <DigitalIdentity BE Base Url>,
    token: <DigitalIdentity Token>,
    correlationId: <Correlation Id>,
    language: <DigitalIdentityUserLanguage>,
    theme: <DigitalIdentitySelfieFlowTheme>
)

DigitalIdentitySdk.shared.launchSelfieLiveness(
    config: config,
    viewcontroller: <viewcontroller instance>,
    helpCenter: DigitalIdentityHelpCenterDelegate
) { result in }
```

### After

```swift
let config = EnterpriseSelfieConfig(
    baseUrl: <DigitalIdentity BE Base Url>,
    token: <DigitalIdentity Token>,
    correlationId: <Correlation Id>,
    language: <GoPayEnterpriseLocale>,
    theme: <DigitalIdentitySelfieFlowTheme>
)

kycManager.launchSelfieLiveness(
   config: config, 
   from: <viewcontroller instance>,
   helpCenter: EnterpriseHelpCenterDelegate) { result in }
```

**Key changes:**

* Config type renamed from `DigitalIdentitySelfieLivenessConfig` → `EnterpriseSelfieConfig`.
* `language` parameter type renamed from`DigitalIdentityUserLanguage`→ `GoPayEnterpriseLocale`
* Call site moved from `DigitalIdentitySdk.shared` → `kycManager`.
* Presenter parameter label changed from `viewcontroller:` → `from:`
* Helpcenter delegate type renamed from `DigitalIdentityHelpCenterDelegate` → `EnterpriseHelpCenterDelegate`
* Completion closure:
  * `DigitalIdentityDocumentVerificationResult`→`EnterpriseDocumentVerificationResult`
  * `DigitalIdentityDocumentVerificationResultStatus`→ `EnterpriseDocumentVerificationResultStatus`
  * `DigitalIdentityResultExtraData`→ `EnterpriseResultExtraData`
  * `DigitalIdentityFlowErrorCode` → `EnterpriseFlowErrorCode`

**No changes:**.

* baseUrl
* token
* correlationId
* theme

***

## 4. Face Verification

### Before

```swift
let config = DigitalIdentitySelfieVerificationConfig(
    baseUrl: <DigitalIdentity BE Base Url>,
    token: <DigitalIdentity Token>,
    correlationId: <Correlation Id>,
    language: <DigitalIdentityUserLanguage>,
    theme: <DigitalIdentitySelfieFlowTheme>
)

DigitalIdentitySdk.shared.launchSelfieVerification(
    config: config,
    viewcontroller: <viewcontroller instance>,
    helpCenter: DigitalIdentityHelpCenterDelegate
) { result in }
```

### After

```swift
let config = EnterpriseSelfieConfig(
    baseUrl: <DigitalIdentity BE Base Url>,
    token: <DigitalIdentity Token>,
    correlationId: <Correlation Id>,
    language: <GoPayEnterpriseLocale>,
    theme: <DigitalIdentitySelfieFlowTheme>
)

kycManager.launchSelfieVerification(
  config: config, 
  from: <viewcontroller instance>,
  helpCenter: EnterpriseHelpCenterDelegate) { result in }
```

**Key changes:**

* Config type renamed from `DigitalIdentitySelfieVerificationConfig` → `EnterpriseSelfieConfig` (same type as Selfie Liveness).
* `language` parameter type renamed from`DigitalIdentityUserLanguage`→ `GoPayEnterpriseLocale`
* Call site moved from `DigitalIdentitySdk.shared` → `kycManager`
* Presenter parameter label changed from `viewcontroller:` → `from:`.
* Helpcenter delegate type renamed from `DigitalIdentityHelpCenterDelegate` → `EnterpriseHelpCenterDelegate`
* Completion closure:
  * `DigitalIdentityDocumentVerificationResult`→`EnterpriseDocumentVerificationResult`
  * `DigitalIdentityDocumentVerificationResultStatus`→ `EnterpriseDocumentVerificationResultStatus`
  * `DigitalIdentityResultExtraData`→ `EnterpriseResultExtraData`
  * `DigitalIdentityFlowErrorCode` → `EnterpriseFlowErrorCode`

**No changes:**.

* baseUrl
* token
* correlationId
* theme

***

## 5. Identity Verification (KYC Verification)

### Before

```swift
let config = DigitalIdentityKYCVerificationConfig(
    baseUrl: <DigitalIdentity BE Base Url>,
    token: <DigitalIdentity Token>,
    correlationId: <Correlation Id>,
    language: <DigitalIdentityUserLanguage>,
    theme: <DigitalIdentityKYCVerificationFlowTheme>
)

DigitalIdentitySdk.shared.launchKYCVerification(
    config: config,
    viewcontroller: <viewcontroller instance>,
    helpCenter: DigitalIdentityHelpCenterDelegate
) { result in }
```

### After

```swift
let config = EnterpriseKYCVerificationConfig(
    baseUrl: <DigitalIdentity BE Base Url>,
    token: <DigitalIdentity Token>,
    correlationId: <Correlation Id>,
    language: <GoPayEnterpriseLocale>,
    theme: <DigitalIdentityKYCVerificationFlowTheme>
)

kycManager.launchKYCVerification(
  config: config, 
  from: <viewcontroller instance>,
  helpCenter: EnterpriseHelpCenterDelegate
  ) { result in }
```

**Key changes:**

* Config type renamed from `DigitalIdentityKYCVerificationConfig` → `EnterpriseKYCVerificationConfig`.
* Call site moved from `DigitalIdentitySdk.shared` → `kycManager`.
* Presenter parameter label changed from `viewcontroller:` → `from:`.
* Helpcenter delegate type renamed from `DigitalIdentityHelpCenterDelegate` → `EnterpriseHelpCenterDelegate`
* Completion closure:
  * `DigitalIdentityDocumentVerificationResult`→`EnterpriseDocumentVerificationResult`
  * `DigitalIdentityDocumentVerificationResultStatus`→ `EnterpriseDocumentVerificationResultStatus`
  * `DigitalIdentityResultExtraData`→ `EnterpriseResultExtraData`
  * `DigitalIdentityFlowErrorCode` → `EnterpriseFlowErrorCode`

**No changes:**.

* baseUrl
* token
* correlationId
* theme

<br />