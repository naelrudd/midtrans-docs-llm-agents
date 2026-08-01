---
updatedAt: 2026-04-10T10:34:05.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Error Codes

# GoPayEnterpriseError

Represents an error returned by the SDK.

| Field name | Type   | Description                                                                                    |
| :--------- | :----- | :--------------------------------------------------------------------------------------------- |
| code       | String | Enterprise Error constant specifying the exact error being observed during initialization etc. |
| message    | String | Localized Error message                                                                        |
| title      | String | Localized Error Title                                                                          |

| Value    | Description                                                                                   | Retriable | Action by Client                                                                                                                                                                       |
| :------- | :-------------------------------------------------------------------------------------------- | :-------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GPE-2201 | The SDK configuration is invalid or missing required fields.                                  |     No    | Ensure `GoPayEnterpriseConfig` is properly configured before initializing the SDK.                                                                                                     |
| GPE-2202 | The token passed by the client is expired or unauthorized.                                    |    Yes    | Refresh the token on your backend and retry the flow with an updated `token`.                                                                                                          |
| GPE-2203 | There was a connection error while connecting to the network service.                         |    Yes    | **KYC flow:** Retry the flow; if the issue persists, check the device's network connectivity. **Other flows:** Not required — the SDK already shows a dialog. No client action needed. |
| GPE-2204 | Feature is not whitelisted.                                                                   |     No    | Contact the GoPay team to verify feature entitlements for your `clientID`.                                                                                                             |
| GPE-2205 | Unknown error.                                                                                |     No    | Report the full `GoPayEnterpriseError` (`code`, `title`, `message`) to the GoPay team.                                                                                                 |
| GPE-2206 | The request is missing required fields (`requestId` or `userCorrelationId`).                  |     No    | Ensure both fields are non-blank before calling `verify()`.                                                                                                                            |
| GPE-2207 | User cancelled or dropped out of the flow.                                                    |    Yes    | **KYC flow:** Prompt the user to restart the flow if needed. **Other flows:** No action required.                                                                                      |
| GPE-2208 | Credential exchange failed. The exchange handler returned `ExchangeResult.Failure`.           |     No    | Check `error.message` for the reason string from `ExchangeResult.Failure`; fix the backend exchange.                                                                                   |
| GPE-2209 | Credential exchange timed out. The exchange handler did not return within the allowed time.   |    Yes    | Ensure the exchange handler completes promptly; check for network or backend latency.                                                                                                  |
| GPE-2210 | Camera is unavailable or could not be accessed during the flow (e.g. KYC document scan).      |    Yes    | Prompt the user to check camera availability and retry the flow.                                                                                                                       |
| GPE-2211 | A required permission was denied by the user (e.g. camera during KYC).                        |    Yes    | Prompt the user to grant the required permission in device settings and retry the flow.                                                                                                |
| GPE-2212 | The verification process failed (e.g. liveness or document check failed during KYC).          |    Yes    | Prompt the user to retry the flow.                                                                                                                                                     |
| GPE-2213 | User navigated away from the flow by tapping the Help button (e.g. during KYC).               |    Yes    | No action required; the user chose to exit the flow voluntarily.                                                                                                                       |
| GPE-2214 | A security check failed during the flow (e.g. rooted or tampered device detected during KYC). |     No    | No action required — the SDK blocks the flow on unsupported devices.                                                                                                                   |
| GPE-2215 | An API error occurred during a network request in the flow (e.g. during KYC).                 |    Yes    | Retry the flow; if the issue persists, report the `GoPayEnterpriseError` to the GoPay team.                                                                                            |