---
updatedAt: 2025-11-10T23:03:09.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# QRIS

QRIS is a QR payment standard in Indonesia, developed by Bank Indonesia (BI). Users can scan and pay the QR from any payment providers registered as the issuer [here](https://www.bi.go.id/PJSPQRIS/default.aspx).

For QRIS, we are currently integrated with the acquirers given below.

1. GoPay
2. AirPay Shopee (ShopeePay)

The steps to integrate with QRIS are given below.

1. Send the charge API request to Midtrans with the selected acquirer.
2. Show the rendered QR string to the users.
3. [Handle notifications](/reference/notifications-handling).

Send a Charge API request with the details of the transaction such as `payment_type`, `qris`, `transaction_details`, `item_details`, and `customer_details`. Successful request returns a QR code image URL.

<br />

***

<br />

## QRIS Charge API Request

<br />

```json Sample Request - Charge API
{
  "payment_type": "qris",
  "transaction_details": {
    "order_id": "order03",
    "gross_amount": 275000
  },
  "item_details": [
    {
      "id": "id1",
      "price": 275000,
      "quantity": 1,
      "name": "Bluedio H+ Turbine Headphone with Bluetooth 4.1 -"
    }
  ],
  "customer_details": {
    "first_name": "Budi",
    "last_name": "Utomo",
    "email": "budi.utomo@midtrans.com",
    "phone": "081223323423"
  },
  "qris": {
    "acquirer": "gopay"
  }
}
```

| JSON Attribute       | Description                                                                    | Type                                     | Required |
| -------------------- | ------------------------------------------------------------------------------ | ---------------------------------------- | -------- |
| payment\_type        | Set QRIS payment method. Value: `qris`                                         | String                                   | Required |
| transaction\_details | The details of the specific transaction such as `order_id` and `gross_amount`. | [Object](https://docs.midtrans.com/reference/transaction-details-object) | Required |
| item\_details        | Details of the item(s) purchased by the customer.                              | [Object](https://docs.midtrans.com/reference/item-details-object)        | Optional |
| customer\_details    | Details of the customer.                                                       | [Object](https://docs.midtrans.com/reference/customer-details-object)    | Optional |
| qris                 | Charge details using QRIS.                                                     | [Object](https://docs.midtrans.com/reference/qris-object)                | Optional |

<br />

***

<br />

## QRIS Charge Response and Notifications

<br />

```json Success
{
    "status_code": "201",
    "status_message": "QRIS transaction is created",
    "transaction_id": "0d8178e1-c6c7-4ab4-81a6-893be9d924ab",
    "order_id": "order03",
    "merchant_id": "M099098",
    "gross_amount": "275000.00",
    "currency": "IDR",
    "payment_type": "qris",
    "transaction_time": "2020-09-29 11:46:13",
    "transaction_status": "pending",
    "fraud_status": "accept",
    "acquirer": "gopay",
    "actions": [
        {
            "name": "generate-qr-code",
            "method": "GET",
            "url": "https://api.midtrans.com/v2/qris/0d8178e1-c6c7-4ab4-81a6-893be9d924ab/qr-code"
        },
				{
            "name": "generate-qr-code-v2",
            "method": "GET",
            "url": "https://api.midtrans.com/v4/qris/A120250718094848HaVD2xS9VKID/qr-code"
        }
    ]
}
```
```json Pending
{
  "transaction_time":"2020-09-29 11:18:06",
  "transaction_status":"pending",
  "transaction_id":"ce0a3584-5a0c-4049-ad88-5590a96be4fe",
  "status_message":"midtrans payment notification",
  "status_code":"201",
"signature_key":"b1798748303cf0817733c1e312d630793b84d8125a96af0cb7251f8266d5c5256285084ba3ffbfae1f264a031d41927124fba0b552f249ee68180e9c7566448e",
  "payment_type":"qris",
  "order_id":"order03",
  "merchant_id":"M099098",
  "gross_amount":"275000.00",
  "fraud_status":"accept",
  "currency":"IDR",
  "acquirer":"gopay"
}
```
```json Settlement
{
  "transaction_type":"on-us",
  "transaction_time":"2020-09-29 11:27:33",
  "transaction_status":"settlement",
  "transaction_id":"9f07920a-6145-4d1e-9fc2-66e6fd6bc6fc",
  "status_message":"midtrans payment notification",
  "status_code":"200",
"signature_key":"155b03b554092326ad9d2ed936f5765fe759b6bc491c0161a26e4340978fb6e8f07683bf012552a9498bfc919abab834aade57eda01f7a18a3490a515cf17632",
  "settlement_time":"2020-09-29 11:30:44",
  "payment_type":"qris",
  "order_id":"order03",
  "merchant_id":"M099098",
  "issuer":"gopay",
  "gross_amount":"275000.00",
  "fraud_status":"accept",
  "currency":"IDR",
  "acquirer":"gopay",
  "shopeepay_reference_number": "144854469038383602",
  "reference_id": "QR-ZbbffKucJPEksDmXMFChZa"
}
```
```json Expired
{
  "transaction_time":"2020-09-29 11:31:39",
  "transaction_status":"expire",
  "transaction_id":"9728e0fd-a49c-4c25-8c88-404ef1c45e0e",
  "status_message":"midtrans payment notification",
  "status_code":"202",
"signature_key":"4580d8fc6c4a8dca3319efc1f629b8b33e923ec62b2e6ad7254ed6230ef0e57977b2f6124ba8f2a7a71c53ac7368f3f795ffbdecac3b5cf23e82f1ca5440ad1a",
  "payment_type":"qris",
  "order_id":"order03",
  "merchant_id":"M099098",
  "gross_amount":"275000.00",
  "fraud_status":"accept",
  "currency":"IDR",
  "acquirer":"gopay"
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
        Transaction payment method.
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
        Status of QRIS transaction. Possible values are<br/>`pending`, `settlement`, `expire`, `deny`.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        transaction\_type
      </td>

      <td>
        To determine how the transaction is being acquired. Possible values are `on-us` or `off-us`.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        issuer
      </td>

      <td>
        The provider that is making the payment over the QR.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        actions
      </td>

      <td>
        Actions which can be performed with this transaction.   

        Use `generate-qr-code` action to render the QR code image without any border (PNG format).   

        Use `generate-qr-code-v2` action to render the QR code image with ASPI's border (PNG format, *see reference on the callout below*).
      </td>

      <td>
        Array([Object](https://docs.midtrans.com/reference/action-object))
      </td>
    </tr>

    <tr>
      <td>
        acquirer
      </td>

      <td>
        The provider creating the QR and accepting the payment. The value is the same as the one set in the charge request.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        merchant\_id
      </td>

      <td>
        Merchant ID given by Midtrans.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        currency
      </td>

      <td>
        ISO-4217 representation of three-letter alphabetic currency code. Value: `IDR`.<br /> **Note**: Currently only `IDR` is supported.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        signature\_key
      </td>

      <td>
        Combination of parameters such as `order_id`, `status_code`, `gross_amount`, `server_key` to verify integrity of payload/response.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        shopeepay\_reference\_number
      </td>

      <td>
        Reference number given by ShopeePay. Only available for acquirer airpay shopee
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        reference\_id
      </td>

      <td>
        Reference id given by payment provider. Only available for acquirer airpay shopee
      </td>

      <td>
        String
      </td>
    </tr>
  </tbody>
</Table>

<br />

> 📘 Note
>
> Possible error codes are **400**, **401**, **402**, **406**, **410**

<Callout icon="🇮🇩" theme="default">
  ### Generating QR using ASPI's format

  We are introducing a new method for merchants to generate QR codes. In the response’s actions array, we have added a new object containing a URL that merchants can use to generate a QR code in ASPI’s format. You can use the URL inside the new object named *generate-qr-code-v2* to create the QR code.

  Reference

  <Image align="center" width="200px" src="https://files.readme.io/8b4ab6e37458ceecfdb71b323ef641796d84cc0dffd0641d53258c3b05c246fd-image.png" />
</Callout>

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "info": {
    "title": "core-api-qris",
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
        "summary": "QRIS",
        "description": "",
        "operationId": "qris",
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
                    "default": "qris"
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
                        "default": "order_id-0123"
                      },
                      "gross_amount": {
                        "type": "integer",
                        "default": 100000,
                        "format": "int32"
                      }
                    }
                  },
                  "qris": {
                    "type": "object",
                    "required": [
                      "acquirer"
                    ],
                    "properties": {
                      "acquirer": {
                        "type": "string",
                        "default": "gopay"
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
                    "value": "{\n    \"status_code\": \"201\",\n    \"status_message\": \"QRIS transaction is created\",\n    \"transaction_id\": \"0d8178e1-c6c7-4ab4-81a6-893be9d924ab\",\n    \"order_id\": \"order03\",\n    \"merchant_id\": \"M099098\",\n    \"gross_amount\": \"275000.00\",\n    \"currency\": \"IDR\",\n    \"payment_type\": \"qris\",\n    \"transaction_time\": \"2020-09-29 11:46:13\",\n    \"transaction_status\": \"pending\",\n    \"fraud_status\": \"accept\",\n    \"acquirer\": \"gopay\",\n    \"actions\": [\n        {\n            \"name\": \"generate-qr-code\",\n            \"method\": \"GET\",\n            \"url\": \"https://api.midtrans.com/v2/qris/0d8178e1-c6c7-4ab4-81a6-893be9d924ab/qr-code\"\n        }\n    ]\n}"
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
                      "example": "QRIS transaction is created"
                    },
                    "transaction_id": {
                      "type": "string",
                      "example": "0d8178e1-c6c7-4ab4-81a6-893be9d924ab"
                    },
                    "order_id": {
                      "type": "string",
                      "example": "order03"
                    },
                    "merchant_id": {
                      "type": "string",
                      "example": "M099098"
                    },
                    "gross_amount": {
                      "type": "string",
                      "example": "275000.00"
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
                      "example": "2020-09-29 11:46:13"
                    },
                    "transaction_status": {
                      "type": "string",
                      "example": "pending"
                    },
                    "fraud_status": {
                      "type": "string",
                      "example": "accept"
                    },
                    "acquirer": {
                      "type": "string",
                      "example": "gopay"
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
                            "example": "https://api.midtrans.com/v2/qris/0d8178e1-c6c7-4ab4-81a6-893be9d924ab/qr-code"
                          }
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