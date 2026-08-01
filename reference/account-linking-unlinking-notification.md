---
updatedAt: 2025-11-10T23:15:09.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Account Linking and Unlinking Notification

| Path              | /\{version}/registration-account/notify |
| :---------------- | :-------------------------------------- |
| HTTP Method       | POST                                    |
| Version           | v1.0                                    |
| SNAP service code | 88                                      |

> 📘
>
> This API is not part of the BI-SNAP API specification provided by ASPI, hence merchant is not required to test this API during dev site test and functional test.

Midtrans will be send HTTP post notification to merchants during account linking completion and unlinking as shown in the diagram below:

**Account Linking**

<Image align="center" src="https://files.readme.io/e2fc24a970b336f73ad1e98914fd1952cd41582f47af0ddeea22e8f2f807ec02-SNAP_based_account_linking_flow-Copy_of_linking.drawio.png" />

<br />

**Account Unlinking**

<Image align="center" src="https://files.readme.io/b668f88f8633460401f9d4fde1e687082e7d803b0cdce049f184a09f8b052bf5-SNAP_based_account_linking_flow-Copy_of_linking.jpg" />

## Setting up

To start receiving notification on account linking and unlinking flow, merchant will first need to follow these steps:

1. Set up a notification URL and share this URL to Midtrans team during onboarding process. Merchant can only set 1 notification URL prefix and this will be used for both account linking and payment notification.
2. Midtrans will append a different path for each of notification type. For account linking notification the full URL endpoint will be **\[merchant's URL prefix]/v1.0/registration-account/notify**
3. Ensure merchant has whitelisted Midtrans outgoing IP address as follows:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Environment
      </th>

      <th>
        IP address
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Sandbox
      </td>

      <td>
        34.142.147.133/32\
        34.142.169.131/32\
        34.142.231.22/32\
        35.240.161.215/32\
        34.142.227.232/32\
        34.124.184.175/32\
        35.197.130.2/32\
        34.142.233.114/32\
        8.215.26.211/32\
        8.215.22.135/32\
        8.215.93.92/32\
        8.215.93.214/32\
        8.215.93.76/32\
        8.215.33.37/32\
        8.215.26.148/32\
        8.215.194.225/32\
        8.215.12.199/32\
        149.129.255.111/32
      </td>
    </tr>

    <tr>
      <td>
        Staging
      </td>

      <td>
        3.1.141.98/32\
        52.76.190.190/32\
        13.251.192.204/32\
        8.215.39.156/32\
        8.215.77.79/32\
        147.139.213.119/32\
        8.215.56.11/32\
        8.215.39.87/32\
        8.215.42.0/32\
        8.215.59.158/32\
        149.129.222.246/32\
        8.215.26.108/32\
        8.215.13.84/32
      </td>
    </tr>

    <tr>
      <td>
        Production
      </td>

      <td>
        13.228.166.126/32\
        52.220.80.5/32\
        3.1.123.95/32\
        8.215.30.222/32\
        147.139.209.49/32\
        8.215.32.142/32\
        147.139.163.77/32\
        8.215.25.24/32\
        8.215.3.193/32\
        147.139.210.20/32\
        149.129.238.95/32\
        8.215.9.206/32\
        147.139.134.22/32
      </td>
    </tr>
  </tbody>
</Table>

<br />

## Request Header

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
        Content-type
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
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

      <td>
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

      <td>
        Created using asymmetric signature. Asymmetric-Signature format :  

        SHA256withRSA (privateKey, stringToSign) with  

        stringToSign = HTTPMethod +”:“+ EndpointUrl +":“+ Lowercase(HexEncode(SHA-256(minify(RequestBody)))) + ":“ + TimeStamp
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
        Unique identifier for merchant. Merchant can send any value.
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
        Alphanumeric string. Reference number that should be unique in the same day or 1 day idempotency key.
      </td>
    </tr>
  </tbody>
</Table>

```text Request Header
Content-type:application/json
X-TIMESTAMP:2024-03-19T14:30:00+07:00
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
X-PARTNER-ID: BMRI
X-EXTERNAL-ID:12345678901234567890
```

<br />

## Request Body

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
        additionalInfo
      </td>

      <td>
        Object
      </td>

      <td>
        M
      </td>

      <td>
        Some additional info
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.accessToken
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Access token used for transaction (used for Authorization-Customer header). Can be acquired during Registration Account Binding API.
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
        Merchant's Midtrans merchant ID. Sample format: GXXXXXX
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.subMerchantId
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Merchant's Midtrans PoP ID. <br /><br /> Midtrans will return the PoP ID stated by merchant during Binding, or if merchant is **NOT** passing the PoP ID value, Midtrans will return a default PoP ID. 
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.paymentType
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Payment type used for linking. Example: `gopay`
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.accountStatus
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        `ENABLED`: Account is linked <br /> `DISABLED`: Account is unlinked
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.statusMessage
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Status message <br /> - `Account linked` <br /> - `User changed phone number` <br /> - `Account unlinked`
      </td>
    </tr>
  </tbody>
</Table>

```text Request Body
{
"additionalInfo": 
	{  
  	"accessToken":"MjAyMjEwMTM2NjE1OGRiMS00NmM1LTQxMWQtYmU4NC01ODk1ZTdhMjg2NmY6OGNmM2U4NWUtZTc3Mi00NTJmLWFkYmEtNDcyNjRiOWZiZWIw",
  	"merchantId": "G123123",
  	"subMerchantId": "pop-id",
  	"paymentType": "gopay",
  	"accountStatus":"ENABLED"
  	"statusMessage":"Account linked"
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
X-TIMESTAMP: 2024-03-19T14:30:00+07:00
```

<br />

## Response Body

| Field Name      | Field Type   | Mandatory | Field Description                          |
| :-------------- | :----------- | :-------- | :----------------------------------------- |
| responseCode    | String (7)   | M         | Error code to specify the error returned.  |
| responseMessage | String (150) | M         | Debug message to provide more information. |

```Text Response Body
{
   "responseCode":"2008800",
   "responseMessage":"Request has been processed successfully"
}
```

<br />

### List of Response Code

| Response Code | HTTP Status Code | Response Message      |
| :------------ | :--------------- | :-------------------- |
| 2008800       | 200              | Successful            |
| 5008800       | 500              | Internal Server Error |

<br />

## Notification retry mechanism for Open API

In case we got an error response when sending notification (non 2xx response) to merchants, Midtrans will retry up to 3 times with exponential intervals. For now, our retry mechanism is as follows:

1st retry delay time = 20ms\
2nd retry delay time = 40ms\
3rd retry delay time = 80ms

Notes: this interval can change at any time as part of improvement, we will update it periodically.