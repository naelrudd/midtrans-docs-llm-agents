---
updatedAt: 2025-11-12T16:21:42.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Cancel API

## Initiating cancel for GoPay and GoPay Tokenization (non Pre-Auth) transaction

This section will describe how a merchant can initiate cancel for GoPay and GoPay Tokenization (non-Pre Auth) transactions.

| Path              | /\{version}/debit/cancel |
| :---------------- | :----------------------- |
| HTTP Method       | POST                     |
| Version           | v1.0                     |
| SNAP Service Code | 57                       |

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
   <td colspan="2" >
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
   <td colspan="2" >
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
   <td colspan="2" >
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
   <td colspan="2" >
   Created using symmetric signature HMAC_SHA512 algorithm
   </td>
  </tr>
  <tr>
   <td>
   Authorization
   </td>
   <td>
   String
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   Represents access_token of a request; string starts with keyword “Bearer ” followed by access_token. Can get this token from Access Token B2B API response.
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
   <td colspan="2" >
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
   <td colspan="2" >

      Alphanumeric string. We suggest merchant to use UUID format. The value should be unique. <br /> In case of timeout, merchant can do:

      1. Use this value in get status API to get status transaction or <br />
      2. Retry this request with the same X-EXTERNAL-ID and request body to avoid creating duplicate transaction

      </td>
     </tr>
     <tr>
      <td>
      CHANNEL-ID
      </td>
      <td>
      String
      </td>
      <td>
      M
      </td>
      <td colspan="2" >
      Mandatory field from Bank Indonesia that can take any value with correct format 5 digits numeric string
      </td>
     </tr>
   </table>

