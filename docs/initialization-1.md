---
updatedAt: 2026-05-22T08:03:23.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Initialization

<br />

```swift
public enum GoPayEnterpriseEnvironment {
    case STAGING, PRODUCTION
}

public enum GoPayEnterpriseLocale: String {
    case id, en
}

public struct GoPayEnterpriseConfiguration {
    var clientID: String
    var environment: GoPayEnterpriseEnvironment
    var enableDebugLogs: Bool
    var additionalData: [String: String]?
    var locale: GoPayEnterpriseLocale

    public init(
        clientID: String,
        environment: GoPayEnterpriseEnvironment,
        enableDebugLogs: Bool = false,
        additionalData: [String: String]? = nil,
        locale: GoPayEnterpriseLocale = .en
    )
}

public protocol GoPayEnterpriseCallbackDelegate: AnyObject {
    func onDismiss()
    func onFailure(error: GoPayEnterpriseError)
}

public struct GoPayEnterpriseError: Error {
    public var code: String
    public var message: String
    public var title: String
}

public enum GoPayEnterpriseFactory {
    public static func createEnterpriseSdk(
        configuration: GoPayEnterpriseConfiguration,
        callbackDelegate: GoPayEnterpriseCallbackDelegate
    ) -> GoPayEnterpriseSdk
}

public protocol GoPayEnterpriseSdk: AnyObject {
    func getFeatureManager() -> FeatureManager
    func getKycManager() -> KycManager
    func logout()
}
```

# Specifications

## GoPayEnterpriseFactory

```swift
public enum GoPayEnterpriseFactory {
    public static func createEnterpriseSdk(
        configuration: GoPayEnterpriseConfiguration,
        callbackDelegate: GoPayEnterpriseCallbackDelegate
    ) -> GoPayEnterpriseSdk
}
```

### Description

Initializes the GoPay Enterprise SDK with the provided configuration and returns the entry-point `GoPayEnterpriseSdk` instance.

### Parameters

| Parameter        | Type                            | Description                                                                                                                    |
| :--------------- | :------------------------------ | :----------------------------------------------------------------------------------------------------------------------------- |
| configuration    | GoPayEnterpriseConfiguration    | The SDK configuration object. Contains `clientID`, `environment`, `locale`, debug log settings, and optional `additionalData`. |
| callbackDelegate | GoPayEnterpriseCallbackDelegate | A weakly-held delegate that receives top-level SDK events: dismissal and initialization or runtime failures.                   |

### Return Value

Returns a `GoPayEnterpriseSdk` instance. Store this instance for the lifetime of the user session — it is the entry point for all subsequent SDK operations.

### Usage Notes

* Call once before invoking any other SDK method.
* If initialization fails (e.g. invalid `clientID`), `callbackDelegate.onFailure` is called with a `GoPayEnterpriseError`.
* Always set `enableDebugLogs` to `false` in production builds to avoid leaking sensitive request/response data.
* The delegate is held **weakly** — ensure the object conforming to `GoPayEnterpriseCallbackDelegate` is retained by your view controller or coordinator.
* Call `createEnterpriseSdk` again only after `logout()` or when a new configuration is required.
* Call on the **main thread**.

### Example Usage

```swift
let configuration = GoPayEnterpriseConfiguration(
    clientID: "YOUR_CLIENT_ID",
    environment: .STAGING,
    enableDebugLogs: true,
    additionalData: ["phone_number": "+628XXXXXXXXX"],
    locale: .en
)

let sdk = GoPayEnterpriseFactory.createEnterpriseSdk(
    configuration: configuration,
    callbackDelegate: self
)
```

```swift
extension MyViewController: GoPayEnterpriseCallbackDelegate {
    func onDismiss() {
        // SDK container was dismissed
    }

    func onFailure(error: GoPayEnterpriseError) {
        print("SDK error [\(error.code)]: \(error.title) — \(error.message)")
    }
}
```

### Field Reference

#### GoPayEnterpriseConfiguration

An object containing configuration parameters required to initialize the GoPay Enterprise SDK.

| Parameter       | Type                       | Description                                                                                                                                                                                       |
| :-------------- | :------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| clientID        | String                     | Unique identifier provided by GoPay as part of your SDK integration.                                                                                                                              |
| environment     | GoPayEnterpriseEnvironment | Determines the environment. Use `.STAGING` for development and testing; `.PRODUCTION` before going live.                                                                                          |
| enableDebugLogs | Bool                       | Enables verbose console logging. Always `false` in production builds.                                                                                                                             |
| locale          | GoPayEnterpriseLocale      | Sets the display language of SDK UI. `.en` for English (default), `.id` for Bahasa Indonesia.                                                                                                     |
| additionalData  | \[String: String]?         | Optional key-value pairs forwarded to the backend for validations or security enhancements. For example, pass the user's phone number using the `"phone_number"` key. Pass `nil` if not required. |

#### GoPayEnterpriseCallbackDelegate

A protocol implemented by the host app to receive top-level SDK lifecycle events.

| Method                                   | Description                                                                                            |
| :--------------------------------------- | :----------------------------------------------------------------------------------------------------- |
| `onDismiss()`                            | Called when the SDK container is closed or popped from the navigation stack.                           |
| `onFailure(error: GoPayEnterpriseError)` | Called when the SDK encounters an initialization or runtime failure. Inspect `error.code` for details. |

#### GoPayEnterpriseError

Represents an error returned by the SDK.

| Field   | Type   | Description                                                                                                   |
| :------ | :----- | :------------------------------------------------------------------------------------------------------------ |
| code    | String | Error constant identifying the specific failure. See [Error Codes Reference](gopayenterprise-error-codes.md). |
| message | String | Localized, human-readable error message.                                                                      |
| title   | String | Localized error title.                                                                                        |

#### GoPayEnterpriseSDK

`GoPayEnterpriseSdk` is the main handle for the SDK. It provides access to feature and KYC flows, and session management.

| Function          | Description                                                                                       |
| :---------------- | :------------------------------------------------------------------------------------------------ |
| getFeatureManager | Returns a `FeatureManager` instance for launching verify and login flows.                         |
| getKycManager     | Returns a `KycManager` instance for KTP scan, selfie liveness, selfie verification, and full KYC. |
| logout            | Clears cached credential state and ends the current session.                                      |

## logout

```swift
func logout()
```

Clears any cached authentication tokens and user-related state from the SDK.

**Parameters:** None

**Return Value:** None

**Usage Notes:**

* Call when the user signs out of your application or when session invalidation is required.
* After calling `logout()`, call `GoPayEnterpriseFactory.createEnterpriseSdk` again before making further SDK calls.

```swift
sdk.logout()
```