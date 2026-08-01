---
updatedAt: 2026-04-26T13:34:29.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Overview

<Callout icon="📘" theme="info">
  Please contact your Midtrans sales representative to integrate with the API.
</Callout>

This section covers API references for the Standar Nasional Open API Pembayaran (SNAP) version of Midtrans' Core API.

Standar Nasional Open API Pembayaran, or in short **SNAP**, is a national payment open API standard published by Bank Indonesia as per enacted in BI Governor Decree No. 23/10/KEP.GBI/2021, dated 16th of August 2021.

SNAP covers aspects of the payment integration between payment providers and merchants that includes:

1. Technical and security standards that include data standards and technical specifications
2. Governance guidelines for interconnected and interoperable open API payments

<br />

# What Change?

<Callout icon="📘" theme="info">
  For more details on **merchant migration & backward compatibility,** please refer to this **[page](https://docs.midtrans.com/reference/merchants-migration-backward-compatibality)**
</Callout>

As regulated by Bank Indonesia, merchants will need to integrate to BI-SNAP-based Core API. This section describes how Midtrans merchant can integrate to this new API, we will also explain in detail what are the differences between BI-SNAP-based Core API and Midtrans existing Core API.

## API Domain

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Environment
      </th>

      <th>
        Legacy Core API
      </th>

      <th>
        BI-SNAP-based Core API
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Sandbox
      </td>

      <td>
        api.sandbox.midtrans.com
      </td>

      <td>
        * [Get Auth Code API](https://docs.midtrans.com/reference/get-auth-code-api) : merchants-app.sbx.midtrans.com <br /> - All other APIs: merchants.sbx.midtrans.com
      </td>
    </tr>

    <tr>
      <td>
        Production
      </td>

      <td>
        api.midtrans.com
      </td>

      <td>
        * [Get Auth Code API](https://docs.midtrans.com/reference/get-auth-code-api): merchants-app.midtrans.com <br /> - All other APIs: merchants.midtrans.com
      </td>
    </tr>
  </tbody>
</Table>

<br />

### API Architecture

The BI-SNAP Core API uses a **RESTful architecture over HTTPS**, aligning with the ASPI standard requirement. All communication between merchants and Midtrans occurs over encrypted TLS channels using standard HTTP request/response patterns with JSON payloads.

#### System Components & Roles

The BI-SNAP integration involves three primary roles:

| Role                                          | Description                                                                                                                                                                                      |
| :-------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Merchant (Client)**                         | Initiates API calls to create payments, check status, request refunds, and manage account linking. The merchant's backend authenticates using signed requests.                                   |
| **Midtrans (PJP / Payment Service Provider)** | Acts as the authorization server (issuing access tokens) and the resource server (processing payment transactions). Midtrans validates signatures, routes transactions, and sends notifications. |
| **Payment Network / Acquiring Bank**          | Underlying payment infrastructure (GoPay, bank networks, QRIS acquirers) that processes the actual fund transfer. Abstracted from the merchant by Midtrans.                                      |

### &#x20;Data Format & Character Encoding

***

All BI-SNAP Core API request and response bodies use **JSON (JavaScript Object Notation) format** with **UTF-8 character encoding**, in line with the BI-SNAP technical standard.

| Aspect                 | Standard                                                                                 |
| :--------------------- | :--------------------------------------------------------------------------------------- |
| **Data format**        | JSON (`Content-Type: application/json`)                                                  |
| **Character encoding** | UTF-8                                                                                    |
| **Timestamp format**   | ISO-8601 (`YYYY-MM-DDTHH:MM:SS±HH:MM`), using Western Indonesian Time (GMT+7)            |
| **Numeric values**     | Transmitted as strings where specified by BI-SNAP (e.g., `amount.value` as `"10000.00"`) |
| **Boolean values**     | JSON native `true`/`false`                                                               |

<br />

## HTTP Methods

***

The BI-SNAP Core API uses a limited, well-defined set of HTTP methods. Each method is used consistently across the API according to its semantic meaning:

| HTTP Method | Usage                                                                                                          | BI-SNAP Endpoints                                          |
| :---------- | :------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------- |
| **POST**    | Create resources, initiate actions (token generation, payment creation, refunds, cancellations, notifications) | Access Token, Charge/Payment, Refund, Cancel, Notification |
| **GET**     | Retrieve resource state without side effects (status inquiry, auth code retrieval)                             | Get Transaction Status, Get Auth Code                      |

<br />

## Standardized URI Path

***

### URI Structure

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

***

## Authorization

### Merchant Credentials

| Legacy Core API | Credentials       | Definition                                                                                           |
| :-------------- | :---------------- | :--------------------------------------------------------------------------------------------------- |
|                 | Server key        | Merchant’s key generated by Midtrans that is used for BASIC AUTH authentication for all Midtrans API |
|                 | Merchant ID (MID) | Merchant’s unique ID generated by Midtrans as part of the onboarding process                         |

<br /> While in SNAP-based Core API, the credentials differ based on the API scope as follow:

| BI-SNAP-based Core API  | Credentials           | Definition                                                                     | Remarks  |
| :---------------------- | :-------------------- | :----------------------------------------------------------------------------- | :------- |
| Both API scope          | Merchant ID (MID)     | Merchant’s unique ID generated by Midtrans                                     | Existing |
| Access Token API scope  | Merchant's public key | Created by merchant. Will be used by Midtrans to validate merchant’s signature | New      |
|                         | Client ID             | Provided by Midtrans. Will be used as X-CLIENT-KEY on request header           | New      |
| Transactional API scope | Client secret         | Provided by Midtrans. Will be used for signature generation                    | New      |
|                         | Partner ID            | Provided by Midtrans. Will be used as X-PARTNER-ID on request header           | New      |

<br />

### Authorization Behavior

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Legacy Core API
      </th>

      <th>
        BI-SNAP-based Core API
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Merchant will only need to use server key to initiate API calls
      </td>

      <td>
        1. Merchant need to call **Access Token API** first to generate a token that will be used for subsequent APIs, up until the token expired <br /> 2. Merchant need to create signature for all API calls. Please refer to [`Signature Generation section`](https://docs.midtrans.com/reference/signature-generation).
      </td>
    </tr>
  </tbody>
</Table>

***

### Transaction Status

| Legacy Core API         | BI-SNAP-based Core API |
| :---------------------- | :--------------------- |
| PENDING                 | 03 (Pending)           |
| AUTHORIZE               | 01 (Initiated)         |
| SETTLEMENT              | 00 (Success)           |
| REFUND & PARTIAL REFUND | 04 (Refunded)          |
| CANCEL                  | 05 (Canceled)          |
| FAILURE                 | 06 (Failed)            |
| EXPIRY                  | 08 (Expiry)            |
| DENY                    | 09 (Rejected)          |

<Callout icon="📘" theme="info">
  * Only transaction status on API response that will change. Transaction status on Midtrans dashboard and reporting will remain the same as Legacy API.* We will only return the transaction status numeric value in the actual API response. The text value (...) is only the status code description that won't be returned.
</Callout>

***

### Transaction & Account Identification

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Legacy Core API
      </th>

      <th>
        BI-SNAP-based Core API
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        * *transaction_id** <br /> Midtrans generated transaction unique ID that is generated after transaction is successfully created. This ID can be used on all Midtrans APIs, such as in status API, cancel API, and refund API.
      </td>

      <td>
        * *referenceNo**<br />Same definition and usage as**transaction_id** in legacy API.
      </td>
    </tr>

    <tr>
      <td>
        * *order_id** <br /> Merchant generated transaction ID that is unique per successful transaction. This ID can be used on all Midtrans APIs, such as in status API, cancel API, and refund API.
      </td>

      <td>
        * *partnerReferenceNo**<br /> Same definition as **order_id**, this ID will be shown as merchant's order ID on the dashboard and reporting.<br /><br /> ** X-EXTERNAL-ID**<br /> Merchant generated ID that needs to be unique for all transactions. This ID can be passed in subsequent API calls (status, refund, cancel API) as an alternative value for **originalExternalId**. Please note we highly recommend merchant to use UUID format to avoid duplication. The TTL for this ID is 24 hours.<br /><br /> Note: Unlike **order_id**in the legacy API,**partnerReferenceNo**doesn't have unique validation and is not recommended to be used as a value in subsequent APIs. Instead, we highly recommend merchant to use**originalReferenceNo**(referenceNo value that is generated by Midtrans) or**originalExternalId** (X-EXTERNAL-ID value) in subsequent API calls.
      </td>
    </tr>

    <tr>
      <td>
        * *Idempotency-Key** <br /> Key that is sent by merchant to ensure that transaction is only created once. If transaction already succeed and merchant re-send the same idempotency-key on request, Midtrans will response the same successful response as the first request.
      </td>

      <td>
        * *X-EXTERNAL-ID** <br /> Has the same usage as idempotency-key in legacy API.
      </td>
    </tr>

    <tr>
      <td>
        * *account_id**_(only for GoPay Tokenization)_ <br /> Midtrans account unique ID that is generated as part of the account linking process. Will be used for initiating transaction.
      </td>

      <td>
        * *Authorization-Customer**&#xNAN;_(only for GoPay Tokenization)_ <br /> Same definition as **account_id**in legacy API. For account that has been linked using the legacy API, merchant need to exchange the account_id with**Authorization-Customer** token to initiate transaction in SNAP-based API.
      </td>
    </tr>
  </tbody>
</Table>

***

### Notification

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Legacy Core API
      </th>

      <th>
        BI-SNAP-based Core API
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Merchant only required to share one notification URL for all payment type notification in Midtrans
      </td>

      <td>
        There will be differences in notification’s relative path per payment type flow. Merchant required to share their notification URL domain, where Midtrans will attach the dynamic relative path. <br /><br /> Sample: <br /> Merchant’s SNAP-based URL: [https://www.merchant.open-api.com/1.0](https://www.merchant.open-api.com/1.0)

        URL that will be dynamically created by Midtrans will be:

        * Direct Debit API: [https://www.merchant.open-api.com/1.0/debit/notify](https://www.merchant.open-api.com/1.0/debit/notify)
        * MPM API: [https://www.merchant.open-api.com/1.0/qr/qr-mpm-notify](https://www.merchant.open-api.com/1.0/qr/qr-mpm-notify) <br /><br /> _Note_: Virtual Account will still uses the legacy Midtrans post notification
      </td>
    </tr>
  </tbody>
</Table>

To be able to receive notification from Midtrans, **merchant will need to whitelist this set of IPs** based on the environment.

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Environment
      </th>

      <th>
        IPs
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Staging
      </td>

      <td>
        3.1.141.98/32  
        52.76.190.190/32  
        13.251.192.204/32  
        8.215.39.156/32  
        8.215.77.79/32  
        147.139.213.119/32  
        8.215.56.11/32  
        8.215.39.87/32  
        8.215.42.0/32  
        8.215.59.158/32  
        149.129.222.246/32  
        8.215.26.108/32  
        8.215.13.84/32
      </td>
    </tr>

    <tr>
      <td>
        Sandbox
      </td>

      <td>
        34.142.147.133/32  
        34.142.169.131/32  
        34.142.231.22/32  
        35.240.161.215/32  
        34.142.227.232/32  
        34.124.184.175/32  
        35.197.130.2/32  
        34.142.233.114/32  
        8.215.26.211/32  
        8.215.22.135/32  
        8.215.93.92/32  
        8.215.93.214/32  
        8.215.93.76/32  
        8.215.33.37/32  
        8.215.26.148/32  
        8.215.194.225/32  
        8.215.12.199/32  
        149.129.255.111/32
      </td>
    </tr>

    <tr>
      <td>
        Production
      </td>

      <td>
        13.228.166.126/32  
        52.220.80.5/32  
        3.1.123.95/32  
        8.215.30.222/32  
        147.139.209.49/32  
        8.215.32.142/32  
        147.139.163.77/32  
        8.215.25.24/32  
        8.215.3.193/32  
        147.139.210.20/32  
        149.129.238.95/32  
        8.215.9.206/32  
        147.139.134.22/32
      </td>
    </tr>
  </tbody>
</Table>

<br />

<Callout icon="📘" theme="info">
  You can find BI SNAP official documentation in this <Anchor label="page" target="_blank" href="https://apidevportal.aspi-indonesia.or.id/">page</Anchor> **this page is managed by ASPI Indonesia**
</Callout>