```
Content-type:application/json
X-TIMESTAMP:2024-03-19T14:30:00+07:00
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
Authorization: Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
X-PARTNER-ID: BMRI
X-EXTERNAL-ID:12345678901234567890
CHANNEL-ID:12345
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
   <td colspan="2" >
   <strong>Field Description</strong>
   </td>
  </tr>
  <tr>
   <td>
   originalReferenceNo
   </td>
   <td>
   String(64)
   </td>
   <td>
   C
   </td>
   <td colspan="2" >
   Transaction identifier on service provider system. For e.g: GopayOrderId<strong> </strong>
<p>
Note: either originalExternalId or OriginalReferenceNo need to be passed. If both fields have value, we will use originalReferenceNo as the main identifier.
</p>
   </td>
  </tr>
  <tr>
   <td>
   originalExternalId
   </td>
   <td>
   String (36) 
   </td>
   <td>
   C
   </td>
   <td colspan="2" >
   If merchant got a timeout when calling charge API (POST /v1.0/debit/payment-host-to-host), merchant can pass the value of X-EXTERNAL-ID in the charge API request header as originalExternalId.
<p>
Note: Either originalExternalId or OriginalReferenceNo need to be passed in cancel request.
</p>
   </td>
  </tr>

<tr>
   <td>
   originalPartnerReferenceNo
   </td>
   <td>
   String (64) 
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   Transaction identifier on service consumer system. For e.g: MerchantOrderId

   </td>
  </tr>
</table>

```
{
   "originalReferenceNo" : "gopay-order-id",
   "originalExternalId" : "some-external-id",
   "originalPartnerReferenceNo":"merchant-order-id"
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
   <td colspan="2" >
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
   <td colspan="2" >
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
   <td colspan="2" >
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
   <td colspan="2" >
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
   <td colspan="2" >
   Response code 
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
   <td colspan="2" >
   Response description 
   </td>
  </tr>
  <tr>
   <td>
   originalReferenceNo
   </td>
   <td>
   String (256)
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   Transaction identifier on service provider system. For e.g: GopayOrderId<strong>  </strong>
   </td>
  </tr>

 <tr>
   <td>
   cancelTime
   </td>
   <td>
   String (25)
   </td>
   <td>
   C
   </td>
   <td colspan="2" >
   Cancel time. ISO-8601. Will be sent only if transaction cancellation is successful 
   </td>
  </tr>
</table>

```
{
   "responseCode":"20057000",
   "responseMessage":"Request has been processed successfully",
   "originalReferenceNo": "2020102977770000000009",
   "cancelTime":"2024-09-03T03:52:14Z"
}
```

### List of Response code

<table>
  <tr>
   <td>
   <strong>Response Code</strong>
   </td>
   <td>
   <strong>HTTP Status Code</strong>
   </td>
   <td>
   <strong>Response Message</strong>
   </td>
  </tr>
  <tr>
   <td>
   2005700
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
   4005702
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
   4015700
   </td>
   <td>
   401
   </td>
   <td>
   Unauthorized.
   </td>
  </tr>
  <tr>
   <td>
   4015701
   </td>
   <td>
   401
   </td>
   <td>
   Invalid Token (B2B)
   </td>
  </tr>
  <tr>
   <td>
   4035715
   </td>
   <td>
   403
   </td>
   <td>
   Transaction Not Permitted.[reason].
   </td>
  </tr>
  <tr>
   <td>
   5005701
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
   5045700
   </td>
   <td>
   504
   </td>
   <td>
   Timeout
   </td>
  </tr>
</table>

***

## Initiating cancel for GoPay QRIS transaction

This section will describe how a merchant can initiate cancel for GoPay QRIS transactions.

| Path              | /\{version}/qr/qr-mpm-cancel |
| :---------------- | :--------------------------- |
| HTTP Method       | POST                         |
| Version           | v1.0                         |
| SNAP Service Code | 77                           |

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
   <td colspan="2" >
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
   <td colspan="2" >
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
   <td colspan="2" >
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
   <td colspan="2" >
   Created using symmetric signature HMAC_SHA512 algorithm
   </td>
  </tr>
  <tr>
   <td>
   Authorization
   </td>
   <td>
   String
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   Represents access_token of a request; string starts with keyword “Bearer ” followed by access_token. Can get this token from b2b response.
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
   <td colspan="2" >
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
   <td colspan="2" >

         Alphanumeric string. We suggest merchant to use UUID format. The value should be unique. <br /> In case of timeout, merchant can do:

         1. Use this value in get status API to get status transaction or <br />
         2. Retry this request with the same X-EXTERNAL-ID and request body to avoid creating duplicate transaction

      </td>
     </tr>
     <tr>
      <td>
      CHANNEL-ID
      </td>
      <td>
      String
      </td>
      <td>
      M
      </td>
      <td colspan="2" >
      Mandatory field from Bank Indonesia that can take any value with correct format 5 digits numeric string
      </td>
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
   <td colspan="2" >
   <strong>Field Description</strong>
   </td>
  </tr>
  <tr>
   <td>
   originalPartnerReferenceNo
   </td>
   <td>
   String(64)
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Transaction identifier on service consumer system. For e.g: MerchantOrderId<strong> </strong>
   </td>
  </tr>
  <tr>
   <td>
   originalReferenceNo
   </td>
   <td>
   String(64)
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Transaction identifier on service provider system. For e.g: GopayOrderId<strong> </strong>
<p>
Note: either originalExternalId or OriginalReferenceNo need to be filled
</p>
<p>
If both fields have value, will use originalReferenceNo as the main identifier.
</p>
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
   <td colspan="2" >
   Original External-ID on header message
   </td>
  </tr>
  <tr>
   <td>
   merchantId
   </td>
   <td>
   String(64)
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   Merchant identifier that is unique per each merchant
   </td>
  </tr>
  <tr>
   <td>
   subMerchantId
   </td>
   <td>
   String(32)
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Sub merchant ID
   </td>
  </tr>
  <tr>
   <td>
   externalStoreId
   </td>
   <td>
   String(64)
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Externals store ID
   </td>
  </tr>
  <tr>
   <td>
   reason
   </td>
   <td>
   String(256)
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   Reason for cancellation
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
   <td colspan="2" >
   Amount object 
   </td>
  </tr>
  <tr>
   <td>
   amount.value 
   </td>
   <td>
   String (ISO 4217) (16,2)
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Net amount of the cancel. If it's IDR then the value includes 2 decimal digits.
<p>
e.g. IDR 10.000,- will be placed with 10000.00
</p>
   </td>
  </tr>
  <tr>
   <td>
   amount.currency 
   </td>
   <td>
   String (2) 
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Currency. 
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
   <td colspan="2" >
   Additional information if merchant’s need to pass. 
   </td>
  </tr>
</table>

```
{
   "originalPartnerReferenceNo":"2020102900000000000001",
   "originalReferenceNo":"2020102977770000000009",
   "originalExternalId":"30443786930722726463280097920912",
   "merchantId":"00007100010926",
   "subMerchantId":"310928924949487",
   "externalStoreId":"124928924949487",
   "reason":"cancel reason",
   "amount":{
      "value":"10000.00",
      "currency":"IDR"
   },
   "additionalInfo":{
      "deviceId":"12345679237",
      "channel":"mobilephone"
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
   <td colspan="2" >
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
   <td colspan="2" >
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
   <td colspan="2" >
   Client’s current local time in ISO-8601 format
   </td>
  </tr>
</table>

```
Content-type:application/json
X-TIMESTAMP:2024-03-19T14:30:00+07:00
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
   <td colspan="2" >
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
   <td colspan="2" >
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
   <td colspan="2" >
   Response description 
   </td>
  </tr>
  <tr>
   <td>
   originalPartnerReferenceNo
   </td>
   <td>
   String(64)
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Original transaction identifier on merchant
   </td>
  </tr>
  <tr>
   <td>
   originalReferenceNo
   </td>
   <td>
   String(64)
   </td>
   <td>
   C
   </td>
   <td colspan="2" >
   Original transaction identifier on GoPay
   </td>
  </tr>
  <tr>
   <td>
   originalExternalId
   </td>
   <td>
   String(32)
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Original customer reference number
   </td>
  </tr>
  <tr>
   <td>
   cancelTime 
   </td>
   <td>
   String(25) 
   </td>
   <td>
   C 
   </td>
   <td colspan="2" >
   Cancel time. ISO 8601
   </td>
  </tr>
  <tr>
   <td>
   transactionDate
   </td>
   <td>
   yyyyMMddHHmmss
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Transaction Date
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
   <td colspan="2" >
   Additional information if merchant’s need to pass. 
   </td>
  </tr>
</table>

```
{
   "responseCode":"2007700",
   "responseMessage":"Request has been processed successfully",
   "originalPartnerReferenceNo":"2020102900000000000001",
   "originalReferenceNo":"2020102977770000000009",
   "originalExternalId":"30443786930722726463280097920912",
   "cancelTime":"2020-10-20T17:56:57",
   "transactionDate":"2020-10-20 17:56:57",
   "additionalInfo":{
      "deviceId":"12345679237",
      "channel":"mobilephone"
   }
```

***

## Initiating cancel for GoPay Tokenization (Pre Auth) transaction

This section will describe how a merchant can release/cancel authorized transactions for GoPay Tokenization (Pre-Auth) transactions.

| Path              | /v1.0/auth/void |
| :---------------- | :-------------- |
| HTTP Method       | POST            |
| Version           | v1.0            |
| SNAP Service Code | 67              |

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
   <td colspan="2" >
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
   <td colspan="2" >
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
   <td colspan="2" >
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
   <td colspan="2" >
   Created using symmetric signature HMAC_SHA512 algorithm
   </td>
  </tr>
  <tr>
   <td>
   Authorization
   </td>
   <td>
   String
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   Represents access_token of a request; string starts with keyword “Bearer ” followed by access_token. Can get this token from Access Token B2B API response.
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
   <td colspan="2" >
   Unique identifier for caller  (client_id)
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
   <td colspan="2" >

      Alphanumeric string. We suggest merchant to use UUID format. The value should be unique. <br /> In case of timeout, merchant can do:

      1. Use this value in get status API to get status transaction or <br />
      2. Retry this request with the same X-EXTERNAL-ID and request body to avoid creating duplicate transaction

      </td>
     </tr>
     <tr>
      <td>
      CHANNEL-ID
      </td>
      <td>
      String
      </td>
      <td>
      M
      </td>
      <td colspan="2" >
      Mandatory field from Bank Indonesia that can take any value with correct format 5 digits numeric string
      </td>
     </tr>
   </table>

```
Content-type:application/json
X-TIMESTAMP:2024-03-19T14:30:00+07:00
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
Authorization: Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
X-PARTNER-ID: BMRI
X-EXTERNAL-ID:12345678901234567890
CHANNEL-ID:12345
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
   <td colspan="2" >
   <strong>Field Description</strong>
   </td>
  </tr>
  <tr>
   <td>
   originalReferenceNo
   </td>
   <td>
   String(64)
   </td>
   <td>
   C
   </td>
   <td colspan="2" >
   Transaction identifier on service provider system. For e.g: GopayOrderId<strong> </strong>
<p>
Note: either originalExternalId or OriginalReferenceNo need to be filled
</p>
<p>
If both fields have value, will use originalReferenceNo as the main identifier.
</p>
   </td>
  </tr>
  <tr>
   <td>
   originalPartnerReferenceNo
   </td>
   <td>
   String (64)
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   Merchant order-id
   </td>
  </tr>
  <tr>
   <td>
   merchantId
   </td>
   <td>
   String(64)
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   Merchant ID
   </td>
  </tr>
  <tr>
   <td>
   partnerVoidNo
   </td>
   <td>
   String (64)
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   Void identifier generated by the partner
   </td>
  </tr>

 <tr>
   <td>
   reason
   </td>
   <td>
   String (256)
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Void reason
   </td>
  </tr>
  <tr>
   <td>
   additionalInfo
   </td>
   <td>
   </td>
   <td>
   </td>
   <td colspan="2" >
   </td>
  </tr>
  <tr>
   <td>
   additionalInfo.originalExternalId
   </td>
   <td>
   String (36) 
   </td>
   <td>
   C
   </td>
   <td colspan="2" >
   If merchant got a timeout from the auth endpoint, merchant can use this field using the X-EXTERNAL-ID value in the direct debit request header.
<p>
Note: either originalExternalId or OriginalReferenceNo need to be filled
</p>
   </td>
  </tr>
</table>

```
{
   "originalReferenceNo":"2020102900000000000001",
   "originalPartnerReferenceNo":"123123123123",
   "partnerVoidNo":"asdv-asdasdv-addasd-1231ewqqw-aaaa",
   "merchantId":"merch00001"
   "title":"aTitle",
   "additionalData":{
          "originalExternalId":"aId",
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
   <td colspan="2" >
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
   <td colspan="2" >
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
   <td colspan="2" >
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
   <td colspan="2" >
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
   <td colspan="2" >
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
   <td colspan="2" >
   Debug message to provide more information.
   </td>
  </tr>
  <tr>
   <td>
   originalReferenceNo
   </td>
   <td>
   String (256)
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Transaction identifier on service provider system. For e.g: GopayOrderId 
   </td>
  </tr>
  <tr>
   <td>
   originalPartnerReferenceNo
   </td>
   <td>
   String (32)
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Transaction identifier on service consumer system
   </td>
  </tr>
  <tr>
   <td>
   voidNo
   </td>
   <td>
   String (64)
   </td>
   <td>
   C
   </td>
   <td colspan="2" >
   PJSP's void identifier. Used to trace the capture when there's any issue occurred.
   </td>
  </tr>
  <tr>
   <td>
   partnerVoidNo
   </td>
   <td>
   String (64)
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   Void identifier generated by the partner
   </td>
  </tr>
  <tr>
   <td>
   voidAmount
   </td>
   <td>
   Object
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   </td>
  </tr>
  <tr>
   <td>
   voidAmount.value
   </td>
   <td>
   String (16,2)
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Transaction amount that will be paid using this payment method If it's IDR then value includes 2 decimal digits.
<p>
e.g. IDR 10.000,- will be placed with 10000.00
</p>
   </td>
  </tr>
  <tr>
   <td>
   voidAmount.currency
   </td>
   <td>
   String 
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Currency. For e.g: IDR
   </td>
  </tr>
   <tr>
   <td>
   voidTime
   </td>
   <td>
   String 
   </td>
   <td>
   C
   </td>
   <td colspan="2" >
   Void time. Must be filled upon successful transaction. Format void time: (ISO 8601) YYYY-MM-DDThh:mm:ss
   </td>
  </tr>
</table>

```Text Successful Response
{
   "responseCode":"20054000",
   "responseMessage":"Request has been processed successfully",
    "originalReferenceNo":"2020102900000000000001",
   "originalPartnerReferenceNo":"123123123123",
   "voidNo":"asdv-asdasdv-addasd-1231ewqqw-aaaa",
    "partnerVoidNo":"asdv-asdasdv-addasd-1231ewqqw-aaaa",
   "voidAmount":{
  	"value":"12345678.00",
  	"currency":"IDR"
   },
   "voidTime": "2009-07-03T12:08:56+07:00"
}
```
```Text Error Response
{
   "responseCode":"4006701",
   "responseMessage":"There is some issue with the transaction request"
}
```

### List of Response code

<table>
  <tr>
   <td>
   <strong>Response Code</strong>
   </td>
   <td>
   <strong>HTTP Status Code</strong>
   </td>
   <td>
   <strong>Response Message</strong>
   </td>
  </tr>
  <tr>
   <td>
   2006700
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
   4006702
   </td>
   <td>
   400
   </td>
   <td>
   Invalid Mandatory Field \{Field Name\}
   </td>
  </tr>
  <tr>
   <td>
   4016700
   </td>
   <td>
   401
   </td>
   <td>
   Unauthorized. Auth token required
   </td>
  </tr>
  <tr>
   <td>
   4016701
   </td>
   <td>
   401
   </td>
   <td>
   Invalid Token (B2B)
   </td>
  </tr>
  <tr>
   <td>
   4036515
   </td>
   <td>
   403
   </td>
   <td>
   Transaction Not Permitted.[reason].
   </td>
  </tr>
  <tr>
   <td>
   5006701
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
   5046700
   </td>
   <td>
   504
   </td>
   <td>
   Timeout
   </td>
  </tr>
</table>

***

## Initiating cancel for bank transfer (virtual account) transaction

This section will describe how a merchant can cancel bank transfer (virtual account) transactions.

| Path              | /\{version}/transfer-va/delete-va |
| :---------------- | :-------------------------------- |
| HTTP Method       | POST                              |
| Version           | v1.0                              |
| SNAP service code | 31                                |

### Request Header

<table>
  <tr>
   <td>
   Field Name
   </td>
   <td>
   Field Type
   </td>
   <td>
   Mandatory
   </td>
   <td>
   Field Description
   </td>
  </tr>
  <tr>
   <td>
   Content-Type
   </td>
   <td>
   String
   </td>
   <td>
   M
   </td>
   <td>
   Represent media type of request e.g “application/json”
   </td>
  </tr>
  <tr>
   <td>
   X-TIMESTAMP
   </td>
   <td>
   String(25)
   </td>
   <td>
   M
   </td>
   <td>
   Client's current local time in “yyyy-MM-ddTHH:mm:ssZ” format
   </td>
  </tr>
  <tr>
   <td>
   Authorization
   </td>
   <td>
   String
   </td>
   <td>
   M
   </td>
   <td>
   Bearer token obtained from Access Token API in the format Bearer AccessToken
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
   <td>
   Created using symmetric signature HMAC_SHA512 algorithm
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
   <td>
   Unique identifier for partner
   </td>
  </tr>
  <tr>
   <td>
   CHANNEL-ID
   </td>
   <td>
   String
   </td>
   <td>
   M
   </td>
   <td>
   Mandatory field from Bank Indonesia that can take any value with correct format 5 digits numeric string
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
   <td>

      Alphanumeric string. We suggest merchant to use UUID format. The value should be unique. <br /> In case of timeout, merchant can do:

      1. Use this value in get status API to get status transaction or <br />
      2. Retry this request with the same X-EXTERNAL-ID and request body to avoid creating duplicate transaction

      </td>
     </tr>
   </table>

```
X-TIMESTAMP 2022-03-04T08:02:09+07:00
X-SIGNATURE yqmBXZ3yV6NPG1LtwXMm3quXzJMRX5Ms+r9ebc5xWIZGSKbZL3Oy871GHb7WQUucLa5nxN/HcnZYoNHc+KkWTQ==
X-PARTNER-ID 668052e34f194aa8be79e15a21e4fc2f
X-EXTERNAL-ID 91919644194391346361915387229113
CHANNEL-ID 95221
Authorization Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIxMmUzODE4Mi00YjIxLTQ0YWMtOTVkNi1mMjFhMjEwZmIxZTAiLCJjbGllbnRJZCI6IjY2ODA1MmUzNGYxOTRhYThiZTc5ZTE1YTIxZTRmYzJmIiwibmJmIjoxNjYzODQwNTU5LCJleHAiOjE2NjM4NDE0NTksImlhdCI6MTY2Mzg0MDU1OX0.fEr0vIbB2kY8alZ-SROl3ftAFbfRd0uU-lGq9XuFi8M
Content-Type application/json
```

### Request Body

<table>
  <tr>
   <td>
   Field Name
   </td>
   <td>
   Field Type
   </td>
   <td>
   Mandatory
   </td>
   <td>
   Field Description
   </td>
  </tr>
  <tr>
   <td>
   partnerServiceId
   </td>
   <td>
   M
   </td>
   <td>
   String(8)
   </td>
   <td>
   Derivative of X- PARTNER- ID, similar to company code, 8 digit left padding space.
   </td>
  </tr>
  <tr>
   <td>
   customerNo
   </td>
   <td>
   M
   </td>
   <td>
   String(20)
   </td>
   <td>
   Unique number (up to 20 digits).
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountNo
   </td>
   <td>
   M
   </td>
   <td>
   String(28)
   </td>
   <td>
   partnerServiceId + customerNo (up to 20 digits).
   </td>
  </tr>
  <tr>
   <td>
   trxId
   </td>
   <td>
   M
   </td>
   <td>
   String(64)
   </td>
   <td>
   Transaction ID in Partner system
   </td>
  </tr>
  <tr>
   <td>
   additionalInfo
   </td>
   <td>
   O
   </td>
   <td>
   Object
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>
   additionalInfo.merchantId
   </td>
   <td>
   M
   </td>
   <td>
   String
   </td>
   <td>
   Merchant ID
   </td>
  </tr>
</table>

```
{
  "partnerServiceId":"  088899",
  "customerNo":"12345678901234567890",
  "virtualAccountNo":"  08889912345678901234567890",
  "trxId":"91919644194391346361915387229113",
  "additionalInfo": {
    "merchant_id": "G12345463"
  }
}
```

### Response Header

| Field Name   | Field Type | Mandatory | Field Description                                |
| :----------- | :--------- | :-------- | :----------------------------------------------- |
| Content-Type | String     | M         | Media type of the resource, i.e application/json |
| X-TIMESTAMP  | String     | M         | Client's current local time in ISO-8601          |

```
Content-type:application/json
X-TIMESTAMP:2024-03-19T14:30:00+07:00
```

### Response Body

<table>
  <tr>
   <td>
   Field Name
   </td>
   <td>
   Field Type
   </td>
   <td>
   Mandatory
   </td>
   <td>
   Field Description
   </td>
  </tr>
  <tr>
   <td>
   responseCode
   </td>
   <td>
   String
   </td>
   <td>
   M
   </td>
   <td>
   Response code
   </td>
  </tr>
  <tr>
   <td>
   responseMessage
   </td>
   <td>
   String
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
   virtualAccountData.partnerServiceId
   </td>
   <td>
   String
   </td>
   <td>
   M
   </td>
   <td>
   Derivative of X- PARTNER- ID, similar to company code, 8 digit left padding space.
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.customerNo
   </td>
   <td>
   String
   </td>
   <td>
   M
   </td>
   <td>
   Unique number (up to 20 digits).
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.virtualAccountNo
   </td>
   <td>
   String
   </td>
   <td>
   M
   </td>
   <td>
   partnerServiceId (8 digit left padding 0) + customerNo (up to 20 digits).
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.trxId
   </td>
   <td>
   String
   </td>
   <td>
   M
   </td>
   <td>
   Transaction ID in Partner system
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
   </td>
  </tr>
</table>

```
{
   "responseCode": "2003100",
   "responseMessage": "Success",
   "virtualAccountData":{
     "partnerServiceId":"  088899",
     "customerNo":"12345678901234567890",
     "virtualAccountNo":"  08889912345678901234567890",
     "trxId":"91919644194391346361915387229113",
     "additionalInfo":{} 
    }
}
```