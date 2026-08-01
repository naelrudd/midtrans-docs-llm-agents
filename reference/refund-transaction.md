---
updatedAt: 2026-04-01T11:20:49.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Refund Transactions

Refund transaction is called to reverse the money back to customers for transactions with payment status `Settlement`. If transaction's status is still `Pending` `Authorize` or `Capture` please use Cancel API instead.

We will use `refund_key` as the unique identifier from merchant. If you want to do retry the same refund request please use the same `refund_key`, but if you want to create a new refund request please use the new `refund_key`. If you don't sent us the `refund_key` we will treat it as a new request and generate the `refund_key` from our side.

Refund transaction is supported only for `credit_card` , `gopay`, `shopeepay` ,`dana`,`ovo`, `QRIS` , `kredivo` and `akulaku` payment methods.

With Refund, refund request is made to Midtrans where Midtrans will then forward it to payment providers.

<br />

Notes on the specific non-GoPay max refund window:

* ShopeePay (QRIS and JumpApp) : 365 days
* Kredivo : 14 days
* DANA : 45 days
* OVO : 7 days for regular merchants, 180 days for OTA merchants

<br />

Max refund window for GoPay :

* QRIS ON-US (*acquirers GoPay x issuer Gopay*) : 45 days
* QRIS OFF-US (*acquirers GoPay x issuer Other Player*) : 7 days
* GoPay Tokenization : 180 days
* GoPay Deeplink : 45 days
* Other GoPay transactions: 180 days

<br />

