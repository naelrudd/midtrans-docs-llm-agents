---
updatedAt: 2026-09-28T11:59:55.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Midtrans Partner API

# List of Partner APIs

<br />

<Anchor target="_blank" href="https://docs.midtrans.com/reference/checkout">Checkout APIs</Anchor>

<Anchor target="_blank" href="https://docs.midtrans.com/reference/core">Core APIs</Anchor>

<Anchor target="_blank" href="https://docs.midtrans.com/reference/midtrans-merchant-api">Merchant APIs</Anchor>

<Anchor target="_blank" href="https://docs.midtrans.com/reference/balance-mutation-api">Balance API</Anchor>

# Base URL

Production: `https://partner-api.midtrans.com`

Staging: `https://partner-api.stg.midtrans.com`

# Request Header

| Field         | Type   | Attribute | Description                                                                                                                                                                                                                                           |
| :------------ | :----- | :-------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Authorization | String | Mandatory | Basic Base64Encode(partnerServerKey:)<br />Sample<br />PARTNER\_SERVER\_KEY = `f58abc7a-c17f-46e4-898a-607f1257fb62`<br />AUTH\_STRING = `Base64("f58abc7a-c17f-46e4-898a-607f1257fb62:")`<br />AUTH\_STRING = `ZjU4YWJjN2EtYzE3Zi00NmU0LTg5OGEtNjA3` |
| X-PARTNER-ID  | String | Mandatory | Unique identifier for partner. Provided by Midtrans.                                                                                                                                                                                                  |
| X-MERCHANT-ID | String | Mandatory | Unique identifier for each merchant under the partner. Provided by Midtrans.                                                                                                                                                                          |
| Accept        | String | Mandatory | application/json                                                                                                                                                                                                                                      |
| Content-Type  | String | Mandatory | application/json                                                                                                                                                                                                                                      |

#