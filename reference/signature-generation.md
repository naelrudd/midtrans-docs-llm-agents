---
updatedAt: 2026-04-22T15:46:03.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Signature Generation

> 📘 BI-SNAP Compliance
>
> This page details the signature generation process for both Access Token and Transactional APIs, mapping to ASPI's "Komponen Struktur Format Header" specifications. It serves as evidence for BI-SNAP audit items on header structure and message signing.

<br />

# B2B Access Token Specification

B2B Access Token API header consists of the following fields:

| Field Name   | Field Type | Mandatory | Field Description                                              |
| :----------- | :--------- | :-------- | :------------------------------------------------------------- |
| Content-type | String     | M         | Media type of the resource, i.e. application/json              |
| X-TIMESTAMP  | String     | M         | Client’s current local time in ISO-8601 format                 |
| X-SIGNATURE  | String     | M         | Created using **asymmetric signature SHA256withRSA** algorithm |
| X-CLIENT-KEY | String     | M         | Client ID                                                      |

```
Content-type: application/json
X-TIMESTAMP: 2023-01-01T00:00:00+07:00
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
X-CLIENT-KEY: 962489e9-de5d-4eb7-92a4-b07d44d64bf4
```

<br />

## Asymmetric Signature SHA256withRSA

Based on the specification above, merchant should use asymmetric signature SHA256withRSA for Access Token API.

Merchant should use this formula to create X-SIGNATURE for Access Token API: <br /> **Client ID + “|” + Timestamp** encrypted with **merchant’s private key** by using SHA256withRSA algorithm

| SHA256withRSA algorithm reference                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 8afe58a2b2955453854b9f65d070a10ef3def877a813f8d8e427d58028398b5ea78f9fc35672a0e3d8a592ff0fc9e53bcb7f1aa478603be714aef91f52ce418430faf722e7ef1a7c87337d45c474503cb9fa70ab4371860954b3649be511737e4c1d23e10ea932c8ebab8f98468c836b899396c8c94d4f5a1a32d1141620638332310e71d752722e7a05c1b4bc4c9e5efeae26528ceba78f55c877bb3904859c9370bcc485ac3c80231a0e2b4219408958dbd3da0c815c5a847e449018e361f616bca325c3e935f79eadc6e48fd8ec04b577c2610a88da0dea580514b9394227039c0010ccbe39b3dd8461e0aa0cdb934c93b275a25b52a128d5dfd93d5341b5 |

