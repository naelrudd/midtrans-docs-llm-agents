---
updatedAt: 2026-04-29T16:52:30.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Get Partner Token

Fetch the partner token needed to call IAB Backend APIs.
The partner token will be valid for 1 hour. After expiry, partners can create a new token.


# OpenAPI definition

```json
{
  "openapi": "3.0.3",
  "info": {
    "title": "eSign API - Authentication",
    "description": "Partner authentication API for getting partner tokens.",
    "version": "1.0.0",
    "contact": {
      "name": "GTF Team"
    }
  },
  "servers": [
    {
      "url": "https://onekyc-token.staging.gopayapi.com",
      "description": "Token Gateway - Staging"
    }
  ],
  "tags": [
    {
      "name": "Authentication",
      "description": "Partner authentication APIs"
    }
  ],
  "paths": {
    "/v1/esign/partner/authentication": {
      "get": {
        "tags": [
          "Authentication"
        ],
        "summary": "Get Partner Token",
        "description": "Fetch the partner token needed to call IAB Backend APIs.\nThe partner token will be valid for 1 hour. After expiry, partners can create a new token.\n",
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
            "description": "Successfully retrieved partner token",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/PartnerTokenResponse"
                }
              }
            }
          },
          "400": {
            "description": "Request headers missing",
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
                      "cause": "MISSING_CLIENT_ID"
                    },
                    {
                      "code": "1539",
                      "cause": "MISSING_PASS_KEY"
                    }
                  ]
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
          "type": "string"
        },
        "example": "01-a234b5cdefghi4b67abf485c3126b92c9-22"
      },
      "PassKey": {
        "name": "pass-key",
        "in": "header",
        "required": true,
        "description": "PassKey provided by GTF",
        "schema": {
          "type": "string"
        },
        "example": "2c7b2893-e49f-4cf3-89e6-1b9c5bf0500b"
      }
    },
    "schemas": {
      "PartnerTokenResponse": {
        "type": "object",
        "properties": {
          "success": {
            "type": "boolean",
            "example": true
          },
          "data": {
            "type": "object",
            "properties": {
              "token": {
                "type": "string",
                "description": "JWT token for authentication"
              },
              "expiry_seconds": {
                "type": "string",
                "description": "Token validity period in seconds",
                "example": "1800"
              }
            }
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
          "data": {
            "type": "object",
            "nullable": true
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
            "description": "Error code"
          },
          "cause": {
            "type": "string",
            "description": "Detailed message of the error"
          },
          "entity": {
            "type": "string",
            "description": "Entity that caused the error"
          }
        }
      }
    }
  }
}
```