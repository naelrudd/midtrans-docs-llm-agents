---
updatedAt: 2026-04-29T07:46:06.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Get submission status

# OpenAPI definition

```json
{
  "openapi": "3.0.3",
  "info": {
    "title": "Get Submission Status API",
    "description": "Retrieves the current status and details of a submission.",
    "version": "1.0.0"
  },
  "servers": [
    {
      "url": "https://onekyc.ky.id.sandbox.gopayapi.com",
      "description": "Sandbox Server"
    }
  ],
  "paths": {
    "/coe/v1/submissions/{submissionId}/status": {
      "get": {
        "summary": "Get submission status",
        "operationId": "getSubmissionStatus",
        "parameters": [
          {
            "name": "submissionId",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "Unique identifier of the submission.",
            "example": "SUBMISSION_123"
          },
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
          }
        ],
        "responses": {
          "200": {
            "description": "Submission status retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/GetSubmissionStatusSuccessResponse"
                },
                "examples": {
                  "Completed": {
                    "value": {
                      "success": true,
                      "data": {
                        "submissionId": "SUBMISSION_123",
                        "status": "COMPLETED",
                        "submissionType": "FACE_VERIFICATION",
                        "createdAt": "2026-04-29T10:00:00Z",
                        "completedAt": "2026-04-29T10:15:30Z",
                        "verificationResult": {
                          "isApproved": true,
                          "riskLevel": "LOW",
                          "confidence": "95"
                        },
                        "documents": {
                          "SELFIE": {
                            "status": "VERIFIED",
                            "documentReference": "UUID_SELFIE_DOC"
                          }
                        }
                      }
                    }
                  },
                  "InProgress": {
                    "value": {
                      "success": true,
                      "data": {
                        "submissionId": "SUBMISSION_124",
                        "status": "IN_PROGRESS",
                        "submissionType": "KTP_SCAN",
                        "createdAt": "2026-04-29T10:00:00Z",
                        "completedAt": null,
                        "verificationResult": null,
                        "documents": {
                          "KTP_FRONT": {
                            "status": "UPLOADED",
                            "documentReference": "UUID_KTP_FRONT_DOC"
                          },
                          "KTP_BACK": {
                            "status": "PENDING",
                            "documentReference": null
                          }
                        }
                      }
                    }
                  },
                  "Error": {
                    "value": {
                      "success": true,
                      "data": {
                        "submissionId": "SUBMISSION_125",
                        "status": "ERROR",
                        "submissionType": "FACE_VERIFICATION",
                        "createdAt": "2026-04-29T10:00:00Z",
                        "completedAt": "2026-04-29T10:05:00Z",
                        "errorMessage": "Face detection failed",
                        "verificationResult": null,
                        "documents": {
                          "SELFIE": {
                            "status": "INVALID",
                            "documentReference": "UUID_SELFIE_DOC"
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
            "description": "Bad request (missing required headers or invalid submission ID)",
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
                  "InvalidSubmissionId": {
                    "value": {
                      "success": false,
                      "errors": [
                        {
                          "code": "1541",
                          "cause": "INVALID_SUBMISSION_ID"
                        }
                      ]
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Submission not found",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ErrorResponse"
                },
                "examples": {
                  "SubmissionNotFound": {
                    "value": {
                      "success": false,
                      "errors": [
                        {
                          "code": "1543",
                          "cause": "SUBMISSION_DOES_NOT_EXIST"
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
      "DocumentStatus": {
        "type": "object",
        "properties": {
          "status": {
            "type": "string",
            "description": "Status of the individual document.",
            "enum": [
              "PENDING",
              "UPLOADED",
              "VERIFIED",
              "INVALID",
              "REJECTED"
            ]
          },
          "documentReference": {
            "type": "string",
            "description": "Unique reference identifier for the document.",
            "nullable": true
          }
        },
        "additionalProperties": true
      },
      "VerificationResult": {
        "type": "object",
        "properties": {
          "isApproved": {
            "type": "boolean",
            "description": "Whether the verification was approved."
          },
          "riskLevel": {
            "type": "string",
            "description": "Risk level of the verification.",
            "enum": [
              "LOW",
              "MEDIUM",
              "HIGH"
            ]
          },
          "confidence": {
            "type": "string",
            "description": "Confidence score of the verification result as a percentage."
          }
        },
        "additionalProperties": true
      },
      "GetSubmissionStatusResponseData": {
        "type": "object",
        "required": [
          "submissionId",
          "status",
          "submissionType",
          "createdAt"
        ],
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
          "submissionType": {
            "type": "string",
            "description": "Type of submission.",
            "enum": [
              "KTP_SCAN",
              "STANDALONE_LIVENESS",
              "FACE_MATCH",
              "FACE_VERIFICATION",
              "KYC_LITE",
              "STANDALONE_IDENTITY_VERIFICATION"
            ]
          },
          "createdAt": {
            "type": "string",
            "format": "date-time",
            "description": "Timestamp when submission was created."
          },
          "completedAt": {
            "type": "string",
            "format": "date-time",
            "description": "Timestamp when submission was completed. Null if not yet completed.",
            "nullable": true
          },
          "verificationResult": {
            "$ref": "#/components/schemas/VerificationResult",
            "description": "Verification result. Null if submission is not yet completed.",
            "nullable": true
          },
          "errorMessage": {
            "type": "string",
            "description": "Error message if submission status is ERROR. Null otherwise.",
            "nullable": true
          },
          "documents": {
            "type": "object",
            "description": "Map of document type to document status.",
            "additionalProperties": {
              "$ref": "#/components/schemas/DocumentStatus"
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
      "GetSubmissionStatusSuccessResponse": {
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
            "$ref": "#/components/schemas/GetSubmissionStatusResponseData"
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