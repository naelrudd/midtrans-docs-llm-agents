---
updatedAt: 2026-03-02T04:30:36.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Payment Notification API

In the SNAP-based Core API flow, Midtrans will call Payment Notification API on the merchant side to send payment notifications. Merchant should implement this Payment Notification API as stated in the contract below.

<Callout icon="📘" theme="info">
  Midtrans will generate a pair of **private and public key** for signature generation and share the public key to merchant. Merchant will then need to give Midtrans a **partner id** that will be used in request header as **X-PARTNER-ID**.
</Callout>

<Callout icon="🚧" theme="warn">
  Please make sure to whitelist this set of IPs to be able to accept notification from Midtrans.

  <Table align={["left","left"]}>
    <thead>
      <tr>
        <th style={{ textAlign: "left" }}>
          Environment
        </th>

        <th style={{ textAlign: "left" }}>
          IPs
        </th>
      </tr>
    </thead>

    <tbody>
      <tr>
        <td style={{ textAlign: "left" }}>
          Staging
        </td>

        <td style={{ textAlign: "left" }}>
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
        <td style={{ textAlign: "left" }}>
          Sandbox
        </td>

        <td style={{ textAlign: "left" }}>
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
        <td style={{ textAlign: "left" }}>
          Production
        </td>

        <td style={{ textAlign: "left" }}>
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
</Callout>

> ⚠️ **Notes on Future Compatibility and Best Practices**
>
> To ensure your integration remains robust and scalable, please be aware that Midtrans **may introduce additional parameters** to the payment notification payload in the future, most likely under the additionalInfo section, but not limited to it. These enhancements are designed to provide greater flexibility and support for evolving business needs.
>
> To prevent any issues caused by these future changes, we strongly recommend that merchants always perform **signature verification on the entire payload**, rather than validating fields individually. This practice ensures a seamless, secure, and simple implementation that can adapt to future updates without requiring significant changes on your side.

## Receiving payment notifications for GoPay and GoPay Tokenization (non Pre-Auth) transaction

This section will describe how merchant should implement payment notification API for GoPay and GoPay Tokenization (non-Pre Auth) transactions for Midtrans to call.

| Path              | /`{version}`/debit/notify |
| :---------------- | :------------------------ |
| HTTP Method       | POST                      |
| Version           | v1.0                      |
| SNAP Service Code | 56                        |

<br />

### Request Header

<table>
  <tr>
    <td><strong>Field Name</strong></td>
    <td><strong>Field Type</strong></td>
    <td><strong>Mandatory</strong></td>
    <td colspan="2"><strong>Field Description</strong></td>
  </tr>

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

    <td colspan="2">
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

    <td colspan="2">
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

    <td colspan="2">
      Created using asymmetric signature

      <p>
        Asymmetric-Signature format:
      </p>

      <p>
        SHA256withRSA (privateKey, stringToSign) with
      </p>

      <p>
        stringToSign = HTTPMethod +”:“+ EndpointUrl +":“+ Lowercase(HexEncode(SHA-256(minify(RequestBody)))) + ":“ + TimeStamp
      </p>
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

    <td colspan="2">
      Unique identifier for partner
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

    <td colspan="2">
      Numeric string. Reference number that should be unique in the same day or 1 day idempotency key
    </td>
  </tr>
</table>

```
Content-type:application/json
X-TIMESTAMP:2024-03-19T14:30:00+07:00
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
X-PARTNER-ID: 
X-EXTERNAL-ID:12345678901234567890
CHANNEL-ID:12345
```

<br />

