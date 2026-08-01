---
updatedAt: 2026-07-27T12:25:51.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# KYC callback

<br />

# Description

This is a callback to notify partners BE-BE about the KYC process completion. The endpoint is to be implemented by the partner where we can send the callback as per the contract mentioned.

# Host

To be provided by partner

# Endpoint

/v1/callback/partner

# Method

PUT

<br />

# Headers

| Header Key    | Description                             | Example          |
| ------------- | --------------------------------------- | ---------------- |
| Authorization | Linking token received after login step |                  |
| Content-Type  | Standard HTTP content-type header       | application/json |

<br />

# Request payload

```json
{
  "submissionId": "submission-uuid",
  "partnerSessionId": "<submission.partnerSessionId>",
  "status": "COMPLETED",   
  "result": "VALID",  
  "reasonCode": null      
}
```

<Table>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Description
      </th>

      <th>
        Example
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        submissionId
      </td>

      <td>
        If multiple submissions are made for the same **partnerSessionId**, this field uniquely identifies a **submission**. Currently, the use case suggested is for debugging purposes only.
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        partnerSessionId
      </td>

      <td>
        **request-id** from the start of the Gopay ID process
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        status
      </td>

      <td>
        Identifies whether the KYC process successfully completed or met a technical error
      </td>

      <td>
        **COMPLETED**|**ERROR**
      </td>
    </tr>

    <tr>
      <td>
        result
      </td>

      <td>
        Identifies whether the KYC is approved, rejected&#x20;
      </td>

      <td>
        **VALID**|**INVALID**
      </td>
    </tr>

    <tr>
      <td>
        reasonCode
      </td>

      <td>
        For the following combinations, this field identifies the cause of the same.

        - status = **COMPLETED**, result = **INVALID**
        - status = **ERROR**, result = **null**
      </td>

      <td>

      </td>
    </tr>
  </tbody>
</Table>

<br />

<br />