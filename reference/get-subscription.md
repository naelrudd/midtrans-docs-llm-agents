---
updatedAt: 2025-11-11T00:29:27.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Get Subscription

Retrieve the subscription details of a customer using the `subscription_id`. Successful request returns `subscription object` and `status:active`.

<br />

***

<br />

## Get Subscription Method

| HTTP Method | Endpoint                                       | Description                   |
| ----------- | ---------------------------------------------- | ----------------------------- |
| GET         | BASE\_URL/v1/subscriptions/`{subscription_id}` | Retrieve subscription details |

<br />

***

<br />

## Get Subscription Response

```json Card Sample Response - Success
{
  "id": "d98a63b8-97e4-4059-825f-0f62340407e9",
  "name": "MONTHLY_2019",
  "amount": "14000",
  "currency": "IDR",
  "created_at": "2019-05-29T09:11:01.810452",
  "schedule": {
    "interval": 1,
    "interval_unit": "month",
    "current_interval" : 1,
    "start_time": "2019-05-29T09:11:01.803677",
    "previous_execution_at": "2019-05-29T09:11:01.803677",
    "next_execution_at": "2019-06-29T09:11:01.803677"
  },
  "status": "active",
  "token": "48111111sHfSakAvHvFQFEjTivUV1114",
  "payment_type": "credit_card",
  "transaction_ids": [
    "9beb839d-8fe2-41ec-bc5e-045e5001d286",
    "eb47cd5d-acd3-4e53-a155-7bd41aa38052",
    "9d286585-bd19-43be-95dc-da3d32ab18af",
    "ec3175c6-9f0a-4ce5-9332-abfb1db0852f",
    "00f7d40d-26e2-4624-a797-9ddc54ca9987",
    "421bd123-d8b2-4476-bcea-165f9e176cbb"
  ],
  "metadata": {
    "description": "Recurring payment for A"
  },
  "customer_details": {
    "first_name": "John",
    "last_name": "Doe",
    "email": "johndoe@email.com",
    "phone": "+62812345678"
  }
}
```
```json GoPay Sample Response - Success
{
  "id": "d98a63b8-97e4-4059-825f-0f62340407e9",
  "name": "MONTHLY_2019",
  "amount": "14000",
  "currency": "IDR",
  "created_at": "2019-05-29T09:11:01.810452",
  "schedule": {
    "interval": 1,
    "interval_unit": "month",
	  "current_interval" : 1,
    "start_time": "2019-05-29T09:11:01.803677",
    "previous_execution_at": "2019-05-29T09:11:01.803677",
    "next_execution_at": "2019-06-29T09:11:01.803677"
  },
  "status": "active",
  "token": "48111111sHfSakAvHvFQFEjTivUV1114",
  "payment_type": "credit_card",
  "metadata": {
    "description": "Recurring payment for A"
  },
  "customer_details": {
    "first_name": "John",
    "last_name": "Doe",
    "email": "johndoe@email.com",
    "phone": "+62812345678"
  },
  "gopay": {                                                    
    "account_id": "phy56f8f-2683-4248-8080-e59b36c6bbgf"
  }
}
```
```json Sample Response - Status Code: 404
{
  "status_message": "Subscription doesn't exist."
}
```
```json Sample Response - Status Code: 500
{
  "status_message": "Sorry, Our system is recovering from unexpected issues. Please retry."
}
```

