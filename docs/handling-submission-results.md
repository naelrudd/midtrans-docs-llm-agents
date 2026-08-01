---
updatedAt: 2026-06-10T10:01:43.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Handling Submission Results

After you call Confirm Upload, the Esign platform processes the submission asynchronously. The result is delivered to you in two ways:

1. **Callback** (primary) — an HTTP request sent to your registered endpoint
2. **Poll** (fallback) — call the Get Submission Details API yourself

This page explains how to set up callbacks, interpret the result, and handle errors.

***

## Setting Up Callbacks

To receive submission results automatically, you need to provide the Esign team with the following information:

| Item                | Description                                        | Example                                         |
| ------------------- | -------------------------------------------------- | ----------------------------------------------- |
| **Endpoint URL**    | HTTPS URL where we will send the callback          | `https://api.yourcompany.com/v1/esign/callback` |
| **HTTP Method**     | POST, PUT, or PATCH                                | `POST`                                          |
| **Authentication**  | (Optional) Basic Auth, Bearer Token, API Key, etc. | `Bearer YOUR_TOKEN`                             |
| **IP Whitelisting** | (Optional) Whitelist our callback server IPs       | We'll provide the IP list                       |

Once you share these details, the Esign team will configure callbacks in their system. Your endpoint should:

1. Accept the configured callback HTTP method (`POST`, `PUT`, or `PATCH`)
2. Respond with `200 OK` immediately (within a few seconds)
3. Process the submission result asynchronously in the background
4. Use `submissionId` as an idempotency key to avoid duplicate processing

***

## Callback

The Esign platform sends an HTTP callback request to your registered callback URL once processing is complete.

### Callback Request Format

* **Method:** Configurable (`POST`, `PUT`, or `PATCH`) based on your callback setup
* **Content-Type:** `application/json`
* **Body:** JSON payload containing submission result data

### Callback Examples

```json User Verification Done
{
  "submissionId": "d208917d-84a1-4edc-98b0-af2c2f4fcf5e",
  "userId": "user-12345",
  "userIdType": "CLIENT_X_USER_ID",
  "partnerSessionId": "session-abc-001",
  "status": "PARTIALLY_COMPLETED",
  "result": "VALID",
  "processedAt": "2026-05-08T10:30:00Z",
  "submissionDetails": {
    "verificationResult": {
      "nik": "PASS",
      "name": "PASS",
      "dateOfBirth": "PASS",
      "selfie": "PASS"
    },
    "eligibleToActivate": false,
    "onboardingCode": "NEW_USER",
    "shouldSkipActivation": true
  }
}
```
```json Completed
{
  "submissionId": "d208917d-84a1-4edc-98b0-af2c2f4fcf5e",
  "userId": "user-12345",
  "userIdType": "CLIENT_X_USER_ID",
  "partnerSessionId": "session-abc-001",
  "status": "COMPLETED",
  "result": "VALID",
  "processedAt": "2026-05-08T10:30:00Z",
  "submissionDetails": {
    "verificationResult": {
      "nik": "PASS",
      "name": "PASS",
      "dateOfBirth": "PASS",
      "selfie": "PASS"
    },
    "registrationId": "6dab7f08-0dcb-4852-8459-59cb7c25f4dc",
    "eligibleToActivate": false,
    "onboardingCode": "NEW_USER",
    "shouldSkipActivation": true
  }
}
```
```json Rejected
{
  "submissionId": "d208917d-84a1-4edc-98b0-af2c2f4fcf5e",
  "userId": "user-12345",
  "userIdType": "CLIENT_X_USER_ID",
  "partnerSessionId": "session-abc-001",
  "status": "COMPLETED",
  "result": "INVALID",
  "processedAt": "2026-05-08T10:30:00Z",
  "submissionDetails": {
    "verificationResult": {
      "nik": "PASS",
      "name": "PASS",
      "dateOfBirth": "PASS",
      "selfie": "FAIL"
    },
    "eligibleToActivate": false,
    "onboardingCode": "NEW_USER",
    "shouldSkipActivation": true
  }
}
```

<br />

***

## Understanding `status` and `result`

The two fields you should always evaluate together are `status` and `result`.

| `status`              | `result`  | Meaning                                                                                         | Action                                                                                  |
| --------------------- | --------- | ----------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `COMPLETED`           | `VALID`   | ✅ **Approved.** User passed verification and certificate has been generated.                    | Mark user as registered. Proceed to document signing if needed.                         |
| `PARTIALLY_COMPLETED` | `VALID`   | ⏳ **In progress.** User passed verification and certificate is being generated (not yet ready). | Wait for a follow-up `COMPLETED` + `VALID` callback before marking as fully registered. |
| `COMPLETED`           | `INVALID` | ❌ **Rejected.** User did not pass verification.                                                 | Inform the user with a reason. Check `reasonCode` for the specific cause.               |
| `ERROR`               | *(any)*   | 🔴 **System error.** Processing failed due to an unexpected issue.                              | Check `reasonCode`. Retry the submission or contact support if the issue persists.      |