### Request Body

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td>
      <strong>Field Description</strong>
    </td>
  </tr>

  <tr>
    <td>
      createdTime
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td>
      Transaction created timestamp
    </td>
  </tr>

  <tr>
    <td>
      latestTransactionStatus
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Latest transaction status

      <p>
        <strong>Possible Values: </strong>
      </p>

      <ul>
        <li>00 - Success</li>

        <li>03 - Pending</li>

        <li>04 - Refunded</li>

        <li>05 - Canceled</li>

        <li>06 - Failure</li>

        <li> 08 - Expiry </li>

        <li> 09 - Rejected</li>
      </ul>
    </td>
  </tr>

  <tr>
    <td>
      originalReferenceNo
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Transaction identifier on service provider system. For e.g: GopayOrderId<strong> </strong>
    </td>
  </tr>

  <tr>
    <td>
      finishedTime
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td>
      Transaction completed timestamp (for latestTranscationStatus = 00)
    </td>
  </tr>

  <tr>
    <td>
      originalPartnerReferenceNo
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td>
      Original transaction identifier on service consumer system. (Merchant’s orderId)
    </td>
  </tr>

  <tr>
    <td>
      originalExternalId
    </td>

    <td>
      String(36)
    </td>

    <td>
      O
    </td>

    <td>
      Original External-ID on header message when doing charge (/payment-host-to-host)
    </td>
  </tr>

  <tr>
    <td>
      merchantId
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td>
      Merchant ID
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
      O
    </td>

    <td>
      Transaction amount
    </td>
  </tr>

  <tr>
    <td>
      amount.value
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Transaction amount
    </td>
  </tr>

  <tr>
    <td>
      amount.currency
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Transaction currency
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
      M
    </td>

    <td>
      Additional info
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory
    </td>

    <td>
      Array of Object
    </td>

    <td>
      C
    </td>

    <td>
      Array of refund transactions. Only available if transaction status is <code>refund</code>
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundNo
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Unique identifier of refund transaction generated by provider.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundStatus
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Refund status. Possible values:<br />

      * 00 --> Refund success<br />
      * 06 --> Refund failed
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.partnerRefundNo
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Unique identifier of refund transaction generated by client.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundAmount
    </td>

    <td>
      Object
    </td>

    <td>
      M
    </td>

    <td>
      Refund amount
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundAmount.value
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Net amount of the refund. If it's IDR then the value includes 2 decimal digits.

      <p>
        e.g. IDR 10.000,- will be placed with 10000.00
      </p>
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundAmount.currency
    </td>

    <td>
      String
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
      additionalInfo.refundHistory.reason
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Refund reason
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundTime
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Refund time
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.totalRefundAmount
    </td>

    <td>
      Object
    </td>

    <td>
      C
    </td>

    <td>
      Total refund amount. Only available if transaction status is <code>refund</code> or <code>partial refund</code>.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.totalRefundAmount.value
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Total refund amount. If it's IDR then the value includes 2 decimal digits.

      <p>
        e.g. IDR 10.000,- will be placed with 10000.00
      </p>
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.totalRefundAmount.currency
    </td>

    <td>
      String
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
      additionalInfo.userPaymentDetails
    </td>

    <td>
      Array of object
    </td>

    <td>
      M
    </td>

    <td>
      Payment option used by user. This will be not available for deeplink redirection payment flow with <b>pending</b> status.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.userPaymentDetails.payMethod
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Payment method used by user. E.g: gopay
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.userPaymentDetails.payOption
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Payment option used by user. <br /> Possible value: <br /> - GoPay = `GOPAY_WALLET` <br /> - GoPay Later = `PAY_LATER` <br /> - GoPay Tabungan by Jago = `GOPAY_SAVINGS`
    </td>
  </tr>
</table>

```
{
    "createdTime": "2020-01-01T00:00:00+07:00",
    "latestTransactionStatus": "00",
    "originalReferenceNo": "gopayOrderId",
    "finishedTime": "2020-01-02T00:00:00+07:00",
    "originalPartnerReferenceNo": "merchant-order-id",
    "transactionStatusDesc": "desc",
   "originalExternalId":"merchant-order-id",
    "additionalInfo": { 
        "userPaymentDetails": [
         {
           "payMethod": "gopay",
           "payOption": "GOPAY_WALLET"
         }
        ],
         "refundHistory":[
  	{
     	     	"refundNo":"96194816941239812",
      			"refundStatus":"00",
     	     	"partnerReferenceNo":"239850918204981205970",
          		"refundAmount":{
          	   	     	"value":"12345678.00",
         	    	     	"currency":"IDR"
     	     	},
     	     	"refundDate":"2020-12-23T07:44:16+07:00",
          		"reason":"Customer Complain"
  	}
   ]
    }
}
```

