---
updatedAt: 2025-11-10T23:00:22.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# BIN API (Card Payment)

Obtain user's card properties information based on BIN (Bank Identification Number)

BIN API is called to get metadata for a particular <Glossary>BIN</Glossary>, such as card type (Credit or Debit), the card network provider (Visa, MasterCard), and so on. BIN API is available for in both Snap and Core API integrations.

<br />

> 📘 Important Note
>
> BIN data is sourced directly from card principals (Visa, Mastercard, JCB, etc.) and issuing banks. As such, certain values (e.g., bank name, capitalization, or length) may change over time or sometimes be empty.
>
> We recommend not treating BIN values as part of a strict contract or using them for validation, since these fields are subject to unannounced changes. Instead, BIN data should be considered as informational and advisory, to help with general use cases such as UI display or analytics.

***

## BIN API Method

See sample on the right -- try it yourself!

| HTTP Method | Endpoint                       | Definition        |
| ----------- | ------------------------------ | ----------------- |
| GET         | BASE\_URL/v1/bins/`bin_number` | Get Bin Metadata. |

<br />

***

## BIN API Response

```json Sample Response - Success
{
    "data": {
        "country_name": "Indonesia",
        "country_code": "id",
        "brand": "visa",
        "bin_type": "credit",
        "bin_class": "gold",
        "bin": "45563300",
        "bank_code": "bca",
        "bank": "bank central asia"
    }
}
```

<HTMLBlock>{`
<table>
<tr><th colspan="2">JSON Attribute</th><th>Description</th><th>Type</th><th>Required</th></tr>
<tr><td colspan="2">data</td><td>Information about the card.</td><td>Object</td><td>Conditional</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;country_name</td><td>Name of the country from which the card is issued. For example, <code>Indonesia</code>. </td><td>String</td><td>Optional</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;country_code</td><td>The country code. For example, <code>id</code>.</td><td>String</td><td>Optional</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;brand</td><td>The card network provider. For example, <code>visa</code>.</td><td>String</td><td>Optional</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;bin_type</td><td>The type of BIN. For example, <code>credit</code>. </td><td>String</td><td>Required</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;bin_class</td><td>The class of BIN. For example, <code>gold</code>.</td><td>String</td><td>Optional</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;bin</td><td>Requested Bin number. For example, <code>455633</code>.</td><td>String</td><td>Required</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;bank_code</td><td>The three letter bank code. For example, <code>bca</code>.</td><td>String</td><td>Optional</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;bank</td><td>Name of the bank on the card. For example, <code>Bank Central Asia</code>.</td><td>String</td><td>Optional</td></tr>
</table>
`}</HTMLBlock>

<br />

***

## Authorization Header

The request is authorized using the same method as [HTTP(S) Request](/reference/https-request-1). Either the Midtrans Client Key or Midtrans Server key can be used.

It is highly recommended to use Midtrans Client Key if the request is made from a browser or a mobile device.

<br />

***

## Rate Limit

Bin requests are rate-limited by 100 requests per minute. If the number of attempted requests exceeds the limit, Midtrans API responds with `409` status code.

<br />

***

## Response Codes

| Code | Description                                                                   |
| ---- | ----------------------------------------------------------------------------- |
| 200  | OK.                                                                           |
| 404  | Particular Bin does not exist.                                                |
| 401  | Credential is empty or wrong. Please recheck the authorization configuration. |
| 409  | Request exceeds the rate limit.                                               |

<br />

***

## Response Object

