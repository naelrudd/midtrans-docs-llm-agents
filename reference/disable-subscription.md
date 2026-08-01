---
updatedAt: 2025-11-11T00:29:28.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Disable Subscription

Disable a customer's subscription account with a specific `subscription_id` so that the customer is not charged for the subscription in the future. Successful request returns `status_message` indicating that the subscription details are updated.

> 📘 Note
>
> Disable subscription does not stop any pending retries on subscription. Pending retry is caused by failure on previous subscription payment. Any pending retries will still be executed after subscription is disabled for trying to resolve previous pending payments.
>
> To disable subscription and stop all pending retries, you can use [Cancel Subscription](https://docs.midtrans.com/reference/cancel-subscription) instead.

***

<br />

## Disable Subscription Method

| HTTP Method | Endpoint                                               | Description          |
| ----------- | ------------------------------------------------------ | -------------------- |
| POST        | BASE\_URL/v1/subscriptions/`{subscription_id}`/disable | Disable subscription |

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
    "/v1/subscriptions/{subscription_id}/disable": {
      "post": {
        "summary": "Disable Subscription",
        "description": "",
        "operationId": "disable-subscription",
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