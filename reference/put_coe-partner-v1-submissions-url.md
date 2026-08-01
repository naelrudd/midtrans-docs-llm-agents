---
updatedAt: 2026-04-29T16:28:12.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Confirm upload for submission

# OpenAPI definition

```json
{
  "openapi": "3.0.3",
  "info": {
    "title": "Confirm Upload API",
    "description": "Confirms upload for a submission and triggers server-side processing.",
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
      "put": {
        "summary": "Confirm upload for submission",
        "operationId": "confirmUploadForSubmission",
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
          }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/ConfirmUploadRequest"
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Upload confirmation accepted successfully",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ConfirmUploadSuccessResponse"
                },
                "examples": {
                  "Success": {
                    "value": {
                      "success": true,
                      "data": {
                        "submissionId": "SUBMISSION_123",
                        "uiMessages": {
                          "message_1": {
                            "title": "Processing",
                            "message": "Your submission is being processed"
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
            "description": "Bad request (missing required headers or request validation error)",
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
                          "cause": "X_SDK_SESSION_ID_CAN_NOT_BE_EMPTY"
                        }
                      ]
                    }
                  },
                  "InvalidRequestBody": {
                    "value": {
                      "success": false,
                      "errors": [
                        {
                          "code": "1542",
                          "cause": "INVALID_CONFIRM_UPLOAD_REQUEST"
                        }
                      ]
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ErrorResponse"
                },
                "examples": {
                  "Unauthorized": {
                    "value": {
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
              }
            }
          },
          "403": {
            "description": "Forbidden",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ErrorResponse"
                },
                "examples": {
                  "Forbidden": {
                    "value": {
                      "success": false,
                      "errors": [
                        {
                          "code": "110",
                          "cause": "FORBIDDEN"
                        }
                      ]
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Submission or related entity not found",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ErrorResponse"
                },
                "examples": {
                  "NotFound": {
                    "value": {
                      "success": false,
                      "errors": [
                        {
                          "code": "404",
                          "cause": "SUBMISSION_DOES_NOT_EXIST"
                        }
                      ]
                    }
                  }
                }
              }
            }
          },
          "409": {
            "description": "Conflict (invalid state transition or duplicate confirmation)",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ErrorResponse"
                },
                "examples": {
                  "Conflict": {
                    "value": {
                      "success": false,
                      "errors": [
                        {
                          "code": "409",
                          "cause": "SUBMISSION_STATE_CONFLICT"
                        }
                      ]
                    }
                  }
                }
              }
            }
          },
          "422": {
            "description": "Unprocessable entity (semantic validation failure)",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ErrorResponse"
                },
                "examples": {
                  "UnprocessableEntity": {
                    "value": {
                      "success": false,
                      "errors": [
                        {
                          "code": "422",
                          "cause": "INVALID_UPLOAD_ARTIFACT"
                        }
                      ]
                    }
                  }
                }
              }
            }
          },
          "429": {
            "description": "Too many requests",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ErrorResponse"
                },
                "examples": {
                  "RateLimit": {
                    "value": {
                      "success": false,
                      "errors": [
                        {
                          "code": "429",
                          "cause": "TOO_MANY_REQUESTS"
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
                          "cause": "GENERIC_SERVICE_ERROR"
                        }
                      ]
                    }
                  }
                }
              }
            }
          },
          "503": {
            "description": "Service unavailable",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ErrorResponse"
                },
                "examples": {
                  "ServiceUnavailable": {
                    "value": {
                      "success": false,
                      "errors": [
                        {
                          "code": "903",
                          "cause": "SERVICE_UNAVAILABLE"
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
      "ConfirmUploadRequest": {
        "type": "object",
        "required": [
          "submissionId"
        ],
        "properties": {
          "submissionId": {
            "type": "string",
            "description": "Unique identifier for the submission"
          },
          "metadata": {
            "type": "object",
            "description": "Additional metadata for the submission (JSON object)",
            "additionalProperties": true
          }
        }
      },
      "ConfirmUploadResponseData": {
        "type": "object",
        "properties": {
          "submissionId": {
            "type": "string",
            "description": "Unique identifier for the submission"
          },
          "uiMessages": {
            "type": "object",
            "description": "UI messages to display to the user, keyed by message identifier",
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
      "ConfirmUploadSuccessResponse": {
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
            "$ref": "#/components/schemas/ConfirmUploadResponseData"
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