| JSON Attribute    | Description                                                                                                                            | Type                                                      |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| id                | Subscription ID given by Midtrans.                                                                                                     | String                                                    |
| name              | Subscription name given by you.                                                                                                        | String                                                    |
| amount            | Amount specified by you for recurring charge.                                                                                          | String                                                    |
| currency          | ISO-4217 representation of three-letter alphabetic currency code. Value: `IDR`.<br />**Note**: Currently only `IDR` is supported.      | String                                                    |
| created\_at       | Timestamp at which the subscription schedule is created in ISO 8601 format. Time Zone (GMT+7).                                         | String                                                    |
| schedule          | Details of the subscription schedule.                                                                                                  | [Object](/reference/subscription-schedule-object)         |
| status            | Current subscription Status. <br />**Note**: Possible status values are `active` and `inactive`.                                       | String                                                    |
| token             | Payment token used for subscription.                                                                                                   | String                                                    |
| payment\_type     | The payment method used by the customer. Value: `credit_card`. <br />**Note**: Currently only `credit_card` and `gopay` are supported. | String                                                    |
| transaction\_ids  | List of transaction IDs which are successfully charged.                                                                                | Array(String)                                             |
| metadata          | Metadata of subscription specified by you. <br />**Note**: Limit the size to less than 1KB.                                            | Object                                                    |
| customer\_details | Details of the customer.                                                                                                               | [Object](/reference/subscription-customer-details-object) |
| status\_message   | Description of the error                                                                                                               | String                                                    |

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
    "/v1/subscriptions/{subscription_id}": {
      "get": {
        "summary": "Get Subscription",
        "description": "",
        "operationId": "get-subscription",
        "parameters": [
          {
            "name": "subscription_id",
            "in": "path",
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
                    "value": "{\n  \"id\": \"d98a63b8-97e4-4059-825f-0f62340407e9\",\n  \"name\": \"MONTHLY_2019\",\n  \"amount\": \"14000\",\n  \"currency\": \"IDR\",\n  \"created_at\": \"2019-05-29T09:11:01.810452\",\n  \"schedule\": {\n    \"interval\": 1,\n    \"interval_unit\": \"month\",\n    \"start_time\": \"2019-05-29T09:11:01.803677\",\n    \"previous_execution_at\": \"2019-05-29T09:11:01.803677\",\n    \"next_execution_at\": \"2019-06-29T09:11:01.803677\"\n  },\n  \"status\": \"active\",\n  \"token\": \"48111111sHfSakAvHvFQFEjTivUV1114\",\n  \"payment_type\": \"credit_card\",\n  \"transaction_ids\": [\n    \"9beb839d-8fe2-41ec-bc5e-045e5001d286\",\n    \"eb47cd5d-acd3-4e53-a155-7bd41aa38052\",\n    \"9d286585-bd19-43be-95dc-da3d32ab18af\",\n    \"ec3175c6-9f0a-4ce5-9332-abfb1db0852f\",\n    \"00f7d40d-26e2-4624-a797-9ddc54ca9987\",\n    \"421bd123-d8b2-4476-bcea-165f9e176cbb\"\n  ],\n  \"metadata\": {\n    \"description\": \"Recurring payment for A\"\n  },\n  \"customer_details\": {\n    \"first_name\": \"John\",\n    \"last_name\": \"Doe\",\n    \"email\": \"johndoe@email.com\",\n    \"phone\": \"+62812345678\"\n  }\n}"
                  }
                },
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "example": "d98a63b8-97e4-4059-825f-0f62340407e9"
                    },
                    "name": {
                      "type": "string",
                      "example": "MONTHLY_2019"
                    },
                    "amount": {
                      "type": "string",
                      "example": "14000"
                    },
                    "currency": {
                      "type": "string",
                      "example": "IDR"
                    },
                    "created_at": {
                      "type": "string",
                      "example": "2019-05-29T09:11:01.810452"
                    },
                    "schedule": {
                      "type": "object",
                      "properties": {
                        "interval": {
                          "type": "integer",
                          "example": 1,
                          "default": 0
                        },
                        "interval_unit": {
                          "type": "string",
                          "example": "month"
                        },
                        "start_time": {
                          "type": "string",
                          "example": "2019-05-29T09:11:01.803677"
                        },
                        "previous_execution_at": {
                          "type": "string",
                          "example": "2019-05-29T09:11:01.803677"
                        },
                        "next_execution_at": {
                          "type": "string",
                          "example": "2019-06-29T09:11:01.803677"
                        }
                      }
                    },
                    "status": {
                      "type": "string",
                      "example": "active"
                    },
                    "token": {
                      "type": "string",
                      "example": "48111111sHfSakAvHvFQFEjTivUV1114"
                    },
                    "payment_type": {
                      "type": "string",
                      "example": "credit_card"
                    },
                    "transaction_ids": {
                      "type": "array",
                      "items": {
                        "type": "string",
                        "example": "9beb839d-8fe2-41ec-bc5e-045e5001d286"
                      }
                    },
                    "metadata": {
                      "type": "object",
                      "properties": {
                        "description": {
                          "type": "string",
                          "example": "Recurring payment for A"
                        }
                      }
                    },
                    "customer_details": {
                      "type": "object",
                      "properties": {
                        "first_name": {
                          "type": "string",
                          "example": "John"
                        },
                        "last_name": {
                          "type": "string",
                          "example": "Doe"
                        },
                        "email": {
                          "type": "string",
                          "example": "johndoe@email.com"
                        },
                        "phone": {
                          "type": "string",
                          "example": "+62812345678"
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