<br />

### Response Header

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td colspan="2">
      <strong>Field Description</strong>
    </td>
  </tr>

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

    <td colspan="2">
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

    <td colspan="2">
      Client’s current local time in ISO-8601 format
    </td>
  </tr>
</table>

```
Content-type: application/json
X-TIMESTAMP: 2024-03-19T14:30:00+07:00
```

<br />

### Response Body

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td colspan="2">
      <strong>Field Description</strong>
    </td>
  </tr>

  <tr>
    <td>
      responseCode
    </td>

    <td>
      String (7)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Error code to specify the error returned.
    </td>
  </tr>

  <tr>
    <td>
      responseMessage
    </td>

    <td>
      String (150)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Debug message to provide more information.
    </td>
  </tr>
</table>

```
{
   "responseCode":"2005600",
   "responseMessage":"Request has been processed successfully"
}
```

<br />

***

## Receiving payment notifications for GoPay QRIS transaction

This section will describe how merchant should implement payment notification API for GoPay QRIS transactions for Midtrans to call.

| Path              | /`{version}`/qr/qr-mpm-notify |
| :---------------- | :---------------------------- |
| HTTP Method       | POST                          |
| Version           | v1.0                          |
| SNAP service code | 52                            |

### Request Header

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td colspan="2">
      <strong>Field Description</strong>
    </td>
  </tr>

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

    <td colspan="2">
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

    <td colspan="2">
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

    <td colspan="2">
      Created using asymmetric signature

      <p>
        Asymmetric-Signature format :
      </p>

      <p>
        SHA256withRSA (privateKey, stringToSign) with
      </p>

      <p>
        stringToSign = HTTPMethod +”:“+ EndpointUrl +":“+ Lowercase(HexEncode(SHA-256(minify(RequestBody)))) + ":“ + TimeStamp
      </p>
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

    <td colspan="2">
      Unique identifier for caller
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

    <td colspan="2">
      Numeric string. Reference number that should be unique in the same day or 1 day idempotency key
    </td>
  </tr>
</table>

```
Content-type:application/json
X-TIMESTAMP:2020-01-01T00:00:00+07:00
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
X-PARTNER-ID: 
X-EXTERNAL-ID:12345678901234567890
```

