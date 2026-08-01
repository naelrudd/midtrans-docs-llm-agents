---
updatedAt: 2026-04-13T03:03:02.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Migration Guide

This is a guide for existing oneKYC SDK partners who needs to migrate to Enterprise SDK.

# Digital Identity White Label flow - Migration Guide: DigitalIdentity SDK → GoPayEnterprise SDK

This guide covers the breaking changes and updated APIs when migrating from the `DigitalIdentitySdk` to `GoPayEnterpriseSdk`.

## Overview of Changes

| Area                                | Old                                        | New                                               |
| ----------------------------------- | ------------------------------------------ | ------------------------------------------------- |
| SDK initialization                  | `DigitalIdentityProvider.getInstance(...)` | `GoPayEnterpriseFactory.createEnterpriseSdk(...)` |
| KYC entry point                     | Direct on shared instance                  | Via `KycManager` obtained from SDK instance       |
| Config type — KTP Scan              | `DigitalIdentityKTPScanConfig`             | `EnterpriseKTPScanConfig`                         |
| Config type — Selfie Liveness       | `DigitalIdentitySelfieLivenessConfig`      | `EnterpriseSelfieLivenessConfig`                  |
| Config type — Face Verification     | `DigitalIdentitySelfieVerificationConfig`  | `EnterpriseSelfieVerificationConfig`              |
| Config type — Identity Verification | `DigitalIdentityKYCVerificationConfig`     | `EnterpriseKYCVerificationConfig`                 |
| Helpcenter Interface                | `DigitalIdentityHelpCenter`                | `EnterpriseHelpCenter`                            |
| Helpcenter Enum                     | `DigitalIdentityHelpCenterType`            | `EnterpriseHelpCenterType`                        |
| Result callback data                | `DocumentVerificationResult`               | `EnterpriseDocumentVerificationResult`            |
| Result status                       | `DocumentVerificationResultStatus`         | `EnterpriseDocumentVerificationResultStatus`      |
| Extra data                          | `DigitalIdentityExtraData`                 | `EnterpriseExtraData`                             |
| Extra error code                    | `DigitalIdentityFlowErrorCode`             | `EnterpriseFlowErrorCode`                         |

***

## 1. SDK Initialization

### Before

```kotlin
private val myClientConfig: DigitalIdentityClientConfig = DigitalIdentityClientConfig(
	userId = <user_id_string>,
	userName = <optional_user_name_string>,
	environment = ClientEnvironment.PRODUCTION // or ClientEnvironment.STAGING
)

private val myEventTracker: IDigitalIdentityEventTracker = object: IDigitalIdentityEventTracker {
	override fun track(
		eventName: String,
    eventProperties: Map<String, Any?>,
    productName: String?
	) {
			// Callback is triggered by SDK with event and data to be tracked if required
	}
}

val sdkInstance: DigitalIdentitySdk = DigitalIdentityProvider.getInstance(
	appContext = applicationContext,
  clientConfig = myClientConfig,
  eventTracker = myEventTracker
)
```

### After

```kotlin
val configuration = GoPayEnterpriseConfiguration(
	clientID = <client_id_string>,
  environment = GoPayEnterpriseEnvironment.PRODUCTION, // or .GoPayEnterpriseEnvironment.STAGING
  enableDebugLogs = true,	// or false
  additionalData = emptymap(),
  locale = GoPayEnterpriseLocale.en	// or GoPayEnterpriseLocale.id
)

val sdk = GoPayEnterpriseFactory.createEnterpriseSdk(
	context = applicationContext,
  configuration = configuration,
  callbackDelegate = <GoPayEnterpriseCallbackDelegate>
)

// Obtain KycManager from the initialized SDK instance
val kycManager = sdk.getKycManager()
```

**Key changes:**

* The singleton `DigitalIdentityProvider` is replaced with the Enterprise sdk instance. `GoPayEnterpriseFactory.createEnterpriseSdk(...)` returns an SDK instance you own.
* All Whitelabel flows are now accessed through a `KycManager` instance retrieved via`sdk.getKycManager()`.

***

## 2. KTP Scan

### Before

```kotlin
val config = DigitalIdentityKTPScanConfig(
	baseUrl = <base_url_string>,
  token = <token_string>,
  correlationId = <correlation_id_string>,
  theme = <DigitalIdentityKTPScanFlowTheme>
)

val helpCenter: DigitalIdentityHelpCenter = object : DigitalIdentityHelpCenter {
	override fun isHelpCTAVisible(helpCenterType: HelpCenterType): Boolean {
    return when(helpCentertype) { ... } // true or false
	}

  override fun onHelpCTAClicked(helpCenterType: HelpCenterType): Boolean {
		// Handle helpcenter loading
    return false // or true
	}
}

sdkInstance.launchKTPScan(
	activity = <Activity>,
	config = config,
	helpCenter = helpCenter
)

sdkInstance.observeKTPScan(
	owner = <Activity as LifeCycleOwner>
) { result ->
		// Handle Completion
}
```

### After

