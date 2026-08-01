---
updatedAt: 2026-05-07T10:59:38.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Create Pay Account (GoPay)

Link customer account  - GoPay Tokenizations

Create Pay Account is triggered to link the customer's account to be used for payments using specific payment channel.

| HTTP Method | Endpoint                 | Definition                                                          |
| ----------- | ------------------------ | ------------------------------------------------------------------- |
| POST        | BASE\_URL/v2/pay/account | Link the customer account to be used for specific payment channels. |

<br />

***

## Create Pay Account Request

```json Sample Request - Create Pay Account Request
{
  "payment_type": "gopay",
  "gopay_partner": {
    "phone_number": "81212345678",
    "country_code": "62",
    "redirect_url": "https://www.gojek.com"
  }
}
```

<HTMLBlock>{`
<div></div>

<style></style><table>
<tr><th colspan="2">JSON Attribute</th><th>Description</th><th>Type</th><th>Required</th></tr>
<tr><td colspan="2">payment_type</td><td>Payment channel where the account is register to.</td><td>String</td><td>Required</td></tr>
<tr><td colspan="2">gopay_partner</td><td>GoPay linking specific parameters.</td><td>Object</td><td>Conditional</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;phone_number</td><td>Phone number linked to the customer's account.</td><td>String</td><td>Required</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;country_code</td><td>Country code associated with the phone number.</td><td>String</td><td>Required</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;redirect_url</td><td>URL where user is redirected to after finishing the confirmation on Gojek app.</td><td>String</td><td>Optional</td></tr>
<tr></tr>

</table>
`}</HTMLBlock>

<br />

***

## Create Pay Account Response

```json Sample Response - Success
"status_code": "201",
  "payment_type": "gopay",
  "account_id": "00000269-7836-49e5-bc65-e592afafec14",
  "account_status": "PENDING",
  "actions": [
    {
      "name": "activation-link-url",
      "method": "GET",
      "url": "http://api.midtrans.com/v2/gopay/redirect/gpar_6123269-1425-21e3-bc44-e592afafec14/link"
    },
    {
      "name": "activation-link-app",
      "method": "GET",
      "url": "http://api.midtrans.com/v2/gopay/redirect/gpad_6123269-1425-21e3-bc44-e592afafec14/link"
    }
  ]
}
```
```json Sample Response - Failed
{
  "status_code": "202",
  "payment_type": "gopay",
  "channel_response_code": "2903",
  "channel_response_message": "invalid scheme"
}
```

| JSON Attribute             | Description                                                                                 | Type                                      |
| -------------------------- | ------------------------------------------------------------------------------------------- | ----------------------------------------- |
| status\_code               | Status code of the API result.                                                              | String                                    |
| payment\_type              | Payment channel associated with the account.                                                | String                                    |
| account\_id                | Customer account id to be used for payment.                                                 | String                                    |
| account\_status            | Status of the account. Possible values are `PENDING`, `EXPIRED`, `ENABLED`, and `DISABLED`. | String                                    |
| channel\_response\_code    | Response code from payment channel provider.                                                | String                                    |
| channel\_response\_message | Response message from payment channel provider.                                             | String                                    |
| actions                    | Follow up actions to be performed.                                                          | Array([Object](/reference/action-object)) |

<br />

Use any one of the two redirection URLs given below.

* `activation-link-url` is for customer authentication in browser or WebView. This redirection is recommended for desktop. The customer needs to scan the QR code shown on this page using their Gojek app to verify the linking. Once the linking is verified, then this page is redirected back to the merchant page. For merchants with special agreement with GoPay, this page may show OTP/PIN page instead.

* `activation-link-app` is for customer authentication in Gojek app (This might not be applicable for all merchants). The customer needs to input OTP/PIN from the Gojek app.

**Merchant should no longer use`activation-deeplink`as it will be deprecated soon.**

<br />

> 📘 Note
>
> Merchant can use these phone numbers to perform failed linking scenarios on Sandbox environment
>
> * User not registered: 123450001
> * User is blocked: 123450002

***

## Pay Account Link Notification

```json Sample Notification - Pay Account Link Notification
{
  "account_id": "00000269-7836-49e5-bc65-e592afafec14",
  "merchant_id": "M099098",
  "payment_type": "gopay",
  "signature_key": "ad7ccda03d8ec6f2f415661fb511d47fcd17dcc7d7e1ade96a305dd5d3bc2bea5438a8bdfe1aeedabdefb226000338ac169fc18d5ae73788fd5e78dbac945ce4",
  "status_code": "200",
  "account_status": "ENABLED",
  "status_message": "Midtrans account_linked notification"
}
```

Pay Account link notification will be sent to merchant after user have been redirected to provider app and successfully input their pin/OTP. This notification sample can be seen on the side, and you can see [Handle notifications](/reference/notifications-handling) section to know how to handle the notifications.

Specifically for GoPay Tokenization, after notification is recived, merchant needs to call [Get Pay Account](https://docs.midtrans.com/reference/get-pay-account) to fetch the account balance, status, and payment option token.

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
    "/v2/pay/account": {
      "post": {
        "summary": "Create Pay Account (GoPay)",
        "description": "Link customer account  - GoPay Tokenizations",
        "operationId": "create-pay-account",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "payment_type": {
                    "type": "string",
                    "description": "Payment channel where the account is register to.",
                    "default": "gopay"
                  },
                  "gopay_partner": {
                    "type": "object",
                    "description": "GoPay linking specific parameters.",
                    "properties": {
                      "phone_number": {
                        "type": "string",
                        "default": "81212345678"
                      },
                      "country_code": {
                        "type": "string",
                        "default": "62"
                      },
                      "redirect_url": {
                        "type": "string",
                        "default": "https://www.gojek.com"
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
                    "value": "  \"status_code\": \"201\",\n  \"payment_type\": \"gopay\",\n  \"account_id\": \"00000269-7836-49e5-bc65-e592afafec14\",\n  \"account_status\": \"PENDING\",\n  \"actions\": [\n    {\n      \"name\": \"activation-link-url\",\n      \"method\": \"GET\",\n      \"url\": \"http://api.midtrans.com/v2/gopay/redirect/gpar_6123269-1425-21e3-bc44-e592afafec14/link\"\n    },\n    {\n      \"name\": \"activation-link-app\",\n      \"method\": \"GET\",\n      \"url\": \"http://api.midtrans.com/v2/gopay/redirect/gpad_6123269-1425-21e3-bc44-e592afafec14/link\"\n    }\n  ]\n}"
                  },
                  "Failed": {
                    "value": "{\n  \"status_code\": \"202\",\n  \"payment_type\": \"gopay\",\n  \"channel_response_code\": \"105\",\n  \"channel_response_message\": \"User Not Found\"\n}"
                  }
                },
                "schema": {
                  "type": "object",
                  "properties": {
                    "status_code": {
                      "type": "string",
                      "example": "202"
                    },
                    "payment_type": {
                      "type": "string",
                      "example": "gopay"
                    },
                    "channel_response_code": {
                      "type": "string",
                      "example": "105"
                    },
                    "channel_response_message": {
                      "type": "string",
                      "example": "User Not Found"
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
                    "value": "{\n    \"status_code\": \"401\",\n    \"status_message\": \"Transaction cannot be authorized with the current client/server key.\",\n    \"id\": \"ea5c461f-338a-4530-ad00-f0fb6bff1749\"\n}"
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
                    },
                    "id": {
                      "type": "string",
                      "example": "ea5c461f-338a-4530-ad00-f0fb6bff1749"
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