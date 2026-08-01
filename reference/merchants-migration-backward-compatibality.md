---
updatedAt: 2025-11-11T00:43:28.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Merchants Migration & Backward Compatibality

When migrating transactional API to BI-SNAP-based Core API, these are a few things that merchants need to take note of.

## Transactional API Migration

When migrating transactional API to BI-SNAP-based Core API, these are a few things that merchants need to take note of:

1. Transaction that is created on legacy API cannot be processed on BI-SNAP-based API. For example, `transaction_id` or `order_id` that is created on legacy API, cannot be used in any BI-SNAP-based API including status, cancel and refund API.
2. Transaction that is created on BI-SNAP-based API will be able to be processed on legacy API, by adding an extra header value (transaction-source header with value `SNAP_API`). This header can be used on status API, cancel API, refund API, and capture API.

**Sample scenario:**

Given that a transaction is created using BI-SNAP-based API, the transaction can be refunded using legacy API in 2 ways:

* Refund with `transaction_id`:  pass **referenceNo** value (from SNAP-based API) as `transaction_id `and add **transaction-source: SNAP\_API** on the refund request header in legacy API.
* Refund with `order_id`: pass **X-EXTERNAL-ID** value (from SNAP-based API) as `order_id` and add **transaction-source: SNAP\_API** on the refund request header in legacy API.

<br />

***

## Account API Migration

1. Once moved to BI-SNAP-based Core API, merchant doesn't need to re-initiate linking to an already linked GoPay account. But instead, merchant will need to exchange the **account\_id** (provided from linking process in legacy API) with **authorization-customer** token by calling **BI-SNAP-based Binding Inquiry API**.
2. Linking that is created on BI-SNAP-based API can be used on transaction API in the  legacy flow by sending a new parameter **Authorization-Customer** in the request header and send the Authorization Customer token (the accessToken acquired from Binding API ([link](https://docs.midtrans.com/reference/binding-api)) with the format below:

```Text Request header of Legacy Charge API
...
Authorization-Customer: Bearer [accessToken from BI-SNAP Binding API]
...
```

<br />

***

## Notification API Migration

1. If a transaction is created using the BI-SNAP-based API, Midtrans will send all notifications related to that transaction using the BI-SNAP-based API specification.
2. In case merchant decided to roll back to legacy flow, all transaction notifications will still use  BI-SNAP-based API specification.