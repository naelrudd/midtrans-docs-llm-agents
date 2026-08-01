---
updatedAt: 2026-04-22T15:45:29.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Security Specification

> 📘 BI-SNAP Compliance
>
> This page describes how Midtrans implements BI-SNAP security standards for encryption, TLS, key management, and authentication. It maps directly to ASPI's "Komponen Standar Enkripsi" and "Secured Channel Communication" specifications.

<br />

There are two kinds of API Scope, which are called **B2B Access Token API**  and **Transactional API**. Both of these APIs have different sets of security specifications.

This is the flow that merchants will commonly use for all integrations, showing how both of these API scopes will be used throughout the integration:

<Image align="center" width="450px" src="https://files.readme.io/29364d9-Screen_Shot_2023-08-22_at_09.35.08.png" />

As you can see on the above image, merchant will be required to call for B2B Access Token API to get the `Access Token` that will be used for subsequent Transactional API until the access token given expired.

<br />

***

<br />

# Encryption Standards

***

<br />

Midtrans BI-SNAP Core API implements three categories of cryptographic standards, aligned with ASPI's specification:

## Asymmetric Signature (Standard Asymmetric Encryption Signature)

| Aspect                 | Specification                                                                                                                         |
| :--------------------- | :------------------------------------------------------------------------------------------------------------------------------------ |
| **Algorithm**          | SHA256withRSA                                                                                                                         |
| **Minimum key length** | RSA 2048-bit                                                                                                                          |
| **Key format**         | PKCS#8, PEM-encoded                                                                                                                   |
| **Used for**           | B2B Access Token API signature (`X-SIGNATURE` header) — merchant signs with private key, Midtrans verifies with merchant's public key |
| **Also used for**      | Notification callback signature — Midtrans signs with its private key, merchant verifies with Midtrans' public key                    |

<br />

## Symmetric Signature (Standard Symmetric Encryption Signature)

| Aspect                   | Specification                                                                                                                                       |
| :----------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Algorithm**            | HMAC\_SHA512                                                                                                                                        |
| **Key**                  | Client secret (provided by Midtrans during credential exchange)                                                                                     |
| **Used for**             | Transactional API signature (`X-SIGNATURE` header) — ensuring message integrity and authenticity for payment, refund, cancel, and status operations |
| **StringToSign formula** | `HTTPMethod + ":" + EndpointUrl + ":" + AccessToken + ":" + Lowercase(HexEncode(SHA-256(minify(RequestBody)))) + ":" + Timestamp`                   |

<br />

## Symmetric Encryption (Standard Symmetric Encryption)

| Aspect             | Specification                                                                                                                 |
| :----------------- | :---------------------------------------------------------------------------------------------------------------------------- |
| **Algorithm**      | AES-256                                                                                                                       |
| **Key derivation** | Client secret                                                                                                                 |
| **Used for**       | Encryption of sensitive payload fields where applicable (e.g., credential exchange payloads transmitted via secured channels) |

For detailed signature generation examples and step-by-step walkthroughs, refer to the [Signature Generation](/reference/signature-generation) page.

<br />

***

<br />

# TLS Version & Cipher Suites (Secured Channel Communication)

***

<br />

Midtrans implements secure channel communication to ensure the confidentiality of transmitted messages.

| Aspect                        | Specification                                                                   |
| :---------------------------- | :------------------------------------------------------------------------------ |
| **Minimum supported version** | TLS 1.2                                                                         |
| **Preferred version**         | TLS 1.3                                                                         |
| **Protocol enforcement**      | All BI-SNAP Core API endpoints require HTTPS. Plain HTTP requests are rejected. |
| **Weaker protocols**          | SSL 2.0, SSL 3.0, TLS 1.0, and TLS 1.1 are **disabled** on all endpoints        |

<br />

### Supported Cipher Suites

Midtrans supports the following GCM-based cipher suites aligned with BI-SNAP requirements:

| Cipher Suite                            | TLS Version |
| :-------------------------------------- | :---------- |
| `TLS_AES_256_GCM_SHA384`                | TLS 1.3     |
| `TLS_AES_128_GCM_SHA256`                | TLS 1.3     |
| `TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384` | TLS 1.2     |
| `TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256` | TLS 1.2     |

Non-GCM and CBC-mode cipher suites are disabled to prevent known vulnerabilities.

> 🚧 TLS 1.2 Sunset
>
> In accordance with Bank Indonesia's directive, TLS 1.2 will remain supported until the regulatory sunset date (30 June 2026). After that date, only TLS 1.3 will be accepted. Merchants are encouraged to upgrade their systems to support TLS 1.3 ahead of this deadline.

<br />

***

<br />

# Key Management Lifecycle

***

<br />

## Key Types

