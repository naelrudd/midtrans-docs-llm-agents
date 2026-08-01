---
updatedAt: 2025-11-11T00:32:48.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Akulaku PayLater

In addition to their shopping mall business, Akulaku has been enabling E-commerce to sell their merchandise in installment. It allows their customers to pay in installment without a payment card as long as they are registered to Akulaku.

The steps to integrate with Akulaku PayLater *Cardless Credit* are given below.

1. Send the charge API request to Midtrans with the selected acquirer.
2. Redirect the customer to the provider's website.
3. Redirect your customer back to your page by configuring Finish URL in Midtrans's Dashboard > [Settings > Payments](https://dashboard.midtrans.com/settings/payment).
4. [Handle notifications](/reference/notifications-handling).

Send a Charge API request with the details of the transaction such as `payment_type`, `transaction_details`, `item_details`, and `customer_details`. Successful request returns a URL to Akulaku's website.

By default, Akulaku's transaction expiry is 2 hours (min 20s, max 180 days).

<br />

***

<br />

## Akulaku PayLater Charge API Request

<br />

```json Sample Request - Akulaku PayLater Charge
{
  "payment_type": "akulaku",
  "transaction_details": {
    "order_id": "orderid-01",
    "gross_amount": 11000
  },
  "item_details": [
    {
      "id": "1",
      "price": 11000,
      "quantity": 1,
      "name": "Sepatu "
    }
  ],
  "customer_details":{
    "first_name": "John",
    "last_name": "Baker",
    "email": "john.baker@email.com",
    "phone": "08123456789"
  }
}
```

