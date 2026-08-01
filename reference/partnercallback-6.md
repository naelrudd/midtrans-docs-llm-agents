---
updatedAt: 2026-04-29T18:12:52.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Partner Callback

This is API implemented in your system that we will call on completed submissions.

# OpenAPI definition

```json
{
  "openapi": "3.0.3",
  "info": {
    "title": "eSign API - Partner Callback",
    "description": "Webhook callback API that OneKYC calls on the partner's server upon submission completion.",
    "version": "1.0.0",
    "contact": {
      "name": "GTF Team"
    }
  },
  "servers": [
    {
      "url": "https://partner-server.com",
      "description": "Partner's callback server"
    }
  ],
  "tags": [
    {
      "name": "Callback",
      "description": "Webhook callback definitions"
    }
  ],
  "paths": {
    "/partner-callback-endpoint": {
      "servers": [
        {
          "url": "https://partner-server.com"
        }
      ],
      "post": {
        "servers": [
          {
            "url": "https://partner-server.com"
          }
        ],
        "tags": [
          "Callback"
        ],
        "summary": "Partner Callback",
        "description": "This is API implemented in your system that we will call on completed submissions.",
        "operationId": "partnerCallback",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/SubmissionData"
              },
              "examples": {
                "submissionValid": {
                  "$ref": "#/components/examples/submissionValid"
                },
                "submissionPartiallyCompleted": {
                  "$ref": "#/components/examples/submissionPartiallyCompleted"
                },
                "submissionRejected": {
                  "$ref": "#/components/examples/submissionRejected"
                }
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Callback processed successfully"
          }
        }
      }
    }
  },
  "components": {
    "schemas": {
      "SubmissionData": {
        "type": "object",
        "properties": {
          "submissionId": {
            "type": "string",
            "format": "uuid",
            "description": "Unique identification of submission record"
          },
          "flow": {
            "type": "string",
            "description": "Identification of submission type",
            "example": "STANDALONE_IDENTITY_VERIFICATION"
          },
          "userId": {
            "type": "string",
            "description": "User ID of the current session"
          },
          "userIdType": {
            "type": "string",
            "description": "Detailed name of the User ID"
          },
          "partnerSessionId": {
            "type": "string",
            "description": "Session ID used as correlation ID"
          },
          "status": {
            "type": "string",
            "description": "Status of the submission",
            "enum": [
              "COMPLETED",
              "IN_PROGRESS",
              "PARTIALLY_COMPLETED",
              "ERROR"
            ]
          },
          "result": {
            "type": "string",
            "description": "Result of the document verification",
            "enum": [
              "VALID",
              "INVALID",
              "REJECTED"
            ]
          },
          "processedAt": {
            "type": "string",
            "format": "date-time",
            "description": "Timestamp when the submission was processed"
          },
          "reasonCode": {
            "type": "string",
            "description": "Code indicating the reason of rejection",
            "enum": [
              "FRAUD_REJECT",
              "NOT_EKTP",
              "DUKCAPIL_REJECTED",
              "AETHER_VERIFICATION_FAILED",
              "LIVENESS_CHECK_FAILED",
              "EMAIL_HAS_BEEN_USED",
              "PHONE_HAS_BEEN_USED",
              "SYSTEM_ERROR"
            ]
          },
          "submissionDetails": {
            "$ref": "#/components/schemas/SubmissionDetails"
          }
        }
      },
      "SubmissionDetails": {
        "type": "object",
        "properties": {
          "ktpData": {
            "$ref": "#/components/schemas/KtpData"
          },
          "verificationResult": {
            "$ref": "#/components/schemas/VerificationResult"
          },
          "imageUrls": {
            "$ref": "#/components/schemas/ImageUrls"
          },
          "certificateRegistration": {
            "$ref": "#/components/schemas/CertificateRegistrationResult"
          }
        }
      },
      "KtpData": {
        "type": "object",
        "description": "Extracted values from the submitted eKTP",
        "properties": {
          "nik": {
            "type": "string",
            "description": "ID number (NIK) on the eKTP"
          },
          "name": {
            "type": "string",
            "description": "Name of the person"
          },
          "region": {
            "type": "string",
            "description": "Region of the person's residence (Place of Birth)"
          },
          "dateOfBirth": {
            "type": "string",
            "description": "Date of birth (DD-MM-YYYY)"
          },
          "bloodType": {
            "type": "string",
            "description": "Blood type of the person"
          },
          "religion": {
            "type": "string",
            "description": "Religion of the person"
          },
          "province": {
            "type": "string",
            "description": "Province of person's residence"
          },
          "city": {
            "type": "string",
            "description": "City of person's residence"
          },
          "address": {
            "type": "string",
            "description": "Address of the person's residence"
          },
          "district": {
            "type": "string",
            "description": "District of the person's residence"
          },
          "town": {
            "type": "string",
            "description": "Town of the person's residence"
          },
          "gender": {
            "type": "string",
            "description": "Gender of the person",
            "enum": [
              "male",
              "female"
            ]
          },
          "rt": {
            "type": "string",
            "description": "RT of the person's residence"
          },
          "rw": {
            "type": "string",
            "description": "RW of the person's residence"
          },
          "occupation": {
            "type": "string",
            "description": "Occupation of the person"
          },
          "validUntil": {
            "type": "string",
            "description": "Validity period of eKTP"
          },
          "citizenship": {
            "type": "string",
            "description": "Citizenship (WNI for Indonesia)"
          },
          "maritalStatus": {
            "type": "string",
            "description": "Marital status of the person"
          },
          "issuanceDate": {
            "type": "string",
            "description": "Issue date of the eKTP"
          }
        }
      },
      "VerificationResult": {
        "type": "object",
        "description": "Verification results",
        "properties": {
          "nik": {
            "type": "string",
            "description": "NIK verification status",
            "enum": [
              "PASS",
              "FAIL"
            ]
          },
          "name": {
            "type": "string",
            "description": "Name verification status",
            "enum": [
              "PASS",
              "FAIL"
            ]
          },
          "dateOfBirth": {
            "type": "string",
            "description": "Date of birth verification status",
            "enum": [
              "PASS",
              "FAIL"
            ]
          },
          "selfie": {
            "type": "string",
            "description": "User selfie verification status",
            "enum": [
              "PASS",
              "FAIL"
            ]
          }
        }
      },
      "ImageUrls": {
        "type": "object",
        "description": "URLs to uploaded document images",
        "properties": {
          "KTP": {
            "type": "string",
            "format": "uri",
            "description": "URL to KTP image"
          },
          "SELFIE": {
            "type": "string",
            "format": "uri",
            "description": "URL to selfie image"
          },
          "ADDITIONAL_SELFIE": {
            "type": "string",
            "format": "uri",
            "description": "URL to additional selfie image"
          }
        }
      },
      "CertificateRegistrationResult": {
        "type": "object",
        "description": "Certificate Registration results",
        "properties": {
          "eligibleToActivate": {
            "type": "boolean"
          },
          "shouldSkipActivation": {
            "type": "boolean"
          },
          "onboardingCode": {
            "type": "string",
            "enum": [
              "NEW_USER"
            ]
          }
        }
      }
    },
    "examples": {
      "submissionValid": {
        "summary": "Completed and Valid",
        "value": {
          "submissionId": "c64b4c8c-9a8f-4e9c-b86a-0908291c855e",
          "userId": "421453511adsasdl",
          "userIdType": "MY_USER_ID",
          "partnerSessionId": "b719f79b-ae7a-440a-8f9c-5f661ca34e7",
          "status": "COMPLETED",
          "result": "VALID",
          "submissionDetails": {
            "verificationResult": {
              "nik": "PASS",
              "name": "PASS",
              "dateOfBirth": "PASS",
              "selfie": "PASS"
            },
            "ktpData": {
              "nik": "3208201808850001",
              "name": "JOHN DOE",
              "region": "SEMARANG",
              "dateOfBirth": "18-02-1960",
              "bloodType": "-",
              "religion": "KRISTEN",
              "province": "JAWA TIMUR",
              "city": "KOTA SURABAYA",
              "address": "SEMARANG SELATAN",
              "district": "WAYANG",
              "town": "BUBUTAN",
              "gender": "male",
              "rt": "008",
              "rw": "020",
              "occupation": "PELAJAR/MAHASISWA",
              "validUntil": "",
              "citizenship": "INDONESIA",
              "maritalStatus": "BELUM KAWIN",
              "issuanceDate": "28-12-2017"
            },
            "certificateRegistration": {
              "eligibleToActivate": true,
              "onboardingCode": "NEW_USER",
              "shouldSkipActivation": true
            },
            "imageUrls": {
              "KTP": "https://al-ky-id-s-esign-service.oss-ap-southeast-5.aliyuncs.com/STANDALONE_IDENTITY_VERIFICATION/555ba11a-d6e1-4110-b621-55d8e00b1c97_KTP?",
              "SELFIE": "https://al-ky-id-s-esign-service.oss-ap-southeast-5.aliyuncs.com/STANDALONE_IDENTITY_VERIFICATION/11117b7b-4444-4ef0-933b-d510ea920ec9_SELFIE?",
              "ADDITIONAL_SELFIE": "https://al-ky-id-s-esign-service.oss-ap-southeast-5.aliyuncs.com/STANDALONE_IDENTITY_VERIFICATION/333333db-2266-4d68-930c-6df0f059b88c_ADDITIONAL_SELFIE"
            }
          }
        }
      },
      "submissionPartiallyCompleted": {
        "summary": "Partially Completed",
        "value": {
          "submissionId": "c64b4c8c-9a8f-4e9c-b86a-0908291c855e",
          "userId": "421453511adsasdl",
          "userIdType": "MY_USER_ID",
          "partnerSessionId": "b719f79b-ae7a-440a-8f9c-5f661ca34e7",
          "status": "PARTIALLY_COMPLETED",
          "result": "VALID",
          "submissionDetails": {
            "verificationResult": {
              "nik": "PASS",
              "name": "PASS",
              "dateOfBirth": "PASS",
              "selfie": "PASS"
            },
            "ktpData": {
              "nik": "3208201808850001",
              "name": "JOHN DOE",
              "region": "SEMARANG",
              "dateOfBirth": "18-02-1960",
              "bloodType": "-",
              "religion": "KRISTEN",
              "province": "JAWA TIMUR",
              "city": "KOTA SURABAYA",
              "address": "SEMARANG SELATAN",
              "district": "WAYANG",
              "town": "BUBUTAN",
              "gender": "male",
              "rt": "008",
              "rw": "020",
              "occupation": "PELAJAR/MAHASISWA",
              "validUntil": "",
              "citizenship": "INDONESIA",
              "maritalStatus": "BELUM KAWIN",
              "issuanceDate": "28-12-2017"
            },
            "imageUrls": {
              "KTP": "https://al-ky-id-s-esign-service.oss-ap-southeast-5.aliyuncs.com/STANDALONE_IDENTITY_VERIFICATION/555ba11a-d6e1-4110-b621-55d8e00b1c97_KTP?X-Amz-Security-Token=CAIS2QJ1q6Ft5B2yfSjIr5rHH8rQg7JU0KGxSWCCkEcmeNkVnKLsmDz2IHhMfHhsBO0Wsv0ymGFY5v8ZlrF0TZJGVEeBdchrq80Irl7xOdSZ4JPtsOdcLQlC2tjIWXDBx8b3T7jTbrG0I4WACT3tkit03sGJF1GLVECkNpukkINuas9tMCCzcTtBAqU9RGIg0rh4U0HcLvGwKBXnr3PNBU5zwGpGhHh49L60z7%2F3iHOcriWnk7VL996gc8P6MJI8YsshabrvgrwmJpim%2BTVL9h1H%2BJ1xiKF54jrdtrmfeQIJu03Xb7eJooE2cVMoNvhjQLQ5oeP9mvs9oeHJiYX8xlNEJfkQXD%2FfVD5KeEodqgbI3L8bAlWbUxylurjnXhJ1NjD445zCTBxQjdw4BHVGGzImhM22RVRfAKkDk8ZKqmFkIXDnKFOULpQhLLBhXTvwqM1yun1wrvxKxR1AX3YagAEPOJHYBLG3yU3nDzQtoQM3dBI9eitetxHD7vMIVRc3tM1pPQRim08WPNWP7si%2BAwBK8bj8uw8BJFwOKM1c4qx1SvXlk%2FRW0Q%2BHxDkIC%2FF1dZQlXMiWkF%2FbmCeKarOntvV3I%2FPdbsCbAkRF7GrIIrWxGLgx%2FD7MYpiWTGUSjTsu3CAA&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20260413T053201Z&X-Amz-SignedHeaders=host&X-Amz-Credential=LTAI5tK86mktEnBbhjUrMadp%2F20260413%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Expires=432000&X-Amz-Signature=3906a4e5fdd07ffaebb61a15a7baa99754a7f1177cc1fb9d7aa6b29780ea5710",
              "SELFIE": "https://al-ky-id-s-esign-service.oss-ap-southeast-5.aliyuncs.com/STANDALONE_IDENTITY_VERIFICATION/11117b7b-4444-4ef0-933b-d510ea920ec9_SELFIE?X-Amz-Security-Token=CAIS2QJ1q6Ft5B2yfSjIr5rHH8rQg7JU0KGxSWCCkEcmeNkVnKLsmDz2IHhMfHhsBO0Wsv0ymGFY5v8ZlrF0TZJGVEeBdchrq80Irl7xOdSZ4JPtsOdcLQlC2tjIWXDBx8b3T7jTbrG0I4WACT3tkit03sGJF1GLVECkNpukkINuas9tMCCzcTtBAqU9RGIg0rh4U0HcLvGwKBXnr3PNBU5zwGpGhHh49L60z7%2F3iHOcriWnk7VL996gc8P6MJI8YsshabrvgrwmJpim%2BTVL9h1H%2BJ1xiKF54jrdtrmfeQIJu03Xb7eJooE2cVMoNvhjQLQ5oeP9mvs9oeHJiYX8xlNEJfkQXD%2FfVD5KeEodqgbI3L8bAlWbUxylurjnXhJ1NjD445zCTBxQjdw4BHVGGzImhM22RVRfAKkDk8ZKqmFkIXDnKFOULpQhLLBhXTvwqM1yun1wrvxKxR1AX3YagAEPOJHYBLG3yU3nDzQtoQM3dBI9eitetxHD7vMIVRc3tM1pPQRim08WPNWP7si%2BAwBK8bj8uw8BJFwOKM1c4qx1SvXlk%2FRW0Q%2BHxDkIC%2FF1dZQlXMiWkF%2FbmCeKarOntvV3I%2FPdbsCbAkRF7GrIIrWxGLgx%2FD7MYpiWTGUSjTsu3CAA&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20260413T053201Z&X-Amz-SignedHeaders=host&X-Amz-Credential=LTAI5tK86mktEnBbhjUrMadp%2F20260413%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Expires=432000&X-Amz-Signature=1b6c3eed9717ae5db92de2c2958d3ce76111dc4310db5d2dc54aec8f6689628a",
              "ADDITIONAL_SELFIE": "https://al-ky-id-s-esign-service.oss-ap-southeast-5.aliyuncs.com/STANDALONE_IDENTITY_VERIFICATION/333333db-2266-4d68-930c-6df0f059b88c_ADDITIONAL_SELFIE?X-Amz-Security-Token=CAIS2QJ1q6Ft5B2yfSjIr5rHH8rQg7JU0KGxSWCCkEcmeNkVnKLsmDz2IHhMfHhsBO0Wsv0ymGFY5v8ZlrF0TZJGVEeBdchrq80Irl7xOdSZ4JPtsOdcLQlC2tjIWXDBx8b3T7jTbrG0I4WACT3tkit03sGJF1GLVECkNpukkINuas9tMCCzcTtBAqU9RGIg0rh4U0HcLvGwKBXnr3PNBU5zwGpGhHh49L60z7%2F3iHOcriWnk7VL996gc8P6MJI8YsshabrvgrwmJpim%2BTVL9h1H%2BJ1xiKF54jrdtrmfeQIJu03Xb7eJooE2cVMoNvhjQLQ5oeP9mvs9oeHJiYX8xlNEJfkQXD%2FfVD5KeEodqgbI3L8bAlWbUxylurjnXhJ1NjD445zCTBxQjdw4BHVGGzImhM22RVRfAKkDk8ZKqmFkIXDnKFOULpQhLLBhXTvwqM1yun1wrvxKxR1AX3YagAEPOJHYBLG3yU3nDzQtoQM3dBI9eitetxHD7vMIVRc3tM1pPQRim08WPNWP7si%2BAwBK8bj8uw8BJFwOKM1c4qx1SvXlk%2FRW0Q%2BHxDkIC%2FF1dZQlXMiWkF%2FbmCeKarOntvV3I%2FPdbsCbAkRF7GrIIrWxGLgx%2FD7MYpiWTGUSjTsu3CAA&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20260413T053201Z&X-Amz-SignedHeaders=host&X-Amz-Credential=LTAI5tK86mktEnBbhjUrMadp%2F20260413%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Expires=432000&X-Amz-Signature=5964ff76bad7b1e39a3da0122cbdd438a80fc11ccc4731ec47c53f194232b6d6"
            }
          }
        }
      },
      "submissionRejected": {
        "summary": "Rejected",
        "value": {
          "submissionId": "c64b4c8c-9a8f-4e9c-b86a-0908291c855e",
          "userId": "421453511adsasdl",
          "userIdType": "MY_USER_ID",
          "partnerSessionId": "b719f79b-ae7a-440a-8f9c-5f661ca34e7",
          "status": "COMPLETED",
          "result": "INVALID",
          "reasonCode": "NOT_EKTP",
          "submissionDetails": {
            "rejectionReasonTranslations": {
              "en_ID": {
                "title": "Verification rejected",
                "message": "ID submitted is not eKTP"
              },
              "id_ID": {
                "title": "Proses verifikasi ditolak",
                "message": "Kartu identitas bukan eKTP"
              }
            },
            "imageUrls": {
              "KTP": "https://al-ky-id-s-esign-service.oss-ap-southeast-5.aliyuncs.com/STANDALONE_IDENTITY_VERIFICATION/555ba11a-d6e1-4110-b621-55d8e00b1c97_KTP?X-Amz-Security-Token=CAIS2QJ1q6Ft5B2yfSjIr5rHH8rQg7JU0KGxSWCCkEcmeNkVnKLsmDz2IHhMfHhsBO0Wsv0ymGFY5v8ZlrF0TZJGVEeBdchrq80Irl7xOdSZ4JPtsOdcLQlC2tjIWXDBx8b3T7jTbrG0I4WACT3tkit03sGJF1GLVECkNpukkINuas9tMCCzcTtBAqU9RGIg0rh4U0HcLvGwKBXnr3PNBU5zwGpGhHh49L60z7%2F3iHOcriWnk7VL996gc8P6MJI8YsshabrvgrwmJpim%2BTVL9h1H%2BJ1xiKF54jrdtrmfeQIJu03Xb7eJooE2cVMoNvhjQLQ5oeP9mvs9oeHJiYX8xlNEJfkQXD%2FfVD5KeEodqgbI3L8bAlWbUxylurjnXhJ1NjD445zCTBxQjdw4BHVGGzImhM22RVRfAKkDk8ZKqmFkIXDnKFOULpQhLLBhXTvwqM1yun1wrvxKxR1AX3YagAEPOJHYBLG3yU3nDzQtoQM3dBI9eitetxHD7vMIVRc3tM1pPQRim08WPNWP7si%2BAwBK8bj8uw8BJFwOKM1c4qx1SvXlk%2FRW0Q%2BHxDkIC%2FF1dZQlXMiWkF%2FbmCeKarOntvV3I%2FPdbsCbAkRF7GrIIrWxGLgx%2FD7MYpiWTGUSjTsu3CAA&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20260413T053201Z&X-Amz-SignedHeaders=host&X-Amz-Credential=LTAI5tK86mktEnBbhjUrMadp%2F20260413%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Expires=432000&X-Amz-Signature=3906a4e5fdd07ffaebb61a15a7baa99754a7f1177cc1fb9d7aa6b29780ea5710",
              "SELFIE": "https://al-ky-id-s-esign-service.oss-ap-southeast-5.aliyuncs.com/STANDALONE_IDENTITY_VERIFICATION/11117b7b-4444-4ef0-933b-d510ea920ec9_SELFIE?X-Amz-Security-Token=CAIS2QJ1q6Ft5B2yfSjIr5rHH8rQg7JU0KGxSWCCkEcmeNkVnKLsmDz2IHhMfHhsBO0Wsv0ymGFY5v8ZlrF0TZJGVEeBdchrq80Irl7xOdSZ4JPtsOdcLQlC2tjIWXDBx8b3T7jTbrG0I4WACT3tkit03sGJF1GLVECkNpukkINuas9tMCCzcTtBAqU9RGIg0rh4U0HcLvGwKBXnr3PNBU5zwGpGhHh49L60z7%2F3iHOcriWnk7VL996gc8P6MJI8YsshabrvgrwmJpim%2BTVL9h1H%2BJ1xiKF54jrdtrmfeQIJu03Xb7eJooE2cVMoNvhjQLQ5oeP9mvs9oeHJiYX8xlNEJfkQXD%2FfVD5KeEodqgbI3L8bAlWbUxylurjnXhJ1NjD445zCTBxQjdw4BHVGGzImhM22RVRfAKkDk8ZKqmFkIXDnKFOULpQhLLBhXTvwqM1yun1wrvxKxR1AX3YagAEPOJHYBLG3yU3nDzQtoQM3dBI9eitetxHD7vMIVRc3tM1pPQRim08WPNWP7si%2BAwBK8bj8uw8BJFwOKM1c4qx1SvXlk%2FRW0Q%2BHxDkIC%2FF1dZQlXMiWkF%2FbmCeKarOntvV3I%2FPdbsCbAkRF7GrIIrWxGLgx%2FD7MYpiWTGUSjTsu3CAA&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20260413T053201Z&X-Amz-SignedHeaders=host&X-Amz-Credential=LTAI5tK86mktEnBbhjUrMadp%2F20260413%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Expires=432000&X-Amz-Signature=1b6c3eed9717ae5db92de2c2958d3ce76111dc4310db5d2dc54aec8f6689628a",
              "ADDITIONAL_SELFIE": "https://al-ky-id-s-esign-service.oss-ap-southeast-5.aliyuncs.com/STANDALONE_IDENTITY_VERIFICATION/333333db-2266-4d68-930c-6df0f059b88c_ADDITIONAL_SELFIE?X-Amz-Security-Token=CAIS2QJ1q6Ft5B2yfSjIr5rHH8rQg7JU0KGxSWCCkEcmeNkVnKLsmDz2IHhMfHhsBO0Wsv0ymGFY5v8ZlrF0TZJGVEeBdchrq80Irl7xOdSZ4JPtsOdcLQlC2tjIWXDBx8b3T7jTbrG0I4WACT3tkit03sGJF1GLVECkNpukkINuas9tMCCzcTtBAqU9RGIg0rh4U0HcLvGwKBXnr3PNBU5zwGpGhHh49L60z7%2F3iHOcriWnk7VL996gc8P6MJI8YsshabrvgrwmJpim%2BTVL9h1H%2BJ1xiKF54jrdtrmfeQIJu03Xb7eJooE2cVMoNvhjQLQ5oeP9mvs9oeHJiYX8xlNEJfkQXD%2FfVD5KeEodqgbI3L8bAlWbUxylurjnXhJ1NjD445zCTBxQjdw4BHVGGzImhM22RVRfAKkDk8ZKqmFkIXDnKFOULpQhLLBhXTvwqM1yun1wrvxKxR1AX3YagAEPOJHYBLG3yU3nDzQtoQM3dBI9eitetxHD7vMIVRc3tM1pPQRim08WPNWP7si%2BAwBK8bj8uw8BJFwOKM1c4qx1SvXlk%2FRW0Q%2BHxDkIC%2FF1dZQlXMiWkF%2FbmCeKarOntvV3I%2FPdbsCbAkRF7GrIIrWxGLgx%2FD7MYpiWTGUSjTsu3CAA&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20260413T053201Z&X-Amz-SignedHeaders=host&X-Amz-Credential=LTAI5tK86mktEnBbhjUrMadp%2F20260413%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Expires=432000&X-Amz-Signature=5964ff76bad7b1e39a3da0122cbdd438a80fc11ccc4731ec47c53f194232b6d6"
            }
          }
        }
      }
    }
  }
}
```