---
updatedAt: 2026-05-08T09:07:21.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Certificate Registration

# Certificate Registration — Introduction

## What Is Certificate Registration?

Certificate Registration is a service provided through the Esign APIs that allows you, as a partner, to generate a legally recognised **electronic certificate** for your users.

You submit your user's identity data (name, NIK, date of birth, email, phone number) together with their KTP (national ID card) and selfie images. The platform then performs identity verification against government databases and, once verified, issues a digital certificate bound to that user's identity.

This certificate is the foundation for subsequent electronic signing operations — a user without a certificate cannot sign documents electronically.

***

## Why Does It Matter?

Indonesian regulations require that electronic signatures be backed by a verified digital certificate that proves the signer's identity. Without this step your users would not be able to participate in legally binding e-signing workflows.

Certificate Registration handles the complex verification pipeline for you:

* Identity cross-check against the **Dukcapil** (Directorate General of Population and Civil Registration) database
* Selfie verification against **Dukcapil** data
* Duplicate detection for email and phone numbers
* Asynchronous certificate issuance once verification passes

***

## Is This Right for Your Use Case?

Certificate Registration is a good fit if you need to:

| Scenario                                                              | Suitable?                           |
| --------------------------------------------------------------------- | ----------------------------------- |
| Onboard users for the first time before they sign documents           | ✅ Yes                               |
| Register users on behalf of your platform via server-to-server API    | ✅ Yes                               |
| Verify Indonesian citizens (NIK holders)                              | ✅ Yes                               |
| Issue certificates for users who have already been verified elsewhere | ✅ Yes                               |
| Sign documents without prior certificate registration                 | ❌ No — certificate must exist first |

***

## High-Level Flow

```
Your Server                          Esign Platform
     │                                      │
     │ 1. Get Auth Token                    │
     │─────────────────────────────────────>│
     │<─────────────────────────────────────│
     │          token (30 min TTL)          │
     │                                      │
     │ 2. Get Presigned URLs (CERT_REG)     │
     │─────────────────────────────────────>│
     │<─────────────────────────────────────│
     │    submissionId + KTP/Selfie URLs    │
     │                                      │
     │ 3. Upload KTP image to presigned URL │
     │─────────────────────────────────────>│ (Object Storage)
     │                                      │
     │ 4. Upload Selfie to presigned URL    │
     │─────────────────────────────────────>│ (Object Storage)
     │                                      │
     │ 5. Confirm Upload (with user details)│
     │─────────────────────────────────────>│
     │<─────────────────────────────────────│
     │           submissionId               │
     │                                      │
     │            [async processing]        │
     │                                      │
     │<─────────────────────────────────────│
     │    6. Callback (POST to your server) │
```

***

## Environments

| Environment | Base URL                                    |
| ----------- | ------------------------------------------- |
| Staging     | `https://onekyc.ky.id.staging.gopayapi.com` |
| Production  | `https://onekyc.ky.id.gopayapi.com`         |

> **Note:** Authentication uses a separate base URL. See [Getting Authentication Token](https://docs.midtrans.com/docs/getting-an-authentication-token) for details.