For a better understanding, please refer to this sample scenario for generating signature using the formula above on B2B Access Token API:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        No.
      </th>

      <th>
        Steps
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        1
      </td>

      <td>
        Given merchant has private key <br /><br /> \-----BEGIN PRIVATE KEY-----\
        MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQCVZu2WHd4z5tbe\
        fkAWPjbB10Lgvu1CpsuIIVtO/wrrvKeD2LArmYSf5QxeJGG8HYlVYVp8I8/EVqay\
        JUbcyOd4aMLQFiCambDipecCfI7ecJ0K4+2ZneWOEq9JM91ZnGtwuLVdr1X/4/Nv\
        yGuNvmLAyfpJkU14yZliAUqJJ656jpM+WfY+hOpcLOzUe2wzx5RV7wYCyMl7/d1i\
        X33afJc6kbbUaA27yjlPdY6m0+DoZ0NNaRNZS7jzfJFtVXLTg/PgvwMNlMO/5Zyw\
        BWIOfWsD+MHUC6P9QYrHai8ZwEf9r+GivlNsAFs4NTpw9MdPngrexJm29k1Xh4UM\
        HV//jB1/AgMBAAECggEADcXGyitns/4oOauGyeYjUxw+eIxxP88zfRGiIralMZUb\
        Fi7wEpzc2oaZbMZK0jYg1mOanU4J1a4tQMfp7+l/WRzDNL6Nc+MOKN6lXJfR7dSQ\
        zZO0cBBbvIyhZwymb5/ZUbNdWM0UjvnbE6d0rsTpwp77+TMxYpynDJ9U2S70ySxe\
        fGi7x4rK02/8xmj1fY/Ls+uoYhF4IbGJIkFvrlAdWyFvv6sCGBYxl5sPuitgQxPv\
        Yc7dS7HE+6nZ+wWgoIXjC4CfxHBa9u3dfu3XAnPY3xpnVsbxCAH9OOIrZPY0C/Pq\
        gj+EElCBChUzDiedV3XipKUweDA+64sNm5NjqlqU8QKBgQDFf5a9vHVf9r2CTOgm\
        z5wTrK7aTwKwCNC4zpZUxDR8k7AV2gTelabpPWqUMZyRMUPs2hyBvhEWVNKxx3qs\
        7BAVpmcttuS5/dLNVdhNPUC2IgZqf3jWH2aS3lkci8DATQCphrEXZ3jrNaIRtrSC\
        kflE+yY8YP8b7ObktgvHz39JMQKBgQDBqCsMmOsQAveIQk5FGAMxsFU9G7OIBFHo\
        xpwkKUCjoqGxM+YQqDvcVeXNd/HdLnmR05//eoONemuDyYy8XRoud4tpaRKU/FK7\
        06WdljztB5rn2+cdUbmcU0fZiRQk+WuXsopZn3GUNvA/fQOW9qs7B5Rm5W71FeGk\
        ZgsvlAUlrwKBgQCUgFFaLWCcXa01UpqkxCp5aLi5EfvVXWuD6mKDLlzA51PZums6\
        6o/shO+kqoEtczu91mrk64NxpSof3vxRFdcqUEr4xrLJXx+oocnYmhwUVxU38s1r\
        Q4UfHe0nV7YBYmUDE3IJRRZY1aUdaKHmI9iok6e2csCfwMwEYRYOkekFoQKBgCyy\
        Oa1gpfA+Hw+N7i64ShRv1FyURi2Agb8uB9+4vbiG0rbpeZIioh5KnQ19P4+DKH/l\
        zinTBwXiWWpDXH4lJuPOp5ierbFBQ38ibDkg8dLrTG9zK7ZypFpWRmEI6GNYReLv\
        TEs/J6HDxFOC8Q8ow4COUUwmbCOY90lQXAiRK1b1AoGAScK1db9X5Ct+JtnjYyzi\
        GYLwyPhHCQIVmEDfuvbMs74woQsrBm3dBB3b2vf9pqcSZB4WAbTQ3wCdxCJKg6MN\
        6eXBO1M1lcIpZjCDyiXXi7PozNmkasRDUyDFwxlnyDLdRHL3FD+dh6do32FwGLBQ\
        u256RIyMB13qIuqrc91Z0hM=\
        \-----END PRIVATE KEY-----
      </td>
    </tr>

    <tr>
      <td>
        2
      </td>

      <td>
        Given merchant wants to create a request with header:\
        `Content-type: application/json`\
        `X-TIMESTAMP: 2023-07-31T07:10:00+07:00`\
        `X-CLIENT-KEY: G1234325-SNAP`
      </td>
    </tr>

    <tr>
      <td>
        3
      </td>

      <td>
        X-SIGNATURE value for encryption will be: <br /> `G1234325-SNAP\|2023-07-31T07:10:00+07:00`<br /><br /> \*same value as **X-CLIENT-KEY  + “|” +  X-TIMESTAMP**
      </td>
    </tr>

    <tr>
      <td>
        4
      </td>

      <td>
        By using merchant’s private key to encrypt the value with SHA256withRSA algorithm, merchant will generate <br /> `iv5YorKVVFOFS59l0HChDvPe+HeoE/jY5CfVgCg5i16nj5/DVnKg49ilkv8PyeU7y38apHhgO+cUrvkfUs5BhDD69yLn7xp8hzN9RcR0UDy5+nCrQ3GGCVSzZJvlEXN+TB0j4Q6pMsjrq4+YRoyDa4mTlsjJTU9aGjLRFBYgY4MyMQ5x11JyLnoFwbS8TJ5e/q4mUozrp49VyHe7OQSFnJNwvMSFrDyAIxoOK0IZQIlY29PaDIFcWoR+RJAY42H2FryjJcPpNfeercbkj9jsBLV3wmEKiNoN6lgFFLk5QicDnAAQzL45s92EYeCqDNuTTJOydaJbUqEo1d/ZPVNBtQ==`
      </td>
    </tr>

    <tr>
      <td>
        5
      </td>

      <td>
        Final result of merchant's header will be: <br /> `Content-type: application/json`\
        `X-TIMESTAMP: 2023-07-31T07:10:00+07:00`\
        `X-CLIENT-KEY: G1234325-SNAP`\
        `X-SIGNATURE: <SIGNATURE SAMPLE RESULT>`
      </td>
    </tr>
  </tbody>