Refund API can be used in both Core API and Snap integrations. If Refund capabilities is not available for you, please [request for activation](https://midtrans.com/contact-us/transaction-information/prosedur-refund-pengembalian-dana) to Midtrans's support team.

<br />

> 📘 Direct Refund Notice
>
> Merchant can now just use 1 refund endpoint `/refund` for all refund usecases. [Direct Refund](/reference/direct-refund-transaction) endpoint however can still be used for existing merchants.

<br />

***

<br />

## Refund Transaction Method

<br />

| HTTP Method | Endpoint                                                | Definition         |
| ----------- | ------------------------------------------------------- | ------------------ |
| POST        | BASE\_URL/v2/\{order\_id **OR** transaction\_id}/refund | Refund Transaction |

<br />

> 🚧 Refunding GoPay Static QRIS transaction
>
> **Starting January 2024**, GoPay Static QRIS transaction can only be refunded by passing the Midtrans transaction ID (transaction\_id) on the refund API call. Please ensure that your system can accommodate this change.

***

## Refund Transaction Request

<br />

See sample on the right -- try it yourself!

<br />

```json Sample Request - Refund Charge
{
  "refund_key": "reference1",
  "amount": 5000,
  "reason": "for some reason"
}
```

<Table align={["left","left","left","left"]}>
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
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        refund_key
      </td>

      <td>
        Merchant refund ID. If not passed then Midtrans creates a new one. It is recommended to use this parameter to avoid double refund attempt. Allowed characters are alphabets, numbers, dash (`-`), and underscore (`_`). <br /> <br /> In the case where merchant needs to reattempt a refund with the same refund key, the reattempt can only be done max 7 days after the first refund attempt. After 7 days, the same refund key cannot be used anymore and merchant needs to use a new refund key to initiate a refund. <br /><br /> Reattempt of refunds may be needed if the previous attempt failed due to a retriable error (e.g insufficient merchant balance).
      </td>

      <td>
        String
      </td>

      <td>
        Optional
      </td>
    </tr>

    <tr>
      <td>
        amount
      </td>

      <td>
        Amount to be refunded. By default whole transaction amount is refunded. Note :  
        `Shopeepay` and `OVO` does not support partial refund at the moment.
      </td>

      <td>
        Long
      </td>

      <td>
        Optional
      </td>
    </tr>

    <tr>
      <td>
        reason
      </td>

      <td>
        Reason justifying the refund. <br /> <hr />For GoPay & GoPay Tokenization payments, reason will be shown on customers' GoPay transaction history. <br /> <hr />Reason is mandatory for card payment with BNI as acquiring bank. If the value is not sent, Midtrans will autofill it with "refund request from merchant" to BNI.
      </td>

      <td>
        String(255)
      </td>

      <td>
        Optional
      </td>
    </tr>
  </tbody>
</Table>

<br />

***

<br />

## Refund Transaction Response and Notification

<br />

### Sample Response

<br />

```json Success
{
  "status_code": "200",
  "status_message": "Success, refund request is approved",
  "transaction_id": "447e846a-403e-47db-a5da-d7f3f06375d6",
  "order_id": "vtcc05",
  "payment_type": "credit_card",
  "transaction_time": "2015-06-15 13:36:24",
  "transaction_status": "refund",
  "gross_amount": "10000.00",
  "refund_chargeback_id": 1,
  "refund_amount": "10000.00",
  "refund_key": "reference1",
  "payer_phone_number" : "081111111", // only applicable for OVO as payment method
  "merchant_invoice" : "INV20251112001" // only applicable for OVO as payment method
}
```
```json Success (Partial Refund)
{
  "status_code": "200",
  "status_message": "Success, refund request is approved",
  "transaction_id": "447e846a-403e-47db-a5da-d7f3f06375d6",
  "order_id": "vtcc05",
  "payment_type": "credit_card",
  "transaction_time": "2015-06-15 13:36:24",
  "transaction_status": "partial_refund",
  "gross_amount": "10000.00",
  "refund_chargeback_id": 1,
  "refund_amount": "5000.00",
  "refund_key": "reference1"
}
```
```json Error (Invalid Refund)
{
  "status_code" : "412",
  "status_message" : "Merchant cannot modify the status of the transaction"
}
```
```json Error (Invalid Amount)
{
  "status_code" : "414",
  "status_message" : "Refund request is rejected due to invalid amount"
}
```
```json Error (Invalid Refund ID)
{
  "status_code" : "406",
  "status_message" : "Duplicate refund ID"
}
```
```json Notification
{
  "status_code" : "200",
  "status_message" : "midtrans payment notification",
  "transaction_id" : "249fc620-6017-4540-af7c-5a1c25788f46",
  "masked_card" : "48111111-1114",
  "order_id" : "example-1424936368",
  "payment_type" : "credit_card",
  "transaction_time" : "2021-02-26 14:39:33",
  "transaction_status" : "partial_refund",
  "fraud_status" : "accept",
  "approval_code" : "1424936374393",
  "signature_key" : "2802a264cb978fbc59f631c68d120cbda8dc853f5dfdc52301c615cf4f14e7a0b09aa...",
  "bank" : "bni",
  "gross_amount" : "30000.00",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "card_type": "credit",
  "refund_amount": "12000.00",
  "refunds": [
    {
      "refund_chargeback_id": 1,
      "refund_amount": "5000.00",
      "created_at": "2015-02-27 00:14:20",
      "reason": "some reason",
      "refund_key": "reference1",
      "refund_method": "online"
    },
    {
      "refund_chargeback_id": 2,
      "refund_amount": "7000.00",
      "created_at": "2015-02-28 01:23:15",
      "reason": "",
      "refund_key": "reference2",
      "refund_method": "offline"
    },
  ]
}
```
```json Notification (Bank Confirmed)
{
  "status_code" : "200",
  "status_message" : "midtrans payment notification",
  "transaction_id" : "249fc620-6017-4540-af7c-5a1c25788f46",
  "masked_card" : "48111111-1114",
  "order_id" : "example-1424936368",
  "payment_type" : "credit_card",
  "transaction_time" : "2021-02-26 14:39:33",
  "transaction_status" : "partial_refund",
  "fraud_status" : "accept",
  "approval_code" : "1424936374393",
  "signature_key" : "2802a264cb978fbc59f631c68d120cbda8dc853f5dfdc52301c615cf4f14e7a0b09aa...",
  "bank" : "bni",
  "gross_amount" : "30000.00",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "card_type": "credit",
  "refund_amount": "12000.00",
  "refunds": [
    {
      "refund_chargeback_id": 1,
      "refund_amount": "5000.00",
      "created_at": "2015-02-27 00:14:20",
      "reason": "some reason",
      "refund_key": "reference1",
      "refund_method": "online",
      "bank_confirmed_at": "2015-02-27 02:30:20"
    },
    {
      "refund_chargeback_id": 2,
      "refund_amount": "7000.00",
      "created_at": "2015-02-28 01:23:15",
      "reason": "",
      "refund_key": "reference2",
      "refund_method": "offline",
      "bank_confirmed_at": "2015-02-27 02:30:20"
    },
  ]
}
```

| JSON Attribute         | Description                                                                                                                                                           | Type   |
| :--------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----- |
| status\_code           | Status code of transaction charge result.                                                                                                                             | String |
| status\_message        | Description of transaction charge result.                                                                                                                             | String |
| transaction\_id        | Transaction ID given by Midtrans.                                                                                                                                     | String |
| order\_id              | Order ID specified by you.                                                                                                                                            | String |
| payment\_type          | The payment method used by the customer.                                                                                                                              | String |
| transaction\_time      | Timestamp of transaction in ISO 8601 format. Time Zone: GMT+7.                                                                                                        | String |
| transaction\_status    | Transaction status after refund action. Possible values are<br />`refund` : Transaction is fully refunded. <br />`partial_refund`: transaction is partially refunded. | String |
| gross\_amount          | Total amount of transaction in IDR.                                                                                                                                   | String |
| refund\_chargeback\_id | Identification of the refund process.                                                                                                                                 | String |
| refund\_amount         | Total amount to be refunded in IDR.                                                                                                                                   | String |
| refund\_key            | Merchant refund reference key.                                                                                                                                        | String |
| payer\_phone\_number   | Customer's phone number that used to create payment request to payment provider.                                                                                      | String |
| merchant\_invoice      | Unique identifier for payment provider specific request.                                                                                                              | String |

For notification JSON attributes, please follow the description on [Get Status Response](https://docs.midtrans.com/reference/get-transaction-status).

<Callout icon="📘" theme="info">
  Midtrans will return 2 refund post notifications to merchant - without and with **bank_confirmed_at**. We suggest for merchant to use the later refund post notification with **bank_confirmed_at** to mark the refund has been succesfully confirmed by the bank/payment providers.
</Callout>

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
    "/v2/{order_id}/refund": {
      "post": {
        "summary": "Copy of Refund Transactions",
        "description": "",
        "operationId": "post_v2order_idrefund-1",
        "parameters": [
          {
            "in": "path",
            "name": "order_id",
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
                "properties": {
                  "refund_key": {
                    "type": "string",
                    "default": "reference1"
                  },
                  "amount": {
                    "type": "integer",
                    "default": 5000,
                    "format": "int32"
                  },
                  "reason": {
                    "type": "string",
                    "default": "for some reason"
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
                    "value": "{\n  \"status_code\": \"200\",\n  \"status_message\": \"Success, refund request is approved\",\n  \"transaction_id\": \"447e846a-403e-47db-a5da-d7f3f06375d6\",\n  \"order_id\": \"vtcc05\",\n  \"payment_type\": \"credit_card\",\n  \"transaction_time\": \"2015-06-15 13:36:24\",\n  \"transaction_status\": \"refund\",\n  \"gross_amount\": \"10000.00\",\n  \"refund_chargeback_id\": 1,\n  \"refund_amount\": \"10000.00\",\n  \"refund_key\": \"reference1\"\n}"
                  },
                  "Error - Invalid Refund": {
                    "value": "{\n  \"status_code\" : \"412\",\n  \"status_message\" : \"Merchant cannot modify the status of the transaction\"\n}"
                  },
                  "Error - Invalid Amount": {
                    "value": "{\n  \"status_code\" : \"414\",\n  \"status_message\" : \"Refund request is rejected due to invalid amount\"\n}"
                  },
                  "Error - Invalid Refund ID": {
                    "value": "{\n  \"status_code\" : \"406\",\n  \"status_message\" : \"Duplicate refund ID\"\n}"
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
                          "example": "Success, refund request is approved"
                        },
                        "transaction_id": {
                          "type": "string",
                          "example": "447e846a-403e-47db-a5da-d7f3f06375d6"
                        },
                        "order_id": {
                          "type": "string",
                          "example": "vtcc05"
                        },
                        "payment_type": {
                          "type": "string",
                          "example": "credit_card"
                        },
                        "transaction_time": {
                          "type": "string",
                          "example": "2015-06-15 13:36:24"
                        },
                        "transaction_status": {
                          "type": "string",
                          "example": "refund"
                        },
                        "gross_amount": {
                          "type": "string",
                          "example": "10000.00"
                        },
                        "refund_chargeback_id": {
                          "type": "integer",
                          "example": 1,
                          "default": 0
                        },
                        "refund_amount": {
                          "type": "string",
                          "example": "10000.00"
                        },
                        "refund_key": {
                          "type": "string",
                          "example": "reference1"
                        }
                      }
                    },
                    {
                      "title": "Error - Invalid Refund",
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
                    },
                    {
                      "title": "Error - Invalid Amount",
                      "type": "object",
                      "properties": {
                        "status_code": {
                          "type": "string",
                          "example": "414"
                        },
                        "status_message": {
                          "type": "string",
                          "example": "Refund request is rejected due to invalid amount"
                        }
                      }
                    },
                    {
                      "title": "Error - Invalid Refund ID",
                      "type": "object",
                      "properties": {
                        "status_code": {
                          "type": "string",
                          "example": "406"
                        },
                        "status_message": {
                          "type": "string",
                          "example": "Duplicate refund ID"
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