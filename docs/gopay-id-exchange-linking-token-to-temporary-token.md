---
updatedAt: 2026-04-15T09:20:53.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Get Temporary Access Token 

Temporary Token is a token that can be used to invoke Verify with GoPay without user auth.

# Description

* This API allows Midtrans partners to exchange a user's GoPay payment linking token for a temporary token.
* The temporary token then can be used to initiate "Verify with Gopay" flow on behalf of the user, without asking the user to re-do the authentication process (Input Phone Number, OTP challenge, and Pin challenge).
* This is a backend-to-backend API. The caller must have a valid x-merchant-id, and must supply the user's GoPay payment linking token obtained from GoPay.

# Request

| Attribute | Value                                          |
| :-------- | :--------------------------------------------- |
| Method    | `GET`                                          |
| Path      | `/forward/gopay-id/identity/v1/gopay-id/token` |

## Request Headers

| Key             | Type     | Required? | Description                                                                       |
| :-------------- | :------- | :-------- | :-------------------------------------------------------------------------------- |
| `x-merchant-id` | `string` | YES       | Merchant identifier issued by Gopay.                                              |
| `authorization` | `string` | YES       | The user's Gopay payment linking token. Do not prefix with Bearer.                |
| `request-id`    | `string` | YES       | A unique ID for this request, used for distributed tracing. Recommended: UUID v4. |

# Response

## HTTP Status Codes

| HTTP Status                 | Scenario                                                                |
| :-------------------------- | :---------------------------------------------------------------------- |
| `200 OK`                    | Token exchange successful.                                              |
| `400 Bad Request`           | Missing or invalid request headers, or merchant not configured.         |
| `500 Internal Server Error` | Upstream service failure during token generation or account resolution. |
| `503 Service Unavailable`   | A dependency is temporarily unreachable.                                |

## Success Response

| Field        | Type      | Description                                                  |
| :----------- | :-------- | :----------------------------------------------------------- |
| `success`    | `boolean` | `true` on success.                                           |
| `data.token` | `string`  | Base64-encoded token. Pass this to the Gopay Enterprise SDK. |

## Error Responses

All error responses share the following structure:

| Field             | Type      | Description                                    |
| :---------------- | :-------- | :--------------------------------------------- |
| `success`         | `boolean` | `false` on error.                              |
| `errors[].code`   | `string`  | Machine-readable error code.                   |
| `errors[].entity` | `string`  | The field or resource related to the error.    |
| `errors[].cause`  | `string`  | Human-readable description of what went wrong. |

### Error Codes

| HTTP Code                     | **Code** | Cause                   |
| :---------------------------- | :------- | :---------------------- |
| `400 - Bad Request`           | `1539`   | Missing required header |
| `500 - Internal Server Error` | `900`    | Internal Server Error   |

<br />