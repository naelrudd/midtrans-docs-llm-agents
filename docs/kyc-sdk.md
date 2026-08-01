---
updatedAt: 2026-07-30T09:55:07.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# iOS SDK - OneKYC SDK

```swift
public protocol GoPayEnterpriseSdk: AnyObject {
    func getKycManager() -> KycManager
}

public protocol KycManager: AnyObject {
    func launchKTPScan(
        config: EnterpriseKTPScanConfig,
        from viewController: UIViewController,
        completion: @escaping (EnterpriseDocumentVerificationResult) -> Void
    )

    func launchSelfieLiveness(
        config: EnterpriseSelfieLivenessConfig,
        from viewController: UIViewController,
        helpCenter: EnterpriseHelpCenterDelegate?,
        completion: @escaping (EnterpriseDocumentVerificationResult) -> Void
    )

    func launchSelfieVerification(
        config: EnterpriseSelfieVerificationConfig,
        from viewController: UIViewController,
        helpCenter: EnterpriseHelpCenterDelegate?,
        completion: @escaping (EnterpriseDocumentVerificationResult) -> Void
    )

    func launchKYCVerification(
        config: EnterpriseKYCVerificationConfig,
        from viewController: UIViewController,
        helpCenter: EnterpriseHelpCenterDelegate?,
        completion: @escaping (EnterpriseDocumentVerificationResult) -> Void
    )

    func dispose()

    func clearCache()
}

public protocol EnterpriseHelpCenterDelegate: AnyObject {
    func isHelpCTAEnabled(for type: EnterpriseHelpCenterType) -> Bool
    func onHelpCTAClicked(in viewController: UIViewController, type: EnterpriseHelpCenterType)
}

public enum EnterpriseHelpCenterType: String {
    case verificationExhausted
    case verificationFailed
    case selfieCaptureExhausted
}
```

`KycManager` exposes four independent KYC flows. Each flow is launched with a single call that also accepts a completion closure — there are no separate register/observe steps.

<br />

| Flow                | Launch function            | Config type                       | Description                                        |
| :------------------ | :------------------------- | :-------------------------------- | :------------------------------------------------- |
| KTP Scan            | `launchKTPScan`            | `EnterpriseKTPScanConfig`         | Captures and OCR-reads a KTP (Indonesian ID card). |
| Selfie Liveness     | `launchSelfieLiveness`     | `EnterpriseSelfieConfig`          | Detects a live selfie to prevent spoofing.         |
| Selfie Verification | `launchSelfieVerification` | `EnterpriseSelfieConfig`          | Matches a selfie against a reference document.     |
| KYC Verification    | `launchKYCVerification`    | `EnterpriseKYCVerificationConfig` | Full KYC combining document and selfie checks.     |

In addition to the launch functions, `KycManager` exposes two lifecycle methods:

| Method         | Description                                                                 |
| :------------- | :-------------------------------------------------------------------------- |
| `dispose()`    | Tears down the underlying KYC SDK instance and releases held resources.     |
| `clearCache()` | Clears any cached data stored by the KYC SDK (e.g. session or token cache). |

***

# Configuration Types

## EnterpriseKTPScanConfig

```swift
public struct EnterpriseKTPScanConfig {
    public let baseUrl: String
    public let token: String
    public let correlationId: String
    public let language: GoPayEnterpriseLocale
    public let theme: DigitalIdentityKTPScanFlowTheme?

    public init(baseUrl: String, token: String, correlationId: String, language: String,
                theme: DigitalIdentityKTPScanFlowTheme? = nil)
}
```

## EnterpriseSelfieLivenessConfig.

```swift
public struct EnterpriseSelfieLivenessConfig {
    public let baseUrl: String
    public let token: String
    public let correlationId: String
    public let language: GoPayEnterpriseLocale
    public let theme: DigitalIdentitySelfieFlowTheme?

    public init(baseUrl: String, token: String, correlationId: String, language: String,
                theme: DigitalIdentitySelfieFlowTheme? = nil)
}
```

## EnterpriseSelfieVerificationConfig

```swift
public struct EnterpriseSelfieVerificationConfig {
    public let baseUrl: String
    public let token: String
    public let correlationId: String
    public let language: GoPayEnterpriseLocale
    public let theme: DigitalIdentitySelfieFlowTheme?

    public init(baseUrl: String, token: String, correlationId: String, language: String,
                theme: DigitalIdentitySelfieFlowTheme? = nil)
}
```

