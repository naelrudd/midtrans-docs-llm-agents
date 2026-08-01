---
updatedAt: 2025-11-10T23:03:51.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# ShopeePay

ShopeePay is an *E-Money* payment method by Shopee. Users will be redirected from the merchant app to pay using the Shopee app.

The steps to integrate with ShopeePay are given below.

1. Send the charge API request to Midtrans.
2. Open the redirect url in the response to get redirected to Shopee app.
3. Handle the redirect from Shopee app back to merchant app via `shopeepay` JSON object or configure via Dashboard > Settings > Payments.
4. [Handle notifications](/reference/notifications-handling).

Send a Charge API request with the details of the transaction such as `payment_type`, `shopeepay`, `transaction_details`, `item_details`, and `customer_details`. Successful request returns a redirect URL.

By default, Shopeepay JumpApp and QRIS's transaction expiry is 15 minutes. The maximum expiry time is 5 days.

<br />

***

<br />

## ShopeePay Charge API Request

<br />

```json ShopeePay Charge Request
{
    "payment_type": "shopeepay",
    "transaction_details": {
        "order_id": "test-order-shopeepay-001",
        "gross_amount": 25000
    },
    "item_details": [
        {
            "id": "id1",
            "price": 25000,
            "quantity": 1,
            "name": "Brown sugar boba milk tea"
        }
    ],
    "customer_details": {
        "first_name": "John",
        "last_name": "Brandon",
        "email": "john.brandon@go-jek.com",
        "phone": "0819323212312"
    },
    "shopeepay": {
        "callback_url": "https://midtrans.com/"
    }
}
```

