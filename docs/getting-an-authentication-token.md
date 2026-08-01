---
updatedAt: 2026-06-10T09:59:28.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Getting Authentication Token

All Esign API calls (except this one) require a valid **OneKYC partner token** passed in the `x-onekyc-token` request header. This page explains how to generate that token.

***

## Prerequisites

You must have received the following credentials from the GoTo OneKYC team during onboarding:

| Credential  | Description                                 |
| ----------- | ------------------------------------------- |
| `client-id` | Your unique partner client ID (UUID format) |
| `pass-key`  | Your secret pass key (UUID format)          |

Keep these credentials **server-side only**. Never expose them in client-side code or public repositories.

***

## API Reference

> Full API spec: [Get Partner Token](https://docs.midtrans.com/reference/getpartnertoken)

### Endpoint

```
GET /v1/esign/partner/authentication
```

### Base URLs

| Environment | Base URL                                    |
| ----------- | ------------------------------------------- |
| Sandbox     | `https://onekyc-token.sandbox.gopayapi.com` |
| Production  | `https://onekyc-token.ky.id.gopayapi.com`   |

> Note: The authentication endpoint uses a **different base URL** from the rest of the Esign APIs.

### Request Headers

| Header      | Type            | Required | Description                          |
| ----------- | --------------- | -------- | ------------------------------------ |
| `client-id` | `string (uuid)` | ✅        | Client ID provided during onboarding |
| `pass-key`  | `string (uuid)` | ✅        | Pass key provided during onboarding  |

### Example Request

```bash
curl -X GET "https://onekyc-token.sandbox.gopayapi.com/v1/esign/partner/authentication" \
  -H "client-id: b31fa508-331c-4e9e-9a60-b0f28c3f7e13" \
  -H "pass-key: 2c7b2893-e49f-4cf3-89e6-1b9c5bf0500b"
```

### Success Response — `200 OK`

```json
{
  "success": true,
  "data": {
    "token": "eyJraWQiOiJlY8sLk182F3J4wNDkwLTQxODgtYTRjZ.....",
    "expiry_seconds": "1800",
    "expires_at": "1783336059"
  }
}
```

| Field            | Description                                                              |
| ---------------- | ------------------------------------------------------------------------ |
| `token`          | The partner token to include as `x-onekyc-token` in subsequent API calls |
| `expiry_seconds` | How long the token is valid, in seconds (default: `1800` = 30 minutes)   |
| `expires_at`     | Unix epoch timestamp when the token expires                              |

### Error Responses

`400 Bad Request`**&#x20;— Missing headers**

```json
{
  "success": false,
  "errors": [
    { "code": "1650", "cause": "MISSING_CLIENT_ID" },
    { "code": "1650", "cause": "MISSING_PASS_KEY" }
  ]
}
```

`401 Unauthorized`**&#x20;— Invalid credentials**

```json
{
  "success": false,
  "errors": [
    { "code": "110", "cause": "UNAUTHORIZED" }
  ]
}
```

***

## Token Lifecycle and Caching

* Tokens are valid for **30 minutes** by default (`expiry_seconds: 1800`).
* You should **cache the token** on your server and reuse it for multiple API calls within its validity window.
* Regenerate the token proactively **before it expires** to avoid disruption. A good strategy is to refresh when less than 5 minutes remain (i.e., when the current time is greater than `expires_at - 300`).
* Do **not** generate a new token on every API call — this is unnecessary and may result in rate limiting.

***

## Using the Token

Once obtained, include the token in the `x-onekyc-token` header of every subsequent Esign API call:

```bash
curl -X GET "https://onekyc.ky.id.sandbox.gopayapi.com/esign-partner/v1/submissions/urls" \
  -H "x-onekyc-token: eyJraWQiOiJlY8sLk182F3J4..." \
  -H "x-esign-onboarding-partner: CLIENT_X-BE-CERT_REG" \
  -H "x-partner-user-id: user-12345" \
  -H "x-partner-user-id-type: CLIENT_X_USER_ID" \
  -H "x-partner-session-id: session-abc-001"
```

<br />