```kotlin
val config = EnterpriseKTPScanConfig(
	baseUrl = <base_url_string>,
  token = <token_string>,
  correlationId = <correlation_id_string>,
  theme = <DigitalIdentityKTPScanFlowTheme>
)

val helpCenter: EnterpriseHelpCenter = object : EnterpriseHelpCenter {
	override fun isHelpCTAVisible(helpCenterType: EnterpriseHelpCenterType): Boolean {
    return when(helpCentertype) { ... } // true or false
	}

  override fun onHelpCTAClicked(helpCenterType: EnterpriseHelpCenterType): Boolean {
		// Handle helpcenter loading
    return false // or true
	}
}

kycManager.launchKTPScan(
	activity = <Activity>,
	config = config,
	helpCenter = helpCenter
)

kycManager.observeKTPScan(
	owner = <Activity as LifeCycleOwner>
) { result ->
		// Handle Completion
}
```

**Key changes:**

* Config type renamed from `DigitalIdentityKTPScanConfig` → `EnterpriseKTPScanConfig`
* Call site moved from `sdkInstance` → `kycManager`
* HelpCenter changed from `DigitalIdentityHelpCenter` → `EnterpriseHelpCenter`
* Result Callback changed from `DocumentVerificationResult` → `EnterpriseDocumentVerificationResult`
* Completion callback:
  * `DigitalIdentityDocumentVerificationResult` → `EnterpriseDocumentVerificationResult`
  * `DigitalIdentityDocumentVerificationResultStatus` → `EnterpriseDocumentVerificationResultStatus`
  * `DigitalIdentityResultExtraData` → `EnterpriseResultExtraData`
  * `DigitalIdentityFlowErrorCode` → `EnterpriseFlowErrorCode`

**No changes:**

* baseUrl
* token
* correlationId
* theme

***

## 3. Selfie Liveness

### Before

```kotlin
val config = DigitalIdentitySelfieLivenessConfig(
	baseUrl = <base_url_string>,
  token = <token_string>,
  correlationId = <correlation_id_string>,
  theme = <DigitalIdentitySelfieLivenessFlowTheme>
)

val helpCenter: DigitalIdentityHelpCenter = object : DigitalIdentityHelpCenter {
	override fun isHelpCTAVisible(helpCenterType: HelpCenterType): Boolean {
    return when(helpCentertype) { ... } // true or false
	}

  override fun onHelpCTAClicked(helpCenterType: HelpCenterType): Boolean {
		// Handle helpcenter loading
    return false // or true
	}
}

sdkInstance.launchSelfieLiveness(
	activity = <Activity>,
	config = config,
	helpCenter = helpCenter
)

sdkInstance.observeSelfieLiveness(
	owner = <Activity as LifeCycleOwner>
) { result ->
		// Handle Completion
}
```

### After

```kotlin
val config = EnterpriseSelfieLivenessConfig(
	baseUrl = <base_url_string>,
  token = <token_string>,
  correlationId = <correlation_id_string>,
  theme = <DigitalIdentitySelfieLivenessFlowTheme>
)

val helpCenter: EnterpriseHelpCenter = object : EnterpriseHelpCenter {
	override fun isHelpCTAVisible(helpCenterType: EnterpriseHelpCenterType): Boolean {
    return when(helpCentertype) { ... } // true or false
	}

  override fun onHelpCTAClicked(helpCenterType: EnterpriseHelpCenterType): Boolean {
		// Handle helpcenter loading
    return false // or true
	}
}

kycManager.launchSelfieLiveness(
	activity = <Activity>,
	config = config,
	helpCenter = helpCenter
)

kycManager.observeSelfieLiveness(
	owner = <Activity as LifeCycleOwner>
) { result ->
		// Handle Completion
}
```

**Key changes:**

* Config type renamed from `DigitalIdentitySelfieLivenessConfig` → `EnterpriseSelfieLivenessConfig`
* Call site moved from `sdkInstance` → `kycManager`
* HelpCenter changed from `DigitalIdentityHelpCenter` → `EnterpriseHelpCenter`
* Result Callback changed from `DocumentVerificationResult` → `EnterpriseDocumentVerificationResult`
* Completion callback:
  * `DigitalIdentityDocumentVerificationResult` → `EnterpriseDocumentVerificationResult`
  * `DigitalIdentityDocumentVerificationResultStatus` → `EnterpriseDocumentVerificationResultStatus`
  * `DigitalIdentityResultExtraData` → `EnterpriseResultExtraData`
  * `DigitalIdentityFlowErrorCode` → `EnterpriseFlowErrorCode`

**No changes:**

* baseUrl
* token
* correlationId
* theme

***

## 4. Face Verification

### Before

```kotlin
val config = DigitalIdentitySelfieVerificationConfig(
	baseUrl = <base_url_string>,
  token = <token_string>,
  correlationId = <correlation_id_string>,
  theme = <DigitalIdentitySelfieVerificationFlowTheme>
)

val helpCenter: DigitalIdentityHelpCenter = object : DigitalIdentityHelpCenter {
	override fun isHelpCTAVisible(helpCenterType: HelpCenterType): Boolean {
    return when(helpCentertype) { ... } // true or false
	}

  override fun onHelpCTAClicked(helpCenterType: HelpCenterType): Boolean {
		// Handle helpcenter loading
    return false // or true
	}
}

sdkInstance.launchSelfieVerification(
	activity = <Activity>,
	config = config,
	helpCenter = helpCenter
)

sdkInstance.observeSelfieVerification(
	owner = <Activity as LifeCycleOwner>
) { result ->
		// Handle Completion
}
```

