---
updatedAt: 2025-11-10T23:01:38.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Cancel Transaction on Card

Cancel transaction is triggered to void the transaction. If transaction is already settled (status : `settlement`) you should perform `refund` instead if the payment method supports it.

Cancel API can be used in both Core API and Snap integrations.

<br />

***

## Card Payment

Card payment can be voided with Cancel method if the transaction has not been settled. The time interval during which the pre-authorized transaction can be cancelled depends on the Acquiring Bank.

| Acquiring Bank                | Trigger Cancel Method                                         |
| ----------------------------- | ------------------------------------------------------------- |
| **BNI**                       | After pre-authorization payment has been captured.            |
| **Mandiri**                   | After the initial charge of the pre-authorized payment.       |
| **BCA**, **BRI**, **MAYBANK** | Before and after pre-authorization payment has been captured. |

<br />

***

## Cancel Transaction Method

See sample on the right -- try it yourself!

| HTTP Method | Endpoint                                                | Definition         |
| ----------- | ------------------------------------------------------- | ------------------ |
| POST        | BASE\_URL/v2/\{order\_id **OR** transaction\_id}/cancel | Cancel transaction |

<br />

***

## Cancel Transaction Response and Notification

```json Sample Response - Success
{
  "status_code" : "200",
  "status_message" : "Success, transaction is canceled",
  "transaction_id" : "249fc620-6017-4540-af7c-5a1c25788f46",
  "masked_card" : "48111111-1114",
  "order_id" : "example-1424936368",
  "payment_type" : "credit_card",
  "transaction_time" : "2015-02-26 14:39:33",
  "transaction_status" : "cancel",
  "fraud_status" : "accept",
  "bank" : "bni",
  "gross_amount" : "30000.00",
  "channel": "dragon",
  "expiry_time":"2015-03-06 14:39:33",
  "settlement_time":"2015-02-26 19:00:00"
}
```
```json Sample Response - Error
{
  "status_code" : "412",
  "status_message" : "Merchant cannot modify the status of the transaction"
}
```
```json Sample Response - Success Notification
{
  "masked_card": "48111111-1114",
  "approval_code": "325511",
  "bank": "mandiri",
  "eci": "05",
  "transaction_time": "2016-07-04 13:32:44",
  "gross_amount": "244108.00",
  "order_id": "160288131764",
  "payment_type": "credit_card",
  "signature_key": "71f3b14d3036d2a60dac7fef1cdde7bebdbb2dbeebc68bcf5e7819fe8be7c9241611ea1e769e0c6775735805174c02b9d6b5cf89a11de1861d5efb298c9898b7",
  "status_code": "202",
  "transaction_id": "ffd82cd2-4f0d-4b24-b4b8-e201b0c3d80e",
  "transaction_status": "cancel",
  "fraud_status": "accept",
  "status_message": "midtrans payment notification"
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
        Status code of transaction cancel result.
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
        Description of transaction cancel result.
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
        First 8-digits and last 4-digits of customer's credit card number.
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
        Transaction status after charge credit card transaction. Possible values are<br/>`capture` : Transaction is accepted by the bank and ready for settlement. <br /> **Note**: Cancel transaction to deny / cancel it. Otherwise, transaction is settled automatically. <br/>`deny`: transaction is denied by the bank or FDS.<br/>`authorize`: Credit card is authorized in pre-authorization feature.
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
        The acquiring bank of the transaction.
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
    "/v2/{order_id}/cancel?": {
      "post": {
        "summary": "Cancel Transaction on Card",
        "description": "",
        "operationId": "cancel-transaction-card",
        "parameters": [
          {
            "name": "order_id",
            "in": "path",
            "description": "order_id or transaction_id",
            "schema": {
              "type": "string"
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
                    "value": "{\n  \"status_code\" : \"200\",\n  \"status_message\" : \"Success, transaction is canceled\",\n  \"transaction_id\" : \"249fc620-6017-4540-af7c-5a1c25788f46\",\n  \"masked_card\" : \"48111111-1114\",\n  \"order_id\" : \"example-1424936368\",\n  \"payment_type\" : \"credit_card\",\n  \"transaction_time\" : \"2015-02-26 14:39:33\",\n  \"transaction_status\" : \"cancel\",\n  \"fraud_status\" : \"accept\",\n  \"bank\" : \"bni\",\n  \"gross_amount\" : \"30000.00\"\n}"
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
                          "example": "Success, transaction is canceled"
                        },
                        "transaction_id": {
                          "type": "string",
                          "example": "249fc620-6017-4540-af7c-5a1c25788f46"
                        },
                        "masked_card": {
                          "type": "string",
                          "example": "48111111-1114"
                        },
                        "order_id": {
                          "type": "string",
                          "example": "example-1424936368"
                        },
                        "payment_type": {
                          "type": "string",
                          "example": "credit_card"
                        },
                        "transaction_time": {
                          "type": "string",
                          "example": "2015-02-26 14:39:33"
                        },
                        "transaction_status": {
                          "type": "string",
                          "example": "cancel"
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