| JSON Attribute       | Description                                                                    | Type                                     | Required |
| -------------------- | ------------------------------------------------------------------------------ | ---------------------------------------- | -------- |
| payment\_type        | Set ShopeePay payment method. Value: `shopeepay`                               | String                                   | Required |
| transaction\_details | The details of the specific transaction such as `order_id` and `gross_amount`. | [Object](https://docs.midtrans.com/reference/transaction-details-object) | Required |
| item\_details        | Details of the item(s) purchased by the customer.                              | [Object](https://docs.midtrans.com/reference/item-details-object)        | Optional |
| customer\_details    | Details of the customer.                                                       | [Object](https://docs.midtrans.com/reference/customer-details-object)    | Optional |
| shopeepay            | Charge details using ShopeePay.                                                | [Object](https://docs.midtrans.com/reference/shopeepay-object)           | Required |

<br />

***

<br />

## ShopeePay Charge Response and Notifications

<br />

```json Success
{
    "status_code": "201",
    "status_message": "ShopeePay transaction is created",
    "channel_response_code": "0",
    "channel_response_message": "success",
    "transaction_id": "bb379c3a-218b-47c7-9b0b-25f71f0f1231",
    "order_id": "test-order-shopeepay-001",
    "merchant_id": "YON001",
    "gross_amount": "25000.00",
    "currency": "IDR",
    "payment_type": "shopeepay",
    "transaction_time": "2020-09-29 11:16:23",
    "transaction_status": "pending",
    "fraud_status": "accept",
    "actions": [
        {
            "name": "deeplink-redirect",
            "method": "GET",
            "url": "https://wsa.uat.wallet.airpay.co.id/universal-link/wallet/pay?deep_and_deferred=1&token=dFhkbmR1bTBIamhW5n7WPz2OrczCvb8_XiHliB9nROFMVByjtwKMAl6G0Ax0cMr79M4hwjs"
        }
    ]
}
```
```json Pending
{
  "transaction_time":"2020-09-29 11:16:23",
  "transaction_status":"pending",
  "transaction_id":"bb379c3a-218b-47c7-9b0b-25f71f0f1231",
  "status_message":"midtrans payment notification",
  "status_code":"201",
  "signature_key":"dd627b40a8951f8c15af2d0f4e96ceae748af857e1d697f4bdb631a37227a4de45952a909c5f08d92228dd27e590586996ab1cf82b658ee99fae08d3e26f3348",
  "payment_type":"shopeepay",
  "order_id":"test-order-shopeepay-001",
  "merchant_id":"YON001",
  "gross_amount":"25000.00",
  "fraud_status":"accept",
  "currency":"IDR"
}
```
```json Settlement
{
  "transaction_time":"2020-09-29 11:22:38",
  "transaction_status":"settlement",
  "transaction_id":"6f4595c8-7ed6-4ade-818f-865fdd0e47aa",
  "status_message":"midtrans payment notification",
  "status_code":"200",
  "signature_key":"a8abc37da315aa7c01c18817f4740db68392a15aa2e01fe4637dbaff49364e18e9367731a53569d23a90c06e8e06794eec9d5395c2bd5f39c0a58d0ab8d2d059",
  "settlement_time":"2020-09-29 11:23:44",
  "payment_type":"shopeepay",
  "order_id":"test-order-shopeepay-003",
  "merchant_id":"YON001",
  "gross_amount":"25000.00",
  "fraud_status":"accept",
  "currency":"IDR",
  "shopeepay_reference_number": "103995032913255264",
  "reference_id": "DL-dduIy7XtGtvxJtNNpOfbAt"
}
```
```json Expired
{
  "transaction_time":"2020-09-29 11:24:57",
  "transaction_status":"expire",
  "transaction_id":"6637ee65-69cd-44ff-8650-5fb746c492aa",
  "status_message":"midtrans payment notification",
  "status_code":"202",
  "signature_key":"d6452333ab67dfb2adb784f529d9c27dc149adffb74fcc1d45d98418f7c7a68a2e86a6f5ede9be83795aa147d27e030282343a36f11d14858d6b5425de153362",
  "payment_type":"shopeepay",
  "order_id":"test-order-shopeepay-004",
  "merchant_id":"YON001",
  "gross_amount":"25000.00",
  "fraud_status":"accept",
  "currency":"IDR"
}
```

| JSON Attribute               | Description                                                                                                                        | Type                               |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| status\_code                 | Status code of transaction charge result.                                                                                          | String                             |
| status\_message              | Description of transaction charge result.                                                                                          | String                             |
| actions                      | Actions which can be performed with this transaction. Use `deeplink-redirect` action to redirect to Shopee apps.                   | Array([Object](https://docs.midtrans.com/reference/action-object)) |
| channel\_response\_code      | Response code from payment channel provider.                                                                                       | String                             |
| channel\_response\_message   | Response message from payment channel provider.                                                                                    | String                             |
| transaction\_id              | Transaction ID given by Midtrans.                                                                                                  | String                             |
| order\_id                    | Order ID specified by you.                                                                                                         | String                             |
| gross\_amount                | Total amount of transaction in IDR.                                                                                                | String                             |
| payment\_type                | Transaction payment method.                                                                                                        | String                             |
| transaction\_time            | Timestamp of transaction in ISO 8601 format. Time Zone: GMT+7.                                                                     | String                             |
| transaction\_status          | Status of ShopeePay transaction. Possible values are<br/>`pending`, `settlement`, `expire`, `deny`.                                | String                             |
| signature\_key               | Combination of parameters such as `order_id`, `status_code`, `gross_amount`, `server_key` to verify integrity of payload/response. | String                             |
| currency                     | ISO-4217 representation of three-letter alphabetic currency code. Value: `IDR`.<br /> **Note**: Currently only `IDR` is supported. | String                             |
| shopeepay\_reference\_number | Reference number given by ShopeePay.                                                                                               | String                             |
| reference\_id                | Reference id given by ShopeePay.                                                                                                   | String                             |

<br />

> 📘 Note
>
> Possible error codes are **400**, **401**, **402**, **406**, **410**

<br />

***

<br />

## Implementing ShopeePay Deeplink Callback

In addition to the standard mobile apps flow, you can implement deeplink callback to redirect customer back from ShopeePay to your app.

To implement it, please set `callback_url` with the deeplink URL redirecting to your app (look at ShopeePay Charge API Request for sample implementation), or configure it via Dashboard > [Settings > Payments](https://dashboard.midtrans.com/settings/payment) in Finish URL.