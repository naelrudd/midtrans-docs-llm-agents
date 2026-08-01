---
updatedAt: 2025-11-10T23:19:25.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Transaction History Detail API

> 📘
>
> Please make sure to use BI SNAP Credentials to utilize any of the Reporting APIs. Refer to [here](/reference/getting-started-1) to understand how to retrieve your credentials.

<br />

This API is used to get merchant's transaction history detail

| Path              | /\{version}/transaction-history-detail |
| :---------------- | :------------------------------------- |
| HTTP Method       | POST                                   |
| Version           | v1.0                                   |
| SNAP Service Code | 13                                     |

## Request Header

| Field Name    | Field Type | Mandatory | Field Description                                                                                                                                        |
| :------------ | :--------- | :-------- | :------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Content-type  | String     | M         | Media type of the resource, i.e. application/json                                                                                                        |
| X-TIMESTAMP   | String     | M         | Client’s current local time in ISO-8601 format                                                                                                           |
| X-SIGNATURE   | String     | M         | Unique identifier for partner                                                                                                                            |
| Authorization | String     | M         | Represents access\_token of a request; string starts with keyword “Bearer ” followed by access\_token. Can get this token from Access Token B2B response |
| X-PARTNER-ID  | String     | M         | Unique identifier for partner                                                                                                                            |
| X-EXTERNAL-ID | String     | M         | Alphanumeric string. Preferably UUID. Reference number that should be unique in the same day or 1 day idempotency key                                    |
| CHANNEL-ID    | String     | M         | Device identification on which the API services are currently being accessed by the end user. Given by BI                                                |

```
Content-type: application/json
X-TIMESTAMP: 2020-12-18T15:34:40+07:00
X-SIGNATURE: 85be817c55b2c135157c7e89f52499bf0c25ad6eeebe04a986e8c862561b19a5
Authorization: Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CUpvIJbU1mMU4a11MNDZ7Sg5u9a
X-PARTNER-ID: 82150823919040624621823174737537
X-EXTERNAL-ID: 41807553358950093184162180797837
CHANNEL-ID: 95221
```

<br />

## Request Body

| Field Name                 | Field Type | Mandatory | Field Description                                 |
| :------------------------- | :--------- | :-------- | :------------------------------------------------ |
| originalPartnerReferenceNo | String(64) | M         | Transaction identifier on service consumer system |
| additionalInfo             | Object     | M         | Additional information                            |
| additionalInfo.referenceNo | String(64) | M         | Transaction identifier on service provider system |

```
{
  "originalPartnerReferenceNo": "2020102900000000000001",
  "additionalInfo": {
    "referenceNo": "2020102977770000000009"
  }
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
X-TIMESTAMP: 2020-12-18T15:34:40+07:00
```

<br />

