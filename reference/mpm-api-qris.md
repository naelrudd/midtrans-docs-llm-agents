---
updatedAt: 2026-04-21T06:23:38.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Payment Method: QRIS

<Callout icon="📘" theme="info">
  Both **GoPay QRIS** and **ShopeePay QRIS** are available on SNAP-based flow.
</Callout>

In QRIS flow, merchant will receive QRIS code which can be paid by users. Users can scan the QRIS code using e-wallet app that already is QRIS compatible, such as GoPay, ShopeePay, etc.

This section will explain how merchants can initiate GoPay QRIS transactions using SNAP-based CoreAPI specification.

<br />

# Creating GoPay/ShopeePay QRIS transaction

<Image align="center" src="https://files.readme.io/d5e33a5-SNAP_based_account_linking_flow-gopay_qris.drawio.png" />

<br />

| Path              | /\{version}/qr/qr-mpm-generate |
| :---------------- | :----------------------------- |
| HTTP Method       | POST                           |
| Version           | v1.0                           |
| SNAP Service Code | 47                             |

## Request Header

<table>
  <tr>
    <td><strong>Field Name</strong></td>
    <td><strong>Field Type</strong></td>
    <td><strong>Mandatory</strong></td>
    <td colspan="2"><strong>Field Description</strong></td>
  </tr>

  <tr>
    <td>Content-type</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Media type of the resource, i.e. application/json</td>
  </tr>

  <tr>
    <td>X-TIMESTAMP</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Client’s current local time in ISO-8601 format</td>
  </tr>

  <tr>
    <td>X-SIGNATURE</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Created using symmetric signature HMAC\_SHA512 algorithm</td>
  </tr>

  <tr>
    <td>Authorization</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Represents access\_token of a request; string starts with keyword “Bearer ” followed by access\_token. Can get this token from Access Token B2B response.</td>
  </tr>

  <tr>
    <td>X-PARTNER-ID</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Unique identifier for caller (client\_id)</td>
  </tr>

  <tr>
    <td>X-EXTERNAL-ID</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Alphanumeric string. We suggest merchant to use UUID format. The value should be unique. <br /> In case of timeout, merchant can do: <br /> 1. Use this value in get status API to get status transaction <br /> The value should also be the same as request\_body.partnerReferenceNo</td>
  </tr>

  <tr>
    <td>CHANNEL-ID</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Mandatory field from Bank Indonesia that can take any value with correct format 5 digits numeric string</td>
  </tr>
</table>

```
Content-type:application/json
X-TIMESTAMP:2024-03-19T14:30:00+07:00
X-SIGNATURE:da1fa417c72d6b91c257e01e54fac824
Authorization:Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
X-PARTNER-ID:BMRI
X-EXTERNAL-ID:12345678901234567890
CHANNEL-ID:12345
```

<br />

## Request Body

<table>
  <tr>
    <td><strong>Field Name</strong></td>
    <td><strong>Field Type</strong></td>
    <td><strong>Mandatory</strong></td>
    <td colspan="2"><strong>Field Description</strong></td>
  </tr>

  <tr>
    <td>partnerReferenceNo</td>
    <td>String(36)</td>
    <td>O</td>
    <td colspan="2">Alphanumeric string. Preferably UUID. Reference number that should be unique across 3 months. This value should be filled with the same value as X-EXTERNAL-ID<br></br><b>Note:</b> Allowed Symbols are dash(-), underscore(_), tilde (~), and dot (.). Any request containing unauthorized symbols will be automatically declined.</td>
  </tr>

  <tr>
    <td>amount</td>
    <td>Object</td>
    <td>O</td>
    <td colspan="2">Amount object</td>
  </tr>

  <tr>
    <td>amount.value</td>
    <td>String(16,2)</td>
    <td>M</td>
    <td colspan="2">Transaction amount</td>
  </tr>

  <tr>
    <td>amount.currency</td>
    <td>String(3)</td>
    <td>M</td>
    <td colspan="2">Transaction currency</td>
  </tr>

  <tr>
    <td>merchantId</td>
    <td>String(64)</td>
    <td>O</td>
    <td colspan="2">Merchant identifier that is unique per each merchant</td>
  </tr>

  <tr>
    <td>validityPeriod</td>
    <td>String(25)</td>
    <td>O</td>
    <td colspan="2">The time when the QRIS will automatically expire. <br /> The time when the payment will be automatically expired. The format is defined by ISO 8601. <br /> (Maximum value : 180 days from trx time, Minimum value : 20 second, default value : 15 min)</td>
  </tr>

  <tr>
    <td>additionalInfo</td>
    <td>Object</td>
    <td>O</td>
    <td colspan="2">Additional information</td>
  </tr>

  <tr>
    <td>additionalInfo.acquirer</td>
    <td>String</td>
    <td>O</td>
    <td colspan="2">Acquirer name, possible value for now: GOPAY, AIRPAY SHOPEE. If not given, default value is GOPAY</td>
  </tr>
</table>

```
{
  "partnerReferenceNo": "2020102900000000000001",
  "amount": {
    "value": "12345678.00",
    "currency": "IDR"
  },
  "merchantId": "00007100010926",
  "validityPeriod": "2009-07-03T12:08:56-07:00",
  "additionalInfo": {
    "acquirer": "gopay"
  }
}
```

<br />

## Response Header

<table>
  <tr>
    <td><strong>Field Name</strong></td>
    <td><strong>Field Type</strong></td>
    <td><strong>Mandatory</strong></td>
    <td colspan="2"><strong>Field Description</strong></td>
  </tr>

  <tr>
    <td>Content-type</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Media type of the resource, i.e. application/json</td>
  </tr>

  <tr>
    <td>X-TIMESTAMP</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Client’s current local time in ISO-8601 format</td>
  </tr>