### Request Body

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td>
      <strong>Field Description</strong>
    </td>
  </tr>

  <tr>
    <td>
      originalReferenceNo
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Transaction identifier on service provider system. For e.g: GopayOrderId<strong> </strong>
    </td>
  </tr>

  <tr>
    <td>
      originalPartnerReferenceNo
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td>
      Original transaction identifier on service consumer system. (Merchant’s orderId)
    </td>
  </tr>

  <tr>
    <td>
      latestTransactionStatus
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Latest transaction status

      <p>
        <strong>Possible Values: </strong>
      </p>

      <ul>
        <li>00 - Success</li>

        <li>03 - Pending</li>

        <li>04 - Refunded</li>

        <li>05 - Canceled</li>

        <li>06 - Failure</li>

        <li> 08 - Expiry</li>

        <li> 09 - Rejected</li>
      </ul>
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
      O
    </td>

    <td>
      Amount of the order
    </td>
  </tr>

  <tr>
    <td>
      amount.value
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Transaction amount
    </td>
  </tr>

  <tr>
    <td>
      amount.currency
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Transaction currency
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
      M
    </td>

    <td>
      Additional info
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory
    </td>

    <td>
      Array of Object
    </td>

    <td>
      C
    </td>

    <td>
      Array of refund transactions. Only available if transaction status is <code>refund</code>
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundNo
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Unique identifier of refund transaction generated by provider.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.partnerReferenceNo
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Unique identifier of refund transaction generated by client.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundAmount
    </td>

    <td>
      Object
    </td>

    <td>
      M
    </td>

    <td>
      Refund amount
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundAmount.value
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Net amount of the refund. If it's IDR then the value includes 2 decimal digits.

      <p>
        e.g. IDR 10.000,- will be placed with 10000.00
      </p>
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundAmount.currency
    </td>

    <td>
      String
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
      additionalInfo.refundHistory.reason
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Refund reason
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundDate
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Refund time
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.qris
    </td>

    <td>
      Array of Object
    </td>

    <td>
      C
    </td>

    <td>
      Array of QRIS transaction information, based on ASPI's regulation
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.qris.issuerName
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Issuer company for the payment process
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.qris.acquirerName
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Acquirer company for the payment process
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.qris.transactionType
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      ASPI Transaction type based on the combination of issuer and acquirer (if the issuer and acquirer is the same will be ON-US, if it's different will become OFF-US)
    </td>
  </tr>
</table>

```
{
   "originalReferenceNo":"2020102977770000000009",
   "originalPartnerReferenceNo":"2020102900000000000001",
   "latestTransactionStatus":"00",
   "transactionStatusDesc":"success",
   "amount":{
      "value":"12345678.00",
      "currency":"IDR"
   },
   "externalStoreID":"124928924949487",
   "additionalInfo":{
     "qris" :{
       "issuerName":"gopay"
       "acquirerName":"gopay"
       "transactionType":"ON-US"
     }
   }
}
```

### Response Header

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td colspan="2">
      <strong>Field Description</strong>
    </td>
  </tr>

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

    <td colspan="2">
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

    <td colspan="2">
      Client’s current local time in ISO-8601 format
    </td>
  </tr>
</table>

```
Content-type: application/json
X-TIMESTAMP: 2024-03-19T14:30:00+07:00
```

### Response Body

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td colspan="2">
      <strong>Field Description</strong>
    </td>
  </tr>

  <tr>
    <td>
      responseCode
    </td>

    <td>
      String (7)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Error code to specify the error returned.
    </td>
  </tr>

  <tr>
    <td>
      responseMessage
    </td>

    <td>
      String (150)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Debug message to provide more information.
    </td>
  </tr>
</table>

```
{
   "responseCode":"2005200",
   "responseMessage":"Request has been processed successfully"
}
```

### List of response code

<table>
  <tr>
    <td>
      <strong>Response Code</strong>
    </td>

    <td>
      <strong>HTTP Status</strong>
    </td>

    <td>
      <strong>Description</strong>
    </td>
  </tr>

  <tr>
    <td>
      2005200
    </td>

    <td>
      200
    </td>

    <td>
      Successful
    </td>
  </tr>

  <tr>
    <td>
      2025200
    </td>

    <td>
      202
    </td>

    <td>
      Transaction still on process
    </td>
  </tr>

  <tr>
    <td>
      4005200
    </td>

    <td>
      400
    </td>

    <td>
      General request failed error, including message parsing failed.
    </td>
  </tr>

  <tr>
    <td>
      4005201
    </td>

    <td>
      400
    </td>

    <td>
      Invalid format
    </td>
  </tr>

  <tr>
    <td>
      4005202
    </td>

    <td>
      400
    </td>

    <td>
      Missing or invalid format on mandatory field
    </td>
  </tr>

  <tr>
    <td>
      4015200
    </td>

    <td>
      401
    </td>

    <td>
      General unauthorized error (No Interface Def, API is Invalid, Oauth Failed, Verify Client Secret Fail, Client Forbidden Access API, Unknown Client, Key not Found)
    </td>
  </tr>

  <tr>
    <td>
      4015201
    </td>

    <td>
      401
    </td>

    <td>
      Token found in request is invalid (Access Token Not Exist, Access Token Expiry)
    </td>
  </tr>

  <tr>
    <td>
      4015203
    </td>

    <td>
      401
    </td>

    <td>
      Token not found in the system. This occurs on any API that requires token as input parameter
    </td>
  </tr>

  <tr>
    <td>
      4035200
    </td>

    <td>
      403
    </td>

    <td>
      Transaction expired
    </td>
  </tr>

  <tr>
    <td>
      4035201
    </td>

    <td>
      403
    </td>

    <td>
      This merchant is not allowed to call Direct Debit APIs
    </td>
  </tr>

  <tr>
    <td>
      4035202
    </td>

    <td>
      403
    </td>

    <td>
      Exceeds Transaction Amount Limit
    </td>
  </tr>

  <tr>
    <td>
      4035203
    </td>

    <td>
      403
    </td>

    <td>
      Suspected Fraud
    </td>
  </tr>

  <tr>
    <td>
      4035204
    </td>

    <td>
      403
    </td>

    <td>
      Too many request, Exceeds Transaction Frequency Limit
    </td>
  </tr>

  <tr>
    <td>
      4035205
    </td>

    <td>
      403
    </td>

    <td>
      Account or User status is abnormal
    </td>
  </tr>

  <tr>
    <td>
      4035206
    </td>

    <td>
      403
    </td>

    <td>
      Cut off In Progress
    </td>
  </tr>

  <tr>
    <td>
      4035209
    </td>

    <td>
      403
    </td>

    <td>
      The account is dormant
    </td>
  </tr>

  <tr>
    <td>
      4035214
    </td>

    <td>
      403
    </td>

    <td>
      Insufficient Funds
    </td>
  </tr>

  <tr>
    <td>
      4035215
    </td>

    <td>
      403
    </td>

    <td>
      Transaction Not Permitted
    </td>
  </tr>

  <tr>
    <td>
      4035216
    </td>

    <td>
      403
    </td>

    <td>
      Suspend Transaction
    </td>
  </tr>

  <tr>
    <td>
      4035218
    </td>

    <td>
      403
    </td>

    <td>
      Indicates inactive account
    </td>
  </tr>

  <tr>
    <td>
      4035219
    </td>

    <td>
      403
    </td>

    <td>
      Merchant is suspended from calling any APIs
    </td>
  </tr>

  <tr>
    <td>
      4035220
    </td>

    <td>
      403
    </td>

    <td>
      Merchant aggregated purchase amount on that day exceeds the agreed limit
    </td>
  </tr>

  <tr>
    <td>
      4035221
    </td>

    <td>
      403
    </td>

    <td>
      Set limit not allowed on particular token
    </td>
  </tr>

  <tr>
    <td>
      4035222
    </td>

    <td>
      403
    </td>

    <td>
      The token limit desired by the merchant is not within the agreed range between the merchant and the Issuer
    </td>
  </tr>

  <tr>
    <td>
      4035223
    </td>

    <td>
      403
    </td>

    <td>
      Account aggregated purchase amount on that day exceeds the agreed limit
    </td>
  </tr>

  <tr>
    <td>
      4045200
    </td>

    <td>
      404
    </td>

    <td>
      Invalid transaction status
    </td>
  </tr>

  <tr>
    <td>
      4045201
    </td>

    <td>
      404
    </td>

    <td>
      Transaction not found
    </td>
  </tr>

  <tr>
    <td>
      4045202
    </td>

    <td>
      404
    </td>

    <td>
      Invalid Routing
    </td>
  </tr>

  <tr>
    <td>
      4045204
    </td>

    <td>
      404
    </td>

    <td>
      Transaction is cancelled by customer
    </td>
  </tr>

  <tr>
    <td>
      4045208
    </td>

    <td>
      404
    </td>

    <td>
      Merchant does not exist or status abnormal
    </td>
  </tr>

  <tr>
    <td>
      4045210
    </td>

    <td>
      404
    </td>

    <td>
      Invalid API transition within a journey
    </td>
  </tr>

  <tr>
    <td>
      4045213
    </td>

    <td>
      404
    </td>

    <td>
      The amount doesn't match with what supposed to
    </td>
  </tr>

  <tr>
    <td>
      4045216
    </td>

    <td>
      404
    </td>

    <td>
      Partner number can't be found
    </td>
  </tr>

  <tr>
    <td>
      4045217
    </td>

    <td>
      404
    </td>

    <td>
      Terminal does not exist in the system
    </td>
  </tr>

  <tr>
    <td>
      4045218
    </td>

    <td>
      404
    </td>

    <td>
      Inconsistent request parameter
    </td>
  </tr>

  <tr>
    <td>
      4055200
    </td>

    <td>
      405
    </td>

    <td>
      Requested function is not supported
    </td>
  </tr>

  <tr>
    <td>
      4055201
    </td>

    <td>
      405
    </td>

    <td>
      Requested operation to cancel/refund transaction Is not allowed at this time.
    </td>
  </tr>

  <tr>
    <td>
      4095200
    </td>

    <td>
      409
    </td>

    <td>
      Cannot use same X-EXTERNAL-ID in same day
    </td>
  </tr>

  <tr>
    <td>
      4095201
    </td>

    <td>
      409
    </td>

    <td>
      Transaction has previously been processed indicates the same partnerReferenceNo already success
    </td>
  </tr>

  <tr>
    <td>
      4295200
    </td>

    <td>
      429
    </td>

    <td>
      Maximum transaction limit exceeded
    </td>
  </tr>

  <tr>
    <td>
      5005200
    </td>

    <td>
      500
    </td>

    <td>
      General Error
    </td>
  </tr>

  <tr>
    <td>
      5005201
    </td>

    <td>
      500
    </td>

    <td>
      Unknown Internal Server Failure, Please retry the process again
    </td>
  </tr>

  <tr>
    <td>
      5005202
    </td>

    <td>
      500
    </td>

    <td>
      Backend system failure, etc
    </td>
  </tr>

  <tr>
    <td>
      5045200
    </td>

    <td>
      504
    </td>

    <td>
      timeout from the issuer
    </td>
  </tr>
</table>

## Receiving payment notifications for Bank Transfer (VA)

This section will describe how merchant should implement payment notification API for Bank Transfer (VA) transactions for Midtrans to call.

| Path              | /`{version}`/transfer-va/payment |
| :---------------- | :------------------------------- |
| HTTP Method       | POST                             |
| Version           | v1.0                             |
| SNAP service code | 25                               |

### Request Header

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td colspan="2">
      <strong>Field Description</strong>
    </td>
  </tr>

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

    <td colspan="2">
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

    <td colspan="2">
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

    <td colspan="2">
      Created using asymmetric signature

      <p>
        Asymmetric-Signature format :
      </p>

      <p>
        SHA256withRSA (privateKey, stringToSign) with
      </p>

      <p>
        stringToSign = HTTPMethod +”:“+ EndpointUrl +":“+ Lowercase(HexEncode(SHA-256(minify(RequestBody)))) + ":“ + TimeStamp
      </p>
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

    <td colspan="2">
      Unique identifier for caller
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

    <td colspan="2">
      Numeric string. Reference number that should be unique in the same day or 1 day idempotency key
    </td>
  </tr>
</table>

```
Content-type:application/json
X-TIMESTAMP:2020-01-01T00:00:00+07:00
X-SIGNATURE:da1fa417c72d6b91c257e01e54fac824
X-PARTNER-ID:G12345678
X-EXTERNAL-ID:12345678901234567890
```

### Request Body

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td colspan="2">
      <strong>Field Description</strong>
    </td>
  </tr>

  <tr>
    <td>
      partnerServiceId
    </td>

    <td>
      String(8)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      partnerServiceId from the virtual account number
    </td>
  </tr>

  <tr>
    <td>
      customerNo
    </td>

    <td>
      String(20)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      customerNo from the virtual account number
    </td>
  </tr>

  <tr>
    <td>
      virtualAccountNo
    </td>

    <td>
      String(28)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Virtual account number for the transaction
    </td>
  </tr>

  <tr>
    <td>
      virtualAccountName
    </td>

    <td>
      String(255)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      The customer name
    </td>
  </tr>

  <tr>
    <td>
      virtualAccountEmail
    </td>

    <td>
      String(255)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      The customer’s email
    </td>
  </tr>

  <tr>
    <td>
      virtualAccountPhone
    </td>

    <td>
      String(30)
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      The customer’s phone number
    </td>
  </tr>

  <tr>
    <td>
      trxId
    </td>

    <td>
      String(64)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      This value will be the <em>trxId </em>used in the create VA request.
    </td>
  </tr>

  <tr>
    <td>
      paymentRequestId
    </td>

    <td>
      String
    </td>

    <td>
      C
    </td>

    <td colspan="2">
      Unique identifier for this Payment from Midtrans.

      <p>
        This value will exist if the payment has been completed
      </p>
    </td>
  </tr>

  <tr>
    <td>
      paidAmount
    </td>

    <td>
      Object
    </td>

    <td>
      C
    </td>

    <td colspan="2">
      Amount paid for this transaction

      <p>
        This value will exist if the payment has been completed
      </p>
    </td>
  </tr>

  <tr>
    <td>
      paidAmount.value
    </td>

    <td>
      String(16, 2)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      The numeric string of the amount up to two decimal places
    </td>
  </tr>

  <tr>
    <td>
      paidAmount.currency
    </td>

    <td>
      String(3)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      The currency of the value paid. Should be IDR
    </td>
  </tr>

  <tr>
    <td>
      referenceNo
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td colspan="2">
      Payment auth code generated by Midtrans
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

    <td colspan="2" />
  </tr>

  <tr>
    <td>
      additionalInfo.bank
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Indicates the bank chosen to create the VA at. The banks that can be used will differ based on the banks chosen by the merchant during the onboarding process. Possible values are

      <ul>
        <li>Permata</li>

        <li>BCA</li>

        <li>Mandiri</li>

        <li>CIMB</li>

        <li>BNI</li>

        <li>BRI</li>
      </ul>
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.merchantId
    </td>

    <td>
      String(10)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      This is the <em>merchantId </em>shared by Midtrans during the onboarding process
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.paymentFlagStatus
    </td>

    <td>
      String(2)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Status for Payment Flag

      <p>
        00 - Success
      </p>

      <p>
        01 - Initiated
      </p>

      <p>
        02 - Paying
      </p>

      <p>
        03 - Pending
      </p>

      <p>
        04 - Refunded
      </p>

      <p>
        05 - Canceled
      </p>

      <p>
        06 - Failed
      </p>

      <p>
        07 - Not found
      </p>

      <p>
        08 - Expired
      </p>

      <p>
        09 - Denied
      </p>
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.paidTime
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Time when transaction is settled.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customField
    </td>

    <td>
      Object
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      A collection of up to three fields sent by the merchant. It will also be displayed on the Dashboard under “order detail”
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customField.1
    </td>

    <td>
      String(255)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      First field that contains the custom data set by the merchant
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customField.2
    </td>

    <td>
      String(255)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Second field that contains the custom data set by the merchant
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.customField.3
    </td>

    <td>
      String(255)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Third field that contains the custom data set by the merchant
    </td>
  </tr>
</table>

```
{
    "partnerServiceId":"  088899",
    "customerNo":"12345678901234567890",
    "virtualAccountNo":"  08889912345678901234567890",
    "virtualAccountName":"Jokul Doe",
    "virtualAccountEmail":"jokul@email.com",
    "virtualAccountPhone":"6281828384858",
    "trxId":"abcdefgh1234",
    "paymentRequestId":"abcdef-123456-abcdef",
    "paidAmount":{
       "value":"12345678.00",
       "currency":"IDR"
    },
    "referenceNo":"123456789012345",
    "additionalInfo":{
       "bank":"BCA",
       "paymentFlagStatus": "00",
       "merchantId":"G059876677",
       "paidTime":"2020-01-01T00:00:00+07:00",  
       "customField": {
          "1": "custom-field-1",
          "2": "custom-field-2",
          "3": "custom-field-3"
       }
    }
 }

```

### Response Header

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td colspan="2">
      <strong>Field Description</strong>
    </td>
  </tr>

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

    <td colspan="2">
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

    <td colspan="2">
      Client’s current local time in ISO-8601 format
    </td>
  </tr>
</table>

```
Content-type:application/json
X-TIMESTAMP:2020-01-01T00:00:00+07:00
```

### Response Body

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td colspan="2">
      <strong>Field Description</strong>
    </td>
  </tr>

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

    <td colspan="2">
      Response code
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

    <td colspan="2">
      Response description
    </td>
  </tr>

  <tr>
    <td>
      virtualAccountData
    </td>

    <td>
      Object
    </td>

    <td>
      M
    </td>

    <td colspan="2" />
  </tr>

  <tr>
    <td>
      virtualAccountData.partnerServiceId
    </td>

    <td>
      String(8)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      partnerServiceId from Create VA Response
    </td>
  </tr>

  <tr>
    <td>
      virtualAccountData.customerNo
    </td>

    <td>
      String(29)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      customerNo from Create VA Response
    </td>
  </tr>

  <tr>
    <td>
      virtualAccountData.virtualAccountNo
    </td>

    <td>
      String(28)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Virtual account number for the transaction
    </td>
  </tr>

  <tr>
    <td>
      virtualAccountData.trxId
    </td>

    <td>
      String(64)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      This value will be the <em>trxId </em>used in the create VA request.
    </td>
  </tr>
</table>

```
{
    "responseMessage": "Successful",
    "responseCode": "2002500",
    "virtualAccountData": {
        "partnerServiceId": "  088899",
        "customerNo": "12345678901234567890",
        "virtualAccountNo": "  08889912345678901234567890",
        "trxId": "midtrans-testing-001"
}

```

### List of response code

<table>
  <tr>
    <td>
      <strong>Response Code</strong>
    </td>

    <td>
      <strong>HTTP Status</strong>
    </td>

    <td>
      <strong>Description</strong>
    </td>
  </tr>

  <tr>
    <td>
      2002500
    </td>

    <td>
      200
    </td>

    <td>
      Success
    </td>
  </tr>

  <tr>
    <td>
      4002500
    </td>

    <td>
      400
    </td>

    <td>
      Bad Request
    </td>
  </tr>

  <tr>
    <td>
      4002501
    </td>

    <td>
      400
    </td>

    <td>
      Invalid Field Format X-TIMESTAMP
    </td>
  </tr>

  <tr>
    <td>
      4002502
    </td>

    <td>
      400
    </td>

    <td>
      Invalid Mandatory Field
    </td>
  </tr>

  <tr>
    <td>
      4012500
    </td>

    <td>
      401
    </td>

    <td>
      Unauthorized. Signature
    </td>
  </tr>

  <tr>
    <td>
      4042513
    </td>

    <td>
      404
    </td>

    <td>
      Invalid Amount
    </td>
  </tr>

  <tr>
    <td>
      5002500
    </td>

    <td>
      500
    </td>

    <td>
      Internal Server Error
    </td>
  </tr>

  <tr>
    <td>
      5042500
    </td>

    <td>
      504
    </td>

    <td>
      Timeout
    </td>
  </tr>
</table>

## Notification retry mechanism for Open API

In case we receive an error response when sending notifications to merchants (any non-success response), Midtrans will retry the notification delivery up to a maximum of 5 times with predefined retry intervals. For now, our retry mechanism is as follows:

* 1st retry delay time = 2 minutes
* 2nd retry delay time = 10 minutes
* 3rd retry delay time = 30 minutes
* 4th retry delay time = 90 minutes (1.5 hours)
* 5th retry delay time = 210 minutes (3.5 hours)

Notes:

1. These retry intervals may change at any time as part of continuous improvements. Any changes will be communicated and updated periodically in this documentation.
2. Midtrans will treat any other responses except HTTP status code 200 as an error