***

## Rejection Reason Codes

When `result` is `INVALID` or `status` is `ERROR`, check the `reasonCode` field for the specific cause.

| `reasonCode`            | Description                                                                                                     |
| ----------------------- | --------------------------------------------------------------------------------------------------------------- |
| `DUKCAPIL_REJECTED`     | The user's identity data (name, NIK, date of birth) does not match records in the Dukcapil government database. |
| `DUKCAPIL_SYSTEM_ERROR` | Dukcapil could not process the request with the given data (e.g. data format issues).                           |
| `EMAIL_HAS_BEEN_USED`   | The email address is already associated with a different user or NIK in the system.                             |
| `PHONE_HAS_BEEN_USED`   | The phone number is already associated with a different user or NIK in the system.                              |
| `SYSTEM_ERROR`          | An internal system error occurred during processing.                                                            |

***

## Key Fields in the Submission Result

When evaluating the callback or polling result, focus on these important fields:

| Field                                         | Values                                                                                                                  | What It Means                                                               |
| --------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| `status`                                      | `COMPLETED`, `PARTIALLY_COMPLETED`, `ERROR`                                                                             | Overall status of the submission                                            |
| `result`                                      | `VALID`, `INVALID`                                                                                                      | Verification outcome (if applicable)                                        |
| `reasonCode`                                  | (see [Rejection Reason Codes ](https://docs.midtrans.com/docs/handling-submission-results#rejection-reason-codes)above) | Why the submission failed (if `result` is `INVALID` or `status` is `ERROR`) |
| `submissionDetails.verificationResult.nik`    | `PASS` / `FAIL`                                                                                                         | Whether the NIK passed verification                                         |
| `submissionDetails.verificationResult.selfie` | `PASS` / `FAIL`                                                                                                         | Whether the selfie face-matched the KTP                                     |
| `submissionDetails.registrationId`            | UUID                                                                                                                    | Certificate registration ID — present when verification passed              |

For a complete list of all fields in the submission result, refer to the [Get Submission Details API documentation](https://docs.midtrans.com/reference/getsubmissiondetails).

***

## Handling Callbacks Reliably

### Respond Promptly

Return an HTTP `200 OK` response to the callback as quickly as possible (before doing heavy processing). If the platform does not receive a `2xx` response within the timeout window, it may retry.

```
POST /your-callback-endpoint  ←── platform sends this
200 OK                        ──→ respond immediately
// process the result async in background
```

### Idempotency

Callbacks may occasionally be delivered more than once. Use the `submissionId` as an idempotency key to avoid processing the same result twice:

```
if submission[submissionId].alreadyProcessed:
    return 200 OK  // acknowledge but skip processing
```

### Fallback Polling

If you haven't received a callback within a reasonable window (e.g. 10 minutes after calling Confirm Upload), poll the status using the Get Submission Details API:

```bash
curl -X GET \
  "https://onekyc.ky.id.sandbox.gopayapi.com/esign-partner/v1/submissions" \
  -H "x-onekyc-token: <TOKEN>" \
  -H "x-partner-user-id: user-12345" \
  -H "x-partner-user-id-type: CLIENT_X_USER_ID" \
  -H "x-partner-session-id: session-fallback-001"
```

> Full request/response details: [Integration Guide — Step 6](https://docs.midtrans.com/docs/integration-guide-1#step-6--poll-submission-status-fallback)

***

## Decision Flow for Your Application

```
Receive callback (or poll result)
        │
        ├── status = COMPLETED, result = VALID
        │       └── ✅ Certificate ready → proceed with user activation / signing
        │
        ├── status = PARTIALLY_COMPLETED, result = VALID
        │       └── ⏳ Wait for follow-up COMPLETED callback
        │
        ├── status = COMPLETED, result = INVALID
        │       └── ❌ Check reasonCode → show user-friendly rejection message
        │               ├── DUKCAPIL_REJECTED → identity mismatch
        │               ├── DUKCAPIL_IRRETRIEVABLE_ERROR → ask user to retry
        │               ├── EMAIL_HAS_BEEN_USED → prompt different email
        │               └── PHONE_HAS_BEEN_USED → prompt different phone
        │
        └── status = ERROR
                └── 🔴 Log reasonCode → retry or escalate to support
```

<br />