</table>

```
Content-type:application/json
X-TIMESTAMP:2024-03-19T14:30:00+07:00
```

<br />

## Response Body

<table>
  <tr>
    <td><strong>Field Name</strong></td>
    <td><strong>Field Type</strong></td>
    <td><strong>Mandatory</strong></td>
    <td colspan="2"><strong>Field Description</strong></td>
  </tr>

  <tr>
    <td>responseCode</td>
    <td>String (7)</td>
    <td>M</td>
    <td colspan="2">Response Code (HTTP status code + service code + case code)</td>
  </tr>

  <tr>
    <td>responseMessage</td>
    <td>String (150)</td>
    <td>M</td>
    <td colspan="2">Description of charge result response.</td>
  </tr>

  <tr>
    <td>referenceNo</td>
    <td>String (64)</td>
    <td>O</td>
    <td colspan="2">Transaction identifier on service provider system.</td>
  </tr>

  <tr>
    <td>partnerReferenceNo</td>
    <td>String (36)</td>
    <td>O</td>
    <td colspan="2">partnerReferenceNo from the request body</td>
  </tr>

  <tr>
    <td>qrContent</td>
    <td>String(512)</td>
    <td>M</td>
    <td colspan="2">QR String MPM.</td>
  </tr>

  <tr>
    <td>qrUrl</td>
    <td>String(256)</td>
    <td>M</td>
    <td colspan="2">QR URL for download QR Image</td>
  </tr>

  <tr>
    <td>qrImage</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">base64 from image QRIS.<br />Max length is unlimited.</td>
  </tr>

  <tr>
    <td>additionalInfo</td>
    <td>Object</td>
    <td>O</td>
    <td colspan="2">Additional information</td>
  </tr>

  <tr>
    <td>additionalInfo.acquirer</td>
    <td>Object</td>
    <td>O</td>
    <td colspan="2">Acquirer chosen from request</td>
  </tr>
</table>

```
{
  "responseCode": "2004700",
  "responseMessage": "Request has been processed successfully",
  "referenceNo": "2020102977770000000009",
  "partnerReferenceNo": "2020102900000000000001",
  "qrContent": "xxxxxxxxxxxxxxxx",
  "qrUrl": "https: //qrurl?img=12345",
  "qrImage": "TWFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5IGhpcyByZWFzb24sIGJ1dCAuLi4=",
  "additionalInfo": {
    "acquirer": "gopay"
  }
}
```

<br />

## List of Response code

<table>
  <tr>
    <td><strong>Response Code</strong></td>
    <td><strong>HTTP Status</strong></td>
    <td><strong>Description</strong></td>
  </tr>

  <tr>
    <td>2004700</td>
    <td>200</td>
    <td>Successful</td>
  </tr>

  <tr>
    <td>2024700</td>
    <td>202</td>
    <td>Transaction still on process</td>
  </tr>

  <tr>
    <td>4004700</td>
    <td>400</td>
    <td>General request failed error, including message parsing failed.</td>
  </tr>

  <tr>
    <td>4004701</td>
    <td>400</td>
    <td>Invalid format</td>
  </tr>

  <tr>
    <td>4004702</td>
    <td>400</td>
    <td>Missing or invalid format on mandatory field</td>
  </tr>

  <tr>
    <td>4014700</td>
    <td>401</td>
    <td>General unauthorized error (No Interface Def, API is Invalid, Oauth Failed, Verify Client Secret Fail, Client Forbidden Access API, Unknown Client, Key not Found)</td>
  </tr>

  <tr>
    <td>4014701</td>
    <td>401</td>
    <td>Token found in request is invalid (Access Token Not Exist, Access Token Expiry)</td>
  </tr>

  <tr>
    <td>4014703</td>
    <td>401</td>
    <td>Token not found in the system. This occurs on any API that requires token as input parameter</td>
  </tr>

  <tr>
    <td>4034702</td>
    <td>403</td>
    <td>Exceeds Transaction Amount Limit</td>
  </tr>

  <tr>
    <td>4034703</td>
    <td>403</td>
    <td>Suspected Fraud</td>
  </tr>

  <tr>
    <td>4034715</td>
    <td>403</td>
    <td>Transaction Not Permitted</td>
  </tr>

  <tr>
    <td>4044708</td>
    <td>404</td>
    <td>Merchant does not exist or status abnormal</td>
  </tr>

  <tr>
    <td>4044713</td>
    <td>404</td>
    <td>Invalid format amount</td>
  </tr>

  <tr>
    <td>4094700</td>
    <td>409</td>
    <td>Cannot use same X-EXTERNAL-ID</td>
  </tr>

  <tr>
    <td>5004701</td>
    <td>500</td>
    <td>Unknown Internal Server Failure, Please retry the process again</td>
  </tr>

  <tr>
    <td>5004702</td>
    <td>500</td>
    <td>Backend system failure, etc</td>
  </tr>

  <tr>
    <td>5044700</td>
    <td>504</td>
    <td>Timeout from the issuer</td>
  </tr>
</table>

<br />

# Additional APIs

1. [Refund API](https://docs.midtrans.com/reference/refund-api)
2. [Cancel API](https://docs.midtrans.com/reference/cancel-api)
3. [Get Transaction Status API](https://docs.midtrans.com/reference/get-transaction-status-api)
4. [Payment Notification API](https://docs.midtrans.com/reference/payment-notification-api)