<Table align={["left","left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        JSON Attribute
      </th>

      <th>
        Description
      </th>

      <th>
        Type
      </th>

      <th>
        Required
      </th>

      <th>

      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        bank
      </td>

      <td>
        The name of the bank on the card. For example, `Bank Central Asia`.
      </td>

      <td>
        String
      </td>

      <td>
        Optional
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        bank\_code
      </td>

      <td>
        The bank code. For example, `bca`.
      </td>

      <td>
        String
      </td>

      <td>
        Optional
      </td>

      <td>
        bca
      </td>
    </tr>

    <tr>
      <td>
        bin
      </td>

      <td>
        The requested Bin number. For example, `455633`.
      </td>

      <td>
        String
      </td>

      <td>
        Required
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        bin\_type
      </td>

      <td>
        The type of payment card. For example, `credit` or `debit`.
      </td>

      <td>
        String
      </td>

      <td>
        Required
      </td>

      <td>
        credit
      </td>
    </tr>

    <tr>
      <td>
        bin\_class
      </td>

      <td>
        Card Class. For example, `gold`.
      </td>

      <td>
        String
      </td>

      <td>
        Optional
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        brand
      </td>

      <td>
        The name of the bank issuing the payment card. For example, `visa`.
      </td>

      <td>
        String
      </td>

      <td>
        Optional
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        country\_name
      </td>

      <td>
        Country issuing the payment card. For example, `Indonesia`.
      </td>

      <td>
        String
      </td>

      <td>
        Optional
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        country\_code
      </td>

      <td>
        Code name of the country issuing the payment card. For example, `id`.
      </td>

      <td>
        String
      </td>

      <td>
        Optional
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        registration\_required
      </td>

      <td>
        [DEPRECATED - please use with your own discretion as data from some banks might not be the most updated]Indicate which card needs to be registered with the bank provider for use in online transactions.  

        For example, `true`, `false`or `null`
      </td>

      <td>
        Boolean
      </td>

      <td>
        Optional
      </td>

      <td>

      </td>
    </tr>
  </tbody>
</Table>

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
    "/v1/bins/{bin_number}": {
      "get": {
        "summary": "BIN API (Card Payment)",
        "description": "Obtain user's card properties information based on BIN (Bank Identification Number)",
        "operationId": "bin-api",
        "parameters": [
          {
            "name": "bin_number",
            "in": "path",
            "description": "Requested Bin number",
            "schema": {
              "type": "string",
              "default": "45563300"
            },
            "required": true
          }
        ],
        "responses": {
          "200": {
            "description": "200",
            "content": {
              "application/json": {
                "examples": {
                  "Result": {
                    "value": "{\n    \"data\": {\n        \"country_name\": \"Indonesia\",\n        \"country_code\": \"id\",\n        \"brand\": \"visa\",\n        \"bin_type\": \"credit\",\n        \"bin_class\": \"gold\",\n        \"bin\": \"45563300\",\n        \"bank_code\": \"bca\",\n        \"bank\": \"bank central asia\"\n    }\n}"
                  }
                },
                "schema": {
                  "type": "object",
                  "properties": {
                    "data": {
                      "type": "object",
                      "properties": {
                        "country_name": {
                          "type": "string",
                          "example": "Indonesia"
                        },
                        "country_code": {
                          "type": "string",
                          "example": "id"
                        },
                        "brand": {
                          "type": "string",
                          "example": "visa"
                        },
                        "bin_type": {
                          "type": "string",
                          "example": "credit"
                        },
                        "bin_class": {
                          "type": "string",
                          "example": "gold"
                        },
                        "bin": {
                          "type": "string",
                          "example": "45563300"
                        },
                        "bank_code": {
                          "type": "string",
                          "example": "bca"
                        },
                        "bank": {
                          "type": "string",
                          "example": "bank central asia"
                        }
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
              "text/plain": {
                "examples": {
                  "Result": {
                    "value": "Unauthorized"
                  }
                }
              }
            }
          },
          "404": {
            "description": "404",
            "content": {
              "application/json": {
                "examples": {
                  "Result": {
                    "value": "{\n    \"errors\": [\n        {\n            \"message_title\": \"not found\",\n            \"message\": \"not found\"\n        }\n    ]\n}"
                  }
                },
                "schema": {
                  "type": "object",
                  "properties": {
                    "errors": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "message_title": {
                            "type": "string",
                            "example": "not found"
                          },
                          "message": {
                            "type": "string",
                            "example": "not found"
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