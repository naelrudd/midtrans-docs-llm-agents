---
updatedAt: 2025-11-10T23:04:26.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Indomaret

Using *Over the Counter* payment feature provided by Indomaret, the customer can make a purchase in your web/app and complete the payment at any Indomaret stores. Midtrans sends a real-time notification to you for every incoming payment.

The steps to integrate with Indomaret stores are given below.

1. Send the charge API request to Midtrans with the selected acquirer.
2. Display the payment code to customers.
3. [Handle notifications](/reference/notifications-handling).

By default, default expiry time for Indomaret is 24 hours unless specified by merchant (min 20s, max 180 days).

<br />

> 📘 Note
>
> In some transactions, the transaction\_status **SETTLEMENT** turns into **DENY** within a span of one minute. This is caused by a payment reversal triggered by the corresponding payment provider

<br />

Send a Charge API request with payment details, transaction details, convenience store details, customer details, and item details. Successful request returns `status_code:201`.

<br />

***

<br />

## Indomaret Charge API Request

<br />

```json Sample Request - Indomaret Charge
{
  "payment_type": "cstore",
  "transaction_details": {
    "gross_amount": 162500,
    "order_id": "order04"
  },
  "cstore": {
    "store": "Indomaret",
    "message": "Tiket1 transaction"
  },
  "customer_details": {
    "first_name": "Budi",
    "last_name": "Utomo",
    "email": "budi.utomo@midtrans.com",
    "phone": "0811223344"
  },
  "item_details": [
    {
      "id": "id1",
      "price": 162500,
      "quantity": 1,
      "name": "tiket1"
    }
  ]
}
```