</Table>

<br />

# Transactional API Specification

Transactional API header consists of the following fields. The table below maps each field to the ASPI "Komponen Struktur Format Header – Transaction (B2B)" specification:

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field Name
      </th>

      <th>
        Field Type
      </th>

      <th>
        Mandatory
      </th>

      <th>
        Field Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Content-type
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Media type of the resource, i.e. application/json
      </td>
    </tr>

    <tr>
      <td>
        X-TIMESTAMP
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Client’s current local time in ISO-8601 format
      </td>
    </tr>

    <tr>
      <td>
        X-SIGNATURE
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Created using **symmetric signature HMAC\_SHA512** algorithm
      </td>
    </tr>

    <tr>
      <td>
        Authorization
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Represents access\_token of a request, received from Access Token API response
      </td>
    </tr>

    <tr>
      <td>
        Authorization-Customer
      </td>

      <td>
        String
      </td>

      <td>
        C
      </td>

      <td>
        User Access Token which GoPay will be sharing once linking is complete.  <br />\
        *(Required only for GoPay Tokenization)*
      </td>
    </tr>

    <tr>
      <td>
        X-PARTNER-ID
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Merchant’s partner ID
      </td>
    </tr>

    <tr>
      <td>
        X-EXTERNAL-ID
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Merchant’s unique ID per transaction request
      </td>
    </tr>

    <tr>
      <td>
        CHANNEL-ID
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Mandatory field from Bank Indonesia that can take any value with correct format 5 digits numeric string
      </td>
    </tr>

    <tr>
      <td>
        X-DEVICE-ID
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Device identification on which the API services are currently being accessed by the end user (customer). <br /><vr />
        Sample:\
        Web Application:\
        Mozilla / 5.0(Windows NT 10.0; Win64; x64)AppleWebKit / 537.36(KHTML, like Gecko)Chrome / 75.0.3770.100 Safari / 537.36 OPR / 62.0.3331.99  <br />\
        Mobile Application:\
        Android: android-20013adf6cdd8123f\
        iOS: 72635bdfd223yvjm7246nsdj34hd4559393kjh42
      </td>
    </tr>
  </tbody>
</Table>

```
Content-type:application/json
X-TIMESTAMP:2020-01-01T00:00:00+07:00
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
Authorization: Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
Authorization-Customer: Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
X-PARTNER-ID: BMRI
X-DEVICE-ID: 0987ADCASA
X-EXTERNAL-ID:12345678901234567890
CHANNEL-ID:12345
```

> 📘 X-EXTERNAL-ID behavior
>
> Currently we have 2 usage for X-EXTERNAL-ID:
>
> **Usage #1: For account linking related endpoint (ie. get-auth, binding, unbinding),**
>
> * If merchant sends the same request with same X-EXTERNAL-ID, then Midtrans will return an error conflict (the duration is 24 hour after the first request)
>
> **Usage #2: For payment related endpoint (ie. direct debit, auth payment, etc)**
>
> * If merchant sends the same request with same X-EXTERNAL-ID and the previous response is success, then GoPay will return an idempotency response
>
> Things to note as well, in account linking flow, the external-id will need to be unique for each merchants, means different merchant can use the same X-EXTERNAL-ID to get different response from different request.

<br />

## Symmetric Signature HMAC\_SHA512

Based on the specification above, merchant should use symmetric signature HMAC\_SHA512 for Transactional API.

Merchant should use this formula to create X-SIGNATURE for Transactional API: <br /> **HTTPMethod +”:“+ EndpointUrl +":"+ AccessToken +":“+ Lowercase(HexEncode(SHA-256(minify(RequestBody))))+ ":“ + TimeStamp** encrypted with **merchant’s client secret** by using HMAC\_SHA512 algorithm.

