---
updatedAt: 2026-05-18T11:55:54.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Access Token API

> 📘 BI-SNAP Compliance
>
> This page describes the Access Token API, which implements the BI-SNAP "Komponen Server Authorization dan Authentication Method." Midtrans acts as the authorization server implementing OAuth 2.0 (RFC 6749), issuing access tokens as Bearer tokens (RFC 6750).

<br />

Access Token API is an API call that can be used to acquire B2B access token from Midtrans. This access token will be used for client-level verification and subsequent Transactional API such as initiating payment, refund, and cancel.

## OAuth 2.0 Authorization Model

The BI-SNAP Access Token API follows the **OAuth 2.0 Client Credentials** grant type (RFC 6749 §4.4):

* **Grant type**: `client_credentials` — the merchant authenticates using its own credentials (Client ID + asymmetric signature) rather than on behalf of a resource owner
* **Token type**: `Bearer` (RFC 6750) — the issued access token is included as a `Bearer` token in the `Authorization` header of all subsequent Transactional API calls
* **Token lifetime**: 900 seconds (15 minutes) by default. After expiry, the merchant must request a new token.
* **Signature method**: The merchant proves its identity by signing the request with its **private key** using **SHA256withRSA**. Midtrans verifies the signature using the merchant's registered **public key**.

| Path              | /\{version}/access-token/b2b |
| :---------------- | :--------------------------- |
| HTTP Method       | POST                         |
| Version           | v1.0                         |
| SNAP service code | 73                           |

<br />

## Request Header

| Field Name   | Field Type | Mandatory | Field Description                                                  |
| :----------- | :--------- | :-------- | :----------------------------------------------------------------- |
| Content-type | String     | M         | Media type of the resource, i.e. application/json                  |
| X-TIMESTAMP  | String     | M         | Client’s current local time in ISO-8601 format                     |
| X-SIGNATURE  | String     | M         | Created using asymmetric signature SHA256withRSA algorithm         |
| X-CLIENT-KEY | String     | M         | Client’s client\_id (given at the completion registration process) |

```
Content-type: application/json
X-TIMESTAMP: 2030-01-01T00:00:00+07:00
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
X-CLIENT-KEY: 962489e9-de5d-4eb7-92a4-b07d44d64bf4
```

<br />

## Request Body

| Field Name | Field Type | Mandatory | Field Description                                                                                                                                                                                                                                          |
| :--------- | :--------- | :-------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| grantType  | String     | M         | `client_credentials`: The client can request an access token using only its client credentials (or other supported means of authentication) when the client is requesting access to the protected resources under its control (OAuth 2.0: RFC 6749 & 6750) |

```
{
   "grantType":"client_credentials"
}
```

<br />

## Response Header

| Field Name   | Field Type | Mandatory | Field Description                                 |
| :----------- | :--------- | :-------- | :------------------------------------------------ |
| Content-type | String     | M         | Media type of the resource, i.e. application/json |
| X-TIMESTAMP  | String     | M         | Client’s current local time in ISO-8601 format    |

```
Content-type: application/json
X-TIMESTAMP: 2030-01-01T00:00:00+07:00
```

<br />

## Response Body

| Field Name      | Field Type    | Mandatory | Field Description                                                                                                                                                                                                      |
| :-------------- | :------------ | :-------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| responseCode    | String(7)     | M         | Error code to specify the error returned.                                                                                                                                                                              |
| responseMessage | String (150)  | M         | Debug message to provide more information.                                                                                                                                                                             |
| accessToken     | String (2048) | C         | A string representing an authorization issued to the client that used to access protected resources. <br /><br /> *Will only be returned if API call is successful.*                                                   |
| tokenType       | String        | C         | The access token type provides the client with the information required to successfully utilize the access token to make a protected resource request. <br /><br /> *Will only be returned if API call is successful.* |
| expiresIn       | String        | C         | Time duration when the accessToken will expire. (default = 900 second). <br /><br /> *Will only be returned if API call is successful.*                                                                                |
| referenceNo     | String        | C         | Debug ID to provide more information. <br /><br /> *Will only be returned if API call is failure.*                                                                                                                     |

