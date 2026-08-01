---
updatedAt: 2025-11-11T00:29:18.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Register Card

Register Card for Card Payment Method

Register Card can be triggered to register the card information of the customer for future one click and two click transactions.

<br />

***

## Register Card Status Method

| HTTP Method | Endpoint                   | Definition                                                                                 |
| ----------- | -------------------------- | ------------------------------------------------------------------------------------------ |
| GET         | BASE\_URL/v2/card/register | Register card information (card number and expiry) to be used for two clicks and one click |

<br />

***

## Register Card Request

See sample on the right -- try it yourself!

| Query Parameter  | Description                                                                                                                              | Type   | Required |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- |
| card\_number     | The 16 digits card number.                                                                                                               | String | Required |
| card\_exp\_month | The card expiry month in MM format.                                                                                                      | String | Required |
| card\_exp\_year  | The card expiry year in YYYY format.                                                                                                     | String | Required |
| client\_key      | Partner client key credential. For more details, refer [Retrieving API Access Keys](/docs/midtrans-account#retrieving-api-access-keys) . | String | Required |
| callback         | Function name used for JSONP callback                                                                                                    | String | Optional |

<br />

***

## Register Card Response

```json Sample Response - Success
{
  "status_code": "200",
  "saved_token_id": "436502PjvfpHomPBggDvfipaIYhV0009",
  "transaction_id": "50e7c4ac-772e-43fa-94fb-52559bce4fc0",
  "masked_card": "48111111-1114"
}
```

| JSON Attribute   | Description                                                      | Type   |
| ---------------- | ---------------------------------------------------------------- | ------ |
| transaction\_id  | Transaction ID given by Midtrans.                                | String |
| masked\_card     | First 8-digit and last 4-digit of customer's credit card number. | String |
| status\_code     | Status code of transaction charge result.                        | String |
| saved\_token\_id | Token id used for Two Clicks or One Click.                       | String |

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "info": {
    "title": "coreapi",
    "version": "1.0"
  },
  "servers": [
    {
      "url": "https://api.sandbox.midtrans.com"
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
    "/v2/card/register": {
      "get": {
        "summary": "Register Card",
        "description": "Register Card for Card Payment Method",
        "operationId": "register-card",
        "parameters": [
          {
            "name": "card_number",
            "in": "query",
            "schema": {
              "type": "string",
              "default": "4811111111111114"
            }
          },
          {
            "name": "card_exp_month",
            "in": "query",
            "schema": {
              "type": "string",
              "default": "02"
            }
          },
          {
            "name": "card_exp_year",
            "in": "query",
            "schema": {
              "type": "string",
              "default": "2025"
            }
          },
          {
            "name": "client_key",
            "in": "query",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "callback",
            "in": "query",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "200",
            "content": {
              "application/json": {
                "examples": {
                  "Result": {
                    "value": "{\n  \"status_code\": \"200\",\n  \"saved_token_id\": \"436502PjvfpHomPBggDvfipaIYhV0009\",\n  \"transaction_id\": \"50e7c4ac-772e-43fa-94fb-52559bce4fc0\",\n  \"masked_card\": \"48111111-1114\"\n}"
                  }
                },
                "schema": {
                  "type": "object",
                  "properties": {
                    "status_code": {
                      "type": "string",
                      "example": "200"
                    },
                    "saved_token_id": {
                      "type": "string",
                      "example": "436502PjvfpHomPBggDvfipaIYhV0009"
                    },
                    "transaction_id": {
                      "type": "string",
                      "example": "50e7c4ac-772e-43fa-94fb-52559bce4fc0"
                    },
                    "masked_card": {
                      "type": "string",
                      "example": "48111111-1114"
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
                    "value": "{\n    \"status_code\": \"401\",\n    \"status_message\": \"Transaction cannot be authorized with the current client/server key.\",\n    \"id\": \"ea5c461f-338a-4530-ad00-f0fb6bff1749\"\n}"
                  }
                },
                "schema": {
                  "type": "object",
                  "properties": {
                    "status_code": {
                      "type": "string",
                      "example": "401"
                    },
                    "status_message": {
                      "type": "string",
                      "example": "Transaction cannot be authorized with the current client/server key."
                    },
                    "id": {
                      "type": "string",
                      "example": "ea5c461f-338a-4530-ad00-f0fb6bff1749"
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