### After

```kotlin
val config = EnterpriseSelfieVerificationConfig(
	baseUrl = <base_url_string>,
  token = <token_string>,
  correlationId = <correlation_id_string>,
  theme = <DigitalIdentitySelfieVerificationFlowTheme>
)

val helpCenter: EnterpriseHelpCenter = object : EnterpriseHelpCenter {
	override fun isHelpCTAVisible(helpCenterType: EnterpriseHelpCenterType): Boolean {
    return when(helpCentertype) { ... } // true or false
	}

  override fun onHelpCTAClicked(helpCenterType: EnterpriseHelpCenterType): Boolean {
		// Handle helpcenter loading
    return false // or true
	}
}

kycManager.launchSelfieVerification(
	activity = <Activity>,
	config = config,
	helpCenter = helpCenter
)

kycManager.observeSelfieVerification(
	owner = <Activity as LifeCycleOwner>
) { result ->
		// Handle Completion
}
```

**Key changes:**

* Config type renamed from `DigitalIdentitySelfieVerificationConfig` → `EnterpriseSelfieVerificationConfig`
* Call site moved from `sdkInstance` → `kycManager`
* HelpCenter changed from `DigitalIdentityHelpCenter` → `EnterpriseHelpCenter`
* Result Callback changed from `DocumentVerificationResult` → `EnterpriseDocumentVerificationResult`
* Completion callback:
  * `DigitalIdentityDocumentVerificationResult` → `EnterpriseDocumentVerificationResult`
  * `DigitalIdentityDocumentVerificationResultStatus` → `EnterpriseDocumentVerificationResultStatus`
  * `DigitalIdentityResultExtraData` → `EnterpriseResultExtraData`
  * `DigitalIdentityFlowErrorCode` → `EnterpriseFlowErrorCode`

**No changes:**

* baseUrl
* token
* correlationId
* theme

***

## 5. Identity Verification (KYC Verification)

### Before

```kotlin
val config = DigitalIdentityKYCVerificationConfig(
	baseUrl = <base_url_string>,
  token = <token_string>,
  correlationId = <correlation_id_string>,
  theme = <DigitalIdentityKYCVerificationFlowTheme>
)

val helpCenter: DigitalIdentityHelpCenter = object : DigitalIdentityHelpCenter {
	override fun isHelpCTAVisible(helpCenterType: HelpCenterType): Boolean {
    return when(helpCentertype) { ... } // true or false
	}

  override fun onHelpCTAClicked(helpCenterType: HelpCenterType): Boolean {
		// Handle helpcenter loading
    return false // or true
	}
}

sdkInstance.launchKYCVerification(
	activity = <Activity>,
	config = config,
	helpCenter = helpCenter
)

sdkInstance.observeKYCVerification(
	owner = <Activity as LifeCycleOwner>
) { result ->
		// Handle Completion
}
```

### After

```kotlin
val config = EnterpriseKYCVerificationConfig(
	baseUrl = <base_url_string>,
  token = <token_string>,
  correlationId = <correlation_id_string>,
  theme = <DigitalIdentitySelfieVerificationFlowTheme>
)

val helpCenter: EnterpriseHelpCenter = object : EnterpriseHelpCenter {
	override fun isHelpCTAVisible(helpCenterType: EnterpriseHelpCenterType): Boolean {
    return when(helpCentertype) { ... } // true or false
	}

  override fun onHelpCTAClicked(helpCenterType: EnterpriseHelpCenterType): Boolean {
		// Handle helpcenter loading
    return false // or true
	}
}

kycManager.launchKYCVerification(
	activity = <Activity>,
	config = config,
	helpCenter = helpCenter
)

kycManager.observeKYCVerification(
	owner = <Activity as LifeCycleOwner>
) { result ->
		// Handle Completion
}
```

**Key changes:**

* Config type renamed from `DigitalIdentityKYCVerificationConfig` → `EnterpriseKYCVerificationConfig`
* Call site moved from `sdkInstance` → `kycManager`
* HelpCenter changed from `DigitalIdentityHelpCenter` → `EnterpriseHelpCenter`
* Result Callback changed from `DocumentVerificationResult` → `EnterpriseDocumentVerificationResult`
* Completion callback:
  * `DigitalIdentityDocumentVerificationResult` → `EnterpriseDocumentVerificationResult`
  * `DigitalIdentityDocumentVerificationResultStatus` → `EnterpriseDocumentVerificationResultStatus`
  * `DigitalIdentityResultExtraData` → `EnterpriseResultExtraData`
  * `DigitalIdentityFlowErrorCode` → `EnterpriseFlowErrorCode`

**No changes:**

* baseUrl
* token
* correlationId
* theme