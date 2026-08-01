---
updatedAt: 2026-06-10T10:01:28.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Integration Guide - Certificate Registration

This guide walks you through every step required to submit a Certificate Registration request using the Esign APIs. Follow the steps in order; each step depends on the output of the previous one.

***

## Prerequisites

Before you begin, ensure you have:

* `client-id` and `pass-key` credentials from the GoTo OneKYC team
* Your assigned `x-esign-onboarding-partner` identifier (e.g. `CLIENT_X-BE-CERT_REG`)
* HTTPS-capable server that can reach the Esign API base URLs
* A callback endpoint that can receive `POST` requests from the Esign platform (see [Handling Submission Results](https://docs.midtrans.com/docs/handling-submission-results))

***

## Common Request Headers

The following headers are required on every Esign API call (except authentication):

| Header                       | Description                                                        | Example                |
| ---------------------------- | ------------------------------------------------------------------ | ---------------------- |
| `x-onekyc-token`             | Partner token from Get Partner Token API                           | `eyJraWQiOiJlY...`     |
| `x-esign-onboarding-partner` | Identifies your integration (provided by OneKYC team)              | `CLIENT_X-BE-CERT_REG` |
| `x-partner-user-id`          | Your internal user identifier for the current user                 | `user-12345`           |
| `x-partner-user-id-type`     | The type/label of your user ID                                     | `CLIENT_X_USER_ID`     |
| `x-partner-session-id`       | A unique ID for this specific invocation (use a new UUID per call) | `session-abc-001`      |

***

## Step 1 — Get an Authentication Token

Generate a partner token that will authenticate all subsequent API calls.

> For detailed instructions, request/response examples, and token caching strategies, see [Getting Authentication Token](https://docs.midtrans.com/docs/getting-an-authentication-token).

You will pass this token as `x-onekyc-token` in all subsequent steps.

***

## Step 2 — Get Presigned Upload URLs

> API Reference: [Get Presigned URLs](https://docs.midtrans.com/reference/getpresignedurls-5)

Initiate a new Certificate Registration submission and receive pre-signed URLs for uploading the user's KTP and selfie images.

### Endpoint

```
GET /esign-partner/v1/submissions/urls?submissionType=CERT_REG
```

**Base URL:** `https://onekyc.ky.id.sandbox.gopayapi.com` (sandbox)

### Request

```bash
curl -X GET \
  "https://onekyc.ky.id.sandbox.gopayapi.com/esign-partner/v1/submissions/urls?submissionType=CERT_REG" \
  -H "x-onekyc-token: <TOKEN>" \
  -H "x-esign-onboarding-partner: CLIENT_X-BE-CERT_REG" \
  -H "x-partner-user-id: user-12345" \
  -H "x-partner-user-id-type: CLIENT_X_USER_ID" \
  -H "x-partner-session-id: session-abc-001"
```

### Query Parameters

| Parameter        | Type     | Required | Value                                           |
| ---------------- | -------- | -------- | ----------------------------------------------- |
| `submissionType` | `string` | ✅        | Must be `CERT_REG` for Certificate Registration |

### Success Response — `200 OK`

```json
{
  "success": true,
  "data": {
    "submissionId": "8a0aef3d-0e27-4a7e-a4ba-2e1b97bcb00c",
    "status": "INITIATED",
    "documents": {
      "KTP": {
        "documentUrl": "https://al-ky-id-s-esign-service.oss-ap-southeast-5.aliyuncs.com/CERT_REG/93134121-bc15-4796-a911-9257913f0020_KTP?...",
        "documentReference": "93134121-bc15-4796-a911-9257913f0020_KTP",
        "expiryInSeconds": "432000"
      },
      "SELFIE": {
        "documentUrl": "https://al-ky-id-s-esign-service.oss-ap-southeast-5.aliyuncs.com/CERT_REG/5e021eb4-d875-47bb-817b-8b1782f0c3bb_SELFIE?...",
        "documentReference": "5e021eb4-d875-47bb-817b-8b1782f0c3bb_SELFIE",
        "expiryInSeconds": "432000"
      }
    }
  }
}
```

| Field                          | Description                                                                    |
| ------------------------------ | ------------------------------------------------------------------------------ |
| `submissionId`                 | Unique ID for this submission — **save this**, you'll need it in Steps 4 and 6 |
| `status`                       | Will be `INITIATED` at this stage                                              |
| `documents.KTP.documentUrl`    | Presigned URL to upload the KTP image                                          |
| `documents.SELFIE.documentUrl` | Presigned URL to upload the selfie image                                       |
| `expiryInSeconds`              | Time (in seconds) before the presigned URL expires — `432000` = 5 days         |

> **Important:** Save the `submissionId` and both `documentUrl` values before proceeding.

***

## Step 3 — Upload KTP and Selfie Images

Upload the user's images directly to the pre-signed URLs received in Step 2. These are direct object storage uploads — **do not** call a platform API here, just `PUT` the file bytes to the URL.

### Upload KTP

```bash
curl -X PUT "<KTP_DOCUMENT_URL>" \
  -H "Content-Type: image/jpeg" \
  --data-binary @/path/to/ktp-image.jpg
```

### Upload Selfie

```bash
curl -X PUT "<SELFIE_DOCUMENT_URL>" \
  -H "Content-Type: image/jpeg" \
  --data-binary @/path/to/selfie-image.jpg
```

### Image Requirements

| Document | Format     | Notes                                                  |
| -------- | ---------- | ------------------------------------------------------ |
| KTP      | JPEG / PNG | Must be a clear photo of the user's physical eKTP card |
| Selfie   | JPEG / PNG | Clear frontal photo of the user's face                 |

> Both uploads must succeed before proceeding to Step 4. A `200` or `204` HTTP response from the presigned URL indicates a successful upload.

***

## Step 4 — Confirm Upload

> API Reference: [Confirm Upload](https://docs.midtrans.com/reference/confirmupload-5)

Once both images are uploaded, call the Confirm Upload API to provide the user's personal details and trigger asynchronous processing.

At least one of user's **addressable contact** is required to issue a certificate, it can be either `email`, `phoneNumber` or both.

And in the case of `Partial RA` integration, whichever **addressable contact** provided to us has to already be verified by you.

### Endpoint

```
PUT /esign-partner/v1/submissions/urls
```

### Request

```json Partial RA with Verified Email
curl -X PUT \
  "https://onekyc.ky.id.sandbox.gopayapi.com/esign-partner/v1/submissions/urls" \
  -H "x-onekyc-token: <TOKEN>" \
  -H "x-esign-onboarding-partner: CLIENT_X-BE-CERT_REG" \
  -H "x-partner-user-id: user-12345" \
  -H "x-partner-user-id-type: CLIENT_X_USER_ID" \
  -H "x-partner-session-id: session-abc-002" \
  -H "Content-Type: application/json" \
  -d '{
    "submissionId": "8a0aef3d-0e27-4a7e-a4ba-2e1b97bcb00c",
    "metadata": {
      "userDetails": {
        "name": "John Doe",
        "nik": 3187888902845410,
        "dateOfBirth": "07-03-1980",
        "email": "johndoe@example.com",
        "dataVerification": {
          "email": {
            "isVerified": true,
            "verificationReferenceId": "5fb51cca-6d64-49bb-a67a-f3ceaad1a913"
          }
        }
      },
      "userLocale": "en_ID",
      "consentData": [
        {
          "entity": "Digi",
          "consentType": "termsAndConditions",
          "consentGiven": true,
          "details": {
            "en_ID": {
              "url": "https://www.digi.com/termsAndConditions?version=v1.0.0",
              "text": "terms and conditions"
            },
            "id_ID": {
              "url": "https://www.digi.com/termsAndConditions?version=v1.0.0",
              "text": "terms and conditions"
            }
          },
          "timeStamp": 1725603017,
          "additionalDetails": {
            "userAgent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36",
            "userIp": "172.217.22.14",
            "deviceDetails": {
              "os": "R",
              "make": "google",
              "model": "KB2001",
              "uniqueId": "AF7KI0bly3aPIsYJ4+O+2QE",
              "networkProvider": "XL Axiata",
              "appId": "gojek",
              "appVersion": "4.96.0"
            }
          }
        }
      ],
      "additionalData": {}
    }
  }'
```
```json Partial RA with Verified Phone
curl -X PUT \
  "https://onekyc.ky.id.staging.gopayapi.com/esign-partner/v1/submissions/urls" \
  -H "x-onekyc-token: <TOKEN>" \
  -H "x-esign-onboarding-partner: CLIENT_X-BE-CERT_REG" \
  -H "x-partner-user-id: user-12345" \
  -H "x-partner-user-id-type: CLIENT_X_USER_ID" \
  -H "x-partner-session-id: session-abc-002" \
  -H "Content-Type: application/json" \
  -d '{
    "submissionId": "8a0aef3d-0e27-4a7e-a4ba-2e1b97bcb00c",
    "metadata": {
      "userDetails": {
        "name": "John Doe",
        "nik": 3187888902845410,
        "dateOfBirth": "07-03-1980",
        "phoneNumber": "62888675678910",
        "dataVerification": {
          "phoneNumber": {
            "isVerified": true,
            "verificationReferenceId": "5fb51cca-6d64-49bb-a67a-f3ceaad1a913"
          }
        }
      },
      "userLocale": "en_ID",
      "consentData": [
        {
          "entity": "Digi",
          "consentType": "termsAndConditions",
          "consentGiven": true,
          "details": {
            "en_ID": {
              "url": "https://www.digi.com/termsAndConditions?version=v1.0.0",
              "text": "terms and conditions"
            },
            "id_ID": {
              "url": "https://www.digi.com/termsAndConditions?version=v1.0.0",
              "text": "terms and conditions"
            }
          },
          "timeStamp": 1725603017,
          "additionalDetails": {
            "userAgent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36",
            "userIp": "172.217.22.14",
            "deviceDetails": {
              "os": "R",
              "make": "google",
              "model": "KB2001",
              "uniqueId": "AF7KI0bly3aPIsYJ4+O+2QE",
              "networkProvider": "XL Axiata",
              "appId": "gojek",
              "appVersion": "4.96.0"
            }
          }
        }
      ],
      "additionalData": {}
    }
  }'
```

### Key Request Fields

**Required fields in the request body:**

* `submissionId` — The submission ID from Step 2
* `metadata.userDetails.name` — Full name (must match KTP)
* `metadata.userDetails.nik` — 16-digit National ID number
* `metadata.userDetails.dateOfBirth` — Format: `DD-MM-YYYY`
* `metadata.userDetails.email` — User's email address (required if `phoneNumber` is not available)
* `metadata.userDetails.phoneNumber` — Phone in international format e.g., `628xxx` (required if `email` is not available)
* `metadata.userDetails.dataVerification` — Email and phone verification status with your reference IDs
* `metadata.consentData` — User's consent to terms and conditions with timestamp and device details

For a complete list of all available fields and their descriptions, refer to the [Confirm Upload API documentation](https://docs.midtrans.com/reference/confirmupload-5).

### Success Response — `200 OK`

```json
{
  "success": true,
  "data": {
    "submissionId": "8a0aef3d-0e27-4a7e-a4ba-2e1b97bcb00c"
  }
}
```

After receiving this response, the submission enters asynchronous processing. You do **not** need to poll immediately — wait for a callback (Step 5).

***

## Step 5 — Receive the Callback

Once the Esign platform finishes processing the submission, it sends a `POST` request to your registered callback endpoint with the result.

You do not need to do anything to trigger this — it happens automatically after Step 4.

> See [Handling Submission Results](https://docs.midtrans.com/docs/handling-submission-results) for the full callback body structure and how to interpret every outcome.

***

## Step 6 — Poll Submission Status (Fallback)

> API Reference: [Get Submission Details](https://docs.midtrans.com/reference/getsubmissiondetails)

If a callback is not received within the expected window (e.g. due to network issues on your endpoint), you can query the submission status directly.

### Endpoint

```
GET /esign-partner/v1/submissions
```

### Request

```bash
curl -X GET \
  "https://onekyc.ky.id.sandbox.gopayapi.com/esign-partner/v1/submissions" \
  -H "x-onekyc-token: <TOKEN>" \
  -H "x-partner-user-id: user-12345" \
  -H "x-partner-user-id-type: CLIENT_X_USER_ID" \
  -H "x-partner-session-id: session-abc-003"
```

> Note: `x-esign-onboarding-partner` is **not** required for this endpoint.

### Success Response — `200 OK`

```json
{
  "success": true,
  "data": {
    "submissionId": "d208917d-84a1-4edc-98b0-af2c2f4fcf5e",
    "userId": "user-12345",
    "userIdType": "CLIENT_X_USER_ID",
    "partnerSessionId": "session-abc-001",
    "status": "COMPLETED",
    "result": "VALID",
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
}
```

> For a full explanation of `status`, `result`, and `reasonCode` values, see [Handling Submission Results](https://docs.midtrans.com/docs/handling-submission-results).

***

## Full Integration Flow Summary

```
Step 1 → GET  /v1/esign/partner/authentication           → obtain token
Step 2 → GET  /esign-partner/v1/submissions/urls         → obtain submissionId + presigned URLs
Step 3 → PUT  <presigned KTP URL>                        → upload KTP image
Step 3 → PUT  <presigned Selfie URL>                     → upload Selfie image
Step 4 → PUT  /esign-partner/v1/submissions/urls         → confirm upload + provide user details
Step 5 ← POST <your callback endpoint>                   ← receive async result
Step 6 → GET  /esign-partner/v1/submissions              → (fallback) poll for result
```

<br />