##

## EnterpriseKYCVerificationConfig

```swift
public struct EnterpriseKYCVerificationConfig {
    public let baseUrl: String
    public let token: String
    public let correlationId: String
    public let language: GoPayEnterpriseLocale
    public let theme: DigitalIdentityKYCVerificationFlowTheme?

    public init(baseUrl: String, token: String, correlationId: String, language: String,
                theme: DigitalIdentityKYCVerificationFlowTheme? = nil)
}
```

**Shared config fields**

| Field         | Type                         | Required | Description                                                                                                          |
| :------------ | :--------------------------- | :------- | :------------------------------------------------------------------------------------------------------------------- |
| baseUrl       | String                       | Yes      | Base URL of the KYC backend service. Provided by GoPay as part of your integration credentials.                      |
| token         | String                       | Yes      | Short-lived JWT for authenticating the KYC request. Issued by your backend for the current user session.             |
| correlationId | String                       | Yes      | Unique identifier linking the client user to GoPay. Typically the `userCorrelationId` from the verify exchange flow. |
| language      | GoPayEnterpriseLocale        | Yes      | Use `id` or `en`to show respective language copy text                                                                |
| theme         | `DigitalIdentity*FlowTheme?` | No       | Optional visual theming for the flow UI. Pass `nil` to use the default GoPay theme. See **Theme** section below.     |

***

# Theme

Each config struct accepts an optional `theme` parameter for customising the visual appearance of the respective flow. The theme types are provided by the `DigitalIdentity` framework.

| Config type                          | Theme type                                |
| :----------------------------------- | :---------------------------------------- |
| `EnterpriseKTPScanConfig`            | `DigitalIdentityKTPScanFlowTheme`         |
| `EnterpriseSelfieLivenessConfig`     | `DigitalIdentitySelfieFlowTheme`          |
| `EnterpriseSelfieVerificationConfig` | `DigitalIdentitySelfieFlowTheme`          |
| `EnterpriseKYCVerificationConfig`    | `DigitalIdentityKYCVerificationFlowTheme` |

All theme parameters default to `nil`, which applies the standard GoPay theme. To apply a custom theme, construct the appropriate `DigitalIdentity*FlowTheme` object and pass it to the config initialiser:

```swift
import DigitalIdentity

let theme = DigitalIdentityKTPScanFlowTheme(/* customise as needed */)

let config = EnterpriseKTPScanConfig(
    baseUrl: "https://kyc.example.com",
    token: "user-jwt-token",
    correlationId: "user-correlation-id",
    language: .id,
    theme: theme
)
```

Refer to the `DigitalIdentity` framework documentation for the available theming properties on each theme type.

***

# HelpCenter

Implement the EnterpriseHelpCenterDelegate method to control help center behaviour in the Selfie Liveness, Face Verification, KYC Verification flows

## `isHelpCTAEnabled`

`isHelpCTAEnabled(for type: EnterpriseHelpCenterType) -> Bool`

The **isHelpCTAEnabled** method will be triggered with the **type** parameter before the Help CTA is shown in the Sdk flow-related screens. Based on the bool return value sdk will show/hide the Help CTA.

### `onHelpCTAClicked`

`onHelpCTAClicked(in viewController: UIViewController, type: EnterpriseHelpCenterType)`

The **onHelpCTAClicked** method will be triggered with **the viewController** and **type** parameters when the user taps the Help CTA in the Sdk flow-related screens.

### `EnterpriseHelpCenterType`

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Flows
      </th>

      <th>
        Applicable HelpCenterType
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        KTP Scan
      </td>

      <td>
        N/A
      </td>
    </tr>

    <tr>
      <td>
        Selfie Liveness & Face Verification
      </td>

      <td>
        1. selfieCaptureExhausted 
        2. verificationFailed 
        3. verificationExhausted
      </td>
    </tr>

    <tr>
      <td>
        Identity Verification
      </td>

      <td>
        1. selfieCaptureExhausted
      </td>
    </tr>
  </tbody>
</Table>

***

# Result Types

## EnterpriseDocumentVerificationResult

Delivered to the completion closure after a flow completes, is cancelled, or errors.

```swift
public struct EnterpriseDocumentVerificationResult {
    public var correlationId: String
    public var status: EnterpriseDocumentVerificationResultStatus
    public var submissionId: String?
    public var extra: EnterpriseResultExtraData?
}

public enum EnterpriseDocumentVerificationResultStatus: String {
    case completed
    case notCompleted
    case error
}
```

