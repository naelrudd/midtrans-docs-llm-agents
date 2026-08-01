---
updatedAt: 2025-11-10T22:59:36.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Charge Transactions

Midtrans provides facility to add more features to Charge Transaction. Using these features, you can -

* Set custom fields
* Set custom expiry
* Add metadata\
  The subsequent sections explain these features in detail.

<br />

***

## Set Custom Field

Set Custom Fields is a feature that enables you to charge a transaction with unique data according to your need. Midtrans provides three custom fields to save custom data about the transaction.

The steps to set these custom fields are given below.

1. Set Custom field label on MAP.

* Login to your [MAP account](https://dashboard.midtrans.com).
* On the Dashboard, go to **Settings** > **General Settings** > **Interface Settings**.
* Enter custom text in **Custom field 1 label**, **Custom field 2 label**, **Custom field 3 label**.
* Click **Save**.

2. Send Charge API request with the custom fields value.
3. The label and value of the custom fields can be checked using the Order ID of a transaction.
4. Midtrans sends HTTP POST Notification with these custom fields to **Payment Notification URL** specified on MAP.

```json Sample Request
{
  "payment_type": "bank_transfer",
  "bank_transfer": {
    "bank": "permata"
  },
  "transaction_details": {
    "order_id": "C17550",
    "gross_amount": 145000
  },
  "custom_field1": "custom field 1 content",
  "custom_field2": "custom field 2 content",
  "custom_field3": "custom field 3 content"
}
```
```json Sample Response
{
    "status_code": "200",
    "status_message": "Success, Credit Card transaction is successful",
    "transaction_id": "1eae238a-cb9e-4f92-b284-aac8b39e4eab",
    "order_id": "C17550",
    "gross_amount": "145000.00",
    "payment_type": "credit_card",
    "transaction_time": "2016-06-28 09:42:20",
    "transaction_status": "capture",
    "fraud_status": "accept",
    "approval_code": "256084",
    "masked_card": "48111111-1114",
    "bank": "bni"
}
```

### Set Custom Field Notifications

```json Sample Reponse
{
  "masked_card": "48111111-1114",
  "approval_code": "256084",
  "bank": "bni",
  "transaction_time": "2016-06-28 09:42:20",
  "custom_field1": "Toko Rani",
  "custom_field2": "Jakarta",
  "custom_field3": "RR",
  "gross_amount": "10000.00",
  "order_id": "C17550",
  "payment_type": "credit_card",
  "signature_key": "ad7ccda03d8ec6f2f415661fb511d47fcd17dcc7d7e1ade96a305dd5d3bc2bea5438a8bdfe1aeedabdefb226000338ac169fc18d5ae73788fd5e78dbac945ce4",
  "status_code": "200",
  "transaction_id": "1eae238a-cb9e-4f92-b284-aac8b39e4eab",
  "transaction_status": "capture",
  "fraud_status": "accept",
  "status_message": "midtrans payment notification"
}
```

| JSON Attribute | Description                  | Type        |
| -------------- | ---------------------------- | ----------- |
| custom\_field1 | The value of custom field 1. | String(255) |
| custom\_field2 | The value of custom field 2. | String(255) |
| custom\_field3 | The value of custom field 3. | String(255) |

<br />

***

## Set Custom Expiry

```json Set Custom Expiry
{
  "payment_type": "bank_transfer",
  "bank_transfer": {
    "bank": "permata"
  },
  "transaction_details": {
    "order_id": "C17550",
    "gross_amount": 145000
  },
  "custom_expiry": {
      "order_time": "2016-12-07 11:54:12 +0700",
      "expiry_duration": 60,
      "unit": "minute"
  }
}
```

Set Custom Expiry feature enables you to set an expiry time for the payment of every transaction with `transaction_status:pending`. The list of payment methods, with `transaction_status:pending` is given below.

* Bank Transfer: [Permata Virtual Account](https://docs.midtrans.com/reference/permata-virtual-account), [BCA Virtual Account](https://docs.midtrans.com/reference/bca-virtual-account), [Mandiri Bill Payment](https://docs.midtrans.com/reference/mandiri-bill-payment), [BNI Virtual Account](https://docs.midtrans.com/reference/bni-virtual-account), [BRI Virtual Account](https://docs.midtrans.com/reference/bri-virtual-account)
* Direct Debit: [BCA KlikPay](https://docs.midtrans.com/reference/bca-klikpay), [KlikBCA](https://docs.midtrans.com/reference/klikbca), [BRImo](/reference/brimo-1), [CIMB Clicks](https://docs.midtrans.com/reference/cimb-clicks), [Danamon Online Banking](https://docs.midtrans.com/reference/danamon-online-banking), [UOB Ezpay](https://docs.midtrans.com/reference/uob-ezpay)
* E-money: [QRIS](https://docs.midtrans.com/reference/qris), [GoPay](https://docs.midtrans.com/reference/gopay), [ShopeePay](https://docs.midtrans.com/reference/shopeepay)
* Over the Counter: [Indomaret](https://docs.midtrans.com/reference/indomaret), [Alfamart](https://docs.midtrans.com/reference/alfamart)
* Cardless Credit: [Akulaku](/reference/akulaku-1), [Kredivo](https://docs.midtrans.com/reference/kredivo)

The transaction is rejected if the custom expiry exceeds the allowed maximum time.

See [Custom Expiry Object](https://docs.midtrans.com/reference/custom-expiry-object) for reference.

> 📘 Note
>
> * For QRIS with acquirer AirPay (Shopee) and ShopeePay, the allowed maximum time of expiry is 5 days.
> * For Gopay, the allowed maximum time of expiry is 7 days.

<br />

***

## Set Metadata

Set Metadata is similar to Set Custom Field which enables you to put free-form JSON object instead of String. You can use this metadata as a transaction tag and retrieve it using [Get Status](https://docs.midtrans.com/reference/get-transaction-status) or HTTP Notifications URL. Additionally, you can also configure the fraud detection rules based on the metadata fields.

```json Sample Request - Set Metadata Charge
{
  "payment_type": "bank_transfer",
  "bank_transfer": {
    "bank": "permata"
  },
  "transaction_details": {
    "order_id": "C17550",
    "gross_amount": 145000
  },
  "metadata": {
    "you": "can",
    "put": "any",
    "parameter": "you like"
  }
}
```
```json Sample Response - Success
{
    "status_code": "200",
    "status_message": "Success, Credit Card transaction is successful",
    "transaction_id": "1eae238a-cb9e-4f92-b284-aac8b39e4eab",
    "order_id": "C17550",
    "gross_amount": "145000.00",
    "payment_type": "credit_card",
    "transaction_time": "2016-06-28 09:42:20",
    "transaction_status": "capture",
    "fraud_status": "accept",
    "approval_code": "256084",
    "masked_card": "48111111-1114",
    "bank": "bni"
}
```
```json Sample Response - Notification
{
  "masked_card": "48111111-1114",
  "approval_code": "256084",
  "bank": "bni",
  "transaction_time": "2016-06-28 09:42:20",
  "gross_amount": "10000.00",
  "order_id": "C17550",
  "payment_type": "credit_card",
  "signature_key": "ad7ccda03d8ec6f2f415661fb511d47fcd17dcc7d7e1ade96a305dd5d3bc2bea5438a8bdfe1aeedabdefb226000338ac169fc18d5ae73788fd5e78dbac945ce4",
  "status_code": "200",
  "transaction_id": "1eae238a-cb9e-4f92-b284-aac8b39e4eab",
  "transaction_status": "capture",
  "fraud_status": "accept",
  "status_message": "midtrans payment notification",
  "metadata": {
    "you": "can",
    "put": "any",
    "parameter": "you like"
  }
}
```

| JSON Attribute | Description                                | Type        |
| -------------- | ------------------------------------------ | ----------- |
| metadata       | Object containing the metadata parameters. | JSON Object |

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
    "/v2/charge": {
      "post": {
        "summary": "Charge Transactions",
        "description": "",
        "operationId": "charge-transactions-1",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "required": [
                  "payment_type",
                  "transaction_details"
                ],
                "properties": {
                  "payment_type": {
                    "type": "string",
                    "default": "gopay"
                  },
                  "transaction_details": {
                    "type": "object",
                    "properties": {
                      "order_id": {
                        "type": "string",
                        "default": "order-id-123"
                      },
                      "gross_amount": {
                        "type": "integer",
                        "default": 100000,
                        "format": "int32"
                      }
                    }
                  },
                  "item_details": {
                    "type": "array",
                    "items": {
                      "properties": {
                        "id": {
                          "type": "string",
                          "default": "id1"
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
                          "default": "name"
                        }
                      },
                      "type": "object"
                    }
                  },
                  "customer_details": {
                    "type": "object",
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
                        "default": "081223323423"
                      },
                      "customer_details_required_fields": {
                        "type": "array",
                        "default": [
                          "email",
                          "first_name",
                          "phone"
                        ],
                        "items": {
                          "type": "string"
                        }
                      }
                    }
                  },
                  "custom_field1": {
                    "type": "string",
                    "default": "custom field 1 content"
                  },
                  "custom_field2": {
                    "type": "string",
                    "default": "custom field 2 content"
                  },
                  "custom_field3": {
                    "type": "string",
                    "default": "custom field 3 content"
                  },
                  "custom_expiry": {
                    "type": "object",
                    "properties": {
                      "expiry_duration": {
                        "type": "integer",
                        "default": 60,
                        "format": "int32"
                      },
                      "unit": {
                        "type": "string",
                        "default": "minute"
                      }
                    }
                  },
                  "metadata": {
                    "type": "object",
                    "properties": {
                      "you": {
                        "type": "string",
                        "default": "can"
                      },
                      "put": {
                        "type": "string",
                        "default": "any"
                      },
                      "parameter": {
                        "type": "string",
                        "default": "you like"
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
                    "value": "{\n  \"status_code\": \"201\",\n  \"status_message\": \"QRIS transaction is created\",\n  \"transaction_id\": \"30a689ba-7251-4052-b8a0-f677fd53e1be\",\n  \"order_id\": \"order-id-12312\",\n  \"merchant_id\": \"G379181825\",\n  \"gross_amount\": \"100000.00\",\n  \"currency\": \"IDR\",\n  \"payment_type\": \"qris\",\n  \"transaction_time\": \"2023-01-05 10:01:39\",\n  \"transaction_status\": \"pending\",\n  \"fraud_status\": \"accept\",\n  \"actions\": [\n    {\n      \"name\": \"generate-qr-code\",\n      \"method\": \"GET\",\n      \"url\": \"https://api.sandbox.midtrans.com/v2/qris/30a689ba-7251-4052-b8a0-f677fd53e1be/qr-code\"\n    }\n  ],\n  \"qr_string\": \"00020101021226620014COM.GO-JEK.WWW011993600914337918182570210G3791818250303UKE51440014ID.CO.QRIS.WWW0215AID7720513752290303UKE5204359353033605802ID5910PAPI LIVE26005KUKAR6105755535409100000.0062475036b1855b6c-70ab-4449-9778-61b8ffe43fd20703A016304C385\",\n  \"acquirer\": \"gopay\",\n  \"expire_time\": \"2023-01-05 11:01:39\"\n}"
                  },
                  "Duplicate order ID": {
                    "value": "{\n    \"status_code\": \"406\",\n    \"status_message\": \"The request could not be completed due to a conflict with the current state of the target resource, please try again\",\n    \"id\": \"2e7d71d2-8f72-4c31-91a5-36731edd0b71\"\n}"
                  }
                },
                "schema": {
                  "oneOf": [
                    {
                      "type": "object",
                      "properties": {
                        "status_code": {
                          "type": "string",
                          "example": "201"
                        },
                        "status_message": {
                          "type": "string",
                          "example": "QRIS transaction is created"
                        },
                        "transaction_id": {
                          "type": "string",
                          "example": "30a689ba-7251-4052-b8a0-f677fd53e1be"
                        },
                        "order_id": {
                          "type": "string",
                          "example": "order-id-12312"
                        },
                        "merchant_id": {
                          "type": "string",
                          "example": "G379181825"
                        },
                        "gross_amount": {
                          "type": "string",
                          "example": "100000.00"
                        },
                        "currency": {
                          "type": "string",
                          "example": "IDR"
                        },
                        "payment_type": {
                          "type": "string",
                          "example": "qris"
                        },
                        "transaction_time": {
                          "type": "string",
                          "example": "2023-01-05 10:01:39"
                        },
                        "transaction_status": {
                          "type": "string",
                          "example": "pending"
                        },
                        "fraud_status": {
                          "type": "string",
                          "example": "accept"
                        },
                        "actions": {
                          "type": "array",
                          "items": {
                            "type": "object",
                            "properties": {
                              "name": {
                                "type": "string",
                                "example": "generate-qr-code"
                              },
                              "method": {
                                "type": "string",
                                "example": "GET"
                              },
                              "url": {
                                "type": "string",
                                "example": "https://api.sandbox.midtrans.com/v2/qris/30a689ba-7251-4052-b8a0-f677fd53e1be/qr-code"
                              }
                            }
                          }
                        },
                        "qr_string": {
                          "type": "string",
                          "example": "00020101021226620014COM.GO-JEK.WWW011993600914337918182570210G3791818250303UKE51440014ID.CO.QRIS.WWW0215AID7720513752290303UKE5204359353033605802ID5910PAPI LIVE26005KUKAR6105755535409100000.0062475036b1855b6c-70ab-4449-9778-61b8ffe43fd20703A016304C385"
                        },
                        "acquirer": {
                          "type": "string",
                          "example": "gopay"
                        },
                        "expire_time": {
                          "type": "string",
                          "example": "2023-01-05 11:01:39"
                        }
                      }
                    },
                    {
                      "title": "Duplicate order ID",
                      "type": "object",
                      "properties": {
                        "status_code": {
                          "type": "string",
                          "example": "406"
                        },
                        "status_message": {
                          "type": "string",
                          "example": "The request could not be completed due to a conflict with the current state of the target resource, please try again"
                        },
                        "id": {
                          "type": "string",
                          "example": "2e7d71d2-8f72-4c31-91a5-36731edd0b71"
                        }
                      }
                    }
                  ]
                }
              }
            }
          },
          "400": {
            "description": "400",
            "content": {
              "application/json": {
                "examples": {
                  "Result": {
                    "value": "{\n    \"status_code\": \"400\",\n    \"status_message\": \"One or more parameters in the payload is invalid.\",\n    \"validation_messages\": [\n        \"transaction_details.order_id is required\"\n    ],\n    \"id\": \"301c2013-7329-4155-a1c2-a302fed6ded7\"\n}"
                  }
                },
                "schema": {
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
                        "example": "transaction_details.order_id is required"
                      }
                    },
                    "id": {
                      "type": "string",
                      "example": "301c2013-7329-4155-a1c2-a302fed6ded7"
                    }
                  }
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
          },
          "429": {
            "description": "429",
            "content": {
              "application/json": {
                "examples": {
                  "API rate limit exceeded": {
                    "value": "{\"message\":\"API rate limit exceeded\"}"
                  }
                },
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "example": "API rate limit exceeded"
                    }
                  }
                }
              }
            }
          }
        },
        "deprecated": false,
        "x-readme": {
          "code-samples": [
            {
              "language": "markdown",
              "code": "\n"
            }
          ],
          "samples-languages": [
            "markdown"
          ]
        }
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