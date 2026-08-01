---
updatedAt: 2026-04-10T10:27:33.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Android SDK - OneKYC SDK

```kotlin
interface GoPayEnterpriseSdk {
    // ..
    fun getKycManager(): KycManager
    // ..
}

interface KycManager {
    fun launchKTPScan(activity: Activity, config: EnterpriseKTPScanConfig, helpCenter: EnterpriseHelpCenter)
    fun observeKTPScan(owner: LifecycleOwner, resultCallback: (EnterpriseDocumentVerificationResult) -> Unit)

    fun launchSelfieLiveness(activity: Activity, config: EnterpriseSelfieLivenessConfig, helpCenter: EnterpriseHelpCenter)
    fun observeSelfieLiveness(owner: LifecycleOwner, resultCallback: (EnterpriseDocumentVerificationResult) -> Unit)

    fun launchSelfieVerification(activity: Activity, config: EnterpriseSelfieVerificationConfig, helpCenter: EnterpriseHelpCenter)
    fun observeSelfieVerification(owner: LifecycleOwner, resultCallback: (EnterpriseDocumentVerificationResult) -> Unit)

    fun launchKYCVerification(activity: Activity, config: EnterpriseKYCVerificationConfig, helpCenter: EnterpriseHelpCenter)
    fun observeKYCVerification(owner: LifecycleOwner, resultCallback: (EnterpriseDocumentVerificationResult) -> Unit)
}
```

`KycManager` exposes four independent KYC flows. Each flow has a paired **launch** function (to start the UI) and an **observe** function (to receive the result asynchronously via a `LifecycleOwner`-scoped callback).

<br />

| Flow                | Launch function            | Observe function            | Description                                        |
| :------------------ | :------------------------- | :-------------------------- | :------------------------------------------------- |
| KTP Scan            | `launchKTPScan`            | `observeKTPScan`            | Captures and OCR-reads a KTP (Indonesian ID card). |
| Selfie Liveness     | `launchSelfieLiveness`     | `observeSelfieLiveness`     | Detects a live selfie to prevent spoofing.         |
| Selfie Verification | `launchSelfieVerification` | `observeSelfieVerification` | Matches selfie against a reference document.       |
| KYC Verification    | `launchKYCVerification`    | `observeKYCVerification`    | Full KYC verification combining document + selfie. |

***

# Configuration Types

All config objects share the same three required fields plus an optional theme.

## EnterpriseKTPScanConfig

```kotlin
data class EnterpriseKTPScanConfig(
    val baseUrl: String,
    val token: String,
    val correlationId: String,
    val theme: DigitalIdentityKTPScanFlowTheme = DigitalIdentityKTPScanFlowTheme()
)
```

## EnterpriseSelfieLivenessConfig

```kotlin
data class EnterpriseSelfieLivenessConfig(
    val baseUrl: String,
    val token: String,
    val correlationId: String,
    val theme: DigitalIdentitySelfieLivenessFlowTheme = DigitalIdentitySelfieLivenessFlowTheme()
)
```

## EnterpriseSelfieVerificationConfig

```kotlin
data class EnterpriseSelfieVerificationConfig(
    val baseUrl: String,
    val token: String,
    val correlationId: String,
    val theme: DigitalIdentitySelfieVerificationFlowTheme = DigitalIdentitySelfieVerificationFlowTheme()
)
```

## EnterpriseKYCVerificationConfig

```kotlin
data class EnterpriseKYCVerificationConfig(
    val baseUrl: String,
    val token: String,
    val correlationId: String,
    val theme: DigitalIdentityKYCVerificationFlowTheme = DigitalIdentityKYCVerificationFlowTheme()
)
```

**Shared config fields**

| Field         | Type        | Required | Description                                                                                 |
| :------------ | :---------- | :------- | :------------------------------------------------------------------------------------------ |
| baseUrl       | String      | Yes      | Base URL of the KYC backend service. Provided by GoPay as part of your integration.         |
| token         | String      | Yes      | Short-lived JWT for authenticating the KYC request.                                         |
| correlationId | String      | Yes      | Unique identifier linking the client user to GoPay (obtained from the credential exchange). |
| theme         | \*FlowTheme | No       | Optional visual theming for the flow UI. Defaults to the standard GoPay theme.              |

***

# EnterpriseHelpCenter

Every launch function requires an `EnterpriseHelpCenter` implementation, which lets the host app control help CTA visibility and handle taps.

```kotlin
interface EnterpriseHelpCenter {
    fun isHelpCTAVisible(helpCenterType: EnterpriseHelpCenterType): Boolean
    fun onHelpCTAClicked(helpCenterType: EnterpriseHelpCenterType): Boolean
}

enum class EnterpriseHelpCenterType {
    SELFIE_TIMEOUT,
    VERIFICATION_EXHAUSTED,
    VERIFICATION_FAILED,
    CAMERA_ISSUE,
    USER_DETAILS,
    USER_CONSENT,
    NON_PROGRESSIVE_USER_CONSENT,
    KYC_STATUS
}
```

| Function         | Description                                                                                                           |
| :--------------- | :-------------------------------------------------------------------------------------------------------------------- |
| isHelpCTAVisible | Return `true` to show the help button for the given context. Return `false` to hide it.                               |
| onHelpCTAClicked | Called when the user taps the help button. Return `true` if you handled the action; `false` to let the SDK handle it. |

***

# Result Types

## EnterpriseDocumentVerificationResult

Delivered to the `observe*` callback after a flow completes, is cancelled, or errors.

