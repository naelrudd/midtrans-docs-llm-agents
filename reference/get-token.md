---
updatedAt: 2025-11-10T22:59:35.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Get Token

Token ID is a unique value that is associated with the customer’s credit card information during a transaction. The GET Token method sends the credit card information via [Midtrans.min.js](https://api.midtrans.com/v2/assets/js/midtrans-new-3ds.min.js) to Midtrans server and returns the Token ID to you.

To utilize Midtrans JavaScript library, add the code given below in your payment page inside the `<head>` tag.

<br />

```javascript Import Midtrans JavaScript Library
<script id= "midtrans-script" src="https://api.midtrans.com/v2/assets/js/midtrans-new-3ds.min.js" data-environment="<production|sandbox>" data-client-key="<INSERT CLIENT KEY HERE>" type="text/javascript"></script>
```

> 📘 Note
>
> The GET Token method and its features are applicable only for card transactions. Read more [here](/reference/payment-card) for API references on various card features to be used in conjuction with this guide.

<br />

***

## Midtrans JavaScript Library

Midtrans JavaScript library consists of two functions as given below.

1. Get Card Token: Securely sends the customer’s payment card details to Midtrans server, without the merchant handling the credit card details.
2. Redirect: Redirects the customer to 3DS authentication page.

> ❗️
>
> Secure token only support 3DS 1.0, need to implement 3DS 2.0 refer Card Feature: 3D Secure (3DS)
>
> 3D Secure 2.0 is an authentication protocol that aims to reduce fraud and enhance security in online card payments.

| Attribute        | Description                                                                                                               |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------- |
| data-environment | The environment which the request is pointing to. Possible values are `production` and `sandbox`.                         |
| data-client-key  | Your Client key. For more details, refer [Retrieving API Access Keys](/docs/midtrans-account#retrieving-api-access-keys). |

> ❗️ 8 Digit Bin
>
> With the oncoming mandates from Visa and other principals, Midtrans will start supporting 8-digit BIN's for card transaction processing flows.\
> The 8-digit bin changes on CoreAPI and will impact the length of token\_id and format of saved\_token\_id.

Changes list:

1. Change on token\_id length from `6 first digit + "-" + 4 last digit + "-" + 36 random digit` into 8 `first digit + "-" + 4 last digit + "-" + 36 random digit` (e.g: `481111-1114-7baba36c-5698-47cf-9170-80efd6a2e973` to `48111111-1114-7baba36c-5698-47cf-9170-80efd6a2e973`)
2. Change on saved\_token\_id length from `6 first digit + 22 random digit + 4 last digit` into `8 first digit + 20 random digit + 4 last digit` (e.g: `481111sHdcfSakAvHvFQFEjTivUV1114` to `48111111sHfSakAvHvFQFEjTivUV1114`)
3. Masked\_card on response, event, log changed from `6 first digit + 4 last digit from card number` into `8 first digit + 4 last digit` from a card number
4. Support 8 Digit bin in Midtrans Fraud Detection System (for Aegis's users)
5. Support 8 digit bin in [Bin API](https://docs.midtrans.com/reference/bin-api)

<br />

***

## Getting Card Token

### GET Card Token Request

The `card` object attributes are given below. Depending on the token type, some parameters are conditional.

```javascript Get Card Token function
// Create the card object with the required fields
var card = {
  card_number: "4811111111111114",
  card_cvv: "123",
  card_exp_month: "12",
  card_exp_year: "2025",
  bank_one_time_token: "12345678"
}

var options = {
  onSuccess: function(response) {
      // Implement success handling here
  },
  onFailure: function(response) {
      // Implement error handling here
  }
}

MidtransNew3ds.getCardToken(card, options);
```

| JSON Attribute         | Description                                                                                                                     | Normal      | Two Clicks  | Remarks                                                                                               |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ----------- | ----------- | ----------------------------------------------------------------------------------------------------- |
| card\_number           | The 16 digits Credit Card number.                                                                                               | Required    | Conditional | Space(` `) is allowed. <br />For example, `4111 1111 1111 1111` or `4111111111111111` both are valid. |
| card\_cvv              | The CVV number printed on the card.                                                                                             | Required    | Required    | For example, `123`.                                                                                   |
| card\_exp\_month       | The card expiry month in MM format.                                                                                             | Required    | Conditional | For example, `12`.                                                                                    |
| card\_exp\_year        | The card expiry year in YYYY format.                                                                                            | Required    | Conditional | For example, `2022`.                                                                                  |
| token\_id              | The token ID of credit card saved previously. Its value is same as the `saved_token_id` retrieved from initial Charge response. | Conditional | Required    | For example, `48111111sHfSakAvHvFQFEjTivUV1114`.                                                      |
| bank\_one\_time\_token | The one-time token is shown on the customer's phone mobile banking                                                              | Conditional | -           | For example, `12345678`                                                                               |

> 📘 Note
>
> bank\_one\_time\_token is only required for KKI (Kartu Kredit Indonesia) transactions, where merchants must send CPAN as card number and OTT as bank\_one\_time\_token to get the Midtrans one-time token.

<br />

### GET Card Token Response

Callback response object attributes are listed below.

| JSON Attribute       | Description                                                                                                                            | Remarks                                                                                                                             |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| status\_code         | Status code of transaction charge result.                                                                                              | "200" for success, "400" when validation error.                                                                                     |
| status\_message      | Status message describing the result of the API request.                                                                               | "OK, success request new token".                                                                                                    |
| validation\_messages | The message describing the error.                                                                                                      | “card\_exp\_year must be greater than this year”, "card\_exp\_month must be greater than this year's month”.                        |
| token\_id            | The token id of the card.                                                                                                              | "48111111-1114-d3d690db-3e18-4edd-9fee-4d061e4eb6f3"<br /> **Note**: `token_id` is required during Card Payment Charge Transaction. |
| hash                 | Produced from one-way hashing of the given card number. This value is irreversible and will always be consistent for each card number. | "6d9df2ff-ae9c-3cee-a5ff-a063dc476077"                                                                                              |

Available options are given below.

| Name      | Description                                                                  |
| --------- | ---------------------------------------------------------------------------- |
| onSuccess | This function is called only when get token responds with status code `200`. |
| onFailure | This function is called for all the other status codes except `200`.         |

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
    "/v2/token": {
      "get": {
        "summary": "Get Token",
        "description": "",
        "operationId": "get-token",
        "parameters": [
          {
            "name": "client_key",
            "in": "query",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "card_number",
            "in": "query",
            "required": true,
            "schema": {
              "type": "string",
              "default": "4811111111111114"
            }
          },
          {
            "name": "card_cvv",
            "in": "query",
            "required": true,
            "schema": {
              "type": "string",
              "default": "123"
            }
          },
          {
            "name": "card_exp_month",
            "in": "query",
            "required": true,
            "schema": {
              "type": "string",
              "default": "12"
            }
          },
          {
            "name": "card_exp_year",
            "in": "query",
            "required": true,
            "schema": {
              "type": "string",
              "default": "2025"
            }
          },
          {
            "name": "token_id",
            "in": "query",
            "schema": {
              "type": "string",
              "default": "12345678"
            }
          },
          {
            "name": "bank_one_time_token",
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
                  "Success Response": {
                    "value": "{\n  \"status_code\": \"200\",\n  \"status_message\": \"Credit card token is created as Token ID.\",\n  \"token_id\": \"48111111-1114-80d5df78-be87-41e0-b4e2-1a0f4e2ea6ae\",\n  \"hash\": \"48111111-1114-mami\"\n}"
                  },
                  "Error Validation": {
                    "value": "{\n  \"status_code\": \"400\",\n  \"status_message\": \"One or more parameters in the payload is invalid.\",\n  \"validation_messages\": [\n    \"card_number does not match with luhn algorithm\"\n  ],\n  \"id\": \"4145737f-deb2-408a-86c1-725f29304d74\"\n}"
                  }
                },
                "schema": {
                  "oneOf": [
                    {
                      "title": "Success Response",
                      "type": "object",
                      "properties": {
                        "status_code": {
                          "type": "string",
                          "example": "200"
                        },
                        "status_message": {
                          "type": "string",
                          "example": "Credit card token is created as Token ID."
                        },
                        "token_id": {
                          "type": "string",
                          "example": "48111111-1114-80d5df78-be87-41e0-b4e2-1a0f4e2ea6ae"
                        },
                        "hash": {
                          "type": "string",
                          "example": "48111111-1114-mami"
                        }
                      }
                    },
                    {
                      "title": "Error Validation",
                      "type": "object",
                      "properties": {
                        "status_code": {
                          "type": "string",
                          "example": "400"
                        },
                        "status_message": {
                          "type": "string",
                          "example": "One or more parameters in the payload is invalid."
                        },
                        "validation_messages": {
                          "type": "array",
                          "items": {
                            "type": "string",
                            "example": "card_number does not match with luhn algorithm"
                          }
                        },
                        "id": {
                          "type": "string",
                          "example": "4145737f-deb2-408a-86c1-725f29304d74"
                        }
                      }
                    }
                  ]
                }
              }
            }
          }
        },
        "deprecated": false,
        "security": []
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