## Response Body

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
        responseCode
      </td>

      <td>
        String(7)
      </td>

      <td>
        M
      </td>

      <td>
        Response code (HTTP status code + service code + case code)
      </td>
    </tr>

    <tr>
      <td>
        responseMessage
      </td>

      <td>
        String(150)
      </td>

      <td>
        M
      </td>

      <td>
        Response description
      </td>
    </tr>

    <tr>
      <td>
        referenceNo
      </td>

      <td>
        String(64)
      </td>

      <td>
        M
      </td>

      <td>
        Transaction identifier on service provider system
      </td>
    </tr>

    <tr>
      <td>
        partnerReferenceNo
      </td>

      <td>
        String(64)
      </td>

      <td>
        M
      </td>

      <td>
        Transaction identifier on service consumer system
      </td>
    </tr>

    <tr>
      <td>
        dateTime
      </td>

      <td>
        String(25)
      </td>

      <td>
        M
      </td>

      <td>
        Transaction created time in ISO-8601 format
      </td>
    </tr>

    <tr>
      <td>
        amount
      </td>

      <td>
        Object
      </td>

      <td>
        M
      </td>

      <td>
        Amount information
      </td>
    </tr>

    <tr>
      <td>
        amount.value
      </td>

      <td>
        String(16,2)
      </td>

      <td>
        M
      </td>

      <td>
        Net amount of the transaction
      </td>
    </tr>

    <tr>
      <td>
        amount.currency
      </td>

      <td>
        String(3)
      </td>

      <td>
        M
      </td>

      <td>
        Currency
      </td>
    </tr>

    <tr>
      <td>
        remark
      </td>

      <td>
        String(256)
      </td>

      <td>
        O
      </td>

      <td>
        Transaction remark (only applicable for Midtrans transaction type DISBURSEMENT)
      </td>
    </tr>

    <tr>
      <td>
        status
      </td>

      <td>
        String(32)
      </td>

      <td>
        M
      </td>

      <td>
        Transaction status (BI-SNAP)
      </td>
    </tr>

    <tr>
      <td>
        type
      </td>

      <td>
        String(32)
      </td>

      <td>
        M
      </td>

      <td>
        Transaction type (BI-SNAP)
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo
      </td>

      <td>
        Object
      </td>

      <td>
        O
      </td>

      <td>
        Additional information
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.status
      </td>

      <td>
        String(32)
      </td>

      <td>
        M
      </td>

      <td>
        Transaction status (Midtrans). List of statuses can be referred [here](https://docs.midtrans.com/reference/transaction-history-values) 
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.type
      </td>

      <td>
        String(32)
      </td>

      <td>
        M
      </td>

      <td>
        Transaction type (Midtrans). List of types can be referred [here](https://docs.midtrans.com/reference/transaction-history-values) 
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.updatedTime
      </td>

      <td>
        String(25)
      </td>

      <td>
        M
      </td>

      <td>
        Transaction updated time in ISO-8601 format
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.channel
      </td>

      <td>
        String(100)
      </td>

      <td>
        M
      </td>

      <td>
        Transaction channel. List of channels can be referred [here](https://docs.midtrans.com/reference/transaction-history-values) 
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerEmail
      </td>

      <td>
        String(100)
      </td>

      <td>
        O
      </td>

      <td>
        Customer email
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.accountNo
      </td>

      <td>
        String(32)
      </td>

      <td>
        O
      </td>

      <td>
        Account number
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.payment
      </td>

      <td>
        Object
      </td>

      <td>
        O
      </td>

      <td>
        Payment related information
      </td>
    </tr>

    <tr>
      <td>
        payment.expiryTime
      </td>

      <td>
        String(25)
      </td>

      <td>
        M
      </td>

      <td>
        Payment expiry time in ISO-8601 format
      </td>
    </tr>

    <tr>
      <td>
        payment.source
      </td>

      <td>
        String(20)
      </td>

      <td>
        M
      </td>

      <td>
        Payment source. List of payment sources can be referred [here](https://docs.midtrans.com/reference/transaction-history-values) 
      </td>
    </tr>

    <tr>
      <td>
        payment.cardNumber
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Credit card number
      </td>
    </tr>

    <tr>
      <td>
        payment.cardType
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Credit card type
      </td>
    </tr>

    <tr>
      <td>
        payment.cardChannelResponseCode
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Credit card response code
      </td>
    </tr>

    <tr>
      <td>
        payment.\
        cardChannelResponseMessage
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Credit card response message
      </td>
    </tr>

    <tr>
      <td>
        payment.issuingBrand
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Credit card issuing brand
      </td>
    </tr>

    <tr>
      <td>
        payment.issuingBank
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Credit card issuing bank
      </td>
    </tr>

    <tr>
      <td>
        payment.issuingCountryCode
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Credit card issuing country code
      </td>
    </tr>

    <tr>
      <td>
        payment.issuingCountryName
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Credit card issuing country name
      </td>
    </tr>

    <tr>
      <td>
        payment.acquiringBank
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Credit card acquiring bank
      </td>
    </tr>

    <tr>
      <td>
        payment.retrievalReferenceNumber
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Credit card retrieval reference number
      </td>
    </tr>

    <tr>
      <td>
        payment.fdsRecommendation
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Credit card FDS recommendation
      </td>
    </tr>

    <tr>
      <td>
        payment.creditCardSecure
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Credit card secure
      </td>
    </tr>

    <tr>
      <td>
        payment.bankMid
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Credit card bank mid
      </td>
    </tr>

    <tr>
      <td>
        payment.bankResponseCode
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Credit card bank response code
      </td>
    </tr>

    <tr>
      <td>
        payment.isOneClick
      </td>

      <td>
        boolean
      </td>

      <td>
        O
      </td>

      <td>
        Credit card is one click
      </td>
    </tr>

    <tr>
      <td>
        payment.isTwoClick
      </td>

      <td>
        boolean
      </td>

      <td>
        O
      </td>

      <td>
        Credit card is two click
      </td>
    </tr>

    <tr>
      <td>
        payment.installmentTerm
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Credit card installment term
      </td>
    </tr>

    <tr>
      <td>
        payment.installmentType
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Credit card installment type
      </td>
    </tr>

    <tr>
      <td>
        payment.redeemedPointsAmount
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Credit card redeemed points amount
      </td>
    </tr>

    <tr>
      <td>
        payment.redeemedPointsQuantity
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Credit card redeemed points quantity
      </td>
    </tr>

    <tr>
      <td>
        payment.networkTransactionId
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Credit card network transaction id
      </td>
    </tr>

    <tr>
      <td>
        payment.store
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Convenient store name, i.e: indomaret, alfamart
      </td>
    </tr>

    <tr>
      <td>
        payment.paymentCode
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Convenient store payment code
      </td>
    </tr>

    <tr>
      <td>
        payment.trackingRef
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Convenient store tracking reference (only for Indomaret)
      </td>
    </tr>

    <tr>
      <td>
        payment.agentTransactionId
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Convenient store agent transaction id (only for Alfarmart)
      </td>
    </tr>

    <tr>
      <td>
        payment.virtualAccountNumber
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Virtual account number
      </td>
    </tr>

    <tr>
      <td>
        payment.bcaVaChannel
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Virtual account channel (only for BCA)
      </td>
    </tr>

    <tr>
      <td>
        payment.bniVaType
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Virtual account type, e.g: open\_payment, fixed\_payment (only for BNI)
      </td>
    </tr>

    <tr>
      <td>
        payment.bniLeftAmount
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Virtual account left amount (only for BNI)
      </td>
    </tr>

    <tr>
      <td>
        payment.qrisOnUs
      </td>

      <td>
        boolean
      </td>

      <td>
        O
      </td>

      <td>
        QRIS is on us
      </td>
    </tr>

    <tr>
      <td>
        payment.qrisReferenceNumber
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        QRIS reference number
      </td>
    </tr>

    <tr>
      <td>
        payment.qrisIssuer
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        QRIS issuer
      </td>
    </tr>

    <tr>
      <td>
        payment.qrisIssuerTransactionId
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        QRIS issuer transaction id
      </td>
    </tr>

    <tr>
      <td>
        payment.qrisAcquirer
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        QRIS acquirer
      </td>
    </tr>

    <tr>
      <td>
        payment.qrisAcquirerTransactionId
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        QRIS acquirer transaction id
      </td>
    </tr>

    <tr>
      <td>
        payment.gopaySource
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        GoPay source
      </td>
    </tr>

    <tr>
      <td>
        payment.gopayPaymentOption
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        GoPay payment options
      </td>
    </tr>

    <tr>
      <td>
        payment.merchantCrossReferenceId
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        GoPay unique ID per merchant as an identifier in tokenization activation
      </td>
    </tr>

    <tr>
      <td>
        payment.mandiriBillKey
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Mandiri Bill key
      </td>
    </tr>

    <tr>
      <td>
        payment.mandiriBillChannelId
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Mandiri Bill channel id
      </td>
    </tr>

    <tr>
      <td>
        payment.mandiriBillInfos
      </td>

      <td>
        Array of String
      </td>

      <td>
        O
      </td>

      <td>
        Mandiri Bill informations
      </td>
    </tr>

    <tr>
      <td>
        payment.mandiriBillPaidBills
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Mandiri Bill paid bills
      </td>
    </tr>

    <tr>
      <td>
        payment.mandiriBillPaymentAmount
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Mandiri Bill payment amount
      </td>
    </tr>

    <tr>
      <td>
        payment.akulakuOrderId
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Akulaku order id
      </td>
    </tr>

    <tr>
      <td>
        payment.akulakuPeriods
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Akulaku periods
      </td>
    </tr>

    <tr>
      <td>
        payment.\
        akulakuMonthlyInstallmentPayment
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Akulaku monthly installment payment
      </td>
    </tr>

    <tr>
      <td>
        payment.kredivoTransactionId
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Kredivo transaction id
      </td>
    </tr>

    <tr>
      <td>
        payment.kredivoInstallmentTerm
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Kredivo installment term
      </td>
    </tr>

    <tr>
      <td>
        payment.shopeepayTransactionId
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        ShopeePay transaction id
      </td>
    </tr>

    <tr>
      <td>
        payment.uobEzpayTransactionTime
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        UOB EZ Pay transaction time
      </td>
    </tr>

    <tr>
      <td>
        payment.uobEzpayNotificationId
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        UOB EZ Pay notification id
      </td>
    </tr>

    <tr>
      <td>
        payment.uobEzpayBankReference
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        UOB EZ Pay bank reference
      </td>
    </tr>

    <tr>
      <td>
        payment.\
        cimbClicksReferenceNumber
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        CIMB Clicks reference number
      </td>
    </tr>

    <tr>
      <td>
        payment.cimbClicksAuthCode
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        CIMB Clicks auth code
      </td>
    </tr>

    <tr>
      <td>
        payment.\
        bcaKlikpayTransactionNumber
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        BCA KlikPay transaction number
      </td>
    </tr>

    <tr>
      <td>
        payment.bcaKlikpayType
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        BCA KlikPay type
      </td>
    </tr>

    <tr>
      <td>
        payment.\
        bcaKlikbcaTransactionNumber
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        KlikBCA transaction number
      </td>
    </tr>

    <tr>
      <td>
        payment.bcaKlikbcaUserId
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        KlikBCA user id
      </td>
    </tr>

    <tr>
      <td>
        payment.\
        briEpayPaymentReferenceNumber
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        e-Pay BRI payment reference number
      </td>
    </tr>

    <tr>
      <td>
        payment.\
        briEpayBillReferenceNumber
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        e-Pay BRI bill reference number
      </td>
    </tr>

    <tr>
      <td>
        payment.briEpayUserFullName
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        e-Pay BRI user full name
      </td>
    </tr>

    <tr>
      <td>
        payment.mandiriEcashId
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Mandiri e-Cash id
      </td>
    </tr>

    <tr>
      <td>
        payment.mandiriEcashTraceNumber
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Mandiri e-Cash trace number
      </td>
    </tr>

    <tr>
      <td>
        payment.mandiriEcashPhoneNumber
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Mandiri e-Cash phone number
      </td>
    </tr>

    <tr>
      <td>
        payment.mandiriEcashDescription
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Mandiri e-Cash description
      </td>
    </tr>

    <tr>
      <td>
        payment.\
        danamonOnline\
        PaymentReferenceNumber
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Danamon Online payment reference number
      </td>
    </tr>

    <tr>
      <td>
        payment.\
        danamonOnlineBillReferenceNumber
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Danamon Online bill reference number
      </td>
    </tr>

    <tr>
      <td>
        payment.linkajaResultCode
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        LinkAja result code
      </td>
    </tr>

    <tr>
      <td>
        payment.linkajaReferenceId
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        LinkAja reference id
      </td>
    </tr>

    <tr>
      <td>
        payment.linkajaReceiptNumber
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        LinkAja receipt number
      </td>
    </tr>

    <tr>
      <td>
        payment.\
        linkajaOriginatorConversationId
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        LinkAja originator conversation id
      </td>
    </tr>

    <tr>
      <td>
        payment.linkajaConversationId
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        LinkAja conversation id
      </td>
    </tr>

    <tr>
      <td>
        payment.dbsPaylahMessageId
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        LinkAja message id
      </td>
    </tr>

    <tr>
      <td>
        payment.dbsPaylahReferenceId
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        DBS Paylah! reference id
      </td>
    </tr>

    <tr>
      <td>
        payment.paypalTransactionId
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        PayPal transaction id
      </td>
    </tr>

    <tr>
      <td>
        payment.refunds
      </td>

      <td>
        Array of Object
      </td>

      <td>
        O
      </td>

      <td>
        Refunds information
      </td>
    </tr>

    <tr>
      <td>
        refunds.id
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Refund id
      </td>
    </tr>

    <tr>
      <td>
        refunds.amount.value
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Refund amount of the transaction
      </td>
    </tr>

    <tr>
      <td>
        refunds.amount.currency
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Refund currency
      </td>
    </tr>

    <tr>
      <td>
        refunds.reason
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Refund reason
      </td>
    </tr>

    <tr>
      <td>
        refunds.createdTime
      </td>

      <td>
        String(25)
      </td>

      <td>
        O
      </td>

      <td>
        Refund created time in in ISO-8601 format
      </td>
    </tr>

    <tr>
      <td>
        refunds.bankConfirmedTime
      </td>

      <td>
        String(25)
      </td>

      <td>
        O
      </td>

      <td>
        Refund bank confirmed time in in ISO-8601 format
      </td>
    </tr>

    <tr>
      <td>
        refunds.cancelledTime
      </td>

      <td>
        String(25)
      </td>

      <td>
        O
      </td>

      <td>
        Refund cancelled time in in ISO-8601 format
      </td>
    </tr>

    <tr>
      <td>
        payment.customer
      </td>

      <td>
        Object
      </td>

      <td>
        O
      </td>

      <td>
        Customer information
      </td>
    </tr>

    <tr>
      <td>
        customer.firstName
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Customer first name
      </td>
    </tr>

    <tr>
      <td>
        customer.lastName
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Customer last name
      </td>
    </tr>

    <tr>
      <td>
        customer.email
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Customer email
      </td>
    </tr>

    <tr>
      <td>
        customer.phone
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Customer phone
      </td>
    </tr>

    <tr>
      <td>
        payment.shippingAddress
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Shipping address information
      </td>
    </tr>

    <tr>
      <td>
        shippingAddress.firstName
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Shipping first name
      </td>
    </tr>

    <tr>
      <td>
        shippingAddress.lastName
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Shipping last name
      </td>
    </tr>

    <tr>
      <td>
        shippingAddress.phone
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Shipping phone
      </td>
    </tr>

    <tr>
      <td>
        shippingAddress.postalCode
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Shipping postalCode
      </td>
    </tr>

    <tr>
      <td>
        shippingAddress.countryCode
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Shipping postal code
      </td>
    </tr>

    <tr>
      <td>
        shippingAddress.city
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Shipping city
      </td>
    </tr>

    <tr>
      <td>
        shippingAddress.address
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Shipping address
      </td>
    </tr>

    <tr>
      <td>
        payment.items
      </td>

      <td>
        Array of Object
      </td>

      <td>
        O
      </td>

      <td>
        Items information
      </td>
    </tr>

    <tr>
      <td>
        items.id
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Item identifier on service provider system
      </td>
    </tr>

    <tr>
      <td>
        items.partnerId
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Item identifier on service consumer system
      </td>
    </tr>

    <tr>
      <td>
        items.name
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Item name
      </td>
    </tr>

    <tr>
      <td>
        items.quantity
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Item quantity
      </td>
    </tr>

    <tr>
      <td>
        items.price.value
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Item price
      </td>
    </tr>

    <tr>
      <td>
        payment.promo
      </td>

      <td>
        Object
      </td>

      <td>
        O
      </td>

      <td>
        Promo information
      </td>
    </tr>

    <tr>
      <td>
        promo.id
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Promo identifier
      </td>
    </tr>

    <tr>
      <td>
        promo.code
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Promo code
      </td>
    </tr>

    <tr>
      <td>
        promo.name
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Promo name
      </td>
    </tr>

    <tr>
      <td>
        promo.sponsor
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Promo sponsor
      </td>
    </tr>

    <tr>
      <td>
        promo.originalAmount.value
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Promo original amount
      </td>
    </tr>

    <tr>
      <td>
        promo.discountAmount.value
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Promo discountAmount
      </td>
    </tr>

    <tr>
      <td>
        promo.userIp
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        User IP address when using the promo
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.withdrawal
      </td>

      <td>
        Object
      </td>

      <td>
        O
      </td>

      <td>
        Withdrawal related information
      </td>
    </tr>

    <tr>
      <td>
        withdrawal.bankName
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Withdrawal bank name
      </td>
    </tr>

    <tr>
      <td>
        withdrawal.bankCode
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Withdrawal bank code
      </td>
    </tr>

    <tr>
      <td>
        withdrawal.accountNo
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Withdrawal account number
      </td>
    </tr>

    <tr>
      <td>
        withdrawal.accountName
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Withdrawal account name
      </td>
    </tr>

    <tr>
      <td>
        withdrawal.requestedTime
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Withdrawal requested time in ISO-8601 format
      </td>
    </tr>

    <tr>
      <td>
        withdrawal.successTime
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Withdrawal success time in ISO-8601 format
      </td>
    </tr>

    <tr>
      <td>
        withdrawal.failedTime
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Withdrawal failed time in ISO-8601 format
      </td>
    </tr>

    <tr>
      <td>
        withdrawal.cancelledTime
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Withdrawal cancelled time in ISO-8601 format
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.disbursement
      </td>

      <td>
        Object
      </td>

      <td>
        O
      </td>

      <td>
        Disbursement related information
      </td>
    </tr>

    <tr>
      <td>
        disbursement.sourceBankCode
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Disbursement source bank code
      </td>
    </tr>

    <tr>
      <td>
        disbursement.sourceAccountNo
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Disbursement source account number
      </td>
    </tr>

    <tr>
      <td>
        disbursement.beneficiaryEmail
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Disbursement beneficiary email
      </td>
    </tr>

    <tr>
      <td>
        disbursement.beneficiaryName
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Disbursement beneficiary name
      </td>
    </tr>

    <tr>
      <td>
        disbursement.beneficiaryBankCode
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Disbursement beneficiary bank code
      </td>
    </tr>

    <tr>
      <td>
        disbursement.beneficiaryBankName
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Disbursement beneficiary bank name
      </td>
    </tr>

    <tr>
      <td>
        disbursement.beneficiaryAccountNo
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Disbursement beneficiary account number
      </td>
    </tr>

    <tr>
      <td>
        disbursement.creatorEmail
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Disbursement creator email
      </td>
    </tr>

    <tr>
      <td>
        disbursement.creatorName
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Disbursement creator name
      </td>
    </tr>

    <tr>
      <td>
        disbursement.approverEmail
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Disbursement approver email
      </td>
    </tr>

    <tr>
      <td>
        disbursement.approverName
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Disbursement approver name
      </td>
    </tr>

    <tr>
      <td>
        disbursement.requestedTime
      </td>

      <td>
        String(25)
      </td>

      <td>
        O
      </td>

      <td>
        Disbursement requested time in ISO-8601 format
      </td>
    </tr>

    <tr>
      <td>
        disbursement.approvedTime
      </td>

      <td>
        String(25)
      </td>

      <td>
        O
      </td>

      <td>
        Disbursement approved time in ISO-8601 format
      </td>
    </tr>

    <tr>
      <td>
        disbursement.rejectedTime
      </td>

      <td>
        String(25)
      </td>

      <td>
        O
      </td>

      <td>
        Disbursement rejected time in ISO-8601 format
      </td>
    </tr>

    <tr>
      <td>
        disbursement.processedTime
      </td>

      <td>
        String(25)
      </td>

      <td>
        O
      </td>

      <td>
        Disbursement processed time in ISO-8601 format
      </td>
    </tr>

    <tr>
      <td>
        disbursement.completedTime
      </td>

      <td>
        String(25)
      </td>

      <td>
        O
      </td>

      <td>
        Disbursement completed time in ISO-8601 format
      </td>
    </tr>

    <tr>
      <td>
        disbursement.failedTime
      </td>

      <td>
        String(25)
      </td>

      <td>
        O
      </td>

      <td>
        Disbursement failed time in ISO-8601 format
      </td>
    </tr>

    <tr>
      <td>
        disbursement.failureMessage
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Disbursement failure message
      </td>
    </tr>

    <tr>
      <td>
        disbursement.failureCode
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Disbursement failure code
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.fee
      </td>

      <td>
        Object
      </td>

      <td>
        M
      </td>

      <td>
        Fee information
      </td>
    </tr>

    <tr>
      <td>
        fee.value
      </td>

      <td>
        String(16,2)
      </td>

      <td>
        M
      </td>

      <td>
        Net amount of fee
      </td>
    </tr>

    <tr>
      <td>
        fee.currency
      </td>

      <td>
        String(3)
      </td>

      <td>
        M
      </td>

      <td>
        Currency
      </td>
    </tr>
  </tbody>
</Table>

```Text 200 OK
{
  "responseCode": "2001300",
  "responseMessage": "Success",
  "referenceNo": "2020102977770000000009",
  "partnerReferenceNo": "2020102900000000000001",
  "dateTime": "2019-07-03T12:08:56+07:00",
  "amount": {
    "value": "12345678.00",
    "currency": "IDR"
  },
  "remark": "Payment to Warung Ikan Bakar",
  "status": "SUCCESS",
  "type": "PAYMENT",
  "additionalInfo": {
    "status": "SETTLEMENT",
    "type": "PAYMENT",
    "updatedTime": "2019-07-03T12:08:56+07:00",
    "channel": "qris",
    "customerEmail": "john.doe@gmail.com",
    "accountNo": "123456",
    "payment": {
      "expiryTime": "2019-07-03T12:08:56+07:00",
      "source": "SNAP",
      "providerReferenceId": "A120240108151754NxoeRNYP4YID",
      "approvalCode": "100127",
      
      // Credit Card
      "cardNumber": "4556 5579 **** 6624",
      "cardType": "credit",
      "cardChannel": "mti",
      "cardChannelResponseCode": "00",
      "cardChannelResponseMessage": "Approved",
      "issuingBrand": "VISA",
      "issuingBank": "bca",
      "issuingCountryCode": "US",
      "issuingCountryName": "UNITEDSTATES",
      "acquiringBank": "mandiri",
      "retrievalReferenceNumber": "736620222955",
      "fdsRecommendation": "accept",
      "creditCardSecure": true,
      "bankMid": "1100889977",
      "bankResponseCode": "00",
      "isOneClick": false,
      "isTwoClick": false,
      "installmentTerm": "",
      "installmentType": "",
      "redeemedPointsAmount": {
        "value": "5000.00",
        "currency": "IDR"
      },
      "redeemedPointsQuantity": "10",
      "networkTransactionId": "606345944234331",
      
      // Convenient Store
      "store": "indomaret",
      "paymentCode": "901083200026",
      "trackingRef": "82851212597196801", // indomaret
      "agentTransactionId": "cZkpKVCOibLOeEp", // alfamart
      
      // Bank Transfer / Virtual Account
      "virtualAccountNumber": "96883778474",
      "bcaVaChannel": "Internet Banking",
      "bniVaType": "open_payment",
      "bniLeftAmount": {
        "value": "-3.00",
        "currency": "IDR"
      },
        
      // QRIS
      "qrisOnUs": false,
      "qrisReferenceNumber": "A120240108151754NxoeRNYP4YID",
      "qrisIssuer": "gopay",
      "qrisIssuerTransactionId": "A120240108151754NxoeRNYP4YID",
      "qrisAcquirer": "gopay",
      "qrisAcquirerTransactionId": "A120240108151754NxoeRNYP4YID",
        
      // GoPay
      "gopaySource": "gopay_online",
      "gopayPaymentOption": "GOPAY_WALLET",
      "merchantCrossReferenceId": "760fbd7c-6720-4bb6-88f9-2a75ad8c1173",
      
      // Mandiri Bill
      "mandiriBillKey": "213916480962",
      "mandiriBillInfos": ["rizvi gopay"],
      "mandiriBillChannelId": "1234",
      "mandiriBillPaidBills": "01",
      "mandiriBillPaymentAmount": {
        "value": "10000.00",
        "currency": "IDR"
      },
      
      // Akulaku
      "akulakuOrderId": "A120240223061624q0ouIEgan1ID-1",
      "akulakuPeriods": "",
      "akulakuMonthlyInstallmentPayment": "5000",
      
      // Kredivo
      "kredivoTransactionId": "12a1c87c-74c9-4819-aa37-4f74acff9c07",
      "kredivoInstallmentTerm": "30_days",
      
      // ShopeePay
      "shopeepayTransactionId": "960774027066627564",
      
      // UOB EZ Pay
      "uobEzpayTransactionTime": "2019-07-03T12:08:56+07:00",
      "uobEzpayNotificationId": "asdfgh",
      "uobEzpayBankReference": "zxcvbn",
     
      // CIMB Clicks
      "cimbClicksReferenceNumber": "000000000000071969",
      "cimbClicksAuthCode": "1708428664718",
     
      // BCA KlikPay
      "bcaKlikpayTransactionNumber": "1693622",
      "bcaKlikpayType": "1",
      
      // KlikBCA
      "bcaKlikbcaTransactionNumber": "12078115af80447e97",
      "bcaKlikbcaUserId": "testuser01",
      
      // e-Pay BRI
      "briEpayPaymentReferenceNumber": "1696937935399",
      "briEpayBillReferenceNumber": "294634661",
      "briEpayUserFullName": "Midtrans",
      
      // Mandiri e-Cash
      "mandiriEcashId": "cf7989fe-1873-4ecd-a933-3c833a8b9f8b",
      "mandiriEcashTraceNumber": "xyzxyz",
      "mandiriEcashPhoneNumber": "0987654321",
      "mandiriEcashDescription": "Transaction Description",
      
      // Danamon Online
      "danamonOnlinePaymentReferenceNumber": "i1ji2X9Rzc19GR",
      "danamonOnlineBillReferenceNumber": "166526",
      
      // LinkAja
      "linkajaResultCode": "0",
      "linkajaReceiptNumber": "D5AF930801",
      "linkajaReferenceId": "test-order-1706005255",
      "linkajaOriginatorConversationId": "6310bd69-ddea-4550-a746-a6afce00a7ef",
      "linkajaConversationId": "01HMTXCNTGZNPHRZ6X4804VFAY",
      
      // DBS PayLah!
      "dbsPaylahReferenceId": "17086717018447aab035",
      "dbsPaylahMessageId": "a4-9c7c-05a98c507aab",
        
      // PayPal
      "paypalTransactionId": "qee0evgt",
      
      "refunds": [
        {
          "id": "12345",
          "amount": {
            "value": "5000.00",
            "currency": "IDR"
          },
          "reason": "need to refund",
          "createdTime": "2019-07-03T12:08:56+07:00",
          "bankConfirmedTime": "2019-07-03T12:08:56+07:00",
          "cancelledTime": "2019-07-03T12:08:56+07:00"
        }
      ],
      "customer": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@gmail.com",
        "phone": "+62812131415"
      },
      "shippingAddress": {
        "firstName": "John",
        "lastName": "Doe",
        "phone": "+62812131415",
        "postalCode": "123456",
        "countryCode": "21",
        "city": "Jakarta",
        "address": "Pasaraya Blok M"
      },
      "items": [
        {
          "id": "2a17f5a2-4150-31db-9880-b10dd503c93d",
          "partnerId": "item001",
          "name": "Test item",
          "quantity": "1",
          "price": {
            "value": "10000.00",
            "currency": "IDR"
          }
        }
      ],
      "promo": {
        "id": "promo1",
        "code": "TESTPROMO",
        "name": "Promo buy 1 get 2",
        "sponsor": "Midtrans",
        "originalAmount": {
          "value": "25000.00",
          "currency": "IDR"
        },
        "discountAmount": {
          "value": "5000.00",
          "currency": "IDR"
        },
        "userIp": "10.128.20.227"
      }
    },
    "withdrawal": {
      "bankName": "PT. BANK MANDIRI (PERSERO) TBK.",
      "bankCode": "mandiri",
      "accountNo": "1111222233333",
      "accountName": "Mandiri Simulator A",
      "requestedTime": "2019-07-03T12:08:56+07:00",
      "successTime": "2019-07-03T12:08:56+07:00",
      "failedTime": "2019-07-03T12:08:56+07:00",
      "cancelledTime": "2019-07-03T12:08:56+07:00"
    },
    "disbursement": {
      "sourceBankCode": "bca",
      "sourceAccountNo": "4433221100",
      "beneficiaryEmail": "rizvi.sofbrina@gojek.com",
      "beneficiaryName": "BCA Simulator A",
      "beneficiaryBankCode": "bca",
      "beneficiaryBankName": "PT. BANK CENTRAL ASIA TBK.",
      "beneficiaryAccountNo": "0011223344",
      "creatorEmail": "mla.creator@gmail.com",
      "creatorName": "MLA creator",
      "approverEmail": "mla.approver@gmail.com",
      "approverName": "MLA approver",
      "requestedTime": "2019-07-03T12:08:56+07:00",
      "approvedTime": "2019-07-03T12:08:56+07:00",
      "rejectedTime": "2019-07-03T12:08:56+07:00",
      "processedTime": "2019-07-03T12:08:56+07:00",
      "completedTime": "2019-07-03T12:08:56+07:00",
      "failedTime": "2019-07-03T12:08:56+07:00",
      "failureMessage": "invalid destination account number",
      "failureCode": "002"
    },
    "fee": {
      "value": "1000.00",
      "currency": "IDR"
    }
  }
}
```
```Text 401 Unauthorized
{
  "responseCode": "4011200", 
  "responseMessage": "Unauthorized. Client"
}
```

<br />

## List of Response Codes

| Response Code | HTTP Status | Description                                                     |
| :------------ | :---------- | :-------------------------------------------------------------- |
| 2001300       | 200         | Successful                                                      |
| 4001301       | 400         | Invalid field format \{........}                                |
| 4001302       | 400         | Missing mandatory field \{........}                             |
| 4011300       | 401         | Unauthorized signature                                          |
| 4011301       | 401         | Access token invalid                                            |
| 4041301       | 404         | Transaction not found                                           |
| 4091300       | 409         | Cannot use same X-EXTERNAL-ID in same day                       |
| 5001301       | 500         | Unknown internal server failure, please retry the process again |