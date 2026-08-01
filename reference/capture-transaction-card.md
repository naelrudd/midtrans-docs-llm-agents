---
updatedAt: 2025-11-10T23:01:37.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Capture Transaction on Card

Capture transaction is triggered to capture the transaction balance when `transaction_status:authorize`. This is only available after [Pre-Authorized Credit Card](https://docs.midtrans.com/reference/card-feature-pre-authorization) or [Pre-Authorized GoPay](/reference/gopay-tokenization#gopay-tokenization-features-pre-auth).

<br />

***

## Capture Transaction Method

See sample on the right -- try it yourself!

| HTTP Method | Endpoint             | Definition                                          |
| ----------- | -------------------- | --------------------------------------------------- |
| POST        | BASE\_URL/v2/capture | Capture an authorized transaction for card payment. |

<br />

***

## Capture Transaction Request

```json Sample Request - Capture
{
  "transaction_id": "be4f3e44-d6ee-4355-8c64-c1d1dc7f4590",
  "gross_amount": 145000
}v
```

| JSON Attribute  | Description                                                                                                                       | Type        | Required |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------- | ----------- | -------- |
| transaction\_id | Transaction ID given by Midtrans.                                                                                                 | String(255) | Required |
| gross\_amount   | Total amount of transaction in IDR. By default it captures whole transaction amount. <br /> **Note**: Decimal values are invalid. | Long        | Optional |

<br />

***

## Capture Transaction Response

```json Sample Response - Success
{
  "status_code" : "200",
  "status_message" : "Success, Credit Card capture transaction is successful",
  "transaction_id" : "ca297170-be4c-45ed-9dc9-be5ba99d30ee",
  "masked_card" : "45111111-1117",
  "order_id" : "testing-0.4555-1414741517",
  "payment_type" : "credit_card",
  "transaction_time" : "2014-10-31 14:46:44",
  "transaction_status" : "capture",
  "fraud_status" : "accept",
  "bank" : "bni",
  "gross_amount" : "30000.00",
  "channel": "dragon",
  "expiry_time":"2014-11-08 14:46:44",
  "settlement_time":"2014-10-31 19:00:00"
}
```
```json Sample Response - Error
{
  "status_code" : "412",
  "status_message" : "Merchant cannot modify the status of the transaction"
}
```

<Table>
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
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        status\_code
      </td>

      <td>
        Status code of transaction capture result.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        status\_message
      </td>

      <td>
        Description of transaction capture result.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        order\_id
      </td>

      <td>
        Order ID specified by you.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        transaction\_id
      </td>

      <td>
        Transaction ID given by Midtrans.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        masked\_card
      </td>

      <td>
        First 8-digits and last 4-digits of customer's card number.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        gross\_amount
      </td>

      <td>
        Total amount of transaction in IDR.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        order\_id
      </td>

      <td>
        Order ID specified by you.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        payment\_type
      </td>

      <td>
        The payment method used by the customer.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        transaction\_time
      </td>

      <td>
        Timestamp of transaction in ISO 8601 format. Time Zone: GMT+7.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        transaction\_status
      </td>

      <td>
        Transaction status after capture card transaction.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        fraud\_status
      </td>

      <td>
        Detection result by Fraud Detection System (FDS). Possible values are<br/>`accept` : Approved by FDS.<br/>`deny`: Denied by FDS. Transaction automatically failed.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        bank
      </td>

      <td>
        The name of the acquiring bank.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        gross\_amount
      </td>

      <td>
        Total amount of transaction in IDR. 
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        channel
      </td>

      <td>
        The name of the payment channel provider. More details on request and possible values are available on [Card Feature: Specific Channel](https://docs.midtrans.com/reference/feature-route-to-specific-channel).
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        expiry\_time
      </td>

      <td>
        For regular card transactions (non-recurring, non-one-click, non-two-click token) and the 3DS redirect\_url expires in 10 minutes. For authorized transaction expires in 8 days.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        settlement\_time
      </td>

      <td>
        Credit card settlement time refers to the duration it takes for a credit card transaction to be processed and transaction\_status change to settlement.
      </td>

      <td>
        String
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
    "/v2/capture?": {
      "post": {
        "summary": "Capture Transaction on Card",
        "description": "",
        "operationId": "capture-transaction-card",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "transaction_id": {
                    "type": "string"
                  },
                  "gross_amount": {
                    "type": "integer",
                    "format": "int64"
                  }
                }
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "200",
            "content": {
              "application/json": {
                "examples": {
                  "Result": {
                    "value": "{\n  \"status_code\" : \"200\",\n  \"status_message\" : \"Success, Credit Card capture transaction is successful\",\n  \"transaction_id\" : \"ca297170-be4c-45ed-9dc9-be5ba99d30ee\",\n  \"masked_card\" : \"45111111-1117\",\n  \"order_id\" : \"testing-0.4555-1414741517\",\n  \"payment_type\" : \"credit_card\",\n  \"transaction_time\" : \"2014-10-31 14:46:44\",\n  \"transaction_status\" : \"capture\",\n  \"fraud_status\" : \"accept\",\n  \"bank\" : \"bni\",\n  \"gross_amount\" : \"30000.00\",\n  \"channel\": \"dragon\",\n  \"expiry_time\":\"2014-08-09 15:39:22\",\n  \"settlement_time\":\"2014-08-09 19:00:00\"\n}"
                  },
                  "Error Validation": {
                    "value": "{\n  \"status_code\" : \"412\",\n  \"status_message\" : \"Merchant cannot modify the status of the transaction\"\n}"
                  }
                },
                "schema": {
                  "oneOf": [
                    {
                      "type": "object",
                      "properties": {
                        "status_code": {
                          "type": "string",
                          "example": "200"
                        },
                        "status_message": {
                          "type": "string",
                          "example": "Success, Credit Card capture transaction is successful"
                        },
                        "transaction_id": {
                          "type": "string",
                          "example": "ca297170-be4c-45ed-9dc9-be5ba99d30ee"
                        },
                        "masked_card": {
                          "type": "string",
                          "example": "45111111-1117"
                        },
                        "order_id": {
                          "type": "string",
                          "example": "testing-0.4555-1414741517"
                        },
                        "payment_type": {
                          "type": "string",
                          "example": "credit_card"
                        },
                        "transaction_time": {
                          "type": "string",
                          "example": "2014-10-31 14:46:44"
                        },
                        "transaction_status": {
                          "type": "string",
                          "example": "capture"
                        },
                        "fraud_status": {
                          "type": "string",
                          "example": "accept"
                        },
                        "bank": {
                          "type": "string",
                          "example": "bni"
                        },
                        "gross_amount": {
                          "type": "string",
                          "example": "30000.00"
                        },
                        "channel": {
                          "type": "string",
                          "example": "dragon"
                        },
                        "expiry_time": {
                          "type": "string",
                          "example": "2014-08-09 15:39:22"
                        },
                        "settlement_time": {
                          "type": "string",
                          "example": "2014-08-09 19:00:00"
                        }
                      }
                    },
                    {
                      "title": "Error Validation",
                      "type": "object",
                      "properties": {
                        "status_code": {
                          "type": "string",
                          "example": "412"
                        },
                        "status_message": {
                          "type": "string",
                          "example": "Merchant cannot modify the status of the transaction"
                        }
                      }
                    }
                  ]
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
                    "value": "{\n    \"status_code\": \"401\",\n    \"status_message\": \"Transaction cannot be authorized with the current client/server key.\"\n}"
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