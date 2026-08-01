---
updatedAt: 2026-07-27T12:49:34.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# KYC Data Pull

# KYC Data Pull API

## Description

This API returns KYC data for the latest submission against a linked user in case the KYC submission is successful.

<br />

## Host

#### Staging

<https://identity.staging.midtrans.com>

No IP whitelisting

#### Production

<https://identity.midtrans.com>

IP whitelisted (Partner needs to provide)

<br />

## Endpoint

/forward/gopay-id/kyc/inbound/v1/users/submissions/current

<br />

## Method

GET

<br />

## Headers

| Header key     | Description                                       | Example     |
| :------------- | :------------------------------------------------ | :---------- |
| x-merchant-id  | Pre-agreed value shared that identifies a partner | FLOQ/PLUANG |
| authorization  | Linking token received after login step           |             |
| correlation-id | A unique ID per request for debugging purposes    |             |

<br />

## Response

### HTTP 200 (Submission approved|rejected)

```json
{
  "success": true,
  "data": {
    "status": "COMPLETED",
    "result": "VALID",
    "submissionId": "<submission_id>",
    "partner": "FLOQ",
    "onboardingPartner": "FLOQ-SDK-GOPAY_ID_KYC",
    "documents": [
      {
        "documentType": "SELFIE",
        "url": "",
        "expiresAt": "2025-11-24T10:16:01.107963"
      },
      {
        "documentType": "ADDITIONAL_SELFIE",
        "url": "",
        "expiresAt": "2025-11-24T10:16:01.110084"
      },
      {
        "documentType": "KYC_PROOF",
        "url": "",
        "expiresAt": "2025-11-24T10:16:01.111676"
      }
    ],
    "submissionData": {
      "ktp": {
        "name": "BCA SIMULATOR A",
        "dob": "1990-09-10",
        "birthPlace": "JAKARTA",
        "gender": "female",
        "documentNumber": "1234123412341234",
        "citizenship": "INDONESIA",
        "province": "DKI JAKARTA",
        "city": "JAKARTA SELATAN",
        "otherAddressDetails": "APT PS-1391 HENDRE",
        "subdistrict": "MANDAKAR",
        "village": "GORONTALO",
        "religion": "BUDHA",
        "maritalStatus": "CERAI MATI",
        "rw": "025",
        "rt": "004",
        "occupation": "ARTIS",
        "issuedAt": "2015-12-07"
      }
    },
    "createdAt": "2025-09-25T04:27:06.68818",
    "updatedAt": "2025-09-25T04:27:06.68818"
  }
}
```

<br />

### HTTP 200 (Submission in progress)

```
{
  "success": true,
  "data": {
    "status": "IN_PROGRESS",
    "submissionId": "<submission_id>",
    "partner": "FLOQ",
    "onboardingPartner": "FLOQ-SDK-GOPAY_ID_KYC"
    "createdAt": "2025-09-25T04:27:06.68818",
    "updatedAt": "2025-09-25T04:27:06.68818"
  }
}
```

<br />

### HTTP 200 (Submission initiated)

```
{
  "success": true,
  "data": {
    "status": "INITIATED",
    "submissionId": "<submission_id>",
    "partner": "FLOQ",
    "onboardingPartner": "FLOQ-SDK-GOPAY_ID_KYC"
    "createdAt": "2025-09-25T04:27:06.68818",
    "updatedAt": "2025-09-25T04:27:06.68818"
  }
}
```

<br />

### HTTP 404 (Submission not found)

```
{
  "success": false,
  "errors": [
    {
      "code": "1519",
      "entity": "FLOW_MANAGER",
      "cause": "SUBMISSION_NOT_FOUND"
    }
  ]
}
```

<br />

### HTTP 500 (Internal server error)

```
{
  "success": false,
  "errors": [
    {
      "code": "some_error_code",
      "entity": "FLOW_MANAGER",
      "cause": "some_error_cause"
    }
  ]
}
```

<br />

<br />