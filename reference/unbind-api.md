---
updatedAt: 2025-11-11T00:45:49.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Unbind API

| Path              | /\{version}/registration-account-unbinding |
| :---------------- | :----------------------------------------- |
| HTTP Method       | POST                                       |
| Version           | v1.0                                       |
| SNAP service code | 09                                         |

<br />

## Request Header

| Field Name             | Field Type | Mandatory | Field Description                                                                                                                                             |
| :--------------------- | :--------- | :-------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Content-type           | String     | M         | Media type of the resource, i.e. application/json                                                                                                             |
| X-TIMESTAMP            | String     | M         | Client’s current local time in ISO-8601 format                                                                                                                |
| X-SIGNATURE            | String     | M         | Created using symmetric signature HMAC\_SHA512 algorithm                                                                                                      |
| Authorization          | String     | M         | Represents access\_token of a request; string starts with keyword “Bearer ” followed by access\_token. Can get this token from Access Token B2B API response. |
| Authorization-Customer | String     | M         | Represents access\_token of a request; string starts with keyword “Bearer ” followed by access\_token from Binding API response                               |
| X-PARTNER-ID           | String     | M         | Unique identifier for merchant. Merchant can send any value.                                                                                                  |
| X-EXTERNAL-ID          | String     | M         | Alphanumeric string. We suggest merchant to use UUID format. Reference number that should be unique in the same day or 1 day idempotency key.                 |
| X-DEVICE-ID            | String     | M         | Device identification on which the API services is currently being accessed by the end user (customer)                                                        |
| CHANNEL-ID             | String     | M         | Mandatory field from Bank Indonesia that can take any value with correct format 5 digits numeric string                                                       |

```
Content-type:application/json
Authorization: Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
Authorization-Customer : Bearer MjAyMjEwMTM2NjE1OGRiMS00NmM1LTQxMWQtYmU4NC01ODk1ZTdhMjg2NmY6OGNmM2U4NWUtZTc3Mi00NTJmLWFkYmEtNDcyNjRiOWZiZWIw
X-TIMESTAMP:2024-03-19T14:30:00+07:00
X-PARTNER-ID: BMRI
X-DEVICE-ID: 0987ADCASA
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
X-EXTERNAL-ID:1234567890123456789
CHANNEL-ID:12345
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
        merchantId
      </td>

      <td>
        String (64)
      </td>

      <td>
        M
      </td>

      <td>
        Merchant ID (use the same value with merchantId in get-auth-code endpoint) <br /><br /> Merchant payment handle, merchant identifier in UUID format. Provided by Midtrans. <br /> Note: this value is not Midtrans Merchant ID, but a different value, here's the sample format: 303b4f89-xxxx-xxxx-xxxx-62a8ffaefaf3 <br /><br /> The value on staging and production is different. Please make sure that you are sending the correct value based on the environment that you are using.
      </td>
    </tr>
  </tbody>
</Table>

```
{
   "merchantId":"550e8400-e29b-41d4-a716-446655440000"
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
| responseCode    | String(7)    | M         | Error code to specify the error returned.  |
| responseMessage | String (150) | M         | Debug message to provide more information. |
| referenceNo     | String       | M         | Debug id to provide more information.      |

```Text Successful Response
{
   "responseCode":"2000900", 
   "responseMessage":"Request has been processed successfully",
   "referenceNo":"19352694-0ef6-4439-8ad1-b1dfb8bbb85f"
}
```
```Text Error Response
{
   "responseCode":"5000900",
   "responseMessage":"Timeout",
   "referenceNo":"19352694-0ef6-4439-8ad1-b1dfb8bbb85f"
}
```

<br />

### List of Response Code

| Response Code | HTTP Status Code | Response Message                                                                                 |
| :------------ | :--------------- | :----------------------------------------------------------------------------------------------- |
| 2000900       | 200              | Success                                                                                          |
| 4000902       | 400              | Invalid Mandatory Field                                                                          |
| 4010900       | 401              | Unauthorized. Signature                                                                          |
| 4010900       | 401              | Unauthorized. Incorrect merchantId value (return if merchant id value in request body not valid) |
| 4010901       | 401              | Invalid Token (B2B)                                                                              |
| 4010902       | 401              | Invalid Customer Token                                                                           |
| 4040905       | 404              | Merchant Is Not Registered For Card Registration Services                                        |
| 5000901       | 500              | Internal Server Error                                                                            |
| 5040900       | 504              | Timeout                                                                                          |