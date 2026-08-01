---
updatedAt: 2026-04-30T10:39:56.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Generate Partner Token

Retrieves a GTF partner-scoped JWT authentication token for use in subsequent API calls. Token validity is typically 1 hour. Partners are encouraged to cache tokens within their validity period to minimize authentication requests. For production environments, NAT whitelisting is mandatory.

# OpenAPI definition

```json
{
  "openapi": "3.0.0",
  "info": {
    "title": "Get Partner Token API",
    "description": "API for obtaining an IAB partner token used to create, confirm, and retrieve details of submissions.",
    "version": "1.1.0"
  },
  "servers": [
    {
      "url": "https://onekyc-token-sandbox.gopayapi.com",
      "description": "Sandbox Server"
    }
  ],
  "paths": {
    "/v1/coe/partner/authentication": {
      "get": {
        "summary": "Generate Partner Token",
        "description": "Retrieves a GTF partner-scoped JWT authentication token for use in subsequent API calls. Token validity is typically 1 hour. Partners are encouraged to cache tokens within their validity period to minimize authentication requests. For production environments, NAT whitelisting is mandatory.",
        "parameters": [
          {
            "name": "client-id",
            "in": "header",
            "required": true,
            "schema": {
              "type": "string",
              "default": "YOUR_CLIENT_ID"
            }
          },
          {
            "name": "pass-key",
            "in": "header",
            "required": true,
            "schema": {
              "type": "string",
              "default": "YOUR_PASS_KEY"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Successful token generation",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "success": {
                      "type": "boolean"
                    },
                    "data": {
                      "type": "object",
                      "properties": {
                        "token": {
                          "type": "string",
                          "description": "IAB partner token generated for the session"
                        },
                        "expiry_seconds": {
                          "type": "string",
                          "description": "Time period in seconds for which the generated token will be valid"
                        },
                        "expires_at": {
                          "type": "string",
                          "description": "End time value in epoch timestamp"
                        }
                      }
                    }
                  }
                },
                "example": {
                  "success": true,
                  "data": {
                    "token": "eyJraW...",
                    "expiry_seconds": "3600",
                    "expires_at": "1738384686"
                  }
                }
              }
            }
          },
          "400": {
            "description": "Bad Request - Missing or improperly formatted headers",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "success": {
                      "type": "boolean"
                    },
                    "data": {
                      "nullable": true
                    },
                    "errors": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "code": {
                            "type": "string"
                          },
                          "entity": {
                            "type": "string"
                          },
                          "cause": {
                            "type": "string"
                          }
                        }
                      }
                    }
                  }
                },
                "example": {
                  "success": false,
                  "data": null,
                  "errors": [
                    {
                      "code": "1539",
                      "entity": "ONEKYC_TOKEN_SERVICE",
                      "cause": "CLIENT_ID_CAN_NOT_BE_EMPTY"
                    }
                  ]
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized - Invalid client-id or pass-key",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "success": {
                      "type": "boolean"
                    },
                    "data": {
                      "nullable": true
                    },
                    "errors": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "code": {
                            "type": "string"
                          },
                          "entity": {
                            "type": "string"
                          },
                          "cause": {
                            "type": "string"
                          }
                        }
                      }
                    }
                  }
                },
                "example": {
                  "success": false,
                  "data": null,
                  "errors": [
                    {
                      "code": "110",
                      "entity": "ONEKYC_TOKEN_SERVICE",
                      "cause": "UNAUTHORIZED"
                    }
                  ]
                }
              }
            }
          },
          "500": {
            "description": "Internal Server Error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "success": {
                      "type": "boolean"
                    },
                    "errors": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "code": {
                            "type": "string"
                          },
                          "cause": {
                            "type": "string"
                          }
                        }
                      }
                    }
                  }
                },
                "example": {
                  "success": false,
                  "errors": [
                    {
                      "code": "900",
                      "cause": "Unknown error processing the request"
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
```