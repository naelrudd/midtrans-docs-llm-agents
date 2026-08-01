---
updatedAt: 2026-05-07T19:42:57.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Get Submission Details

Get submission details and status.

# OpenAPI definition

```json
{
  "openapi": "3.0.3",
  "info": {
    "title": "Esign APIs",
    "description": "APIs for Esign related operations such as certificate registration and document signing.",
    "version": "1.2.0",
    "contact": {
      "name": "GoTo OneKYC Team"
    }
  },
  "servers": [
    {
      "url": "https://onekyc.ky.id.sandbox.gopayapi.com",
      "description": "Sandbox - OneKYC Gateway"
    },
    {
      "url": "https://onekyc.ky.id.gopayapi.com",
      "description": "Production - OneKYC Gateway"
    }
  ],
  "paths": {
    "/esign-partner/v1/submissions": {
      "get": {
        "summary": "Get Submission Details",
        "description": "Get submission details and status.",
        "operationId": "getSubmissionDetails",
        "parameters": [
          {
            "$ref": "#/components/parameters/OneKycToken"
          },
          {
            "$ref": "#/components/parameters/PartnerUserId"
          },
          {
            "$ref": "#/components/parameters/PartnerUserIdType"
          },
          {
            "$ref": "#/components/parameters/PartnerSessionId"
          }
        ],
        "responses": {
          "200": {
            "description": "Successfully retrieved submission data",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/SubmissionResponse"
                },
                "examples": {
                  "CERT_REG": {
                    "summary": "CERT_REG Result",
                    "value": {
                      "success": true,
                      "data": {
                        "submissionId": "d208917d-84a1-4edc-98b0-af2c2f4fcf5e",
                        "userId": "sample-partner-user-id-12345",
                        "userIdType": "SAMPLE_USER_ID_TYPE",
                        "partnerSessionId": "sample-partner-session-id-12345",
                        "status": "COMPLETED",
                        "result": "VALID",
                        "submissionDetails": {
                          "verificationResult": {
                            "nik": "PASS",
                            "name": "PASS",
                            "dateOfBirth": "PASS",
                            "selfie": "PASS"
                          },
                          "registrationId": "6dab7f08-0dcb-4852-8459-59cb7c25f4dc",
                          "eligibleToActivate": false,
                          "onboardingCode": "NEW_USER",
                          "shouldSkipActivation": true
                        }
                      }
                    }
                  },
                  "STANDALONE_IDENTITY_VERIFICATION": {
                    "summary": "STANDALONE_IDENTITY_VERIFICATION Result",
                    "value": {
                      "success": true,
                      "data": {
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
                            "registrationId": "1ae4e009-0617-4ceb-931e-89dfd3b7cea0",
                            "eligibleToActivate": true,
                            "onboardingCode": "NEW_USER",
                            "shouldSkipActivation": true
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
            }
          },
          "400": {
            "$ref": "#/components/responses/BadRequest"
          },
          "401": {
            "$ref": "#/components/responses/Unauthorized"
          },
          "404": {
            "description": "User or submission not found",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ErrorResponse"
                },
                "examples": {
                  "userNotFoundForPartner": {
                    "summary": "User not found for partner",
                    "value": {
                      "success": false,
                      "data": {},
                      "errors": [
                        {
                          "code": "1514",
                          "cause": "USER_NOT_FOUND_FOR_PARTNER_AND_PARTNER_USER_ID_AND_PARTNER_USER_ID_TYPE"
                        }
                      ]
                    }
                  },
                  "userNotFound": {
                    "summary": "User not found",
                    "value": {
                      "success": false,
                      "data": {},
                      "errors": [
                        {
                          "code": "1518",
                          "cause": "USER_NOT_FOUND"
                        }
                      ]
                    }
                  }
                }
              }
            }
          },
          "500": {
            "$ref": "#/components/responses/InternalServerError"
          }
        }
      }
    }
  },
  "components": {
    "parameters": {
      "OneKycToken": {
        "name": "x-onekyc-token",
        "in": "header",
        "required": true,
        "description": "OneKYC Partner token generated using the Get Partner Token API",
        "schema": {
          "type": "string"
        },
        "example": "eyJraWQiOiJlYzdmMjY0ZS0wNDkwLTQxODgtYTRjZS0wMWZlMzQ2MWFmYzUi..."
      },
      "PartnerUserId": {
        "name": "x-partner-user-id",
        "in": "header",
        "required": true,
        "description": "User ID of the current session. OneKYC will tie this info to the resulting submission ID",
        "schema": {
          "type": "string"
        },
        "example": "ddd91k2n-81j2-nsm9-019m-msj1291829ja"
      },
      "PartnerUserIdType": {
        "name": "x-partner-user-id-type",
        "in": "header",
        "required": true,
        "description": "Detailed name of the User ID. OneKYC will tie this info to the resulting submission ID",
        "schema": {
          "type": "string"
        },
        "example": "CLIENT_X_USER_ID"
      },
      "PartnerSessionId": {
        "name": "x-partner-session-id",
        "in": "header",
        "required": true,
        "description": "Session ID (generated by partner) used as correlation ID between partner and OneKYC. Must be unique for each invocation",
        "schema": {
          "type": "string"
        },
        "example": "test-0008"
      }
    },
    "schemas": {
      "SubmissionResponse": {
        "type": "object",
        "properties": {
          "success": {
            "type": "boolean",
            "example": true
          },
          "data": {
            "$ref": "#/components/schemas/SubmissionData"
          }
        }
      },
      "SubmissionData": {
        "type": "object",
        "properties": {
          "submissionId": {
            "$ref": "#/components/schemas/SubmissionId"
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
              "IN_PROGRESS",
              "PARTIALLY_COMPLETED",
              "COMPLETED",
              "ERROR"
            ]
          },
          "result": {
            "type": "string",
            "description": "Result of the document verification",
            "enum": [
              "VALID",
              "INVALID"
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
              "AETHER_VERIFICATION_FAILED",
              "LIVENESS_CHECK_FAILED",
              "FRAUD_REJECT",
              "NOT_EKTP",
              "DUKCAPIL_REJECTED",
              "DUKCAPIL_IRRETRIEVABLE_ERROR",
              "EMAIL_HAS_BEEN_USED",
              "PHONE_HAS_BEEN_USED",
              "SYSTEM_ERROR"
            ]
          },
          "submissionDetails": {
            "oneOf": [
              {
                "$ref": "#/components/schemas/CertRegSubmissionDetails"
              },
              {
                "$ref": "#/components/schemas/SIVSubmissionDetails"
              }
            ]
          }
        }
      },
      "CertRegSubmissionDetails": {
        "type": "object",
        "properties": {
          "verificationResult": {
            "$ref": "#/components/schemas/VerificationResult"
          },
          "registrationId": {
            "type": "string",
            "format": "uuid"
          },
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
      },
      "SIVSubmissionDetails": {
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
      },
      "SubmissionId": {
        "type": "string",
        "format": "uuid",
        "description": "Unique identification of submission record"
      },
      "ErrorResponse": {
        "type": "object",
        "properties": {
          "success": {
            "type": "boolean",
            "example": false
          },
          "errors": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Error"
            }
          }
        }
      },
      "Error": {
        "type": "object",
        "properties": {
          "code": {
            "type": "string",
            "description": "Error code:\n- 110: Unauthorized, invalid token in header parameters\n- 900: Unknown error (500)\n- 1650: Missing header parameters (4XX)\n"
          },
          "entity": {
            "type": "string",
            "description": "Entity where the error occurred"
          },
          "cause": {
            "type": "string",
            "description": "Detailed message of the error"
          }
        }
      }
    },
    "responses": {
      "BadRequest": {
        "description": "Bad Request - Invalid input or missing required parameters",
        "content": {
          "application/json": {
            "schema": {
              "$ref": "#/components/schemas/ErrorResponse"
            },
            "example": {
              "success": false,
              "errors": [
                {
                  "code": "1539",
                  "cause": "PARTNER_USER_ID_CAN_NOT_BE_EMPTY"
                },
                {
                  "code": "1539",
                  "cause": "PARTNER_USER_ID_TYPE_CAN_NOT_BE_EMPTY"
                },
                {
                  "code": "1650",
                  "cause": "ESIGN_PARTNER_CAN_NOT_BE_EMPTY"
                },
                {
                  "code": "1650",
                  "cause": "ESIGN_ONBOARDING_PARTNER_CAN_NOT_BE_EMPTY"
                },
                {
                  "code": "1653",
                  "cause": "SUBMISSION_ID_DOES_NOT_BELONG_TO_CURRENT_USER"
                }
              ]
            }
          }
        }
      },
      "Unauthorized": {
        "description": "Unauthorized - Invalid or missing authentication token",
        "content": {
          "application/json": {
            "schema": {
              "$ref": "#/components/schemas/ErrorResponse"
            },
            "example": {
              "success": false,
              "errors": [
                {
                  "code": "110",
                  "cause": "UNAUTHORIZED"
                }
              ]
            }
          }
        }
      },
      "InternalServerError": {
        "description": "Internal Server Error - An unexpected error occurred on the server",
        "content": {
          "application/json": {
            "schema": {
              "$ref": "#/components/schemas/ErrorResponse"
            },
            "example": {
              "success": false,
              "errors": [
                {
                  "code": "900",
                  "cause": "GENERIC_SERVICE_ERROR"
                }
              ]
            }
          }
        }
      }
    }
  }
}
```