---
updatedAt: 2025-11-10T23:00:13.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Direct Refund Transaction

> 📘 Direct Refund Notice
>
> Merchant can now just use 1 refund endpoint `/refund` for all refund usecases. [Direct Refund](/reference/direct-refund-transaction) endpoint however can still be used for existing merchants.

<br />

<br />

Unlike the [Refund Transaction](https://docs.midtrans.com/reference/refund-transaction), Direct Refund transaction is triggered to send the refund request directly to the bank or to the third-party payment provider for transaction with payment status `Settlement`. If payment status is still in either `Capture`, `Pending` or `Authorize`, use the Cancel API instead.  This method is faster than the standard operation process which may take one to two days, after the initial refund request. The status of corresponding transaction is updated immediately after receiving refund result from the third-party payment provider. HTTP notification is sent only if the refund is successful. Do note that some payment method only supports refunding via [Refund API](/reference/refund-transaction), and vice versa.

Direct Refund transaction is only supported for GoPay, QRIS, ShopeePay, Credit Card, Akulaku and Kredivo payment methods. Currently for Credit Card payment method, Midtrans only supports BCA, MAYBANK, BNI (via Cybersource) and BRI acquiring banks.

For QRIS with acquirers AirPay (Shopee) and ShopeePay, the maximum refund window is 365 days since the transaction is paid. Refund is not allowed from 11:55 PM to 6:00 AM GMT+7. If you send Direct Refund during this timeframe, the request gets rejected by ShopeePay. For Kredivo, the maximum refund window is 14 days.

While the maximum refund window for GoPay is as stated below:

* QRIS with acquirers GoPay: 45 days
* GoPay Tokenization and GoPay deeplink with GoPay payment option GOPAY\_COINS: 90 days
* Other GoPay transactions: 180 days

Direct Refund API can be used in both Core API and Snap integrations. If Refund capabilities is not available for you, please [request for activation](https://midtrans.com/contact-us/transaction-information/prosedur-refund-pengembalian-dana) to Midtrans's support team.

<br />

***

## Direct Refund Transaction Method

<br />

| HTTP Method | Endpoint                                                             | Definition                |
| ----------- | -------------------------------------------------------------------- | ------------------------- |
| POST        | BASE\_URL/v2/`{order_id **OR** transaction_id}`/refund/online/direct | Direct Refund Transaction |

<br />

***

## Direct Refund Transaction Request

<br />

See sample on the right -- try it yourself!

```json Sample Request - Direct Refund Charge
{
  "refund_key": "reference1",
  "amount": 5000,
  "reason": "for some reason"
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

      <th>
        Required
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        refund\_key
      </td>

      <td>
        Merchant refund ID. If not passed then Midtrans creates a new refund ID. It is recommended to use this parameter to avoid double refund attempt.  <br /> <br /> In the case where merchant needs to reattempt a refund with the same refund key, the reattempt can only be done max 7 days after the first refund attempt. After 7 days, the same refund key cannot be used anymore and merchant needs to use a new refund key to initiate a refund. <br /><br /> Reattempt of refunds may be needed if the previous attempt failed due to a retriable error (e.g insufficient merchant balance).
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
        Amount to be refunded. By default whole transaction amount is refund.
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
        Reason justifying the refund. <br /> For GoPay & GoPay Tokenization payments, reason will be shown on customers' GoPay transaction history.
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

## Direct Refund Transaction Response and Notifications

<br />

### Sample Response

<br />

```json Success
{
  "status_code": "200",
  "status_message": "Success, refund request is approved by the bank",
  "transaction_id": "fddb5889-fd39-46fe-809d-30679fe42434",
  "order_id": "MID-1620622357",
  "gross_amount": "10000.00",
  "payment_type": "credit_card",
  "transaction_time": "2016-06-28 09:42:20",
  "transaction_status": "refund",
  "refund_chargeback_id": 47594,
  "refund_amount": "10000.00",
  "refund_key": "01f1f771-b75c-48ef-b21d-193a79f8aa5b"
}
```
```json Rejected Direct Refund
{
  "status_code": "202",
  "status_message": "Refund denied by the bank",
  "transaction_id": "fddb5889-fd39-46fe-809d-30679fe42434",
  "order_id": "MID-1620622357",
  "gross_amount": "10000.00",
  "payment_type": "credit_card",
  "transaction_time": "2016-06-28 09:42:20",
  "transaction_status": "settlement",
  "refund_chargeback_id": 47594,
  "refund_amount": "0.00",
  "refund_key": "01f1f771-b75c-48ef-b21d-193a79f8aa5b"
}
```
```json Error (Invalid Direct Refund)
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
```json Error (Refund ID Already Exists)
{
  "status_code" : "406",
  "status_message" : "Duplicate refund ID"
}
```
```json Notification
{
  "status_code": "200",
  "status_message": "midtrans payment notification",
  "transaction_id": "841c7da8-530b-435a-9f67-c9d632d15537",
  "order_id": "1000176721005355",
  "gross_amount": "698879.00",
  "payment_type": "credit_card",
  "transaction_time": "2015-02-04 00:53:55",
  "transaction_status": "refund",
  "signature_key": "f1066b06ec8a4b7d6ffb941fd9772f6df304618e15e02cf17c2914cec12793e19c71653042f7f617b027eae6ecb6759529c67eca9af55264b736408d8b4df2b9",
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
```Text Notification (Bank Confirmed)
{
  "status_code": "200",
  "status_message": "midtrans payment notification",
  "transaction_id": "841c7da8-530b-435a-9f67-c9d632d15537",
  "order_id": "1000176721005355",
  "gross_amount": "698879.00",
  "payment_type": "credit_card",
  "transaction_time": "2015-02-04 00:53:55",
  "transaction_status": "refund",
  "signature_key": "f1066b06ec8a4b7d6ffb941fd9772f6df304618e15e02cf17c2914cec12793e19c71653042f7f617b027eae6ecb6759529c67eca9af55264b736408d8b4df2b9",
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
```json Notification (Refund Partial Amount)
{
  "status_code": "200",
  "status_message": "midtrans payment notification",
  "transaction_id": "841c7da8-530b-435a-9f67-c9d632d15537",
  "order_id": "1000176721005355",
  "gross_amount": "698879.00",
  "payment_type": "credit_card",
  "transaction_time": "2016-07-04 00:53:55",
  "transaction_status": "partial_refund",
  "signature_key": "f1066b06ec8a4b7d6ffb941fd9772f6df304618e15e02cf17c2914cec12793e19c71653042f7f617b027eae6ecb6759529c67eca9af55264b736408d8b4df2b9"
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
        Transaction status after refund action. Possible values are<br/>`refund` : Transaction is fully refunded. <br/>`partial_refund`: transaction is partially refunded.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        status\_code
      </td>

      <td>
        Status code of transaction charge result.
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
        Description of transaction charge result.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        refund\_chargeback\_id
      </td>

      <td>
        Identification of the refund process.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        refund\_amount
      </td>

      <td>
        Cumulative amount refunded.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        refund\_key
      </td>

      <td>
        Merchant refund reference. Allowed characters are alphabets, numbers, dash (`-`), and underscore (`_`).
      </td>

      <td>
        String
      </td>
    </tr>
  </tbody>
</Table>

<br />

> 📘
>
> Midtrans will return 2 refund post notifications to merchant - without and with **bank\_confirmed\_at**. We suggest for merchant to use the later refund post notification with **bank\_confirmed\_at** to mark the refund has been succesfully confirmed by the bank/payment providers.

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
    "/v2/{order_id}/refund/online/direct": {
      "post": {
        "summary": "Direct Refund Transaction",
        "description": "",
        "operationId": "direct-refund-transaction",
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
                    "type": "string",
                    "default": "5000"
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
                    "value": "{\n  \"status_code\": \"200\",\n  \"status_message\": \"Success, refund request is approved by the bank\",\n  \"transaction_id\": \"fddb5889-fd39-46fe-809d-30679fe42434\",\n  \"order_id\": \"MID-1620622357\",\n  \"gross_amount\": \"10000.00\",\n  \"payment_type\": \"credit_card\",\n  \"transaction_time\": \"2016-06-28 09:42:20\",\n  \"transaction_status\": \"refund\",\n  \"refund_chargeback_id\": 47594,\n  \"refund_amount\": \"10000.00\",\n  \"refund_key\": \"01f1f771-b75c-48ef-b21d-193a79f8aa5b\"\n}"
                  },
                  "Error Validation - Invalid Direct Refund": {
                    "value": "{\n  \"status_code\" : \"412\",\n  \"status_message\" : \"Merchant cannot modify the status of the transaction\"\n}"
                  },
                  "Error Validation - Invalid Refund Amount": {
                    "value": "{\n  \"status_code\" : \"414\",\n  \"status_message\" : \"Refund request is rejected due to invalid amount\"\n}"
                  },
                  "Error Validation - Refund Already Exist": {
                    "value": "{\n  \"status_code\" : \"406\",\n  \"status_message\" : \"Duplicate refund ID\"\n}"
                  },
                  "Rejected Direct Refund": {
                    "value": "{\n  \"status_code\": \"202\",\n  \"status_message\": \"Refund denied by the bank\",\n  \"transaction_id\": \"fddb5889-fd39-46fe-809d-30679fe42434\",\n  \"order_id\": \"MID-1620622357\",\n  \"gross_amount\": \"10000.00\",\n  \"payment_type\": \"credit_card\",\n  \"transaction_time\": \"2016-06-28 09:42:20\",\n  \"transaction_status\": \"settlement\",\n  \"refund_chargeback_id\": 47594,\n  \"refund_amount\": \"0.00\",\n  \"refund_key\": \"01f1f771-b75c-48ef-b21d-193a79f8aa5b\"\n}"
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
                          "example": "Success, refund request is approved by the bank"
                        },
                        "transaction_id": {
                          "type": "string",
                          "example": "fddb5889-fd39-46fe-809d-30679fe42434"
                        },
                        "order_id": {
                          "type": "string",
                          "example": "MID-1620622357"
                        },
                        "gross_amount": {
                          "type": "string",
                          "example": "10000.00"
                        },
                        "payment_type": {
                          "type": "string",
                          "example": "credit_card"
                        },
                        "transaction_time": {
                          "type": "string",
                          "example": "2016-06-28 09:42:20"
                        },
                        "transaction_status": {
                          "type": "string",
                          "example": "refund"
                        },
                        "refund_chargeback_id": {
                          "type": "integer",
                          "example": 47594,
                          "default": 0
                        },
                        "refund_amount": {
                          "type": "string",
                          "example": "10000.00"
                        },
                        "refund_key": {
                          "type": "string",
                          "example": "01f1f771-b75c-48ef-b21d-193a79f8aa5b"
                        }
                      }
                    },
                    {
                      "title": "Error Validation - Invalid Direct Refund",
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
                      "title": "Error Validation - Invalid Refund Amount",
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
                      "title": "Error Validation - Refund Already Exist",
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
                    },
                    {
                      "title": "Rejected Direct Refund",
                      "type": "object",
                      "properties": {
                        "status_code": {
                          "type": "string",
                          "example": "202"
                        },
                        "status_message": {
                          "type": "string",
                          "example": "Refund denied by the bank"
                        },
                        "transaction_id": {
                          "type": "string",
                          "example": "fddb5889-fd39-46fe-809d-30679fe42434"
                        },
                        "order_id": {
                          "type": "string",
                          "example": "MID-1620622357"
                        },
                        "gross_amount": {
                          "type": "string",
                          "example": "10000.00"
                        },
                        "payment_type": {
                          "type": "string",
                          "example": "credit_card"
                        },
                        "transaction_time": {
                          "type": "string",
                          "example": "2016-06-28 09:42:20"
                        },
                        "transaction_status": {
                          "type": "string",
                          "example": "settlement"
                        },
                        "refund_chargeback_id": {
                          "type": "integer",
                          "example": 47594,
                          "default": 0
                        },
                        "refund_amount": {
                          "type": "string",
                          "example": "0.00"
                        },
                        "refund_key": {
                          "type": "string",
                          "example": "01f1f771-b75c-48ef-b21d-193a79f8aa5b"
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