```Text Successful Response
{
   "responseCode":"2007300",
   "responseMessage":"Successful",
  "accessToken":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIyMTFlZThiMi1hN2FlLTRhZGUtYmJlYS1mNzI3MDk3ZmQ0NmEiLCJjbGllbnRJZCI6IjZhZTk1N2M0LTI4NjMtNDcxMy1hY2NlLWJhMTJkZTYzNmNmYyIsIm5iZiI6MTYxMTQ2ODk3OCwiZXhwIjoxNjExNDY5ODc4LCJpYXQiOjE2MTE0Njg5Nzh9.KM7yz9GvuUaDR1bXwei4iO0h4e3g4o1Hct5Ie9VoBdo",
   "tokenType":"Bearer",
   "expiresIn":"900"
}
```
```Text Error Response
{
   "responseCode":"5007300",
   "responseMessage":"Internal Server Error",
   "referenceNo":"19352694-0ef6-4439-8ad1-b1dfb8bbb85f"
}
```

<br />

### List of Response Code

| Response Code | HTTP Status Code | Response Message       |
| :------------ | :--------------- | :--------------------- |
| 2007300       | 200              | Success                |
| 4017300       | 401              | Unauthorized Signature |
| 5007300       | 500              | Internal Server Error  |

<br />

***

<br />

## B2B Access Token Header Structure (ASPI Mapping)

The following table maps the Access Token API header fields to ASPI's "Komponen Struktur Format Header – Access Token (B2B)" specification:

| Header Field   | ASPI Component    | Format / Value                         | Required  | Description                                                                                                                          |
| :------------- | :---------------- | :------------------------------------- | :-------- | :----------------------------------------------------------------------------------------------------------------------------------- |
| `Content-Type` | Content-Type      | `application/json`                     | Mandatory | Media type of the request body                                                                                                       |
| `X-TIMESTAMP`  | Timestamp         | ISO-8601: `YYYY-MM-DDTHH:MM:SS±HH:MM`  | Mandatory | Merchant's current local time. Used in signature generation and for request freshness validation.                                    |
| `X-CLIENT-KEY` | Client ID         | String (provided by Midtrans)          | Mandatory | Identifies the merchant. Corresponds to the `clientId` issued during credential exchange.                                            |
| `X-SIGNATURE`  | Digital Signature | Base64-encoded SHA256withRSA signature | Mandatory | **StringToSign**: `X-CLIENT-KEY + "\|" + X-TIMESTAMP`<br />**Algorithm**: SHA256withRSA<br />**Signing key**: Merchant's private key |

<br />

### Request Body Fields (B2B)

| Field       | ASPI Component | Value                  | Required  | Description                            |
| :---------- | :------------- | :--------------------- | :-------- | :------------------------------------- |
| `grantType` | Grant Type     | `"client_credentials"` | Mandatory | OAuth 2.0 grant type per RFC 6749 §4.4 |

<br />

### Sample Request (B2B)

```text
POST /v1.0/access-token/b2b HTTP/1.1
Host: merchants.midtrans.com
Content-Type: application/json
X-TIMESTAMP: 2024-03-15T10:30:00+07:00
X-CLIENT-KEY: G1234325-SNAP
X-SIGNATURE: iv5YorKVVFOFS59l0HChDvPe+HeoE/jY5CfVgCg5i16nj5/DVnKg49ilkv8PyeU7...

{
  "grantType": "client_credentials"
}
```

### Sample Successful Response

```json
{
  "responseCode": "2007300",
  "responseMessage": "Successful",
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "tokenType": "Bearer",
  "expiresIn": "900"
}
```

<br />

> 📘 Compliance Note
>
> This Access Token API implementation satisfies the BI-SNAP "Server Authorization dan Authentication Method" component. The asymmetric signature (SHA256withRSA) ensures non-repudiation — only the holder of the merchant's private key can generate a valid signature, and Midtrans verifies it using the merchant's registered public key.

<br />

***

<br />

## Related Pages

* **[Signature Generation](/reference/signature-generation)** — Step-by-step signature generation examples for both Access Token and Transactional APIs
* **[Security Specification](/reference/security-specification)** — Encryption standards, TLS, key management lifecycle
* **[Credential Exchange](/reference/credential-exchange-copy)** — How to generate keys and register with Midtrans