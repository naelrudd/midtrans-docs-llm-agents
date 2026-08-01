---
updatedAt: 2026-04-21T05:17:55.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Get Transaction Status

Get Transaction Status is triggered to obtain the `transaction_status` and other details of a specific transaction. Get Status API can be used by both Snap and Core API integration.

<br />

***

## Get Transaction Status Method

See sample on the right -- try it yourself!

| HTTP Method | Endpoint                                           | Definition                     |
| ----------- | -------------------------------------------------- | ------------------------------ |
| GET         | BASE\_URL/v2/`{order_id OR transaction_id}`/status | Get the status of transaction. |

<br />

<Callout icon="🚧" theme="warn">
  If you're using BI SNAP and DANA payment methods, please only use Transaction ID to get status. Otherwise it won't work.
</Callout>

***

## Get Status Transaction Response

```json Sample Response - Success
{
  "status_code" : "200",
  "status_message" : "Success, Credit Card transaction is successful",
  "transaction_id" : "249fc620-6017-4540-af7c-5a1c25788f46",
  "masked_card" : "48111111-1114",
  "order_id" : "example-1424936368",
  "payment_type" : "credit_card",
  "transaction_time" : "2015-02-26 14:39:33",
  "transaction_status" : "capture",
  "fraud_status" : "accept",
  "approval_code" : "1424936374393",
  "signature_key" : "2802a264cb978fbc59f631c68d120cbda8dc853f5dfdc52301c615cf4f14e7a0b09aa...",
  "bank" : "bni",
  "gross_amount" : "30000.00",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "card_type": "credit",
  "payment_option_type": "GOPAY_WALLET",
  "shopeepay_reference_number": "103995032913255264",
  "reference_id": "DL-dduIy7XtGtvxJtNNpOfbAt",
  "merchant_cross_reference_id": "b7a96412-21d5-4213-87b6-4a181a3ebfb7"
}
```
```json Sample Response - Success (Refund)
{
  "status_code" : "200",
  "status_message" : "Success, refund request is approved by the bank",
  "transaction_id" : "249fc620-6017-4540-af7c-5a1c25788f46",
  "masked_card" : "48111111-1114",
  "order_id" : "example-1424936368",
  "payment_type" : "credit_card",
  "transaction_time" : "2015-02-26 14:39:33",
  "transaction_status" : "partial_refund",
  "fraud_status" : "accept",
  "approval_code" : "1424936374393",
  "signature_key" : "2802a264cb978fbc59f631c68d120cbda8dc853f5dfdc52301c615cf4f14e7a0b09aa...",
  "bank" : "bni",
  "gross_amount" : "30000.00",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "card_type": "credit",
  "payment_option_type": "GOPAY_WALLET",
  "refund_amount": "12000.00",
  "refunds": [
    {
      "refund_chargeback_id": 1,
      "refund_amount": "5000.00",
      "created_at": "2015-02-27 00:14:20",
      "reason": "some reason",
      "refund_key": "reference1"
    },
    {
      "refund_chargeback_id": 2,
      "refund_amount": "7000.00",
      "created_at": "2015-02-28 01:23:15",
      "reason": "",
      "refund_key": "reference2"
    },
  ]
}
```
```json Sample Response - Success (Refunded Trx - Bank Confirmed)
{
  "status_code" : "200",
  "status_message" : "Success, refund request is approved by the bank",
  "transaction_id" : "249fc620-6017-4540-af7c-5a1c25788f46",
  "masked_card" : "48111111-1114",
  "order_id" : "example-1424936368",
  "payment_type" : "credit_card",
  "transaction_time" : "2015-02-26 14:39:33",
  "transaction_status" : "partial_refund",
  "fraud_status" : "accept",
  "approval_code" : "1424936374393",
  "signature_key" : "2802a264cb978fbc59f631c68d120cbda8dc853f5dfdc52301c615cf4f14e7a0b09aa...",
  "bank" : "bni",
  "gross_amount" : "30000.00",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "card_type": "credit",
  "payment_option_type": "GOPAY_WALLET",
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
```json Sample Response - Success (JSON with Point Information)
{
  "masked_card": "52412500-0127",
  "approval_code": "T12345",
  "bank": "bni",
  "eci": "02",
  "point_balance_amount": "1644.00",
  "point_redeem_amount": 80000,
  "point_redeem_quantity": 26667,
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "channel": "dragon",
  "three_ds_version": "2",
  "transaction_time": "2023-11-20 07:30:03",
  "custom_field1": "TEST1",
  "custom_field2": "TEST2",
  "gross_amount": "410400.00",
  "currency": "IDR",
  "order_id": "TKP2453912939",
  "payment_type": "credit_card",
  "signature_key": "d60dc0a9c7c3cd5c20399d99d56968c241dbaacc26444c2eebc541d3b0fad594cefb50dd866a83089ecba785bd153ee95c03d81a35ccf82689b15d8f57bdbb80",
  "status_code": "200",
  "transaction_id": "0c8b481d-8b99-4c6a-b735-aec18be92f28",
  "transaction_status": "capture",
  "fraud_status": "accept",
  "expiry_time": "2023-11-20 07:40:03",
  "status_message": "Success, Credit Card transaction is successful",
  "merchant_id": "B200000000000001005476",
  "card_type": "credit",
  "challenge_completion": true
}
```
```json Sample Response - Pending (DANA & ShopeePay)
{
 "status_code": "200",
 "transaction_id": "78068ef3-e797-4eef-945e-e8516a312916",
 "gross_amount": "238429.00",
 "currency": "IDR",
 "order_id": "test-merchant-order-xyz",
 "payment_type": "dana",
 "signature_key": "d60dc0a9c7c3cd5c20399d99d56968c241dbaacc26444c2eebc541d3b0fad594cefb50dd866a83089ecba785bd153ee95c03d81a35ccf82689b15d8f57bdbb80",
 "transaction_status": "PENDING",
 "fraud_status": "accept",
 "status_message": "Success, transaction is found",
 "merchant_id": "G123456",
 "transaction_time": "2025-11-03 12:45:47",
 "expiry_time": "2025-11-03 13:00:47",
 "actions": [
 	{
 		"name": "deeplink-redirect",
 		"method": "GET",
 		"url": "https://m.dana.id/transaction_page"
 	}
}
```
```json Sample Response - Pending (OVO)
{
  "status_code" : "201",
  "status_message" : "Success, transaction is found",
  "transaction_id" : "78068ef3-e797-4eef-945e-e8516a312916",
  "order_id" : "test-merchant-order-xyz",
  "payment_type" : "ovo",
  "transaction_time" : "2025-11-02 14:39:33",
  "transaction_status" : "pending",
  "currency": "IDR",
  "fraud_status" : "accept",
  "signature_key" : "2802a264cb978fbc59f631c68d120cbda8dc853f5dfdc52301c615cf4f14e7a0b09aa...",
  "gross_amount" : "30000.00",
  "merchant_id": "G123456",
  "expiry_time": "2025-11-02 15:44:33",
  "payer_phone_number": "081111111111"
}
```

<HTMLBlock>{`
<table>
<tr><th colspan="2">JSON Attribute</th><th>Description</th><th>Type</th></tr>
<tr><td colspan="2">status_code</td><td>Status code of transaction charge result</td><td>String</td></tr>
<tr><td colspan="2">status_message</td><td>Description of transaction charge result.</td><td>String</td></tr>
<tr><td colspan="2">transaction_id</td><td>Transaction ID given by Midtrans.</td><td>String</td></tr>
<tr><td colspan="2">masked_card</td><td>First 8-digit and last 4-digit of customer's credit card number.</td><td>String</td></tr>
<tr><td colspan="2">order_id</td><td>Order ID specified by you.</td><td>String</td></tr>
<tr><td colspan="2">payment_type</td><td>The payment method used by the customer.</td><td>String</td></tr>
<tr><td colspan="2">transaction_time</td><td>Timestamp of transaction in ISO 8601 format. Time Zone: GMT+7.</td><td>String</td></tr>
<tr><td colspan="2">transaction_status</td><td>Transaction status after charge credit card transaction. Possible values are<br/><code>capture</code>: Transaction is accepted by the bank and ready for settlement. <br/><code>deny</code>: transaction is denied by the bank or FDS.<br/><code>authorize</code>: Credit card is authorized in pre-authorization feature.</td><td>String</td></tr>
<tr><td colspan="2">fraud_status</td><td>Detection result by Fraud Detection System (FDS). Possible values are<br/><code>accept</code>: Approved by FDS.<br/><code>challenge</code>: Questioned by FDS. <b>Note</b>: <a href="/reference/approve-transaction">Approve transaction</a> to accept it or transaction gets automatically canceled during settlement.<br/><code>deny</code>: Denied by FDS. Transaction automatically failed.</td><td>String</td></tr>
<tr><td colspan="2">approval_code</td><td>Approval code from payment provider for successful transaction. It can be used for refund.</td><td>String</td></tr>
<tr><td colspan="2">signature_key</td><td>Signature key to validate if the notification is originated from Midtrans.</td><td>String</td></tr>
<tr><td colspan="2">bank</td><td>The acquiring bank of the transaction.</td><td>String</td></tr>
<tr><td colspan="2">gross_amount</td><td>Total amount of transaction in IDR. </td><td>String</td></tr>
<tr><td colspan="2">channel_response_code</td><td>Response code from payment channel provider.</td><td>String</td></tr>
<tr><td colspan="2">channel_response_message</td><td>Response message from payment channel provider</td><td>String</td></tr>
<tr><td colspan="2">card_type</td><td>Type of card used. Possible values are <code>credit</code>, <code>debit</code>.</td><td>String</td></tr>
<tr><td colspan="2">payment_option_type</td><td>Type of payment that is being used, possible values are <code>GOPAY_WALLET</code>, <code>PAY_LATER</code>, <code>GO_CICIL</code>, <code>GOPAY_COINS</code> (more possible values will be added once we launch more payment option on Gopay). Only available for Gopay payment type.</td><td>String</td></tr>
<tr><td colspan="2">shopeepay_reference_number</td><td>Reference number given by ShopeePay. Only available for ShopeePay payment type and QRIS payment type with acquirer <code>airpay shopee</code>.</td><td>String</td></tr>
<tr><td colspan="2">reference_id</td><td>Reference ID given by payment provider. Only available for ShopeePay payment type and QRIS payment type with acquirer <code>airpay shopee</code>.</td><td>String</td></tr>
<tr><td colspan="2">merchant_cross_reference_id</td><td>Merchant reference ID given by payment provider.<br>Only available for:<ol><li><code>gopay</code> payment type that is being fulfilled using QRIS flow.</li><li><code>qris</code> payment type that using gopay as the acquirer.</li></ol> </td><td>String</td></tr>
<tr><td colspan="2">refund_amount</td><td>Cumulative refund amount in \`IDR\`.</td><td>String</td></tr>
<tr><td colspan="2">refunds</td><td>List of refund details related to the transaction. Only available on transaction status <code>partial_refund</code> or <code>refund</code>.</td><td>JSON Array</td></tr>
<tr><td colspan="2">refund_chargeback_id</td><td>Midtrans refund ID.</td><td>Long</td></tr>
<tr><td colspan="2">refund_amount</td><td>Amount of the specific refund.</td><td>String</td></tr>
<tr><td colspan="2">created_at</td><td>Timestamp of the refund creation.</td><td>String</td></tr>
<tr><td colspan="2">reason</td><td>Reason the refund is created.</td><td>String</td></tr>
<tr><td colspan="2">refund_key</td><td>Merchant refund reference.</td><td>String</td></tr>
<tr><td colspan="2">refund_method</td><td>Refund confirmation method. The value is applied after Midtrans confirm the refund request (1 day after request is made). Possible values are <code>online</code>, <code>offline</code>.</td><td>String</td></tr>
<tr><td colspan="2">bank_confirmed_at</td><td>Timestamp of receipt of refund request confirmation from acquiring bank.</td><td>String</td></tr>
<tr><td colspan="2">point_redeem_amount</td><td>Amount redeemed in IDR.</td><td>Long</td></tr>
<tr><td colspan="2">point_redeem_quantity</td><td>Point representation of point_redeem_amount.</td><td>Long</td></tr>
<tr><td colspan="2">point_balance_amount</td><td>Balance amount in IDR.</td><td>String</td></tr>
  <tr><td colspan="2">actions</td><td>Will be returned only for DANA / ShopeePay payment type with "pending" status.</td><td>Object</td></tr>
<tr><td colspan="2">actions.name</td><td>Name of the action that will be inserted on the "actions" object.</td><td>String</td></tr>
<tr><td colspan="2">actions.method</td><td>HTTP methods.</td><td>String</td></tr>
  <tr><td colspan="2">actions.url</td><td>URL that will be returned incase of "pending" status fro deeplink payment</td><td>String</td></tr>
<tr><td colspan="2">payer_phone_number</td><td>Customer's phone number that used to create payment request to payment provider.</td><td>String</td></tr>
<tr><td colspan="2">merchant_invoice</td><td>Unique identifier for payment provider specific request.</td><td>String</td></tr>
</table>
`}</HTMLBlock>

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
    "/v2/{order_id}/status": {
      "get": {
        "summary": "Get Transaction Status",
        "description": "",
        "operationId": "get_v2{order_id}status-1",
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
                    "value": "{\n  \"status_code\" : \"200\",\n  \"status_message\" : \"Success, transaction found\",\n  \"transaction_id\" : \"249fc620-6017-4540-af7c-5a1c25788f46\",\n  \"masked_card\" : \"48111111-1114\",\n  \"order_id\" : \"example-1424936368\",\n  \"payment_type\" : \"credit_card\",\n  \"transaction_time\" : \"2015-02-26 14:39:33\",\n  \"transaction_status\" : \"capture\",\n  \"fraud_status\" : \"accept\",\n  \"approval_code\" : \"1424936374393\",\n  \"signature_key\" : \"2802a264cb978fbc59f631c68d120cbda8dc853f5dfdc52301c615cf4f14e7a0b09aa...\",\n  \"bank\" : \"bni\",\n  \"gross_amount\" : \"30000.00\",\n  \"channel_response_code\": \"00\",\n  \"channel_response_message\": \"Approved\",\n  \"card_type\": \"credit\",\n  \"payment_option_type\": \"GOPAY_WALLET\",\n  \"shopeepay_reference_number\": \"103995032913255264\",\n  \"reference_id\": \"DL-dduIy7XtGtvxJtNNpOfbAt\"\n}"
                  },
                  "Success - Refund": {
                    "value": "{\n  \"status_code\" : \"200\",\n  \"status_message\" : \"Success, transaction found\",\n  \"transaction_id\" : \"249fc620-6017-4540-af7c-5a1c25788f46\",\n  \"masked_card\" : \"48111111-1114\",\n  \"order_id\" : \"example-1424936368\",\n  \"payment_type\" : \"credit_card\",\n  \"transaction_time\" : \"2015-02-26 14:39:33\",\n  \"transaction_status\" : \"partial_refund\",\n  \"fraud_status\" : \"accept\",\n  \"approval_code\" : \"1424936374393\",\n  \"signature_key\" : \"2802a264cb978fbc59f631c68d120cbda8dc853f5dfdc52301c615cf4f14e7a0b09aa...\",\n  \"bank\" : \"bni\",\n  \"gross_amount\" : \"30000.00\",\n  \"channel_response_code\": \"00\",\n  \"channel_response_message\": \"Approved\",\n  \"card_type\": \"credit\",\n  \"payment_option_type\": \"GOPAY_WALLET\",\n  \"refund_amount\": \"12000.00\",\n  \"refunds\": [\n    {\n      \"refund_chargeback_id\": 1,\n      \"refund_amount\": \"5000.00\",\n      \"created_at\": \"2015-02-27 00:14:20\",\n      \"reason\": \"some reason\",\n      \"refund_key\": \"reference1\"\n    },\n    {\n      \"refund_chargeback_id\": 2,\n      \"refund_amount\": \"7000.00\",\n      \"created_at\": \"2015-02-28 01:23:15\",\n      \"reason\": \"\",\n      \"refund_key\": \"reference2\"\n    },\n  ]\n}"
                  },
                  "Refunded Trx - Bank Confirmed": {
                    "value": "{\n  \"status_code\" : \"200\",\n  \"status_message\" : \"Success, transaction found\",\n  \"transaction_id\" : \"249fc620-6017-4540-af7c-5a1c25788f46\",\n  \"masked_card\" : \"48111111-1114\",\n  \"order_id\" : \"example-1424936368\",\n  \"payment_type\" : \"credit_card\",\n  \"transaction_time\" : \"2015-02-26 14:39:33\",\n  \"transaction_status\" : \"partial_refund\",\n  \"fraud_status\" : \"accept\",\n  \"approval_code\" : \"1424936374393\",\n  \"signature_key\" : \"2802a264cb978fbc59f631c68d120cbda8dc853f5dfdc52301c615cf4f14e7a0b09aa...\",\n  \"bank\" : \"bni\",\n  \"gross_amount\" : \"30000.00\",\n  \"channel_response_code\": \"00\",\n  \"channel_response_message\": \"Approved\",\n  \"card_type\": \"credit\",\n  \"payment_option_type\": \"GOPAY_WALLET\",\n  \"refund_amount\": \"12000.00\",\n  \"refunds\": [\n    {\n      \"refund_chargeback_id\": 1,\n      \"refund_amount\": \"5000.00\",\n      \"created_at\": \"2015-02-27 00:14:20\",\n      \"reason\": \"some reason\",\n      \"refund_key\": \"reference1\",\n      \"refund_method\": \"online\",\n      \"bank_confirmed_at\": \"2015-02-27 02:30:20\"\n    },\n    {\n      \"refund_chargeback_id\": 2,\n      \"refund_amount\": \"7000.00\",\n      \"created_at\": \"2015-02-28 01:23:15\",\n      \"reason\": \"\",\n      \"refund_key\": \"reference2\",\n      \"refund_method\": \"offline\",\n      \"bank_confirmed_at\": \"2015-02-27 02:30:20\"\n    },\n  ]\n}"
                  },
                  "Transaction doesn't exist.": {
                    "value": "{\n    \"status_code\": \"404\",\n    \"status_message\": \"Transaction doesn't exist.\",\n    \"id\": \"ca1774d3-302a-4d47-8495-11524ee306b8\"\n}"
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
                          "example": "Success, transaction found"
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
                          "example": "capture"
                        },
                        "fraud_status": {
                          "type": "string",
                          "example": "accept"
                        },
                        "approval_code": {
                          "type": "string",
                          "example": "1424936374393"
                        },
                        "signature_key": {
                          "type": "string",
                          "example": "2802a264cb978fbc59f631c68d120cbda8dc853f5dfdc52301c615cf4f14e7a0b09aa..."
                        },
                        "bank": {
                          "type": "string",
                          "example": "bni"
                        },
                        "gross_amount": {
                          "type": "string",
                          "example": "30000.00"
                        },
                        "channel_response_code": {
                          "type": "string",
                          "example": "00"
                        },
                        "channel_response_message": {
                          "type": "string",
                          "example": "Approved"
                        },
                        "card_type": {
                          "type": "string",
                          "example": "credit"
                        },
                        "payment_option_type": {
                          "type": "string",
                          "example": "GOPAY_WALLET"
                        },
                        "shopeepay_reference_number": {
                          "type": "string",
                          "example": "103995032913255264"
                        },
                        "reference_id": {
                          "type": "string",
                          "example": "DL-dduIy7XtGtvxJtNNpOfbAt"
                        }
                      }
                    },
                    {
                      "title": "Transaction doesn't exist.",
                      "type": "object",
                      "properties": {
                        "status_code": {
                          "type": "string",
                          "example": "404"
                        },
                        "status_message": {
                          "type": "string",
                          "example": "Transaction doesn't exist."
                        },
                        "id": {
                          "type": "string",
                          "example": "ca1774d3-302a-4d47-8495-11524ee306b8"
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