| JSON Attribute       | Description                                                                    | Type                                     | Required |
| -------------------- | ------------------------------------------------------------------------------ | ---------------------------------------- | -------- |
| payment\_type        | The payment method used by the customer. Value: `cstore`.                      | String                                   | Required |
| transaction\_details | The details of the specific transaction such as `order_id` and `gross_amount`. | [Object](https://docs.midtrans.com/reference/transaction-details-object) | Required |
| cstore               | Details of the convenience store.                                              | [Object](https://docs.midtrans.com/reference/convenience-store-object)   | Required |
| customer\_details    | Details of the customer.                                                       | [Object](https://docs.midtrans.com/reference/customer-details-object)    | Optional |
| item\_details        | Details of the item(s) purchased by the customer.                              | [Object](https://docs.midtrans.com/reference/item-details-object)        | Optional |

<br />

***

<br />

## Indomaret Charge Response and Notifications

<br />

```json Success
{
  "status_code": "201",
  "status_message": "Success, cstore transaction is successful",
  "transaction_id": "e3f0b1b5-1941-4ffb-9083-4ee5a96d878a",
  "order_id": "order04",
  "gross_amount": "162500.00",
  "payment_type": "cstore",
  "transaction_time": "2016-06-19 17:18:07",
  "transaction_status": "pending",
  "payment_code": "25709650945026",
  "expiry_time": "2017-01-09 09:56:44"
}
```
```json Pending
{
  "status_code": "201",
  "status_message": "midtrans payment notification",
  "transaction_id": "e3f0b1b5-1941-4ffb-9083-4ee5a96d878a",
  "order_id": "order04",
  "gross_amount": "162500.00",
  "payment_type": "cstore",
  "transaction_time": "2016-06-19 17:18:07",
  "transaction_status": "pending",
  "signature_key": "2d488c1ff0adc2396ee9b9765807b6d53182a0aa17cd9bb251b99879099d4f727903a75440b1814539f565774f7a80de0a7336c81d2071b4d3efe92f15400e41",
  "payment_code": "25709650945026",
  "store": "indomaret",
  "expiry_time": "2017-01-09 09:56:44"
}
```
```json Settlement
{
  "status_code": "200",
  "status_message": "midtrans payment notification",
  "transaction_id": "991af93c-1049-4973-b38f-d6052c72e367",
  "order_id": "order04",
  "gross_amount": "162500.00",
  "payment_type": "cstore",
  "transaction_time": "2016-06-20 11:44:07",
  "transaction_status": "settlement",
  "approval_code": "59061607081045705101",
  "signature_key": "a198f93ac43cf98171dcb4bd0323c7e3afbee77a162a09e2381f0a218c761a4ef0254d7650602971735c486fea2e8e9c6d41ee65d6a53d65a12fb1c824e86f9f",
  "payment_code": "25709650945026",
  "store": "indomaret",
  "expiry_time": "2017-01-09 09:56:44"
}
```
```json Expired
{
  "status_code": "202",
  "status_message": "midtrans payment notification",
  "transaction_id": "fd70880f-3458-4b16-9f09-289924185977",
  "order_id": "order04",
  "gross_amount": "162500.00",
  "payment_type": "cstore",
  "transaction_time": "2016-06-20 17:18:08",
  "transaction_status": "expire",
  "signature_key": "c260504a448018b4c4831b381f8a8c5088c37f2706dcc60b4d7d99a16e0ae3c22bc8945cb5177742386bab1ddb12e7c175e1f57686b488e215406fa40fc75481",
  "payment_code": "25709650945026",
  "store": "indomaret",
  "expiry_time": "2017-01-09 09:56:44"
}
```

| JSON Attribute      | Description                                                                                                                                                                                   | Type   |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| status\_code        | Status code of transaction charge result.                                                                                                                                                     | String |
| status\_message     | Message describing the status of the result of API request.                                                                                                                                   | String |
| transaction\_id     | Transaction ID given by Midtrans.                                                                                                                                                             | String |
| order\_id           | Order ID specified by merchant.                                                                                                                                                               | String |
| gross\_amount       | Total amount of transaction in IDR.                                                                                                                                                           | String |
| payment\_type       | Payment method used by the customer. Value: `cstore`.                                                                                                                                         | String |
| transaction\_time   | Timestamp of transaction in ISO 8601 format. Time Zone (GMT+7).                                                                                                                               | String |
| transaction\_status | Transaction status of the Indomaret transaction. Possible values are `pending`, `settlement`, and `expire`.                                                                                   | String |
| signature\_key      | Special string to verify the integrity of the response. For more details, refer [Verifying Notification Authenticity](/docs/https-notification-webhooks#verifying-notification-authenticity). | String |
| payment\_code       | Unique payment code for the customer to complete the payment in Indomaret.                                                                                                                    | String |
| store               | Convenience store identifier.                                                                                                                                                                 | String |

<br />

> 📘 Note
>
> Possible error codes are **400**, **401**, **402**, **406**, **410**

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "info": {
    "title": "core-api-indomaret",
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
        "summary": "Indomaret",
        "description": "",
        "operationId": "indomaret-1",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "required": [
                  "payment_type",
                  "transaction_details",
                  "cstore",
                  "customer_details"
                ],
                "properties": {
                  "payment_type": {
                    "type": "string",
                    "default": "cstore"
                  },
                  "transaction_details": {
                    "type": "object",
                    "required": [
                      "order_id"
                    ],
                    "properties": {
                      "order_id": {
                        "type": "string",
                        "default": "order_id-02134"
                      },
                      "gross_amount": {
                        "type": "integer",
                        "default": 100000,
                        "format": "int32"
                      }
                    }
                  },
                  "cstore": {
                    "type": "object",
                    "required": [
                      "store"
                    ],
                    "properties": {
                      "store": {
                        "type": "string",
                        "default": "indomaret"
                      }
                    }
                  },
                  "item_details": {
                    "type": "array",
                    "items": {
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
                      },
                      "required": [
                        "quantity",
                        "name"
                      ],
                      "type": "object"
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
                        "default": "0811223344"
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
                    "value": "{\n  \"status_code\": \"201\",\n  \"status_message\": \"Success, cstore transaction is successful\",\n  \"transaction_id\": \"e3f0b1b5-1941-4ffb-9083-4ee5a96d878a\",\n  \"order_id\": \"order04\",\n  \"gross_amount\": \"162500.00\",\n  \"payment_type\": \"cstore\",\n  \"transaction_time\": \"2016-06-19 17:18:07\",\n  \"transaction_status\": \"pending\",\n  \"payment_code\": \"25709650945026\"\n}"
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
                      "example": "Success, cstore transaction is successful"
                    },
                    "transaction_id": {
                      "type": "string",
                      "example": "e3f0b1b5-1941-4ffb-9083-4ee5a96d878a"
                    },
                    "order_id": {
                      "type": "string",
                      "example": "order04"
                    },
                    "gross_amount": {
                      "type": "string",
                      "example": "162500.00"
                    },
                    "payment_type": {
                      "type": "string",
                      "example": "cstore"
                    },
                    "transaction_time": {
                      "type": "string",
                      "example": "2016-06-19 17:18:07"
                    },
                    "transaction_status": {
                      "type": "string",
                      "example": "pending"
                    },
                    "payment_code": {
                      "type": "string",
                      "example": "25709650945026"
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