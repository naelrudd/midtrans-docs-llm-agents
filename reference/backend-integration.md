---
updatedAt: 2026-05-18T12:03:07.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Backend Integration

Backend integration goal is to acquire `SNAP_TOKEN` by providing payment information. We provide a HTTP API to do this.

Snap validates HTTP requests by using the Basic Authentication method. The username is your `SERVER_KEY` while the password is empty. You can see your `SERVER_KEY` on [Settings - Access Keys](https://dashboard.sandbox.midtrans.com/settings/config_info). The `Authorization` header value must be `AUTH_STRING`, where `AUTH_STRING` is the base64-encoded string of your username and password. `AUTH_STRING` = Base64(`SERVER_KEY` + `:`)

<br />

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "info": {
    "title": "snap-api",
    "version": "1.0"
  },
  "servers": [
    {
      "url": "https://app.sandbox.midtrans.com"
    }
  ],
  "components": {
    "securitySchemes": {
      "sec0": {
        "type": "http",
        "scheme": "basic"
      }
    }
  },
  "security": [
    {
      "sec0": []
    }
  ],
  "paths": {
    "/snap/v1/transactions": {
      "post": {
        "summary": "Backend Integration",
        "description": "",
        "operationId": "backend-integration",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "required": [
                  "transaction_details"
                ],
                "properties": {
                  "transaction_details": {
                    "type": "object",
                    "description": "Specific information regarding the transaction",
                    "required": [
                      "order_id"
                    ],
                    "properties": {
                      "order_id": {
                        "type": "string",
                        "description": "Unique transaction ID. A single ID could be used only once by a Merchant. Allowed Symbols are dash(-), underscore(_), tilde (~), and dot (.)",
                        "default": "order-id"
                      },
                      "gross_amount": {
                        "type": "integer",
                        "description": "Amount to be charged",
                        "default": 10000,
                        "format": "int32"
                      }
                    }
                  },
                  "credit_card": {
                    "type": "object",
                    "properties": {
                      "secure": {
                        "type": "boolean",
                        "default": true
                      }
                    }
                  }
                }
              }
            }
          }
        },
        "responses": {
          "201": {
            "description": "201",
            "content": {
              "application/json": {
                "examples": {
                  "Result": {
                    "value": "{\n  \"token\": \"{{snap_token}}\",\n  \"redirect_url\": \"https://app.sandbox.midtrans.com/snap/v3/redirection/{{snap_token}}\"\n}"
                  }
                },
                "schema": {
                  "type": "object",
                  "properties": {
                    "token": {
                      "type": "string",
                      "example": "{{snap_token}}"
                    },
                    "redirect_url": {
                      "type": "string",
                      "example": "https://app.sandbox.midtrans.com/snap/v3/redirection/{{snap_token}}"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "400",
            "content": {
              "application/json": {
                "examples": {
                  "Result": {
                    "value": "{\n  \"error_messages\": [\n    \"transaction_details.order_id is required\"\n  ]\n}"
                  }
                },
                "schema": {
                  "type": "object",
                  "properties": {
                    "error_messages": {
                      "type": "array",
                      "items": {
                        "type": "string",
                        "example": "transaction_details.order_id is required"
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "401",
            "content": {
              "application/json": {
                "examples": {
                  "Result": {
                    "value": "{\n  \"error_messages\": [\n    \"Access denied due to unauthorized transaction, please check client or server key\",\n    \"Visit https://snap-docs.midtrans.com/#request-headers for more details\"\n  ]\n}"
                  }
                },
                "schema": {
                  "type": "object",
                  "properties": {
                    "error_messages": {
                      "type": "array",
                      "items": {
                        "type": "string",
                        "example": "Access denied due to unauthorized transaction, please check client or server key"
                      }
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "500",
            "content": {
              "application/json": {
                "examples": {
                  "Result": {
                    "value": "{\n    \"error_messages\": [\n        \"Sorry, we encountered internal server error. We will fix this soon.\"\n    ],\n    \"locale\": \"en\"\n}"
                  }
                },
                "schema": {
                  "type": "object",
                  "properties": {
                    "error_messages": {
                      "type": "array",
                      "items": {
                        "type": "string",
                        "example": "Sorry, we encountered internal server error. We will fix this soon."
                      }
                    },
                    "locale": {
                      "type": "string",
                      "example": "en"
                    }
                  }
                }
              }
            }
          }
        },
        "deprecated": false
      }
    }
  },
  "x-readme": {
    "headers": [],
    "explorer-enabled": true,
    "proxy-enabled": true
  },
  "x-readme-fauxas": true
}
```