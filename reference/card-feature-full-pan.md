---
updatedAt: 2026-07-27T09:20:33.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Feature: Full PAN

*Full PAN* simplifies the process of recurring transaction on payment card by removing the tokenization step in a normal [Card Payment](/reference/payment-card) transaction. This can be used only if Merchant has a PCI license. Other than for full payments, Full PAN mode can also be used for recurring payments (see also : [One Click Feature](/reference/card-feature-one-click)) by adding `save_token_id` to the charge request.

To better understand the integration, the transactions are categorized into the following:

* Non-3DS integration
* 3DS Integration

<Callout icon="📘" theme="info">
  ### Prerequisite

  This feature is only available if Merchant is PCI-DSS compliant.
</Callout>

<br />

<Callout icon="📘" theme="info">
  ### Important

  Please avoid sending `token_id` in charge requests with Full PAN domain ([https://panapi.midtrans.com](https://panapi.midtrans.com)). This domain is intended exclusively for Full PAN (card number) transactions.

  If you're processing Non-Full PAN (token-based) transaction, please refer to our official documentation for the correct endpoint and flow: [https://docs.midtrans.com/reference/get-token](https://docs.midtrans.com/reference/get-token).

  Submitting a token with Full PAN domain may result in unexpected or ambiguous behavior, and could lead to the transaction being rejected by our security validation systems. Always ensure that you're using the appropriate domain based on the type of credentials (token or PAN) being submitted.

  For further assistance or clarification, feel free to reach out to our support team.
</Callout>

***

## API Environments

Full PAN integration uses dedicated authentication domain (panapi.midtrans.com) which is separate from the Midtrans Core API domain you use for One Time Token in the charge request. Make sure you hit the matching environment.

| Environment | Charge API                                      | Post-Charge APIs (Status, Cancel, Refund) |
| ----------- | ----------------------------------------------- | ----------------------------------------- |
| Sandbox     | <https://panapi.sandbox.midtrans.com/v2/charge> | <https://api.sandbox.midtrans.com>        |
|             | <https://panapi.midtrans.com/v2/charge>         | <https://api.midtrans.com>                |

***

## Full PAN Non-3DS Integration

<br />

Send a Charge API request with `payment_type`, `transaction_details`, `customer_details`, `item_details`. Successful response returns the `redirect_url`.<br />The steps to integrate with Non-3DS are given below.

1. Send the Charge request to Midtrans.
2. [Handle notifications](/reference/notifications-handling).

<br />

### Non 3DS Full PAN Charge Request

<br />

```json Sample Request - Non 3DS Full PAN Charge
{
  "payment_type": "credit_card",
  "transaction_details": {
    "order_id": "C17550",
    "gross_amount": 145000
  },
  "credit_card": {
    "card": {
      "number": "4811111111111114",
      "expiry_month": "03",
      "expiry_year": "2020",
      "cvv": "123"
    },
    "dynamic_descriptor": {
      "merchant_name": "Fuji Apple Inc",
      "city_name": "Jakarta",
      "country_code": "ID"
    }
  },
  "item_details": [{
      "id": "a1",
      "price": 145000,
      "quantity": 2,
      "name": "Apel",
      "brand": "Fuji Apple",
      "category": "Fruit",
      "merchant_name": "Fruit-store"
    }],
    "customer_details": {
      "first_name": "BUDI",
      "last_name": "UTOMO",
      "email": "test@midtrans.com",
      "phone": "+628123456",
      "billing_address": {
        "first_name": "BUDI",
        "last_name": "UTOMO",
        "email": "test@midtrans.com",
        "phone": "081 2233 44-55",
        "address": "Sudirman",
        "city": "Jakarta",
        "postal_code": "12190",
        "country_code": "IDN"
      },
      "shipping_address": {
        "first_name": "BUDI",
        "last_name": "UTOMO",
        "email": "test@midtrans.com",
        "phone": "0 8128-75 7-9338",
        "address": "Sudirman",
        "city": "Jakarta",
        "postal_code": "12190",
        "country_code": "IDN"
      }
    }
}
```

| JSON Attribute       | Description                                                                    | Type                                     | Required |
| -------------------- | ------------------------------------------------------------------------------ | ---------------------------------------- | -------- |
| payment\_type        | The payment method used by the customer. <br /> Value: `credit_card`.          | String (255)                             | Required |
| transaction\_details | The details of the specific transaction such as `order_id` and `gross_amount`. | [Object](https://docs.midtrans.com/reference/transaction-details-object) | Required |
| credit\_card         | The details of the payment card used for the transaction.                      | [Object](https://docs.midtrans.com/reference/credit-card-object)         | Required |
| item\_details        | Details of the item(s) purchased by the customer.                              | [Object](https://docs.midtrans.com/reference/item-details-object)        | Optional |
| customer\_details    | Details of the customer.                                                       | [Object](https://docs.midtrans.com/reference/customer-details-object)    | Optional |

<br />

The `credit_card` object in Charge request to configure Non-3DS full PAN feature is identical with [Card Charge Request](/reference/charge-transactions-on-card#card-charge-request), with the additional attributes given below.

<HTMLBlock>{`
<table>
<tr>
<th colspan="2">JSON Attribute</th>
<th>Description</th>
<th>Type</th>
<th>Required</th>
</tr>

<tr><td colspan="2">card</td>
<td>The details of the payment card used for the transaction.</td>
<td>Object</td>
<td>Required</td>

<tr><td></td><td style="text-align:right;">number</td>
<td>Primary Account Number (PAN) of credit card.</td>
<td>Integer (13-19)</td>
<td>Required</td>
</tr>
<tr><td></td><td style="text-align:right;">expiry_month</td>
<td>The card expiry month in MM format.</td>
<td>String (2)</td>
<td>Required</td>
</tr>
</tr>
<tr><td></td><td style="text-align:right;">expiry_year</td>
<td>The card expiry year in YYYY format. </td>
<td>String (4)</td>
<td>Required</td>
</tr>
<tr><td></td><td style="text-align:right;">cvv</td>
<td>Also known as Card Verification Code (CVC) shown at the back of the credit card. <br><b>Note</b>: If <code>card.cvv</code> is not passed, then transaction will be treated as recurring. </td>
<td>Integer (3-4)</td>
<td>Required</td>
</tr>
<tr><td colspan= "2">dynamic_descriptor</td>
<td>Details of the merchant.</td>
<td>Object</td>
<td>Required</td>

<tr><td></td><td style="text-align:right;">merchant_name</td>
<td>First 25 digit on customer's billing statement. Mostly used to show merchant name or product name. <br><b>Note</b>: Only works for <code>BNI</code>. </td>
<td>String (25)</td>
<td>Required</td>
</tr>
<tr><td></td><td style="text-align:right;">city_name</td>
<td>First 25 digit on customer's billing statement. Mostly used to show merchant name or product name. <br><b>Note</b>: Only works for <code>BNI</code>. </td>
<td>String (13)</td>
<td>Optional</td>
</tr>
<tr><td></td><td style="text-align:right;">country_code</td>
<td>Last two digit on customer's billing statement. Mostly used to show country code. <br><b>Note</b>: Only works for <code>BNI</code>. </td>
<td>String (2)</td>
<td>Optional</td>
</tr>
</table>
`}</HTMLBlock>

<br />

### Non 3DS Full PAN Charge Response and Notifications

<br />

#### Sample Response

```json Success
{
  "transaction_id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
  "order_id": "C17550",
  "gross_amount": "145000.00",
  "payment_type": "credit_card",
  "transaction_time": "2014-08-24 15:39:22",
  "transaction_status": "capture",
  "fraud_status": "accept",
  "masked_card": "48111111-1114",
  "status_code": "200",
  "bank": "bni",
  "status_message": "Success, Credit Card 3D Secure transaction is successful",
  "approval_code": "1408869563148",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "currency": "IDR",
  "card_type": "credit",
  "on_us": true,
  "channel": "dragon"
}
```
```json Deny Notification
{
  "transaction_id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
  "order_id": "C17550",
  "gross_amount": "145000.00",
  "payment_type": "credit_card",
  "transaction_time": "2014-08-24 15:39:22",
  "transaction_status": "deny",
  "fraud_status": "accept",
  "masked_card": "48111111-1114",
  "status_code": "202",
  "bank": "bni",
  "status_message": "Deny by Bank [CIMB] with code [05] and message [Do not honor]",
  "approval_code": "      ",
  "channel_response_code": "05",
  "channel_response_message": "Do not honor",
  "currency": "IDR",
  "card_type": "credit",
  "on_us": false,
  "channel": "dragon"
}
```
```json Challenge Notification
{
  "transaction_id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
  "order_id": "C17550",
  "gross_amount": "145000.00",
  "payment_type": "credit_card",
  "transaction_time": "2014-08-24 15:39:22",
  "transaction_status": "authorize",
  "fraud_status": "challenge",
  "masked_card": "48111111-1114",
  "status_code": "201",
  "bank": "bni",
  "status_message": "Success, Credit Card 3D Secure transaction is successful",
  "approval_code": "1408869563148",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "currency": "IDR",
  "card_type": "credit",
  "on_us": true,
  "channel": "dragon"
}
```
```json Validation Error Notification
{
    "status_code": "400",
    "status_message": "One or more parameters in the payload is invalid.",
    "id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
    "validation_messages": [
        "unsupported token request parameter(s)"
    ]
}
```
```json Settlement Notification
{
  "masked_card": "48111111-1114",
  "approval_code": "131755",
  "bank": "bni",
  "transaction_time": "2014-08-24 15:39:22",
  "gross_amount": "145000.00",
  "order_id": "C17550",
  "payment_type": "credit_card",
  "signature_key": "49e158a0c3f1913eae0902875324075c562daa39b2824b865db2242adea247a228960d2f1002392fdbc29c3271c2bc78ba72e588db9047a82932d0615ddc811f",
  "status_code": "200",
  "transaction_id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
  "transaction_status": "settlement",
  "fraud_status": "accept",
  "status_message": "midtrans payment notification",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "card_type": "credit"
}
```

| JSON Attribute             | Description                                                                                                                                                                                                                                                                                                                                     | Type    |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| transaction\_id            | Transaction ID given by Midtrans.                                                                                                                                                                                                                                                                                                               | String  |
| order\_id                  | Order ID specified by you.                                                                                                                                                                                                                                                                                                                      | String  |
| gross\_amount              | Total amount of transaction in IDR.                                                                                                                                                                                                                                                                                                             | String  |
| payment\_type              | The payment method used by the customer.                                                                                                                                                                                                                                                                                                        | String  |
| transaction\_time          | Timestamp of transaction in ISO 8601 format. Time Zone: GMT+7.                                                                                                                                                                                                                                                                                  | String  |
| transaction\_status        | Transaction status after charge payment card transaction. Possible values are<br />`capture` : Transaction is accepted by the bank and ready for settlement. <br />`deny`: transaction is denied by the bank or FDS.<br />`authorize`: Payment card is authorized in pre-authorization feature.                                                 | String  |
| fraud\_status              | Detection result by Fraud Detection System (FDS). Possible values are<br />`accept` : Approved by FDS.<br />`challenge`: Questioned by FDS. <br />**Note**: [Approve transaction](/reference/approve-transaction) to accept it or transaction will auto cancel during settlement.<br />`deny`: Denied by FDS. Transaction automatically failed. | String  |
| masked\_card               | First 8-digit and last 4-digit of customer's payment card number.                                                                                                                                                                                                                                                                               | String  |
| status\_code               | Status code of transaction charge result.                                                                                                                                                                                                                                                                                                       | String  |
| bank                       | The acquiring bank of the transaction.                                                                                                                                                                                                                                                                                                          | String  |
| status\_message            | Status message describing the result of the API request.                                                                                                                                                                                                                                                                                        | String  |
| approval\_code             | Approval code. It can be used for refund. This does not exist on denied transaction.                                                                                                                                                                                                                                                            | String  |
| channel\_response\_code    | Response code from payment channel provider.                                                                                                                                                                                                                                                                                                    | String  |
| channel\_response\_message | Response message from payment channel provider.                                                                                                                                                                                                                                                                                                 | String  |
| currency                   | ISO-4217 representation of three-letter alphabetic currency code. Value: `IDR`.<br />**Note**: Currently only `IDR` is supported.                                                                                                                                                                                                               | String  |
| card\_type                 | Type of card used. Possible values are `credit`, `debit`.                                                                                                                                                                                                                                                                                       | String  |
| on\_us                     | Indicate whether issuing and acquiring bank is the same                                                                                                                                                                                                                                                                                         | Boolean |
| channel                    | The name of the payment channel provider. More details on request and possible values are available on [Card Feature: Specific Channel](https://docs.midtrans.com/reference/feature-route-to-specific-channel).                                                                                                                                                                 | String  |

<br />

***

<br />

## Full PAN 3DS Integration

<br />

The steps to integrate using 3DS are given below.

1. Send the charge request to Midtrans.
2. Open Redirect URL.
3. [Handle notifications](/reference/notifications-handling).

Send a Charge API request with `payment_type`, `transaction_details`, `cstore`, `customer_details`, `item_details`. Successful response returns the `redirect_url`.

<br />

### 3DS Full PAN Charge Request

<br />

```json Sample Request - 3DS Full PAN Charge
{
  "payment_type": "credit_card",
  "transaction_details": {
    "order_id": "C17550",
    "gross_amount": 145000
  },
  "credit_card": {
    "card": {
      "number": "4811111111111114",
      "expiry_month": "03",
      "expiry_year": "2020",
      "cvv": "123"
    },
    "dynamic_descriptor": {
      "merchant_name": "Fuji Apple Inc",
      "city_name": "Jakarta",
      "country_code": "ID"
    },
    "authentication": true
  },
  "item_details": [{
      "id": "a1",
      "price": 145000,
      "quantity": 2,
      "name": "Apel",
      "brand": "Fuji Apple",
      "category": "Fruit",
      "merchant_name": "Fruit-store"
    }],
    "customer_details": {
      "first_name": "BUDI",
      "last_name": "UTOMO",
      "email": "test@midtrans.com",
      "phone": "+628123456",
      "billing_address": {
        "first_name": "BUDI",
        "last_name": "UTOMO",
        "email": "test@midtrans.com",
        "phone": "081 2233 44-55",
        "address": "Sudirman",
        "city": "Jakarta",
        "postal_code": "12190",
        "country_code": "IDN"
      },
      "shipping_address": {
        "first_name": "BUDI",
        "last_name": "UTOMO",
        "email": "test@midtrans.com",
        "phone": "0 8128-75 7-9338",
        "address": "Sudirman",
        "city": "Jakarta",
        "postal_code": "12190",
        "country_code": "IDN"
      }
    }
}
```

| JSON Attribute       | Description                                                                    | Type                                            | Required |
| -------------------- | ------------------------------------------------------------------------------ | ----------------------------------------------- | -------- |
| payment\_type        | The payment method used by the customer. <br /> Value is `credit_card`.        | String (255)                                    | Required |
| transaction\_details | The details of the specific transaction such as `order_id` and `gross_amount`. | [Object](/reference/transaction-details-object) | Required |
| credit\_card         | The details of the payment card used for the transaction.                      | [Object](/reference/credit-card-object)         | Required |
| item\_details        | Details of the item(s) purchased by the customer.                              | [Object](/reference/item-details-object)        | Optional |
| customer\_details    | Details of the customer.                                                       | [Object](/reference/customer-details-object)    | Optional |

<br />

The `credit_card` object in Charge request to configure 3DS full PAN feature is identical with [Card Charge Request](/reference/charge-transactions-on-card#card-charge-request), with the additional attributes given below.

| JSON Attribute | Description                                                                                                                                                                                                                                                      | Type    | Required |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- |
| authentication | Flag to enable the 3D secure authentication. Default value is `false`.                                                                                                                                                                                           | Boolean | Optional |
| callback\_type | Determines how the transaction status is updated to the merchant frontend. Possible values are `js_event` (default) and `form`. For more details, refer [Open 3DS Authentication](/docs/coreapi-card-payment-integration#3ds-authentication-page-json-response). | String  | Optional |

<br />

### 3DS Full PAN Charge Response and Notifications

<br />

#### Sample Response

```json Success
{
  "status_code": "201",
  "status_message": "Credit Card transaction is in progress",
  "transaction_id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
  "order_id": "C17550",
  "redirect_url": "https://api.veritrans.co.id/v2/token/rba/redirect/451249-2595-e14aac7f-cfb3-4ab2-98ab-5cc5e70f4b2c",
  "gross_amount": "145000.00",
  "currency": "IDR",
  "payment_type": "credit_card",
  "transaction_time": "2018-09-12 22:10:23",
  "transaction_status": "pending",
  "masked_card": "48111111-1114",
  "card_type": "credit",
  "three_ds_version": "2",
  "on_us": true,
  "channel": "dragon"
}
```
```json Pending after submit OTP 3DS 2.0
{
  "status_code": "201",
  "status_message": "Credit Card transaction is in progress",
  "transaction_id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
  "order_id": "C17550",
  "redirect_url": "https://api.veritrans.co.id/v2/token/rba/redirect/451249-2595-e14aac7f-cfb3-4ab2-98ab-5cc5e70f4b2c",
  "gross_amount": "145000.00",
  "currency": "IDR",
  "payment_type": "credit_card",
  "transaction_time": "2018-09-12 22:10:23",
  "transaction_status": "pending",
  "masked_card": "48111111-1114",
  "card_type": "credit",
  "three_ds_version": "2",
  "three_ds_challenge_completion": false,
  "channel": "dragon"
}
```
```json Validation Error Notification
{
  "status_code": "400",
  "status_message": "One or more parameters in the payload is invalid.",
  "id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
  "validation_messages": [
    "unsupported token request parameter(s)"
  ]
}
```
```json Capture Notification
{
  "masked_card": "48111111-1114",
  "approval_code": "T58755",
  "bank": "bni",
  "eci": "05",
  "transaction_time": "2014-08-24 15:39:22",
  "gross_amount": "145000.00",
  "order_id": "C17550",
  "payment_type": "credit_card",
  "signature_key": "8d22a6b625f395a1a2cf0e62497e20be433cbad3e8a8ff36bf6b40dbd47308125ccda93546eab8a3acd91390155082658ac25b10a6294c6660642e43a5edc8bb",
  "status_code": "200",
  "transaction_id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
  "transaction_status": "capture",
  "fraud_status": "accept",
  "status_message": "midtrans payment notification",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "card_type": "credit",
  "three_ds_version": "2",
  "on_us": false
}
```
```json Capture Notification after submit OTP 3DS 2.0
{
  "masked_card": "48111111-1114",
  "approval_code": "T58755",
  "bank": "bni",
  "eci": "05",
  "transaction_time": "2014-08-24 15:39:22",
  "gross_amount": "145000.00",
  "order_id": "C17550",
  "payment_type": "credit_card",
  "signature_key": "8d22a6b625f395a1a2cf0e62497e20be433cbad3e8a8ff36bf6b40dbd47308125ccda93546eab8a3acd91390155082658ac25b10a6294c6660642e43a5edc8bb",
  "status_code": "200",
  "transaction_id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
  "transaction_status": "capture",
  "fraud_status": "accept",
  "status_message": "midtrans payment notification",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "card_type": "credit",
  "three_ds_version": "2",
  "three_ds_challenge_completion": true
}
```
```json Deny Notification
{
  "masked_card": "48111111-1114",
  "approval_code": "338016",
  "bank": "bni",
  "eci": "06",
  "transaction_time": "2014-08-24 15:39:22",
  "gross_amount": "145000.00",
  "order_id": "C17550",
  "payment_type": "credit_card",
  "signature_key": "763713b31cf59c886d3cc4a0c654a060a8e990080fe29fca75ae9e4ff9de804809c4e20977829844dac01a7ac1464a4eb095ad32482048398918987295dc5022",
  "status_code": "202",
  "transaction_id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
  "transaction_status": "deny",
  "fraud_status": "accept",
  "status_message": "midtrans payment notification",
  "channel_response_code": "05",
  "channel_response_message": "Do not honor",
  "card_type": "credit",
  "three_ds_version": "2"
}
```
```json Challenge Notification
{
  "masked_card": "48111111-1114",
  "approval_code": "315762",
  "bank": "bni",
  "eci": "05",
  "transaction_time": "2014-08-24 15:39:22",
  "gross_amount": "145000.00",
  "order_id": "C17550",
  "payment_type": "credit_card",
  "signature_key": "393f8b6b27f9f6385d8391642942e9534fd20dad20c0631b75b0746bfc314482af4411c93e958b691a63e9154676905b906234d1f12fca031f5be5593f7ec2c6",
  "status_code": "201",
  "transaction_id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
  "transaction_status": "capture",
  "fraud_status": "challenge",
  "status_message": "midtrans payment notification",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "card_type": "credit",
  "three_ds_version": "2"
}
```
```json Settlement Notification
{
  "masked_card": "48111111-1114",
  "approval_code": "131755",
  "bank": "bni",
  "eci": "05",
  "transaction_time": "2014-08-24 15:39:22",
  "gross_amount": "145000.00",
  "order_id": "C17550",
  "payment_type": "credit_card",
  "signature_key": "49e158a0c3f1913eae0902875324075c562daa39b2824b865db2242adea247a228960d2f1002392fdbc29c3271c2bc78ba72e588db9047a82932d0615ddc811f",
  "status_code": "200",
  "transaction_id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
  "transaction_status": "settlement",
  "fraud_status": "accept",
  "status_message": "Midtrans payment notification",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "card_type": "credit",
  "three_ds_version": "2"
}
```

| JSON Attribute                   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                | Type    |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------- |
| transaction\_id                  | Transaction ID given by Midtrans.                                                                                                                                                                                                                                                                                                                                                                                                          | String  |
| order\_id                        | Order ID specified by you.                                                                                                                                                                                                                                                                                                                                                                                                                 | String  |
| gross\_amount                    | Total amount of transaction in IDR.                                                                                                                                                                                                                                                                                                                                                                                                        | String. |
| payment\_type                    | The payment method used by the customer.                                                                                                                                                                                                                                                                                                                                                                                                   | String  |
| transaction\_time                | Timestamp of transaction in ISO 8601 format. Time Zone: GMT+7.                                                                                                                                                                                                                                                                                                                                                                             | String  |
| transaction\_status              | Transaction status after charge payment card transaction. Possible values are <br />`capture`: Transaction is accepted by the bank and ready for settlement. <br />`deny`: transaction is denied by the bank or FDS.<br />`authorize`: Payment card is authorized in pre-authorization feature.<br />`pending`: Credit card is pending and you will need to rely on the http notification webhook to receive the final transaction status. | String  |
| fraud\_status                    | Detection result by Fraud Detection System (FDS). Possible values are<br />`accept`: Approved by FDS.<br />`challenge`: Questioned by FDS. <br />**Note:** [Approve transaction](/reference/approve-transaction) to accept it or transaction will auto cancel during settlement.<br />`deny`: Denied by FDS. Transaction automatically failed.                                                                                             | String  |
| masked\_card                     | First 8-digit and last 4-digit of customer's payment card number.                                                                                                                                                                                                                                                                                                                                                                          | String  |
| status\_code                     | Status code of transaction charge result.                                                                                                                                                                                                                                                                                                                                                                                                  | String  |
| bank                             | The name of the acquiring bank of the transaction.                                                                                                                                                                                                                                                                                                                                                                                         | String  |
| status\_message                  | Status message describing the result of the API request.                                                                                                                                                                                                                                                                                                                                                                                   | String  |
| approval\_code                   | Approval code. It can be used for refund. This does not exist on denied transaction.                                                                                                                                                                                                                                                                                                                                                       | String  |
| eci                              | The 3D secure ECI Code.                                                                                                                                                                                                                                                                                                                                                                                                                    | String  |
| channel\_response\_code          | Response code from payment channel provider.                                                                                                                                                                                                                                                                                                                                                                                               | String  |
| channel\_response\_message       | Response message from payment channel provider.                                                                                                                                                                                                                                                                                                                                                                                            | String  |
| redirect\_url                    | URL to redirect the customer to finish 3DS authentication.                                                                                                                                                                                                                                                                                                                                                                                 | String  |
| currency                         | ISO-4217 representation of three-letter alphabetic currency code. Value: `IDR`.<br />**Note**: Currently only `IDR` is supported.                                                                                                                                                                                                                                                                                                          | String  |
| card\_type                       | Type of card used. Possible values are `credit`, `debit`.                                                                                                                                                                                                                                                                                                                                                                                  | String  |
| three\_ds\_version               | 3DS Version that used for transaction (This field only present for 3DS Transaction). Possible values are `1`, `2`                                                                                                                                                                                                                                                                                                                          | String  |
| three\_ds\_challenge\_completion | 3DS Challenge completion state to indicate the customer has submit the OTP or not(it doesn't matter if the OTP is valid or not). Possible values are `true`, `false`                                                                                                                                                                                                                                                                       | Boolean |
| on\_us                           | Indicate whether issuing and acquiring bank is the same                                                                                                                                                                                                                                                                                                                                                                                    | Boolean |
| channel                          | The name of the payment channel provider. Provided if `channel` attribute on charge api request is present. More details on request and possible values are available on [Card Feature: Specific Channel](https://docs.midtrans.com/reference/feature-route-to-specific-channel).                                                                                                                                                                                          | String  |

<br />

<Callout icon="📘" theme="info">
  ### Note

  If you receive pending transaction_status, you will need to rely on the http notification webhook to receive the final transaction status
</Callout>

<br />