| HMAC\_SHA512 algorithm reference                                                                                                 |
| :------------------------------------------------------------------------------------------------------------------------------- |
| 1529627511dee28c3daa9a4d89f19540d71dbfaee506380288fd011f2961f88297a387ecdab1da1ac14d518d0df2dd2b3e566ce2200700e0839259c271cc2e27 |

For a better understanding, please refer to this sample scenario for generating signature using the formula above on Transactional API:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        No.
      </th>

      <th>
        Steps
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        1
      </td>

      <td>
        Given merchant has client secret `fdppqbF5wq7vVegyvsV1CROMv646nJ7A`
      </td>
    </tr>

    <tr>
      <td>
        2
      </td>

      <td>
        Given merchant wants to create a request with header for POST **[https://api.midtrans.com/v1.0/registration-account-binding](https://api.midtrans.com/v1.0/registration-account-binding)**\
        `Content-type:application/json  `\
        `X-TIMESTAMP:2020-01-01T00:00:00+07:00`\
        `Authorization: Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a`\
        `X-PARTNER-ID: BMRI`\
        `X-DEVICE-ID: 0987ADCASA`\
        `X-EXTERNAL-ID:12345678901234567890`\
        `CHANNEL-ID:12345`
      </td>
    </tr>

    <tr>
      <td>
        3
      </td>

      <td>
        X-SIGNATURE value for encryption will be: <br /> `POST:/v1.0/debit/payment-host-to-host:gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a:56fa5f4999ad8014de49d7898c1d1d53472569db8999de3c1b752a0dd181e98c:2020-01-01T00:00:00+07:00`<br /><br /> \*same value as **HTTPMethod +”:“+ EndpointUrl +":"+ AccessToken +":“+ Lowercase(HexEncode(SHA-256(minify(RequestBody))))+ ":“ + TimeStamp**
      </td>
    </tr>

    <tr>
      <td>
        4
      </td>

      <td>
        By using merchant’s client secret to encrypt the value with HMAC\_SHA512 algorithm, merchant will generate <br /> FSlidRHe4ow9qppNifGVQNcdv67lBjgCiP0BHylh+IKXo4fs2rHaGsFNUY0N8t0rPlZs4iAHAOCDklnCccwuJw==
      </td>
    </tr>

    <tr>
      <td>
        5
      </td>

      <td>
        Final result of merchant's header will be: <br /> `Content-type:application/json`\
        `X-TIMESTAMP:2020-01-01T00:00:00+07:00`\
        `Authorization: Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a`\
        `X-PARTNER-ID: BMRI`\
        `X-DEVICE-ID: 0987ADCASA`\
        `X-EXTERNAL-ID:12345678901234567890`\
        `CHANNEL-ID:12345`\
        `X-SIGNATURE: FSlidRHe4ow9qppNifGVQNcdv67lBjgCiP0BHylh+IKXo4fs2rHaGsFNUY0N8t0rPlZs4iAHAOCDklnCccwuJw==
      </td>
    </tr>
  </tbody>
</Table>

<br />

***

<br />

# BI-SNAP Transaction Header Structure (ASPI Mapping)

<br />

The following tables map Midtrans BI-SNAP Transactional API headers to ASPI's specification for B2B and B2B2C scopes.

## B2B Transaction Headers

| Header Field    | ASPI Component    | Format / Value                        | Required  | Description                                                                                                                                                                                                    |
| :-------------- | :---------------- | :------------------------------------ | :-------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Content-Type`  | Content-Type      | `application/json`                    | Mandatory | Media type of the request body                                                                                                                                                                                 |
| `Authorization` | Access Token      | `Bearer {access_token}`               | Mandatory | B2B access token obtained from [Access Token API](/reference/access-token-api). RFC 6750 Bearer token.                                                                                                         |
| `X-TIMESTAMP`   | Timestamp         | ISO-8601: `YYYY-MM-DDTHH:MM:SS±HH:MM` | Mandatory | Merchant's current local time. Included in signature and used for request freshness validation.                                                                                                                |
| `X-SIGNATURE`   | Digital Signature | Base64-encoded HMAC\_SHA512           | Mandatory | **StringToSign**: `HTTPMethod + ":" + EndpointUrl + ":" + AccessToken + ":" + Lowercase(HexEncode(SHA-256(minify(RequestBody)))) + ":" + Timestamp`<br/>**Algorithm**: HMAC\_SHA512<br/>**Key**: Client secret |
| `X-PARTNER-ID`  | Partner ID        | String (provided by Midtrans)         | Mandatory | Identifies the merchant partner                                                                                                                                                                                |
| `X-EXTERNAL-ID` | External ID       | String (UUID recommended)             | Mandatory | Merchant-generated unique ID per request. Used for idempotency. TTL: 24 hours.                                                                                                                                 |
| `CHANNEL-ID`    | Channel ID        | 5-digit numeric string                | Mandatory | BI-mandated field identifying the channel                                                                                                                                                                      |
| `X-DEVICE-ID`   | Device ID         | String                                | Mandatory | Device identification of the end user's device (user agent for web, device ID for mobile)                                                                                                                      |

<br />

### Sample B2B Transaction Header Block

```text
POST /v1.0/debit/payment-host-to-host HTTP/1.1
Host: merchants.midtrans.com
Content-Type: application/json
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
X-TIMESTAMP: 2024-03-15T10:35:00+07:00
X-SIGNATURE: FSlidRHe4ow9qppNifGVQNcdv67lBjgCiP0BHylh+IKXo4fs2rHaGsFN...
X-PARTNER-ID: G812345678
X-EXTERNAL-ID: 550e8400-e29b-41d4-a716-446655440000
CHANNEL-ID: 12345
X-DEVICE-ID: Mozilla/5.0 (Windows NT 10.0; Win64; x64) Chrome/120.0
```

<br />

## B2B2C Transaction Headers

For payment methods requiring end-customer authorization (e.g., GoPay Tokenization), an additional `Authorization-Customer` header is required:

| Header Field             | ASPI Component        | Format / Value                   | Required    | Description                                                                                            |
| :----------------------- | :-------------------- | :------------------------------- | :---------- | :----------------------------------------------------------------------------------------------------- |
| All B2B headers above    | —                     | —                                | Mandatory   | All B2B headers apply                                                                                  |
| `Authorization-Customer` | Customer Access Token | `Bearer {customer_access_token}` | Conditional | User access token provided by GoPay after account linking. Required only for GoPay Tokenization flows. |
| `X-IP-ADDRESS`           | IP Address            | IPv4 or IPv6 string              | Conditional | End customer's IP address. Required for B2B2C flows where customer device context is relevant.         |
| `X-LATITUDE`             | Latitude              | Decimal string                   | Optional    | Customer's geographic latitude for location-based fraud detection                                      |
| `X-LONGITUDE`            | Longitude             | Decimal string                   | Optional    | Customer's geographic longitude for location-based fraud detection                                     |

<br />

### Sample B2B2C Transaction Header Block (GoPay Tokenization)

```text
POST /v1.0/debit/payment-host-to-host HTTP/1.1
Host: merchants.midtrans.com
Content-Type: application/json
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
Authorization-Customer: Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
X-TIMESTAMP: 2024-03-15T10:35:00+07:00
X-SIGNATURE: pQ8xBd7YkR3nHv5TgmW2cF9jL0sKzNv4aE8rU1oP6bX...
X-PARTNER-ID: G812345678
X-EXTERNAL-ID: 660e8400-e29b-41d4-a716-446655440001
CHANNEL-ID: 12345
X-DEVICE-ID: android-a1b2c3d4e5f6
X-IP-ADDRESS: 103.15.226.50
X-LATITUDE: -6.2088
X-LONGITUDE: 106.8456
```

<br />

> 📘 Compliance Note
>
> The B2B header structure maps to ASPI's "Komponen Struktur Format Header – Transaction (B2B)" and the B2B2C structure maps to "Komponen Struktur Format Header – Transaction (B2B2C)." The symmetric signature (HMAC\_SHA512) ensures message integrity for all transactional requests, while the asymmetric signature (SHA256withRSA) secures the authentication flow.

<br />

***

<br />

# Related Pages

* **[Access Token API](/reference/access-token-api)** — OAuth 2.0 B2B token issuance and Access Token header specification
* **[Security Specification](/reference/security-specification)** — Encryption standards, TLS, key management lifecycle
* **[Security & Architecture](/reference/bi-snap-security-architecture)** — API architecture, data formats, URI standards