| Field         | Description                                                                                    |
| :------------ | :--------------------------------------------------------------------------------------------- |
| correlationId | The correlation ID provided in the config for this flow.                                       |
| status        | `.completed` on success, `.notCompleted` if cancelled/dropped, `.error` if a failure occurred. |
| submissionId  | Backend submission reference for this attempt. Present when `status == .completed`.            |
| extra         | Present when `status == .notCompleted` or `.error`. Carries error code and message details.    |

## EnterpriseResultExtraData

```swift
public struct EnterpriseResultExtraData: Codable {
    public var errorCode: EnterpriseFlowErrorCode?
    public var errorMessage: String?
}

public enum EnterpriseFlowErrorCode: String, Codable {
    case CAMERA
    case PERMISSION
    case NETWORK
    case USER_CANCELLED
    case VERIFICATION
}
```

| Error Code      | Description                                                   |
| :-------------- | :------------------------------------------------------------ |
| CAMERA          | Camera could not be opened or is unavailable.                 |
| PERMISSION      | Required camera permission was not granted by the user.       |
| NETWORK         | A network failure occurred during the flow.                   |
| VERIFICATION    | Verification logic failed (e.g. liveness check not passed).   |
| USER\_CANCELLED | User navigated back or dismissed the flow without completing. |

***

# Example Usage

```swift
// 1. Obtain KycManager from the initialized SDK instance
let kycManager = sdk.getKycManager()

// 2. Build a config
let config = EnterpriseKTPScanConfig(
    baseUrl: "https://kyc.example.com",
    token: "user-jwt-token",
    correlationId: "user-correlation-id",
    language: .id
)

// 3. Launch KTP Scan — result is delivered via completion closure
kycManager.launchKTPScan(config: config, from: self) { result in
    switch result.status {
    case .completed:
        print("KTP scan complete. Submission ID: \(result.submissionId ?? "")")
    case .notCompleted:
        print("KTP scan not completed: \(result.extra?.errorCode?.rawValue ?? "unknown")")
    case .error:
        print("KTP scan error: \(result.extra?.errorMessage ?? "unknown")")
    }
}

// 4. Selfie liveness
let selfieConfig = EnterpriseSelfieConfig(
    baseUrl: "https://kyc.example.com",
    token: "user-jwt-token",
    correlationId: "user-correlation-id",
    language: .id
)

kycManager.launchSelfieLiveness(config: selfieConfig, from: self, helpCenter: self) { result in
    print("Selfie liveness status: \(result.status.rawValue)")
}

// 5. KYC verification (full flow)
let kycConfig = EnterpriseKYCVerificationConfig(
    baseUrl: "https://kyc.example.com",
    token: "user-jwt-token",
    correlationId: "user-correlation-id",
    language: .id
)

kycManager.launchKYCVerification(config: kycConfig, from: self, helpCenter: self) { result in
    switch result.status {
    case .completed:
        print("KYC complete. Submission ID: \(result.submissionId ?? "")")
    case .notCompleted, .error:
        let code = result.extra?.errorCode?.rawValue ?? "none"
        let message = result.extra?.errorMessage ?? ""
        print("KYC did not complete [\(code)]: \(message)")
    }
}
```

# Usage Notes

* Call `getKycManager()` with no arguments. Obtain it from the initialized `GoPayEnterpriseSdk` instance.
* The completion closure is called on the **main thread**.
* Each `launch*` function presents a new UI flow on top of the provided `viewController`. Ensure the view controller is part of an active navigation stack.
* All three config fields (`baseUrl`, `token`, `correlationId`) must be non-empty. Passing blank values may result in a runtime failure from the KYC service.
* `correlationId` is typically the `userCorrelationId` obtained from `ExchangeResult.success` during the verify flow.
* The `theme` parameter is optional and defaults to `nil` (standard GoPay theme). Pass a typed `DigitalIdentity*FlowTheme` instance to apply custom branding. Import the `DigitalIdentity` framework in the file where you construct the theme.
* The SDK must be initialized (via `GoPayEnterpriseFactory.createEnterpriseSdk`) before calling any KYC flow.
* Call `dispose()` when the KYC session is no longer needed (e.g. on user logout or when the host feature is torn down) to free underlying resources held by the SDK.
* Call `clearCache()` to invalidate any cached KYC session data. This is useful when switching users or when a fresh KYC session must be forced.