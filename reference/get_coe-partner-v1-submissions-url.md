---
updatedAt: 2026-04-29T16:23:41.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Get presigned URLs for submission

# OpenAPI definition

```json
{
  "openapi": "3.0.3",
  "info": {
    "title": "Get Presigned URLs API",
    "description": "Generates presigned upload URLs for a new or existing submission.",
    "version": "1.0.0"
  },
  "servers": [
    {
      "url": "https://onekyc.ky.id.sandbox.gopayapi.com",
      "description": "Sandbox Server"
    }
  ],
  "paths": {
    "/coe/v1/submissions/urls": {
      "get": {
        "summary": "Get presigned URLs for submission",
        "operationId": "getPresignedUrls",
        "parameters": [
          {
            "name": "x-partner-session-id",
            "in": "header",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "Partner session identifier.",
            "example": "SESSION_123"
          },
          {
            "name": "x-onekyc-token",
            "in": "header",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "OneKYC User Token",
            "example": "eyJraW...[truncated]...w8d2Y2QgHHJxBQCBYZCAhTdQ7ySty5QquX0zQ8lJYDEbMwwsg"
          },
          {
            "name": "x-sdk-session-id",
            "in": "header",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "SDK session identifier.",
            "example": "SESSION_123"
          },
          {
            "name": "submissionType",
            "in": "query",
            "required": true,
            "schema": {
              "type": "string",
              "enum": [
                "KTP_SCAN",
                "STANDALONE_LIVENESS",
                "FACE_MATCH",
                "FACE_VERIFICATION",
                "KYC_LITE"
              ]
            },
            "description": "Submission type used to determine required document upload URLs.",
            "example": "FACE_VERIFICATION"
          }
        ],
        "responses": {
          "200": {
            "description": "Presigned URLs generated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/GetPresignedUrlsSuccessResponse"
                },
                "examples": {
                  "Success": {
                    "value": {
                      "success": true,
                      "data": {
                        "submissionId": "SUBMISSION_123",
                        "status": "INITIATED",
                        "documents": {
                          "SELFIE": {
                            "documentUrl": "https://storage.example/upload/selfie-url",
                            "documentReference": "UUID_SELFIE_DOC",
                            "expiryInSeconds": "600"
                          },
                          "ADDITIONAL_SELFIE": {
                            "documentUrl": "https://storage.example/upload/additional-selfie-url",
                            "documentReference": "UUID_ADDITIONAL_SELFIE_DOC",
                            "expiryInSeconds": "600"
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
            "description": "Bad request (missing required headers or invalid submission type)",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ErrorResponse"
                },
                "examples": {
                  "MissingRequiredHeader": {
                    "value": {
                      "success": false,
                      "errors": [
                        {
                          "code": "1539",
                          "cause": "COE_PARTNER_CAN_NOT_BE_EMPTY"
                        }
                      ]
                    }
                  },
                  "InvalidSubmissionType": {
                    "value": {
                      "success": false,
                      "errors": [
                        {
                          "code": "1542",
                          "cause": "INVALID_SUBMISSION_TYPE"
                        }
                      ]
                    }
                  }
                }
              }
            }
          },
          "429": {
            "description": "Too many requests (submission attempts exhausted)",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ErrorResponse"
                },
                "examples": {
                  "AttemptsExhausted": {
                    "value": {
                      "success": false,
                      "errors": [
                        {
                          "code": "429",
                          "cause": "SUBMISSION_QUOTA_EXCEEDED"
                        }
                      ]
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ErrorResponse"
                },
                "examples": {
                  "InternalError": {
                    "value": {
                      "success": false,
                      "errors": [
                        {
                          "code": "900",
                          "cause": "SOMETHING_WENT_WRONG"
                        }
                      ]
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
  },
  "components": {
    "schemas": {
      "GetPresignedUrlsResponseData": {
        "type": "object",
        "properties": {
          "submissionId": {
            "type": "string",
            "description": "Unique identifier for submission."
          },
          "status": {
            "type": "string",
            "description": "Current submission status.",
            "enum": [
              "INITIATED",
              "IN_PROGRESS",
              "PARTIALLY_COMPLETED",
              "COMPLETED",
              "ERROR"
            ]
          },
          "documents": {
            "type": "object",
            "description": "Map of document type to upload details.",
            "additionalProperties": {
              "$ref": "#/components/schemas/DocumentDetails"
            }
          },
          "uiMessages": {
            "type": "object",
            "description": "Optional UI messages keyed by message identifier.",
            "additionalProperties": {
              "$ref": "#/components/schemas/ReasonUIMessageDetails"
            }
          }
        },
        "additionalProperties": true
      },
      "DocumentDetails": {
        "type": "object",
        "properties": {
          "documentUrl": {
            "type": "string"
          },
          "documentReference": {
            "type": "string"
          },
          "expiryInSeconds": {
            "type": "string"
          }
        },
        "additionalProperties": true
      },
      "ReasonUIMessageDetails": {
        "type": "object",
        "properties": {
          "title": {
            "type": "string"
          },
          "message": {
            "type": "string"
          }
        },
        "additionalProperties": true
      },
      "GetPresignedUrlsSuccessResponse": {
        "type": "object",
        "required": [
          "success",
          "data"
        ],
        "properties": {
          "success": {
            "type": "boolean",
            "enum": [
              true
            ]
          },
          "data": {
            "$ref": "#/components/schemas/GetPresignedUrlsResponseData"
          }
        }
      },
      "ErrorItem": {
        "type": "object",
        "required": [
          "code",
          "cause"
        ],
        "properties": {
          "code": {
            "type": "string"
          },
          "cause": {
            "type": "string"
          }
        }
      },
      "ErrorResponse": {
        "type": "object",
        "required": [
          "success",
          "errors"
        ],
        "properties": {
          "success": {
            "type": "boolean",
            "enum": [
              false
            ]
          },
          "errors": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/ErrorItem"
            }
          }
        }
      }
    }
  }
}
```