| Key Type                 | Owner               | Purpose                                                                                        |
| :----------------------- | :------------------ | :--------------------------------------------------------------------------------------------- |
| **Merchant private key** | Merchant            | Signs Access Token API requests (SHA256withRSA). Must be kept confidential on merchant's side. |
| **Merchant public key**  | Merchant → Midtrans | Registered with Midtrans to verify merchant signatures on Access Token API requests.           |
| **Midtrans private key** | Midtrans            | Signs notification callbacks sent to merchants. Kept in secure key management infrastructure.  |
| **Midtrans public key**  | Midtrans → Merchant | Provided to merchants to verify notification callback signatures.                              |
| **Client secret**        | Midtrans → Merchant | Shared secret used for HMAC\_SHA512 symmetric signature on Transactional APIs.                 |
| **TLS certificates**     | Midtrans / Merchant | Server certificates for HTTPS endpoints. Issued by trusted Certificate Authorities.            |

<br />

## Key Generation

* **Merchant RSA keypairs**: Generated by merchants using OpenSSL or equivalent tools. Minimum key length is **2048 bits** (RSA). Keys must be in **PKCS#8 format, PEM-encoded**. See [Credential Exchange](/reference/credential-exchange-copy) for generation commands.
* **Midtrans-managed keys**: Generated and stored within secure key management infrastructure with hardware-level protection and strict access controls.
* **Client secrets**: Generated by Midtrans during credential provisioning and delivered via secured channels.

<br />

## Key Storage

| Party        | Storage Controls                                                                                                                                                                                              |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Midtrans** | Keys are stored in hardware-backed key management services (KMS) with encryption at rest, role-based access control, and comprehensive audit logging                                                          |
| **Merchant** | Merchants are responsible for securing their private keys and client secrets. Recommended practices include: use of HSM or KMS, encryption at rest, restricted access, no storage in source code repositories |

<br />

## Key Rotation

* **Time-based rotation**: Merchants may rotate their RSA keypairs at any time by generating a new keypair and registering the new public key via the Dashboard ([Settings > Access Keys](/reference/credential-exchange-copy))
* **Incident-based rotation**: If a key compromise is suspected, merchants should immediately generate new keys, register the new public key, and notify Midtrans support
* **Client secret rotation**: Merchants can request client secret rotation through Midtrans support. The old secret remains valid for a transition period to avoid service disruption
* **Midtrans key rotation**: When Midtrans rotates its signing keys, merchants are notified in advance and provided the new public key via secured channels

<br />

## Key Revocation

* When a merchant is **offboarded**, all associated credentials (Client ID, client secret, partner ID) are revoked and the registered public key is deactivated
* If a key is **compromised**, Midtrans can immediately revoke the affected credentials upon notification, blocking all API access until new credentials are issued
* Revoked keys and secrets cannot be reused

<br />

***

<br />

# End-Customer Authentication Methods

***

<br />

For payment methods that involve end-customer interaction (GoPay, GoPay Tokenization, ShopeePay, DANA, bank transfer), customer authentication is performed by the issuing application or bank — not directly by Midtrans. Midtrans as PJP adheres to BI-SNAP's requirement that customers are authenticated with at least two-factor authentication.

| Payment Method         | Authentication Method                                                                                                  | Factors                                           |
| :--------------------- | :--------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------ |
| **GoPay (Deeplink)**   | Customer authenticates within the GoPay/Gojek app                                                                      | PIN + device possession (2FA)                     |
| **GoPay Tokenization** | Initial linking requires GoPay app authorization; subsequent charges use the linked token with GoPay-side verification | PIN/biometrics + device possession (2FA)          |
| **ShopeePay**          | Customer authenticates within the ShopeePay/Shopee app                                                                 | PIN + device possession (2FA)                     |
| **DANA**               | Customer authenticates within the DANA app                                                                             | PIN + device possession (2FA)                     |
| **QRIS**               | Customer scans QR and authenticates in their e-wallet app                                                              | PIN/biometrics + device possession (2FA)          |
| **Bank Transfer / VA** | Customer authenticates via their banking app or ATM                                                                    | PIN/OTP/biometrics + card/device possession (2FA) |
| **Credit/Debit Card**  | 3D Secure (3DS) authentication via card issuing bank                                                                   | OTP/biometrics + card knowledge (2FA)             |

> 📘 Compliance Note
>
> Midtrans does not directly handle end-customer credentials (PINs, OTPs, biometrics). These are processed entirely within the respective payment provider's secure environment. This separation ensures that customer authentication meets BI-SNAP's multi-factor authentication requirements while minimizing the attack surface.

<br />

***

<br />

# Related Pages

* **[Signature Generation](/reference/signature-generation)** — Detailed signature formulas, step-by-step examples for Access Token and Transactional APIs
* **[Security & Architecture](/reference/bi-snap-security-architecture)** — API architecture, data formats, HTTP methods, URI standards
* **[Credential Exchange](/reference/credential-exchange-copy)** — Public key exchange process and secured delivery methods
* **[Access Token API](/reference/access-token-api)** — OAuth 2.0 B2B token issuance
* **[Operational Reliability & Business Continuity](/reference/bi-snap-operational-reliability)** — Availability, disaster recovery, security controls