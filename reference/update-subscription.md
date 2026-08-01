---
updatedAt: 2025-11-11T00:29:30.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Update Subscription

Update the details of a customer's existing subscription account with the specific `subscription_id`. Successful request returns `status_message` indicating that the subscription details are updated. You can also use the API to reactivate expired/dead subscriptions by updating the subscription's schedule.

<br />

***

<br />

## Update Subscription Method

| HTTP Method | Endpoint                                       | Description         |
| ----------- | ---------------------------------------------- | ------------------- |
| PATCH       | BASE\_URL/v1/subscriptions/`{subscription_id}` | Update subscription |

```json Sample Request Body
{
    "name": "MONTHLY_2019",
    "amount": "14000",
    "currency": "IDR",
    "token": "48111111sHfSakAvHvFQFEjTivUV1114",
    "schedule": {
      "interval": 1
    },
    "retry_schedule": {
  	  "interval": 1,
  	  "interval_unit": "day",
          "max_interval": 3,
    },
    "gopay": {
      "account_id": "0dd2cd90-a9a9-4a09-b393-21162dfb713b"
    }
}
```
```json Sample Response - Successful
{
  "status_message": "Subscription is updated."
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

***

<br />

## Update Subscription Request

| JSON Attribute  | Description                                                                                                                       | Type                                                           | Required |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- | -------- |
| name            | Subscription name specified by you. <br />**Note**: Allowed symbols are dash(-), underscore(\_), tilde (\~), and dot (.).         | String(15)                                                     | Required |
| amount          | Amount specified by you for recurring charge.                                                                                     | String                                                         | Required |
| currency        | ISO-4217 representation of three-letter alphabetic currency code. Value: `IDR`.<br />**Note**: Currently only `IDR` is supported. | String                                                         | Required |
| token           | Saved payment token. <br />**Note**: For `credit_card`, use `saved_token_id` received in Charge response.                         | String                                                         | Required |
| schedule        | Update an ongoing subscription's schedule, or reactivate an expired subscription by updating the schedule.                        | [Object](/reference/update-subscription-schedule-object)       | Optional |
| retry\_schedule | Update an ongoing subscription's retry schedule over failed charge.                                                               | [Object](/reference/create-subscription-retry-schedule-object) | Optional |
| gopay           | GoPay subscription information.                                                                                                   | [Object](/reference/subscription-customer-details-object)      | Optional |

<br />

***

<br />

## Update Subscription Response

| JSON Attribute  | Description                                                 | Type   |
| --------------- | ----------------------------------------------------------- | ------ |
| status\_message | Message describing the status of the result of API request. | String |

<br />

> 📘 Note
>
> * Payment method cannot be updated in the middle of subscription. If merchant wish to change the payment method of an active subscription, the subscription must be disabled first. After that, new subscription with same data can be created again with different payment method.
>
> * Inside `schedule`, only `interval` field can be updated. `schedule.interval_unit` and `schedule.max_interval` can not be updated.
>
> * Any updates to the subscription **interval** schedule will only be effective after the next scheduled payment is processed. For example, consider a subscription scheduled to run at the end of this month. If you update the **interval** field in the middle of the month, change will take effect from the next month. For other parameters, the change will be effective starting from the next scheduled payment.
>
> * To reactivate dead subscriptions, simply update the subscription schedule with future dates. Subscription will then reactivate and resume charging the customer at the date specified at `next_execution_at`.

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
      "patch": {
        "summary": "Update Subscription",
        "description": "",
        "operationId": "update-subscription",
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
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "required": [
                  "name",
                  "amount",
                  "currency",
                  "token",
                  "schedule"
                ],
                "properties": {
                  "name": {
                    "type": "string"
                  },
                  "amount": {
                    "type": "string"
                  },
                  "currency": {
                    "type": "string",
                    "default": "IDR"
                  },
                  "token": {
                    "type": "string"
                  },
                  "schedule": {
                    "type": "object",
                    "properties": {
                      "interval": {
                        "type": "string",
                        "default": "1"
                      }
                    }
                  },
                  "gopay": {
                    "type": "object",
                    "required": [
                      "account_id"
                    ],
                    "properties": {
                      "account_id": {
                        "type": "string"
                      }
                    }
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
                    "value": "{\n  \"status_message\": \"Subscription is updated.\"\n}"
                  }
                },
                "schema": {
                  "type": "object",
                  "properties": {
                    "status_message": {
                      "type": "string",
                      "example": "Subscription is updated."
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