---
updatedAt: 2026-04-22T15:45:25.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Security & Architecture

BI-SNAP Core API architecture overview covering REST design, data formats, HTTP methods, URI standardization, and compliance mapping to ASPI technical standards.

> 📘 BI-SNAP Compliance
>
> This page describes how Midtrans implements the BI-SNAP technical standard for API architecture, data formats, HTTP methods, and URI path standardization. It serves as reference material for both developers integrating with the BI-SNAP Core API and for compliance/audit purposes.

<br />

# API Architecture

***

<br />

## Architecture Type

The BI-SNAP Core API uses a **RESTful architecture over HTTPS**, aligning with the ASPI standard requirement (`Tipe Arsitektur API = REST`). All communication between merchants and Midtrans occurs over encrypted TLS channels using standard HTTP request/response patterns with JSON payloads.

<br />

## System Components & Roles

The BI-SNAP integration involves three primary roles:

| Role                                          | Description                                                                                                                                                                                      |
| :-------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Merchant (Client)**                         | Initiates API calls to create payments, check status, request refunds, and manage account linking. The merchant's backend authenticates using signed requests.                                   |
| **Midtrans (PJP / Payment Service Provider)** | Acts as the authorization server (issuing access tokens) and the resource server (processing payment transactions). Midtrans validates signatures, routes transactions, and sends notifications. |
| **Payment Network / Acquiring Bank**          | Underlying payment infrastructure (GoPay, bank networks, QRIS acquirers) that processes the actual fund transfer. Abstracted from the merchant by Midtrans.                                      |

<br />

## Separation of Concerns

The API is organized into distinct functional groups, each with its own security scope:

| API Group                  | Purpose                                                                             | Security Scope                                                              |
| :------------------------- | :---------------------------------------------------------------------------------- | :-------------------------------------------------------------------------- |
| **Access Token API**       | Authentication — issue B2B access tokens using OAuth 2.0 `client_credentials` grant | Asymmetric signature (SHA256withRSA) with merchant private key              |
| **Transactional APIs**     | Payment creation, refund, cancel, status inquiry                                    | Symmetric signature (HMAC\_SHA512) with client secret + Bearer access token |
| **Notification Callbacks** | Midtrans pushes payment status updates to merchant endpoints                        | Asymmetric signature verification using Midtrans public key                 |
| **Reporting APIs**         | Transaction history queries                                                         | Bearer access token + symmetric signature                                   |

<br />

## Architecture Diagram

```text
┌──────────────┐         HTTPS/TLS 1.2+         ┌──────────────────┐
│              │  ────── Access Token API ──────► │                  │
│   Merchant   │  ────── Transactional APIs ───► │     Midtrans     │
│   (Client)   │  ◄───── HTTP Notifications ──── │   (PJP Server)   │
│              │  ────── Reporting APIs ────────► │                  │
└──────────────┘                                  └────────┬─────────┘
                                                           │
                                                  ┌────────▼─────────┐
                                                  │  Payment Network │
                                                  │  (GoPay, Banks,  │
                                                  │   QRIS, etc.)    │
                                                  └──────────────────┘
```

<br />

***

<br />

# Data Format & Character Encoding

***

<br />

All BI-SNAP Core API request and response bodies use **JSON (JavaScript Object Notation) format** with **UTF-8 character encoding**, in line with the BI-SNAP technical standard.

| Aspect                 | Standard                                                                                 |
| :--------------------- | :--------------------------------------------------------------------------------------- |
| **Data format**        | JSON (`Content-Type: application/json`)                                                  |
| **Character encoding** | UTF-8                                                                                    |
| **Timestamp format**   | ISO-8601 (`YYYY-MM-DDTHH:MM:SS±HH:MM`), using Western Indonesian Time (GMT+7)            |
| **Numeric values**     | Transmitted as strings where specified by BI-SNAP (e.g., `amount.value` as `"10000.00"`) |
| **Boolean values**     | JSON native `true`/`false`                                                               |

For detailed JSON object specifications per payment method, refer to:

* [Request Body (JSON Parameter)](/reference/request-body-json-parameter)
* [JSON Objects](/reference/json-objects)

<br />

***

<br />

# HTTP Methods

***

<br />

The BI-SNAP Core API uses a limited, well-defined set of HTTP methods. Each method is used consistently across the API according to its semantic meaning:

| HTTP Method | Usage                                                                                                          | BI-SNAP Endpoints                                          |
| :---------- | :------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------- |
| **POST**    | Create resources, initiate actions (token generation, payment creation, refunds, cancellations, notifications) | Access Token, Charge/Payment, Refund, Cancel, Notification |
| **GET**     | Retrieve resource state without side effects (status inquiry, auth code retrieval)                             | Get Transaction Status, Get Auth Code                      |

<br />

## Endpoint Summary by HTTP Method

<br />

