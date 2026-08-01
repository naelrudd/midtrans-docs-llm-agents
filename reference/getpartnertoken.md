---
updatedAt: 2026-05-07T18:28:08.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Get Partner Token

Fetch the partner token needed to call any IAB Backend APIs.
The token is generated based on the Client ID and Pass Key provided during onboarding and will be valid for a limited time period.

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
    "/v1/esign/partner/authentication": {
      "servers": [
        {
          "url": "https://onekyc-token.sandbox.gopayapi.com",
          "description": "Sandbox - OneKYC Token Gateway"
        },
        {
          "url": "https://onekyc-token.ky.id.gopayapi.com",
          "description": "Production - OneKYC Token Gateway"
        }
      ],
      "get": {
        "summary": "Get Partner Token",
        "description": "Fetch the partner token needed to call any IAB Backend APIs.\nThe token is generated based on the Client ID and Pass Key provided during onboarding and will be valid for a limited time period.",
        "operationId": "getPartnerToken",
        "parameters": [
          {
            "$ref": "#/components/parameters/ClientId"
          },
          {
            "$ref": "#/components/parameters/PassKey"
          }
        ],
        "responses": {
          "200": {
            "description": "Successful token generation",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/PartnerTokenSuccessResponse"
                }
              }
            }
          },
          "400": {
            "description": "Missing request headers",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ErrorResponse"
                },
                "example": {
                  "success": false,
                  "errors": [
                    {
                      "code": "1650",
                      "cause": "MISSING_CLIENT_ID"
                    },
                    {
                      "code": "1650",
                      "cause": "MISSING_PASS_KEY"
                    }
                  ]
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized - Invalid credentials",
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
          "500": {
            "$ref": "#/components/responses/InternalServerError"
          }
        }
      }
    }
  },
  "components": {
    "parameters": {
      "ClientId": {
        "name": "client-id",
        "in": "header",
        "required": true,
        "description": "Client ID provided by GTF",
        "schema": {
          "type": "string",
          "format": "uuid"
        },
        "example": "b31fa508-331c-4e9e-9a60-b0f28c3f7e13"
      },
      "PassKey": {
        "name": "pass-key",
        "in": "header",
        "required": true,
        "description": "PassKey provided by GTF",
        "schema": {
          "type": "string",
          "format": "uuid"
        },
        "example": "2c7b2893-e49f-4cf3-89e6-1b9c5bf0500b"
      }
    },
    "schemas": {
      "PartnerTokenSuccessResponse": {
        "type": "object",
        "properties": {
          "success": {
            "type": "boolean",
            "example": true
          },
          "data": {
            "$ref": "#/components/schemas/PartnerTokenData"
          }
        },
        "example": {
          "success": true,
          "data": {
            "token": "eyJraWQiOiJlY8sLk182F3J4wNDkwLTQxODgtYTRjZ.....",
            "expiry_seconds": "1800",
            "expires_at": "1783336059"
          }
        }
      },
      "PartnerTokenData": {
        "type": "object",
        "properties": {
          "token": {
            "type": "string",
            "description": "IAB partner token generated for the session"
          },
          "expiry_seconds": {
            "type": "string",
            "description": "Time period in seconds for which the generated token will be valid (default 1800 = 30 minutes)"
          },
          "expires_at": {
            "type": "string",
            "description": "Timestamp indicating when the token will expire (in seconds since epoch)"
          }
        }
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