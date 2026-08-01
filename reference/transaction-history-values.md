---
updatedAt: 2025-11-10T23:19:26.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Transaction History Values

> 📘
>
> Please make sure to use BI SNAP Credentials to utilize any of the Reporting APIs. Refer to [here](/reference/getting-started-1) to understand how to retrieve your credentials.

<br />

This section will cover the list of values for transaction history API

### Types

Below are the list of transaction types that we currently support. We have 2 kind of transaction types: BI-SNAP (field `type`) & Midtrans (field `additionalInfo.type`).

| BI-SNAP        | Midtrans     |
| :------------- | :----------- |
| PAYMENT        | PAYMENT      |
| TOP\_UP        | TOP\_UP      |
| RECEIVE\_MONEY | WITHDRAWAL   |
| SEND\_MONEY    | DISBURSEMENT |

### Statuses (Midtrans)

Below are the list of transaction statuses for each Midtrans transaction type (field `additionalInfo.status`)

| Type         | Status        |               |              |               |              |               |            |            |              |           |           |          |
| :----------- | :------------ | ------------- | ------------ | ------------- | ------------ | ------------- | ---------- | ---------- | ------------ | --------- | --------- | -------- |
| PAYMENT      | AUTHORIZE \\  | SUCCESS \\    | CHALLENGE \\ | SETTLEMENT \\ | REFUND \\    | CHARGEBACK \\ | EXPIRED \\ | PENDING \\ | CANCELLED \\ | FAILED \\ | DENIED \\ | REVERSAL |
| TOP\_UP      | SETTLEMENT \\ | REVERSAL      |              |               |              |               |            |            |              |           |           |          |
| WITHDRAWAL   | REQUESTED \\  | PROCESSING \\ | SUCCESS \\   | FAILED \\     | CANCELLED    |               |            |            |              |           |           |          |
| DISBURSEMENT | REQUESTED \\  | REJECTED \\   | APPROVED \\  | PROCESSING \\ | COMPLETED \\ | FAILED        |            |            |              |           |           |          |

### Channels

Below are the list of transaction channels for each Midtrans transaction type (field `additionalInfo.channel`)

| Type         | Channels             |                                  |                                  |                                  |                                   |          |                  |            |            |              |               |                 |                 |                 |              |                   |                    |            |                |        |
| :----------- | :------------------- | -------------------------------- | -------------------------------- | -------------------------------- | --------------------------------- | -------- | ---------------- | ---------- | ---------- | ------------ | ------------- | --------------- | --------------- | --------------- | ------------ | ----------------- | ------------------ | ---------- | -------------- | ------ |
| PAYMENT      | bank\_transfer \\    | credit\_card \\                  | cstore\_indomaret \\             | cstore\_alfamart  \\             | qris \\                           | gopay \\ | mandiri\_bill \\ | akulaku \\ | kredivo \\ | shopeepay \\ | uob\_ezpay \\ | cimb\_clicks \\ | bca\_klikpay \\ | bca\_klikbca \\ | bri\_epay \\ | mandiri\_ecash \\ | danamon\_online \\ | linkaja \\ | dbs\_paylah \\ | paypal |
| TOP\_UP      | balance\_transfer \\ | bca\_virtual\_account\_number \\ | bri\_virtual\_account\_number \\ | bni\_virtual\_account\_number \\ | permata\_virtual\_account\_number |          |                  |            |            |              |               |                 |                 |                 |              |                   |                    |            |                |        |
| WITHDRAWAL   | list of banks        |                                  |                                  |                                  |                                   |          |                  |            |            |              |               |                 |                 |                 |              |                   |                    |            |                |        |
| DISBURSEMENT | list of banks        |                                  |                                  |                                  |                                   |          |                  |            |            |              |               |                 |                 |                 |              |                   |                    |            |                |        |

### Payment Sources

Below are the list of payment sources (field `additionalInfo.payment.source`), and only applicable for Midtrans transaction type `PAYMENT`only. This field can be accessed on transaction history detail API.

| Source       |         |                  |         |
| :----------- | ------- | ---------------- | ------- |
| core\_api \\ | snap \\ | payment\_link \\ | invoice |