| JSON Attribute       | Description                                                                                                                         | Type                                     | Required |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- | -------- |
| payment\_type        | The *Cardless Credit* payment method used by the customer. Value: `akulaku`. <br />**Note**: Currently only `akulaku` is supported. | String                                   | Required |
| transaction\_details | The details of the specific transaction such as `order_id` and `gross_amount`.                                                      | [Object](https://docs.midtrans.com/reference/transaction-details-object) | Required |
| item\_details        | Details of the item(s) purchased by the customer.                                                                                   | [Object](https://docs.midtrans.com/reference/item-details-object)        | Required |
| customer\_details    | Details of the customer.                                                                                                            | [Object](https://docs.midtrans.com/reference/customer-details-object)    | Required |

<br />

***

<br />

## Akulaku PayLater Charge API Response and Notifications

<br />

```json Success
{
	"status_code": "201",
	"status_message": "Success, Akulaku transaction is created",
	"transaction_id": "b3a40398-d95d-4bb9-afe8-9a57bc0786ea",
	"order_id": "orderid-01",
	"redirect_url": "https://api.sandbox.veritrans.co.id/v2/akulaku/redirect/b3a40398-d95d-4bb9-afe8-9a57bc0786ea",
	"gross_amount": "11000.00",
	"currency": "IDR",
	"payment_type": "akulaku",
	"transaction_time": "2018-08-24 16:20:36",
	"transaction_status": "pending",
	"fraud_status": "accept",
	"channel_response_code": "",
	"channel_response_message": ""
}
```
```json Pending
{
  "transaction_time": "2018-08-24 16:20:36",
  "gross_amount": "11000.00",
  "order_id": "orderid-01",
  "payment_type": "akulaku",
  "signature_key": "e47d73b2a10347d291e85a7c39c5fa2a7b760f0af7d9882f9c1b26db06e1af948968184b78f67112158cdeddd2141fe41068fdb37361ce11c3d2509354224a80",
  "status_code": "201",
  "transaction_id": "b3a40398-d95d-4bb9-afe8-9a57bc0786ea",
  "transaction_status": "pending",
  "fraud_status": "accept",
  "status_message": "midtrans payment notification"
}
```
```json Settlement
{
  "transaction_time": "2018-08-24 16:20:36",
  "gross_amount": "11000.00",
  "order_id": "orderid-01",
  "payment_type": "akulaku",
  "signature_key": "35c4111539e184b268b7c1cd62a9c254e5d27c992c8fd55084f930b69b09eaafcfe14b0d512c697648295fdb45de777e1316b401f4729846a91b3de88cde3f05",
  "status_code": "200",
  "transaction_id": "b3a40398-d95d-4bb9-afe8-9a57bc0786ea",
  "transaction_status": "settlement",
  "fraud_status": "accept",
  "status_message": "midtrans payment notification"
}
```
```json Expired
{
  "transaction_time": "2018-08-24 16:20:36",
  "gross_amount": "11000.00",
  "order_id": "orderid-01",
  "payment_type": "akulaku",
  "signature_key": "62a8c432bb5a288a0495dd4f868b0aede4535e0c8a9fbebb3c6e9d4ea0db6f1963e551e70a99e80512030afa5ba8268f9be7b17b13a422ebef4620988c55d5ed",
  "status_code": "202",
  "transaction_id": "b3a40398-d95d-4bb9-afe8-9a57bc0786ea",
  "transaction_status": "expire",
  "fraud_status": "accept",
  "status_message": "midtrans payment notification"
}
```
```json Deny
{
  "transaction_time": "2018-08-24 16:20:36",
  "gross_amount": "11000.00",
  "order_id": "orderid-01",
  "payment_type": "akulaku",
  "signature_key": "c2bdfd8d1b25100f5512b2573ecad8f2d324837a731362491b5a6b0bbd7ec74a032010754129f4c74f77a21796f747258ea611a3d5710648f63342570cdd0bb4",
  "status_code": "202",
  "transaction_id": "b3a40398-d95d-4bb9-afe8-9a57bc0786ea",
  "transaction_status": "deny",
  "fraud_status": "accept",
  "status_message": "midtrans payment notification"
}
```

| JSON Attribute             | Description                                                                                                                                                                                                                                                                                                                                                        | Type    |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------- |
| status\_code               | Status code of transaction charge result.                                                                                                                                                                                                                                                                                                                          | String  |
| status\_message            | Status message describing the result of the API request.                                                                                                                                                                                                                                                                                                           | String  |
| transaction\_id            | Transaction ID given by Midtrans.                                                                                                                                                                                                                                                                                                                                  | String  |
| order\_id                  | Order ID specified by the merchant.                                                                                                                                                                                                                                                                                                                                | String  |
| redirect\_url              | The redirect URL to Akulaku payment page.                                                                                                                                                                                                                                                                                                                          | String  |
| gross\_amount              | Total transaction amount in IDR.                                                                                                                                                                                                                                                                                                                                   | String  |
| currency                   | ISO-4217 representation of three-letter alphabetic currency code. Value: `IDR`.<br />**Note**: Currently only `IDR` is supported.                                                                                                                                                                                                                                  | String  |
| payment\_type              | Payment method used by the customer.                                                                                                                                                                                                                                                                                                                               | String  |
| transaction\_time          | Timestamp of transaction in ISO 8601 format. Time Zone: GMT+7.                                                                                                                                                                                                                                                                                                     | String  |
| transaction\_status        | Transaction status of Akulaku transaction. Possible values are `pending`, `deny`, `settlement`, `expire`.                                                                                                                                                                                                                                                          | String  |
| fraud\_status              | Detection result by Fraud Detection System (FDS). Possible values are `accept` : Approved by FDS and `challenge`: Questioned by FDS.<br />**Note**: You have to [approve](https://docs.midtrans.com/reference/approve-transaction) the transaction to accept it or transaction will get cancelled automatically during settlement.<br/>`deny`: Denied by FDS. Transaction is automatically failed. | String  |
| channel\_response\_code    | Response code from the channel.                                                                                                                                                                                                                                                                                                                                    | Integer |
| channel\_response\_message | Response message from the channel.                                                                                                                                                                                                                                                                                                                                 | String  |

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "info": {
    "title": "core-api-akulaku",
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
    "/v2/charge": {
      "post": {
        "summary": "Akulaku PayLater",
        "description": "",
        "operationId": "akulaku-1",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "required": [
                  "payment_type",
                  "transaction_details",
                  "item_details",
                  "customer_details"
                ],
                "properties": {
                  "payment_type": {
                    "type": "string",
                    "default": "akulaku"
                  },
                  "transaction_details": {
                    "type": "object",
                    "required": [
                      "order_id",
                      "gross_amount"
                    ],
                    "properties": {
                      "order_id": {
                        "type": "string",
                        "default": "orderid-01"
                      },
                      "gross_amount": {
                        "type": "integer",
                        "default": 100000,
                        "format": "int32"
                      }
                    }
                  },
                  "item_details": {
                    "type": "object",
                    "required": [
                      "id",
                      "price",
                      "quantity",
                      "name"
                    ],
                    "properties": {
                      "id": {
                        "type": "string",
                        "default": "id"
                      },
                      "price": {
                        "type": "integer",
                        "default": 100000,
                        "format": "int32"
                      },
                      "quantity": {
                        "type": "integer",
                        "default": 1,
                        "format": "int32"
                      },
                      "name": {
                        "type": "string",
                        "default": "ticket 1"
                      }
                    }
                  },
                  "customer_details": {
                    "type": "object",
                    "required": [
                      "first_name",
                      "last_name",
                      "email",
                      "phone"
                    ],
                    "properties": {
                      "first_name": {
                        "type": "string",
                        "default": "Budi"
                      },
                      "last_name": {
                        "type": "string",
                        "default": "Utomo"
                      },
                      "email": {
                        "type": "string",
                        "default": "budi.utomo@midtrans.com"
                      },
                      "phone": {
                        "type": "string",
                        "default": "08123456789"
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
                    "value": "{\n    \"status_code\": \"201\",\n    \"status_message\": \"Success, Akulaku transaction is created\",\n    \"transaction_id\": \"b3a40398-d95d-4bb9-afe8-9a57bc0786ea\",\n    \"order_id\": \"orderid-01\",\n    \"redirect_url\": \"https://api.sandbox.veritrans.co.id/v2/akulaku/redirect/b3a40398-d95d-4bb9-afe8-9a57bc0786ea\",\n    \"gross_amount\": \"11000.00\",\n    \"currency\": \"IDR\",\n    \"payment_type\": \"akulaku\",\n    \"transaction_time\": \"2018-08-24 16:20:36\",\n    \"transaction_status\": \"pending\",\n    \"fraud_status\": \"accept\",\n    \"channel_response_code\": \"\",\n    \"channel_response_message\": \"\"\n}"
                  }
                },
                "schema": {
                  "type": "object",
                  "properties": {
                    "status_code": {
                      "type": "string",
                      "example": "201"
                    },
                    "status_message": {
                      "type": "string",
                      "example": "Success, Akulaku transaction is created"
                    },
                    "transaction_id": {
                      "type": "string",
                      "example": "b3a40398-d95d-4bb9-afe8-9a57bc0786ea"
                    },
                    "order_id": {
                      "type": "string",
                      "example": "orderid-01"
                    },
                    "redirect_url": {
                      "type": "string",
                      "example": "https://api.sandbox.veritrans.co.id/v2/akulaku/redirect/b3a40398-d95d-4bb9-afe8-9a57bc0786ea"
                    },
                    "gross_amount": {
                      "type": "string",
                      "example": "11000.00"
                    },
                    "currency": {
                      "type": "string",
                      "example": "IDR"
                    },
                    "payment_type": {
                      "type": "string",
                      "example": "akulaku"
                    },
                    "transaction_time": {
                      "type": "string",
                      "example": "2018-08-24 16:20:36"
                    },
                    "transaction_status": {
                      "type": "string",
                      "example": "pending"
                    },
                    "fraud_status": {
                      "type": "string",
                      "example": "accept"
                    },
                    "channel_response_code": {
                      "type": "string",
                      "example": ""
                    },
                    "channel_response_message": {
                      "type": "string",
                      "example": ""
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