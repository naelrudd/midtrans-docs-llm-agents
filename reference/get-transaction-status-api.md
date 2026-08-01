---
updatedAt: 2025-11-12T17:42:33.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Get Transaction Status API

## Fetching transaction status for GoPay and GoPay Tokenization (non Pre-Auth) transaction

This section will describe how a merchant can fetch transaction status for GoPay and GoPay Tokenization (non-Pre Auth) transactions.

| Path              | /`{version}`/debit/status |
| :---------------- | :------------------------ |
| HTTP Method       | POST                      |
| Version           | v1.0                      |
| SNAP Service Code | 55                        |

<br />

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
Note: Either originalExternalId or OriginalReferenceNo need to be passed in refund request.
</p>
   </td>
  </tr> <tr>
   <td>
   serviceCode
   </td>
   <td>
   String (2) 
   </td>
   <td>
   M
   </td>
   <td colspan="2" >Transaction type indicator (service code of the original transaction request). For e.g: 54 </td>
  </tr>
</table>

```
{
    "originalExternalId": "merchant-order-id",
    "originalReferenceNo": "Gopay OrderId",
    "serviceCode": "54"
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
   originalPartnerReferenceNo
   </td>
   <td>
   String (64)
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Original transaction identifier on service consumer system. (Merchant’s orderId)
   </td>
  </tr>
  <tr>

<tr>
   <td>
   originalExternalId
   </td>
   <td>
   String (32)
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Original external identifier 
   </td>
  </tr>
  <tr>

   <td>
   originalReferenceNo
   </td>
   <td>
   String (64)
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   Transaction identifier on service provider system. For e.g: GopayOrderId<strong> </strong>
   </td>
  </tr>
  <tr>
   <td>
   serviceCode
   </td>
   <td>
   String (2)  
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   Transaction type indicator (service code of the original transaction request).  \
 \
For e.g: <strong>54 , 58 </strong>which are serviceCode of Charge and Refund API
   </td>
  </tr>
  <tr>
   <td>
   latestTransactionStatus
   </td>
   <td>
   String (2) 
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   <strong>Possible Values: </strong> 
<ul>
   <li>
   00 (Success)
</li>
   <li>
   03 (Pending)
</li>
   <li>
   04 (Refunded)
</li>
   <li>
   05 (Canceled)
</li>
   <li>
   06 (Failed)
</li>
   <li>
   07 (Not found)
</li>
   <li>
   08 (Expiry)
</li>
   <li>
   09 (Rejected)
   </li>
</ul> 

<br /> We will only return the numeric value on the API response. The text (...) is only the status code description and won't be returned in the actual response.  

   </td>  
  </tr>  
  <tr>  
   <td>
   transAmount  
   </td>  
   <td>
   Object  
   </td>  
   <td>
   O  
   </td>  
   <td colspan="2" >
   Transaction Amount  
   </td>  
  </tr>  
  <tr>  
   <td>
   transAmount.value  
   </td>  
   <td>
   String  
   </td>  
   <td>
   M  
   </td>  
   <td colspan="2" >
   Transaction amount value  
   </td>  
  </tr>  
  <tr>  
   <td>
   transAmount.currency  
   </td>  
   <td>
   String  
   </td>  
   <td>
   M  
   </td>  
   <td colspan="2" >
   Currency,  e.g: IDR  
   </td>  
  </tr>  
  <tr>  
   <td>
   paidTime  
   </td>  
   <td>
   String  
   </td>  
   <td>
   C  
   </td>  
   <td colspan="2" >
   Update time of the individual transaction. The value will be returned for successful payment. Using ISO-8601 timestamp format  
   </td>  
  </tr>  
  <tr>  
   <td>
   refundHistory  
   </td>  
   <td>
   Array of refund Object  
   </td>  
   <td>
   C  
   </td>  
   <td colspan="2" >  
   </td>  
  </tr>  
  <tr>  
   <td>
   refundHistory.refundNo  
   </td>  
   <td>
   String  
   </td>  
   <td>
   M  
   </td>  
   <td colspan="2" >
   Transaction Identifier on Service Provider System  
   </td>  
  </tr>  
  <tr>  
   <td>
   refundHistory.partnerReferenceNo  
   </td>  
   <td>
   String  
   </td>  
   <td>
   M  
   </td>  
   <td colspan="2" >
   ReferenceNumber from merchant for the refund.  
   </td>  
  </tr>  

<tr>  
   <td>
   refundHistory.refundStatus  
   </td>  
   <td>
   String  
   </td>  
   <td>
   M  
   </td>  
   <td colspan="2" >
   Refund status. Possible values: <br /> - 00 --> Refund success <br /> - 06 --> Refund failed
   </td>  
  </tr>
  <tr>  
   <td>
   refundHistory.refundAmount  
   </td>  
   <td>
   Object  
   </td>  
   <td>
   M  
   </td>  
   <td colspan="2" >  
   </td>  
  </tr>  
  <tr>  
   <td>
   refundHistory.refundAmount.value  
   </td>  
   <td>
   String  
   </td>  
   <td>
   M  
   </td>  
   <td colspan="2" >
   Net amount of the refund.  
   </td>  
  </tr>  
  <tr>  
   <td>
   refundHistory.refundAmount.currency  
   </td>  
   <td>
   String  
   </td>  
   <td>
   M  
   </td>  
   <td colspan="2" >
   Currency  
   </td>  
  </tr>  

<tr>
   <td>
   refundHistory.refundDate
   </td>
   <td>
   String
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   Refund trial date (ISO 8601)
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
   Additional Information if a merchant needs to use. 
   </td>
  </tr>
  <tr>
   <td>
   additionalInfo.fraudStatus
   </td>
   <td>
   String 
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Fraud status. Possible values: <br /> - accept --> Transaction is safe to proceed. It is not considered as a fraud. <br /> - deny --> Transaction is considered as fraud. It is rejected by Midtrans.
   </td>
  </tr>
  <tr>
   <td>
   additionalInfo.validUpTo
   </td>
   <td>
   String(25)
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   The time when the payment will be automatically expired. Using ISO 8601 format
   </td>
  </tr>
  <tr>
   <td>
   additionalInfo.payOptionDetails
   </td>
   <td>
   Array of Object 
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   Payment option used by user. <br /><br /> This parameter will be deprecated soon. We encourage merchant to not consume this parameter and instead consume the parameter `additionalInfo.userPaymentDetails` instead. 
   </td>
  </tr>
  <tr>
   <td>
   additionalInfo.payOptionDetails.payMethod
   </td>
   <td>
   String
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   Payment method used by user. E.g: gopay
   </td>
  </tr>
  <tr>
   <td>
   additionalInfo.payOptionDetails.payOption
   </td>
   <td>
   String
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   Payment option used by user. Possible value: <br /> - GOPAY_WALLET = GoPay

<br /> - PAY\_LATER = GoPay Later

<br /> - GOPAY\_SAVINGS = GoPay Tabungan by Jago

   </td>
  </tr>
  <tr>
   <td>
   additionalInfo.metadata
   </td>
   <td>
   Object
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Transaction metadata
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
      <td colspan="2" > 
      Payment option used by user.
      </td>
  </tr>

<br />

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
      <td colspan="2" > 
      Payment method used by user. E.g: gopay
      </td>
  </tr>

<br />

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
         <td colspan="2" > 
         Payment option used by user. 

            <br /> Possible value: <br /> - GOPAY\_WALLET = GoPay

            <br /> - PAY\_LATER = GoPay Later

            <br /> - GOPAY\_SAVINGS = GoPay Tabungan by Jago

         </td>
  </tr>
  </tr>
</table>

```
{
   "responseCode":"2005500",
   "responseMessage":"Request has been processed successfully",
   "originalPartnerReferenceNo": "merchant-order-id",
   "originalReferenceNo":"2020102977770000000009",
   "originalExternalId": "original-external-id",
   "serviceCode":"54",
   "latestTransactionStatus":"00",
   "transAmount":{
      "value":"112345678.00",
      "currency":"IDR"
   },
   "paidTime":"2023-05-15T14:56:11+07:00",
   "refundHistory":[
  	{
     	     	"refundNo":"96194816941239812",
     	     	"partnerReferenceNo":"239850918204981205970",
          		"refundAmount":{
          	   	     	"value":"12345678.00",
         	    	     	"currency":"IDR"
     	     	},
      			"refundStatus": "00",
     	     	"refundDate":"2020-12-23T07:44:16+07:00",
          		"reason":"Customer Complain"
  	}
   ],
   "additionalInfo":{ 
      "fraudStatus":"accept"  ,
       "validUpTo":"2023-07-03T10:36:17+07:00",
       “payOptionDetails” : [{
          "payMethod":"gopay",
          "payOption": "GOPAY_WALLET"
        }], 
        “userPaymentDetails” : [{
          "payMethod":"gopay",
          "payOption": "GOPAY_WALLET"
        }],
   “metadata” : {}
   }
}
```

<br />

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
   2005500
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
   4005502
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
   4015500
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
   4015501
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
   5005501
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
   5045500
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

## Fetching transaction status for GoPay QRIS transaction

This section will describe how a merchant can fetch transaction status for GoPay QRIS transactions.

| Path              | /`{version}`/qr/qr-mpm-query |
| :---------------- | :--------------------------- |
| HTTP Method       | POST                         |
| Version           | v1.0                         |
| SNAP Service Code | 51                           |

<br />

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
   Represents access_token of a request; string starts with keyword “Bearer ” followed by access_token. Can get this token from Access Token B2B response.
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
      Transaction identifier on service provider system. For e.g: GopayOrderId 
      <p>
         Note: either <b>originalExternalId</b> or <b>originalPartnerReferenceNo</b> or <b>OriginalReferenceNo</b> need to be filled. 
      </p>
      If all fields have value, <b>originalReferenceNo</b> will be taken as the main identifier, followed by <b>originalPartnerReferenceNo</b> and then <b>originalExternalId</b>
   </td>
  </tr>
  <tr>
   <td>
      originalPartnerReferenceNo
   </td>
   <td>
      String(36)
   </td>
   <td>
      C
   </td>
   <td colspan="2" >
      partnerReferenceNo of the original transaction.
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
      C
   </td>
   <td colspan="2" >
      This should be filled with the X-EXTERNAL-ID from header of the original create QR payment API - <b>/`{version}`/qr/qr-mpm-generate</b>
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
      O
   </td>
   <td colspan="2" >
      Merchant id, we suggest to send this 
   </td>
  </tr>
  <tr>
   <td>
      serviceCode
   </td>
   <td>
      String (2)  
   </td>
   <td>
      M
   </td>
   <td colspan="2" >
      Transaction type indicator (service code of the original transaction request). For e.g: <strong>47</strong>
   </td>
  </tr>
</table>

```
{
   "originalReferenceNo":"2020102977770000000009",
   "originalPartnerReferenceNo":"12345678901234567890",
   "originalExternalId":"12345678901234567890",
   "merchantId":"00007100010926",
   "serviceCode":"47"
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
   <td colspan="2" >
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
   originalExternalId
   </td>
   <td>
   String(36)
   </td>
   <td>
   C
   </td>
   <td colspan="2" >
   X-EXTERNAL-ID from header of the original create QR payment API - <b>/``{version}``/qr/qr-mpm-generate</b>
   </td>
  </tr>
  <tr>
   <td>
   originalPartnerReferenceNo
   </td>
   <td>
   String(36)
   </td>
   <td>
   C
   </td>
   <td colspan="2" >
   partnerReferenceNo of the original transaction.
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
   Transaction identifier in GoPay system.  \
 \
The value will be returned for successful payment. 
   </td>
  </tr>
  <tr>
   <td>
   serviceCode
   </td>
   <td>
   String(2)  
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   Transaction type indicator (service code of the original transaction request).  \
 \
For e.g: <strong>47 , 77, 78 </strong>which are serviceCode of Payment, Cancel and Refund APIs
   </td>
  </tr>
  <tr>
   <td>
   latestTransactionStatus
   </td>
   <td>
   String (2) 
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
         Status of the transaction.
      <strong> 
      Possible Values:  
      </strong>

      <li>00 (Success)</li>

      <li>03 (Pending)</li>

      <li>04 (Refunded)</li>

      <li>05 (Canceled)</li>

      <li>06 (Failed)</li>

      <li>07 (Not found)</li>

      <li>08 (Expiry)</li>

      <li>09 (Rejected)</li>

      <br /> We will only return the numeric value on the API response. The text (...) is only the status code description and won't be returned in the actual response.   

</td>
  </tr>
  <tr>
   <td>
   transactionStatusDesc
   </td>
   <td>
   String(50)
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Transaction status description
   </td>
  </tr>
  <tr>
   <td>
   paidTime
   </td>
   <td>
   DateTime String
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Transaction time
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
   String(16,2)
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   Transaction amount
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
   <td colspan="2" >
   Transaction currency
   </td>
  </tr>

  <tr>
   <td>
   terminalId
   </td>
   <td>
   String(16)
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Merchant terminal id
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
   Additional information
   </td>
  </tr>
   <tr>
   <td></td>
   <td>
   refundHistory.refundStatus  
   </td>  
   <td>
   String  
   </td>  
   <td>
   M  
   </td>  
   <td colspan="2" >
   Refund status. Possible values: <br /> - 00 --> Refund success <br /> - 06 --> Refund failed
   </td>  
     </tr>
   <tr>
   <td>
   refundHistory
   </td>
   <td>
   Array of Object
   </td>
   <td>
   C
   </td>
   <td colspan="2" >
   Refund history associated with the transaction
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
   <td colspan="2" >
   Reason for the refund. 
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
   <td colspan="2" >
   Refund transaction identifier on service provider system
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
   <td colspan="2" >
   Unique identifier of refund transaction generated by the client.
   </td>
  </tr>

<br />

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
   <td colspan="2" >
   Refund time. ISO 8601
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
   <td colspan="2" >
   Refund amount object
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
   <td colspan="2" >
   Net amount of the refund.
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
   <td colspan="2" >
   Currency of the refund
   </td>
  </tr>

</table>

> 📘 Expected Response
>
> As you can pass any value from : **originalReferenceNo**, or **originalPartnerReferenceNo**, or **originalExternalID**
>
> Here's the expected response for each scenario of acceptable values :
>
> 1. **originalReferenceNo**, Midtrans will return **originalReferenceNo**
> 2. **originalPartnerReferenceNo**, Midtrans will return **originalPartnerReferenceNo** + **originalReferenceNo**
> 3. **originalExternalID**, Midtrans will return **originalExternalID** + **originalReferenceNo**
>
> In short, Midtrans will always return **originalReferenceNo**, for any successful trx.

```
{
  "responseCode": "2005100",
  "responseMessage": "Request has been processed successfully",
  "originalReferenceNo": "2020102977770000000009",
  "originalPartnerReferenceNo":"12345678901234567890",
  "originalExternalId": "12345678901234567890",
  "serviceCode": "47",
  "latestTransactionStatus": "00",
  "transactionStatusDesc": "success",
  "paidTime": "2020-10-20T17:56:57",
  "amount": {
    "value": "12345678.00",
    "currency": "IDR"
  },
  "terminalId": "213141251124",
  "additionalInfo": {
    "refundHistory": [
        	{
            	"reason": "some-reason",
            	"refundNo": "A120240815023459htV0bgKH7TID",
            	"partnerReferenceNo": "1723689297",
            	"refundDate": "2024-08-15T09:34:59+07:00",
              "refundStatus": "00",
            	"refundAmount": {
                	"currency": "IDR",
                	"value": "10.00"
            	}
        	}
    	]
  }
}
```

<br />

### List of response code

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
   2005100
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
   4005102
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
   4015100
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
   5005101
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
   5045100
   </td>
   <td>
   504
   </td>
   <td>
   Timeout
   </td>
  </tr>
</table>

<br />

***

## Fetching transaction status for GoPay Tokenization (Pre Auth) transaction

This section will describe how a merchant can fetch transaction status for GoPay Tokenization (Pre Auth) transactions.

| Path              | /`{version}`/auth/query |
| :---------------- | :---------------------- |
| HTTP Method       | POST                    |
| Version           | v1.0                    |
| SNAP Service Code | 64                      |

<br />

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
If both fields have value, will use originalReferenceNo as the main identifier.
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
    "originalReferenceNo": "Gopay OrderId",
    "originalPartnerReferenceNo": "Merchant OrderId",
    "additionalInfo": {
           "originalExternalId": "external-id"
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
   paidTime
   </td>
   <td>
   String(25)
   </td>
   <td>
   C
   </td>
   <td colspan="2" >
   Transaction paid time. (Will appear only if transaction in success state)
   </td>
  </tr>
  <tr>
   <td>
   latestTransactionStatus
   </td>
   <td>
   String (2)
   </td>
   <td>
   C
   </td>

<strong> 
Possible Values:  
</strong>

   <td colspan="2" >

<p>

00 (Success)  
</p>
<p>

01 (Initiated)
</p>
<p>
04 (Refunded)
</p>
<p>
05 (Canceled)
</p>
<p>
06 (Failed)
</p>
<p>
07 (Not found)
</p>
<p> 08 (Expiry)</p>

<p> 09 (Rejected)</p>

<br /> We will only return the numeric value on the API response. The text (...) is only the status code description and won't be returned in the actual response.  

   </td>  
  </tr>  
  <tr>  
   <td>
   amount  
   </td>  
   <td>  
   </td>  
   <td>
   O  
   </td>  
   <td colspan="2" >  
   </td>  
  </tr>  
  <tr>  
   <td>
   amount.value  
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
   amount.currency  
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
   additionalInfo.fraudStatus  
   </td>  
   <td>
   String  
   </td>  
   <td>
   O  
   </td>  
   <td colspan="2" >
   Fraud status. Possible values: <br /> - accept --> Transaction is safe to proceed. It is not considered as a fraud. <br /> - deny --> Transaction is considered as fraud. It is rejected by Midtrans. 
   </td>  
  </tr>  
  <tr>  
   <td>
   additionalInfo.validUpTo  
   </td>  
   <td>
   String(25)  
   </td>  
   <td>
   O  
   </td>  
   <td colspan="2" >
   The time when the payment will be automatically expired. Using ISO 8601 format  
   </td>  
  </tr>   
  <tr>  
   <td>
   additionalInfo.payOptionDetails.payOption  
   </td>  
   <td>
   String (64)  
   </td>  
   <td>
   M  
   </td>  
   <td colspan="2" >
   Payment option which shows the provider of this payment  
<p>  
e.g. E-Money, Gopay Coins , CICIL_MAB , PayLater 
</p> 
   </td>  
  </tr>  
  <tr>  
   <td>
   additionalInfo.payOptionDetails.payMethod  
   </td>  
   <td>
   String (64)  
   </td>  
   <td>
   M  
   </td>  
   <td colspan="2" >
   Payment Method. e.g. CREDIT_CARD , GOPAY  
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
   <td colspan="2" >
   Reference Number from PJP AIS for the refund.  
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
   <td colspan="2" >
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
   <td colspan="2" >
   Net amount of the refund.  
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
   <td colspan="2" >
   Currency  
   </td>  
  </tr>  

<br />

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
   <td colspan="2" >
   Refund trial date (ISO 8601)
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
   <td colspan="2" >
   Refund No
   </td>
  </tr>
  <tr>
    
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
   <td colspan="2" >
   Refund reason
   </td>
  </tr>
  <tr>
    
       </tr>
   <td>
   additionalInfo.refundHistory.refundStatus
   </td>
   <td>
   String
   </td>
   <td>
   M
   </td>
   <td colspan="2" >
   Refund status
   </td>
  </tr>
  <tr>
    
   <td>
   additionalInfo.metadata
   </td>
   <td>
   Object
   </td>
   <td>
   O
   </td>
   <td colspan="2" >
   Transaction  metadata
   </td>
  </tr>
</table>

```Text Successful Response
{
   "responseCode":"2006400",
   "responseMessage":"Request has been processed successfully",
   "originalPartnerReferenceNo": "merchant-order-id",
   "originalReferenceNo":"2020102977770000000009",
   "latestTransactionStatus":"00",
   "paidTime":"2023-05-15T14:56:11+07:00",
   "additionalInfo":{ 
          "fraudStatus":"accept"  ,
          "validUpTo":"2023-07-03T10:36:17+07:00",
          "refundHistory":[
  	      {
     	     	"refundNo":"96194816941239812",
     	     	"partnerReferenceNo":"239850918204981205970",
          		"refundAmount":{
          	   	     	"value":"12345678.00",
         	    	     	"currency":"IDR"
     	     	},
     	     	"refundDate":"2020-12-23T07:44:16+07:00",
          		"reason":"Customer Complain",
              "refundStatus":"00"
  	}
         ],
         “payOptionDetails” : [{
                "payMethod":"Gopay",
                  "payOption": "Coins"
        }], 
   },
   “metadata” : {}
}
```
```Text Error Response
{
   "responseCode":"4006401",
   "responseMessage":"There is some issue with the transaction request"
}
```

<br />

### List of response code

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
   2006400
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
   4006402
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
   4016400
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
   4016401
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
   5006401
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
   5046400
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

## Fetching transaction status for bank transfer (virtual account) transaction

This section describe how a merchant can fetch transaction status of bank trasnfer

| Path              | /`{version}`/transfer-va/status |
| :---------------- | :------------------------------ |
| HTTP Method       | POST                            |
| Version           | v1.0                            |
| SNAP service code | 26                              |

<br />

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
   String
   </td>
   <td>
   M
   </td>
   <td>
   Client's current local time in “yyyy-MM-
<p>
ddTHH:mm:ssZ” format
</p>
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
   Bearer token obtained from Access Token API in the format Bearer &lt;AccessToken>
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
   StringToSign: &lt;ClientKey>|&lt;X-TIMESTAMP:yyyy-mm-dd HH:mm:ssZ>
<p>
Signature Generation: SHA256withRSA(PrivateKey, StringToSign)
</p>
Encoded Signature: BASE64(Signature)
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
   Unique ID for a partner.
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
   Transaction ID in Partner system. Numeric String. Same value with trxId.
   </td>
  </tr>
</table>

```
X-TIMESTAMP 2022-03-04T08:02:09+07:00
X-SIGNATURE yqmBXZ3yV6NPG1LtwXMm3quXzJMRX5Ms+r9ebc5xWIZGSKbZL3Oy871GHb7WQUucLa5nxN/HcnZYoNHc+KkWTQ==
X-PARTNER-ID 668052e34f194aa8be79e15a21e4fc2f
X-EXTERNAL-ID 91919644194391346361915387229113
CHANNEL-ID 12345
Authorization Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIxMmUzODE4Mi00YjIxLTQ0YWMtOTVkNi1mMjFhMjEwZmIxZTAiLCJjbGllbnRJZCI6IjY2ODA1MmUzNGYxOTRhYThiZTc5ZTE1YTIxZTRmYzJmIiwibmJmIjoxNjYzODQwNTU5LCJleHAiOjE2NjM4NDE0NTksImlhdCI6MTY2Mzg0MDU1OX0.fEr0vIbB2kY8alZ-SROl3ftAFbfRd0uU-lGq9XuFi8M
Content-Type application/json
```

<br />

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
   String(8)
   </td>
   <td>
   M
   </td>
   <td>
   Derivative of X- PARTNER- ID, similar to company code, 8 digit left padding space. The first 8 digits from virtualAccountNo.
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
   <td>
   Unique number (up to 20 digits). The sixth digit until end from virtualAccountNo.
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
   <td>
   partnerServiceId + customerNo (up to 20 digits). From response charge.
   </td>
  </tr>
  <tr>
   <td>
   inquiryRequestId
   </td>
   <td>
   String(128)
   </td>
   <td>
   M
   </td>
   <td>
   Unique identifier from Inquiry
   </td>
  </tr>
  <tr>
   <td>
   paymentRequestId
   </td>
   <td>
   String(128)
   </td>
   <td>
   O
   </td>
   <td>
   Unique identifier from Payment
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
  <tr>
   <td>
   additionalInfo.merchantId
   </td>
   <td>
   String
   </td>
   <td>
   M
   </td>
   <td>
   Merchant ID
   </td>
  </tr>
</table>

```
{
   "partnerServiceId":" 12345",
   "customerNo":123456789012345678,
   "virtualAccountNo":" 12345123456789012345678",
   "inquiryRequestId":"202202111031031234500001136962",
   "paymentRequestId":"202202111031031234500001136962",
   "additionalInfo":{
      "merchant_id": "G12345463"
   }
}
```

<br />

### Response Header

| Field Name   | Field Type | Mandatory | Field Description                                |
| :----------- | :--------- | :-------- | :----------------------------------------------- |
| Content-Type | String     | M         | Media type of the resource, i.e application/json |
| X-TIMESTAMP  | String     | M         | Client's current local time in ISO-8601          |

```
Content-type:application/json
X-TIMESTAMP:2024-03-19T14:30:00+07:00
```

<br />

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
   String(7)
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
   virtualAccountData
   </td>
   <td>
   Object
   </td>
   <td>
   M
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.paymentFlagReason
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
  <tr>
   <td>
   virtualAccountData.paymentFlagReason.english
   </td>
   <td>
   String(200)
   </td>
   <td>
   O
   </td>
   <td>
   Reason for Payment Status in English
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.paymentFlagReason.indonesia
   </td>
   <td>
   String(200)
   </td>
   <td>
   O
   </td>
   <td>
   Reason for Payment Status in English
   </td>
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
   <td>
   Derivative of X- PARTNER- ID, similar to company code, 8 digit left padding space.
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.customerNo
   </td>
   <td>
   String(20)
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
   String(28)
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
   virtualAccountData.inquiryRequestId
   </td>
   <td>
   String(128)
   </td>
   <td>
   M
   </td>
   <td>
   Unique identifier from Inquiry
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.paymentRequestId
   </td>
   <td>
   String(128)
   </td>
   <td>
   C
   </td>
   <td>
   Unique identifier for this Payment from PJP. Mandatory if Payment happened.
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.paidAmount
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
  <tr>
   <td>
   virtualAccountData.paidAmount.Value
   </td>
   <td>
   String(ISO 4217)(16,2)
   </td>
   <td>
   M
   </td>
   <td>
   Paid Amount with 2 decimal
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.paidAmount.Currency
   </td>
   <td>
   String(3)
   </td>
   <td>
   M
   </td>
   <td>
   Currency
<p>
Currency of amount based on ISO 4217
</p>
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.paidBills
   </td>
   <td>
   String(6)
   </td>
   <td>
   O
   </td>
   <td>
   Hexadecimal format of binary of flag of paid bills. If have 24 bills, and paid bills number 1, 4, 6, and 8, will be written in binary 1001010100 0000000000 0000 and converted in Hexa 95000
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.totalAmount
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
  <tr>
   <td>
   virtualAccountData.totalAmount.value
   </td>
   <td>
   String(ISO 4217)(16,2)
   </td>
   <td>
   M
   </td>
   <td>
   Total Amount with 2 decimal
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.paidAmount.currency
   </td>
   <td>
   String(3)
   </td>
   <td>
   M
   </td>
   <td>
   Currency
<p>
Currency of amount based on ISO 4217
</p>
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.trxDateTime
   </td>
   <td>
   Date(25)
   </td>
   <td>
   O
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.transactionDate
   </td>
   <td>
   Date(25)
   </td>
   <td>
   O
   </td>
   <td>
   Payment datetime when the payment happened
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.referenceNo
   </td>
   <td>
   String(15)
   </td>
   <td>
   O
   </td>
   <td>
   Payment auth code generated by PJP
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.paymentType
   </td>
   <td>
   String(1)
   </td>
   <td>
   O
   </td>
   <td>
   Type of payment
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.flagAdvise
   </td>
   <td>
   String(1)
   </td>
   <td>
   O
   </td>
   <td>
   Status is this a retry notification
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.paymentFlagStatus
   </td>
   <td>
   String(2)
   </td>
   <td>
   O
   </td>
   <td>
   <strong>Status for Payment Flag:</strong> <br />
<p>
00 (Success)
</p>
<p>
01 (Initiated)
</p>
<p>
02 (Paying)
</p>
<p>
03 (Pending)
</p>
<p>
04  (Refunded)
</p>
<p>
05 (Canceled)
</p>
<p>
06 (Failed)
</p>
<p>
07 (Not found)
</p>
<p> 08 (Expiry)</p>

<p> 09 (Rejected)</p>

<br /> We will only return the numeric value on the API response. The text (...) is only the status code description and won't be returned in the actual response.

   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.billDetails
   </td>
   <td>
   Array of Objects
   </td>
   <td>
   O
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.billDetails.billCode
   </td>
   <td>
   String(2)
   </td>
   <td>
   O
   </td>
   <td>
   Bill code for Customer choose
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.billDetails.billNo
   </td>
   <td>
   String(18)
   </td>
   <td>
   O
   </td>
   <td>
   Bill number from Partner
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.billDetails.billname
   </td>
   <td>
   String(20)
   </td>
   <td>
   O
   </td>
   <td>
   Bill Name
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.billDetails.billShortName
   </td>
   <td>
   String(10)
   </td>
   <td>
   O
   </td>
   <td>
   Bill Name to shown to
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.billDetails.billDescription.english
   </td>
   <td>
   String(18)
   </td>
   <td>
   O
   </td>
   <td>
   Bill Description in English
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.billDetails.billDescription.indonesia
   </td>
   <td>
   String(18)
   </td>
   <td>
   O
   </td>
   <td>
   Bill Description in Bahasa
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.billDetails.billSubCompany
   </td>
   <td>
   String(5)
   </td>
   <td>
   O
   </td>
   <td>
   Partner’s product code
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.billDetails.billAmount.Value
   </td>
   <td>
   String(ISO 4217)(16,2)
   </td>
   <td>
   M
   </td>
   <td>
   Transaction Amount.
<p>
Nominal inputted by Customer with 2 decimal
</p>
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.billDetails.billAmount
   </td>
   <td>
   Objects
   </td>
   <td>
   O
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.billDetails.billAmount.Currency
   </td>
   <td>
   String(3)
   </td>
   <td>
   M
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.billDetails.billReferenceNo
   </td>
   <td>
   Number(15)
   </td>
   <td>
   O
   </td>
   <td>
   Bill auth code generated by PJP
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.billDetails.status
   </td>
   <td>
   String(2)
   </td>
   <td>
   O
   </td>
   <td>
   Payment status for specific Bill
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.reason.english
   </td>
   <td>
   String(64)
   </td>
   <td>
   O
   </td>
   <td>
   Reason for Payment Status for specific Bill in English
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.reason.indonesia
   </td>
   <td>
   String(64)
   </td>
   <td>
   O
   </td>
   <td>
   Reason for Payment Status for specific Bill in Bahasa
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.freeTexts
   </td>
   <td>
   Array of Objects
   </td>
   <td>
   O
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.freeTexts.english
   </td>
   <td>
   String(32)
   </td>
   <td>
   O
   </td>
   <td>
   Will be shown in Channel
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.freeTexts.indonesia
   </td>
   <td>
   String(32)
   </td>
   <td>
   O
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>
   virtualAccountData.additionalInfo
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
   "responseCode": "2002600",
  "responseMessage": "Success",
  "virtualAccountData": {
    "paymentFlagStatus": "00",
    "paymentFlagReason": {
      "indonesia": "BERHASIL",
      "english": "SUCCESS"
    },
    "partnerServiceId": " 12345",
    "customerNo": "123456789012345678",
    "virtualAccountNo": " 12345123456789012345678",
    "inquiryRequestId": "202202111031031234500001136962",
    "paymentRequestId": "202202111031031234500001136962",
    "paidAmount": {
      "value": "100000.00",
      "currency": "IDR"
    },
    "paidBills": "",
    "totalAmount": {
      "value": "100000.00",
      "currency": "IDR"
    },
    "trxDateTime": "2022-02-12T17:29:57+07:00",
    "transactionDate": "2022-02-11T10:16:04+07:00",
    "referenceNo": "00113696201",
    "paymentType": "",
    "flagAdvise": "",
    "billDetails": [
      {
        "billCode": "",
        "billNo": "123456789012345678",
        "billName": "",
        "billShortName": "",
        "billDescription": {
          "english": "Maintenance",
          "indonesia": "Pemeliharaan"
        },
        "billSubCompany": "00000",
        "billAmount": {
          "value": "100000.00",
          "currency": "IDR"
        },
        "additionalInfo": {
          "value": ""
        },
        "billReferenceNo": "00113696201",
        "status": "00",
        "reason": {
          "english": "Success",
          "indonesia": "Sukses"
        }
      }
    ],
    "freeTexts": [
      {
        "english": "Free text",
        "indonesia": "Tulisan bebas"
      }
    ]
  },
  "additionalInfo": {
    
  }
}
```