```kotlin
data class EnterpriseDocumentVerificationResult(
    val correlationId: String,
    val status: EnterpriseDocumentVerificationResultStatus,
    val submissionId: String,
    val extra: EnterpriseExtraData? = null
)

enum class EnterpriseDocumentVerificationResultStatus {
    COMPLETED, NOT_COMPLETED, ERROR
}
```

| Field         | Description                                                                                  |
| :------------ | :------------------------------------------------------------------------------------------- |
| correlationId | The correlation ID provided in the config for this flow.                                     |
| status        | `COMPLETED` on success, `NOT_COMPLETED` if cancelled/dropped, `ERROR` if a failure occurred. |
| submissionId  | Backend submission reference for this attempt. Available when `status == COMPLETED`.         |
| extra         | Present when `status == NOT_COMPLETED` or `ERROR`. Carries error code and message details.   |

## EnterpriseExtraData

```kotlin
data class EnterpriseExtraData(
    val errorCode: EnterpriseFlowErrorCode = EnterpriseFlowErrorCode.USER_CANCELLED,
    val detailedErrorCode: String = "",
    val errorMessage: String = ""
)

enum class EnterpriseFlowErrorCode {
    CAMERA, PERMISSION, NETWORK, API, VERIFICATION, HELP_CLICKED, SECURITY, USER_CANCELLED
}
```

| Error Code      | Description                                                                        |
| :-------------- | :--------------------------------------------------------------------------------- |
| CAMERA          | Camera could not be opened or is unavailable.                                      |
| PERMISSION      | Required permissions were not granted.                                             |
| NETWORK         | A network failure occurred during the flow.                                        |
| API             | The KYC backend returned an error response.                                        |
| VERIFICATION    | Verification logic failed (e.g. liveness not detected).                            |
| HELP\_CLICKED   | User tapped the help CTA and the host app returned `true` from `onHelpCTAClicked`. |
| SECURITY        | A security check failed (e.g. root detection, spoofing detected).                  |
| USER\_CANCELLED | User navigated back or dismissed the flow without completing.                      |

***

# Example Usage

```kotlin
// 1. Initialize the SDK
val sdk = GoPayEnterpriseFactory.createEnterpriseSdk(
    context = applicationContext,
    configuration = GoPayEnterpriseConfiguration(
        clientID = "YOUR_CLIENT_ID",
        environment = GoPayEnterpriseEnvironment.STAGING,
        enableDebugLogs = true,
        locale = GoPayEnterpriseLocale.en,
    ),
    callbackDelegate = object : GoPayEnterpriseCallbackDelegate {
        override fun onDismiss() { }
        override fun onFailure(error: GoPayEnterpriseError) { }
    }
)

// 2. Get KYC manager
val kycManager = sdk.getKycManager()

// 3. Register observers (do this once, e.g. in onViewCreated)
kycManager.observeKTPScan(owner = this) { result ->
    when (result.status) {
        EnterpriseDocumentVerificationResultStatus.COMPLETED ->
            Log.d(TAG, "KTP scan complete: ${result.submissionId}")
        EnterpriseDocumentVerificationResultStatus.NOT_COMPLETED ->
            Log.w(TAG, "KTP scan not completed: ${result.extra?.errorCode}")
        EnterpriseDocumentVerificationResultStatus.ERROR ->
            Log.e(TAG, "KTP scan error: ${result.extra?.errorMessage}")
    }
}

kycManager.observeSelfieLiveness(owner = this) { result -> /* handle */ }
kycManager.observeSelfieVerification(owner = this) { result -> /* handle */ }
kycManager.observeKYCVerification(owner = this) { result -> /* handle */ }

// 4. Define a help center implementation
val helpCenter = object : EnterpriseHelpCenter {
    override fun isHelpCTAVisible(helpCenterType: EnterpriseHelpCenterType): Boolean = true
    override fun onHelpCTAClicked(helpCenterType: EnterpriseHelpCenterType): Boolean {
        // Open your help screen or show a dialog
        return true
    }
}

// 5. Launch a flow
kycManager.launchKTPScan(
    activity = this,
    config = EnterpriseKTPScanConfig(
        baseUrl = "https://kyc.example.com",
        token = "user-jwt-token",
        correlationId = "user-correlation-id"
    ),
    helpCenter = helpCenter
)

// Launch selfie liveness
kycManager.launchSelfieLiveness(
    activity = this,
    config = EnterpriseSelfieLivenessConfig(
        baseUrl = "https://kyc.example.com",
        token = "user-jwt-token",
        correlationId = "user-correlation-id"
    ),
    helpCenter = helpCenter
)
```

# Usage Notes

* `getKycManager()` takes no parameters. Obtain it directly from the `GoPayEnterpriseSdk` instance.
* Register all `observe*` callbacks **before** calling the corresponding `launch*` function to avoid missing results.
* `observe*` callbacks are scoped to the provided `LifecycleOwner` — they are automatically unregistered when the owner is destroyed.
* All four config types share the same field set (`baseUrl`, `token`, `correlationId`, `theme`). The `theme` field defaults to the standard GoPay theme if not provided.
* `EnterpriseHelpCenter` is required on every launch call. If help functionality is not needed, return `false` from both interface methods.
* All three config fields (`baseUrl`, `token`, `correlationId`) must be non-empty. Passing blank values may result in a runtime error from the KYC service.
* `correlationId` is typically the `userCorrelationId` obtained from `ExchangeResult.Success` during the verify flow.