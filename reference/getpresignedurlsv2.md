---
updatedAt: 2026-06-15T10:18:04.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Get Presigned URLs V2

Get presigned URLs for you to upload required documents based on the submissionType.
After successful uploads, call the Confirm Upload API to start processing.


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
    "/esign-partner/v2/submissions/urls": {
      "get": {
        "summary": "Get Presigned URLs V2",
        "description": "Get presigned URLs for you to upload required documents based on the submissionType.\nAfter successful uploads, call the Confirm Upload API to start processing.\n",
        "operationId": "getPresignedUrlsV2",
        "parameters": [
          {
            "$ref": "#/components/parameters/OneKycToken"
          },
          {
            "$ref": "#/components/parameters/EsignOnboardingPartner"
          },
          {
            "$ref": "#/components/parameters/PartnerSessionId"
          },
          {
            "name": "submissionType",
            "in": "query",
            "required": true,
            "description": "Submission type for certificate registration",
            "schema": {
              "type": "string",
              "enum": [
                "DOCUMENT_SIGNING_WITH_LLC"
              ]
            },
            "example": "DOCUMENT_SIGNING_WITH_LLC"
          }
        ],
        "responses": {
          "200": {
            "description": "Successful presigned URL generation",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/PresignedUrlsSuccessResponse"
                },
                "examples": {
                  "DOCUMENT_SIGNING_WITH_LLC": {
                    "value": {
                      "success": true,
                      "data": {
                        "submissionId": "8a0aef3d-0e27-4a7e-a4ba-2e1b97bcb00c",
                        "status": "INITIATED",
                        "documents": {
                          "DOCUMENT_TO_SIGN": {
                            "documentUrl": "https://al-ky-id-s-esign-service.oss-ap-southeast-5.aliyuncs.com/CERT_REG/5e021eb4-d875-47bb-817b-8b1782f0c3bb_SELFIE?X-Amz-Security-Token=CAIS2QJ1q6Ft5B2yfSjIr5qGIPziqKpwxZuhMVbXsWoCadtn3I%2FzhTz2IHhMfHhsBO0Wsv0ymGFY5v8ZlrF0TZJGVEeBdchrq80IrlP4ONqe45TusOdcIEJ%2B4ODIWXDBx8b3T7jTbrG0I4WACT3tkit03sGJF1GLVECkNpukkINuas9tMCCzcTtBAqU9RGIg0rh4U0HcLvGwKBXnr3PNBU5zwGpGhHh49L60z7%2F3iHOcriWnk7VL996gc8P6MJI8YsshabrvgrwmJpim%2BTVL9h1H%2BJ1xiKF54jrdtrmfeQIJu03Xb7eJooE2cVMoNvhjQLQ5oeP9mvs9oeHJiYX8xlNEJfkQXD%2FfVD5KeEodqgbI3L8bAlWbUxylurjnXhL14xI4yxkQfYXGL2%2BrztOklfiAbnC7TOHusRvhOTzIMIP%2Bi7otmrEOtG7D5rfkaibJLfz3vihwpGvXWx1AX3YagAEc9cDzjyTiGa4217on4KanvDDLEM4S4R1v%2F7i0SSRVa8c4LTrGA28YjM3dv3e%2BYTVLzunP0PT7e8T5JSstO0Mhoi127g2u2ahJRxYrPEfGlOk6NycJNS345QM1k%2BKwVBetpUwWDNf8nosT16O2KjykrmXq66XrGmg6oiKKTUFmHiAA&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20260507T110754Z&X-Amz-SignedHeaders=host&X-Amz-Credential=LTAI5tK86mktEnBbhjUrMadp%2F20260507%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Expires=432000&X-Amz-Signature=9580cba19e5929c2a250eef3f5637571478d27142444bcf33a3fa53c34938884",
                            "documentReference": "5e021eb4-d875-47bb-817b-8b1782f0c3bb_SELFIE",
                            "expiryInSeconds": "432000"
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
      "EsignOnboardingPartner": {
        "name": "x-esign-onboarding-partner",
        "in": "header",
        "required": true,
        "description": "Used to identify the source of the request (generated by OneKYC team)",
        "schema": {
          "type": "string"
        },
        "example": "CLIENT_X-BE-CERT_REG"
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
      "PresignedUrlsSuccessResponse": {
        "type": "object",
        "properties": {
          "success": {
            "type": "boolean",
            "example": true
          },
          "data": {
            "$ref": "#/components/schemas/PresignedUrlsData"
          }
        }
      },
      "PresignedUrlsData": {
        "type": "object",
        "properties": {
          "submissionId": {
            "$ref": "#/components/schemas/SubmissionId"
          },
          "status": {
            "type": "string",
            "description": "Submission status",
            "example": "INITIATED"
          },
          "documents": {
            "$ref": "#/components/schemas/DocumentUrls"
          }
        }
      },
      "DocumentUrls": {
        "type": "object",
        "properties": {
          "KTP": {
            "$ref": "#/components/schemas/DocumentUrlInfo"
          },
          "SELFIE": {
            "$ref": "#/components/schemas/DocumentUrlInfo"
          }
        }
      },
      "DocumentUrlInfo": {
        "type": "object",
        "properties": {
          "documentUrl": {
            "type": "string",
            "format": "uri",
            "description": "Presigned URL where the document must be uploaded",
            "example": "https://al-ky-id-s-esign-service.oss-ap-southeast-5.aliyuncs.com/CERT_REG/5e021eb4-d875-47bb-817b-8b1782f0c3bb_SELFIE?X-Amz-Security-Token=CAIS2QJ1q6Ft5B2yfSjIr5qGIPziqKpwxZuhMVbXsWoCadtn3I%2FzhTz2IHhMfHhsBO0Wsv0ymGFY5v8ZlrF0TZJGVEeBdchrq80IrlP4ONqe45TusOdcIEJ%2B4ODIWXDBx8b3T7jTbrG0I4WACT3tkit03sGJF1GLVECkNpukkINuas9tMCCzcTtBAqU9RGIg0rh4U0HcLvGwKBXnr3PNBU5zwGpGhHh49L60z7%2F3iHOcriWnk7VL996gc8P6MJI8YsshabrvgrwmJpim%2BTVL9h1H%2BJ1xiKF54jrdtrmfeQIJu03Xb7eJooE2cVMoNvhjQLQ5oeP9mvs9oeHJiYX8xlNEJfkQXD%2FfVD5KeEodqgbI3L8bAlWbUxylurjnXhL14xI4yxkQfYXGL2%2BrztOklfiAbnC7TOHusRvhOTzIMIP%2Bi7otmrEOtG7D5rfkaibJLfz3vihwpGvXWx1AX3YagAEc9cDzjyTiGa4217on4KanvDDLEM4S4R1v%2F7i0SSRVa8c4LTrGA28YjM3dv3e%2BYTVLzunP0PT7e8T5JSstO0Mhoi127g2u2ahJRxYrPEfGlOk6NycJNS345QM1k%2BKwVBetpUwWDNf8nosT16O2KjykrmXq66XrGmg6oiKKTUFmHiAA&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20260507T110754Z&X-Amz-SignedHeaders=host&X-Amz-Credential=LTAI5tK86mktEnBbhjUrMadp%2F20260507%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Expires=432000&X-Amz-Signature=9580cba19e5929c2a250eef3f5637571478d27142444bcf33a3fa53c34938884"
          },
          "documentReference": {
            "type": "string",
            "description": "Unique reference for the document within the system",
            "example": "d4b9ddd1-8193-4291-82c9-a0bf72982b86_SELFIE"
          },
          "expiryInSeconds": {
            "type": "string",
            "description": "Time in seconds after which the documentUrl will expire",
            "example": "432000"
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