### POST Endpoints

| Path                                        | Operation                                   | SNAP Service Code |
| :------------------------------------------ | :------------------------------------------ | :---------------- |
| `/{version}/access-token/b2b`               | Generate B2B Access Token                   | 73                |
| `/{version}/debit/payment-host-to-host`     | Direct Debit Payment (GoPay/ShopeePay/DANA) | 54                |
| `/{version}/registration-account-binding`   | Bind Account (GoPay Tokenization)           | 08                |
| `/{version}/registration-account-unbinding` | Unbind Account                              | 08                |
| `/{version}/debit/refund`                   | Refund Transaction                          | 58                |
| `/{version}/debit/cancel`                   | Cancel Transaction                          | —                 |
| `/{version}/qr/qr-mpm-generate`             | Generate QRIS MPM                           | 47                |
| `/{version}/transfer-va/create-va`          | Create Virtual Account (Bank Transfer)      | 27                |

<br />

### GET Endpoints

| Path                      | Operation                          | SNAP Service Code |
| :------------------------ | :--------------------------------- | :---------------- |
| `/{version}/debit/status` | Get Transaction Status             | 55                |
| `/{version}/auth`         | Get Auth Code (GoPay Tokenization) | —                 |

<br />

> 📘 Note
>
> All BI-SNAP API calls require HTTPS. Plain HTTP requests are rejected. The minimum TLS version is 1.2. See [Security Specification](/reference/security-specification) for details.

<br />

***

<br />

# Standardized URI Path

***

<br />

## URI Structure

BI-SNAP Core API endpoints follow a standardized URI pattern aligned with ASPI's specification:

```text
https://{domain_api}/{version}/{service-group}/{operation}
```

| Component         | Description                                    | Example                                                 |
| :---------------- | :--------------------------------------------- | :------------------------------------------------------ |
| `{domain_api}`    | Base domain per environment (see table below)  | `merchants.midtrans.com`                                |
| `{version}`       | API version                                    | `v1.0`                                                  |
| `{service-group}` | Functional grouping (payment type or function) | `debit`, `qr`, `transfer-va`, `access-token`            |
| `{operation}`     | Specific action                                | `payment-host-to-host`, `refund`, `status`, `create-va` |

<br />

## API Base Domains

| Environment    | Domain                       | Notes                                                                                     |
| :------------- | :--------------------------- | :---------------------------------------------------------------------------------------- |
| **Sandbox**    | `merchants.sbx.midtrans.com` | For testing. Get Auth Code uses `merchants-app.sbx.midtrans.com`                          |
| **Staging**    | `merchants.stg.midtrans.com` | For functional testing with Midtrans. Get Auth Code uses `merchants-app.stg.midtrans.com` |
| **Production** | `merchants.midtrans.com`     | Live environment. Get Auth Code uses `merchants-app.midtrans.com`                         |

<br />

## URI Examples

The following examples demonstrate how Midtrans BI-SNAP endpoints map to the ASPI URI standard `/{domain_api}/{version}/{service-group}/{operation}`:

| Full URI                                                         | Domain                   | Version | Service Group  | Operation              |
| :--------------------------------------------------------------- | :----------------------- | :------ | :------------- | :--------------------- |
| `https://merchants.midtrans.com/v1.0/access-token/b2b`           | `merchants.midtrans.com` | `v1.0`  | `access-token` | `b2b`                  |
| `https://merchants.midtrans.com/v1.0/debit/payment-host-to-host` | `merchants.midtrans.com` | `v1.0`  | `debit`        | `payment-host-to-host` |
| `https://merchants.midtrans.com/v1.0/qr/qr-mpm-generate`         | `merchants.midtrans.com` | `v1.0`  | `qr`           | `qr-mpm-generate`      |
| `https://merchants.midtrans.com/v1.0/transfer-va/create-va`      | `merchants.midtrans.com` | `v1.0`  | `transfer-va`  | `create-va`            |
| `https://merchants.midtrans.com/v1.0/debit/status`               | `merchants.midtrans.com` | `v1.0`  | `debit`        | `status`               |

<br />

***

<br />

# Related Pages

For further details on specific security and integration topics:

* **[Security Specification](/reference/security-specification)** — Encryption standards, TLS, key management, and end-customer authentication
* **[Signature Generation](/reference/signature-generation)** — Detailed signature formulas and examples for Access Token and Transactional APIs
* **[Credential Exchange](/reference/credential-exchange-copy)** — Public key exchange process and secured delivery methods
* **[Access Token API](/reference/access-token-api)** — OAuth 2.0 B2B token issuance
* **[Operational Reliability & Business Continuity](/reference/bi-snap-operational-reliability)** — Availability, disaster recovery, and compliance controls
* **[BI-SNAP Overview](/reference/core-api-snap-open-api-overview)** — Migration guide and full endpoint reference