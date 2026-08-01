---
updatedAt: 2026-04-10T10:29:33.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Initialization

```kotlin
enum class GoPayEnterpriseEnvironment {
    STAGING, PRODUCTION
}

enum class GoPayEnterpriseLocale {
    id, en
}

@Parcelize
data class GoPayEnterpriseConfiguration(
    val clientID: String,
    val environment: GoPayEnterpriseEnvironment,
    val enableDebugLogs: Boolean = false,
    val additionalData: Map<String, String>? = null,
    val locale: GoPayEnterpriseLocale,
) : Parcelable

data class GoPayEnterpriseError(
    val code: String,
    val message: String,
    val title: String
)

interface GoPayEnterpriseCallbackDelegate {
    fun onDismiss()
    fun onFailure(error: GoPayEnterpriseError)
}

object GoPayEnterpriseFactory {
    fun createEnterpriseSdk(
        context: Context,
        configuration: GoPayEnterpriseConfiguration,
        callbackDelegate: GoPayEnterpriseCallbackDelegate
    ): GoPayEnterpriseSdk
}

interface GoPayEnterpriseSdk {
    fun getFeatureManager(): FeatureManager
    fun getKycManager(): KycManager
    fun logout()
}
```

# Specifications

## Enterprise Factory

```kotlin
object GoPayEnterpriseFactory {
    fun createEnterpriseSdk(
        context: Context,
        configuration: GoPayEnterpriseConfiguration,
        callbackDelegate: GoPayEnterpriseCallbackDelegate,
    ): GoPayEnterpriseSdk
}
```

### Description

Initializes the GoPay Enterprise SDK with the provided configuration and sets up a delegate to receive SDK events and responses.

### Parameters

| Parameter        | Type                            | Description                                                                                                                                                                    |
| :--------------- | :------------------------------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| context          | Context                         | Android application or activity context used for SDK initialization.                                                                                                           |
| configuration    | GoPayEnterpriseConfiguration    | The SDK configuration object contains clientID, environment, debug log settings, locale, and optional additionalData.                                                          |
| callbackDelegate | GoPayEnterpriseCallbackDelegate | An object conforming to the GoPayEnterpriseCallbackDelegate protocol, used to receive dismissal callback, and any top-level errors \[eg. initialization failure] from the SDK. |

### Return Value

Returns a `GoPayEnterpriseSdk` instance. Store this instance; it is the entry point for all subsequent SDK operations.

### Usage Notes

* Must be called once before invoking any other SDK method.
* If initialization fails (e.g. invalid clientID or configuration), `callbackDelegate.onFailure` will be triggered with a `GoPayEnterpriseError`.
* Ensure `enableDebugLogs` is set to `false` in production to avoid exposing sensitive information.
* The returned `GoPayEnterpriseSdk` instance is not thread-safe; access it from a single thread (typically the main thread).

### Example Usage

```kotlin
val configuration = GoPayEnterpriseConfiguration(
    clientID = "YOUR_CLIENT_ID",
    environment = GoPayEnterpriseEnvironment.STAGING,
    enableDebugLogs = true,
    locale = GoPayEnterpriseLocale.en,
)

val sdk = GoPayEnterpriseFactory.createEnterpriseSdk(
    context = applicationContext,
    configuration = configuration,
    callbackDelegate = object : GoPayEnterpriseCallbackDelegate {
        override fun onDismiss() {
            // Handle SDK dismissal
        }
        override fun onFailure(error: GoPayEnterpriseError) {
            // Handle initialization or runtime failure
        }
    }
)
```

### Field Reference

#### GoPayEnterpriseConfiguration

An object containing configuration parameters required to initialize the GoPay Enterprise SDK

| Parameters      | Type                       | Description                                                                                                                                 |
| :-------------- | :------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------ |
| clientID        | String                     | Unique identifier provided by GoPay as part of the SDK integration.                                                                         |
| environment     | GoPayEnterpriseEnvironment | Enum value that determines the environment (`STAGING` or `PRODUCTION`) where the SDK should operate.                                        |
| enableDebugLogs | Boolean                    | Enables or disables debug logging. Always set to `false` in production.                                                                     |
| locale          | GoPayEnterpriseLocale      | Sets the display language of SDK UI. Supported values: `GoPayEnterpriseLocale.en` (English), `GoPayEnterpriseLocale.id` (Bahasa Indonesia). |
| additionalData  | Map\<String, String>?      | Optional. Key-value pairs forwarded to the backend for validations or security enhancements. Pass `null` if not required.                   |

#### GoPayEnterpriseCallbackDelegate

A protocol/interface that must be implemented by the integrating application to receive SDK lifecycle and error callbacks.

| Interface function | Function description                                                                                           |
| :----------------- | :------------------------------------------------------------------------------------------------------------- |
| onDismiss()        | Whenever the SDK gets closed or removed, this will get called.                                                 |
| onFailure()        | When we are unable to launch the feature we will send this callback, with the respective GoPayEnterpriseError. |

#### GoPayEnterpriseError

Represents an error returned by the SDK.

| Field name | Type   | Description                                                                                    |
| :--------- | :----- | :--------------------------------------------------------------------------------------------- |
| code       | String | Enterprise Error constant specifying the exact error being observed during initialization etc. |
| message    | String | Localized Error message                                                                        |
| title      | String | Localized Error Title                                                                          |

#### GoPayEnterpriseError.code

For a complete list of error codes and their meanings, see the [Error Codes Reference](https://docs.midtrans.com/docs/gopayenterprise-error-codes).

#### GoPayEnterpriseSDK

`GoPayEnterpriseSdk` provides entry points for launching GoPay features, KYC verification, and session management in partner Android apps.

<br />

| Function Name     | Function Description                                                                                                      |
| :---------------- | :------------------------------------------------------------------------------------------------------------------------ |
| getFeatureManager | Returns a `FeatureManager` instance for launching the verify flow.                                                        |
| getKycManager     | Returns a `KycManager` instance exposing KTP scan, selfie liveness, selfie verification, and full KYC verification flows. |
| logout            | Logs out the current session and clears cached credential state.                                                          |

## logout

Clears any cached credential state from the SDK.

Parameters:
None

Return Value:
None

Usage Notes:

* Call when the user signs out of your application or when session invalidation is required.
* After calling `logout()`, you must re-initialize the SDK before making further calls.

```kotlin
sdk.logout()
```