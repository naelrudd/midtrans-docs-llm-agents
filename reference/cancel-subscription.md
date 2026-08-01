---
updatedAt: 2025-11-11T00:29:29.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Cancel Subscription

Cancel a customer's subscription account with a specific `subscription_id` so that the customer is not charged for the subscription in the future. Successful request returns `status_message` indicating that the subscription details are updated.

The difference between cancel subscription and disable subscription is that cancel subscription also stop any pending retries on subscription due to previous failure on charging customer (might be caused by timeout to payment provider or customer balance is insufficient).

<br />

***

<br />

## Cancel Subscription Method

| HTTP Method | Endpoint                                              | Description         |
| ----------- | ----------------------------------------------------- | ------------------- |
| POST        | BASE\_URL/v1/subscriptions/`{subscription_id}`/cancel | Cancel subscription |

<br />

***

<br />

## Disable Subscription Response

```json Sample Response - Success
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
  "status_message": "Sorry, our system is recovering from unexpected issues. Please retry."
}
```

| JSON Attribute  | Description                                                 | Type   |
| --------------- | ----------------------------------------------------------- | ------ |
| status\_message | Message describing the status of the result of API request. | String |

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
    "/v1/subscriptions/{subscription_id}/cancel": {
      "post": {
        "summary": "Cancel Subscription",
        "description": "",
        "operationId": "cancel-subscription",
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