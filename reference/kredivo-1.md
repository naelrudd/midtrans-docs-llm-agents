---
updatedAt: 2025-11-11T00:32:49.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Kredivo

Kredivo has been enabling E-commerce to sell their merchandise in installment. It allows their customers to pay in installment without a payment card as long as they are registered to Kredivo.

The steps to integrate with Kredivo *Cardless Credit* are given below.

1. Send the charge API request to Midtrans with the selected acquirer.
2. Redirect the customer to the provider's website.
3. Redirect your customer back to your page by configuring Finish URL in Midtrans's Dashboard > [Settings > Payments](https://dashboard.midtrans.com/settings/payment).
4. [Handle notifications](/reference/notifications-handling).

By default, Kredivo's transaction expiry is 24 hours (min 20s, max 180 days).

<br />

***

<br />

## Kredivo Charge API Request

<br />

```json Sample Request - Kredivo Charge
{
  "payment_type": "kredivo",
  "transaction_details": {
    "order_id": "orderid-01",
    "gross_amount": 40000,
    "currency": "IDR"
  },
  "customer_details": {
    "email": "john.baker@email.com",
    "first_name": "John",
    "last_name": "Baker",
    "phone": "08123456789",
    "shipping_address": {
      "first_name": "John",
      "last_name": "Baker",
      "phone": "08123456789",
      "address": "Jl. Kemanggisan",
      "city": "Jakarta",
      "postal_code": 12353,
      "country_code": "IND"
    }
  },
  "item_details": [
    {
      "id": "1",
      "name": "Sepatu",
      "price": 40000,
      "category": "Fashion",
      "quantity": 1,
      "url": "http://toko/toko1?item=abc"
    }
  ],
  "seller_details": [
    {
      "id": "sellerId-01",
      "name": "John Seller",
      "email": "seller@email.com",
      "url": "https://tokojohn.com",
      "address": {
        "first_name": "John",
        "last_name": "Seller",
        "phone": "081234567890",
        "address": "Kemanggisan",
        "city": "Jakarta",
        "postal_code": "12190",
        "country_code": "IDN"
      }
    }
  ],
  "custom_expiry": {
		"expiry_duration": 60,
		"unit": "minute"
	}
}
```

| JSON Attribute       | Description                                                                                                                                                                                                       | Type                                     | Required    |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- | ----------- |
| payment\_type        | The *Cardless Credit* payment method used by the customer. Value: `kredivo`. <br />**Note**: Currently only `kredivo` is supported.                                                                               | String                                   | Required    |
| transaction\_details | The details of the specific transaction such as `order_id` and `gross_amount`.                                                                                                                                    | [Object](https://docs.midtrans.com/reference/transaction-details-object) | Required    |
| customer\_details    | Details of the customer. All field in the given sample are **Required**. <br /> **Note**: By default, this field is mandatory. Merchant requires Kredivo approval to make this optional.                          | [Object](https://docs.midtrans.com/reference/customer-details-object)    | Conditional |
| item\_details        | Details of the item(s) purchased by the customer. All field in the given sample are **Required**. <br /> **Note**: By default, this field is mandatory. Merchant requires Kredivo approval to make this optional. | [Object](https://docs.midtrans.com/reference/item-details-object)        | Conditional |
| seller\_details      | Details of the seller(s) where the customer purchased from. All field in the given sample are **Required**. <br /> **Note**: This field is only mandatory for marketplace merchant.                               | [Object](https://docs.midtrans.com/reference/seller-details-object)      | Conditional |
| custom\_expiry       | Details of the expiry time of the specific transaction. Default value: `24 hours`                                                                                                                                 | [Object](https://docs.midtrans.com/reference/custom-expiry-object)       | Optional    |

<br />

***

<br />

## Kredivo Charge API Response and Notifications

<br />

```json Success
{
  "status_code":"201",
  "status_message":"Kredivo transaction is created",
  "transaction_id":"c1b4e32c-fd32-4ce3-98ed-130a6faf0fef",
  "order_id":"orderid-01",
  "redirect_url":"https://api.sandbox.veritrans.co.id/v2/oms/redirect/c1b4e32c-fd32-4ce3-98ed-130a6faf0fef",
  "merchant_id":"M099098",
  "gross_amount":"40000.00",
  "currency":"IDR",
  "payment_type":"kredivo",
  "transaction_time":"2022-04-12 13:55:34",
  "transaction_status":"pending",
  "fraud_status":"accept",
  "channel_response_code":"OK",
  "channel_response_message":"Success Create Transaction"
}
```
```json Pending
{
  "transaction_time": "2018-08-24 16:20:36",
  "gross_amount": "11000.00",
  "order_id": "orderid-01",
  "payment_type": "kredivo",
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
  "payment_type": "kredivo",
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
  "payment_type": "kredivo",
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
  "payment_type": "kredivo",
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
| redirect\_url              | The redirect URL to Kredivo payment page.                                                                                                                                                                                                                                                                                                                          | String  |
| gross\_amount              | Total transaction amount in IDR.                                                                                                                                                                                                                                                                                                                                   | String  |
| currency                   | ISO-4217 representation of three-letter alphabetic currency code. Value: `IDR`.<br />**Note**: Currently only `IDR` is supported.                                                                                                                                                                                                                                  | String  |
| payment\_type              | Payment method used by the customer.                                                                                                                                                                                                                                                                                                                               | String  |
| transaction\_time          | Timestamp of transaction in ISO 8601 format. Time Zone: GMT+7.                                                                                                                                                                                                                                                                                                     | String  |
| transaction\_status        | Transaction status of Kredivo transaction. Possible values are `pending`, `deny`, `settlement`, `expire`.                                                                                                                                                                                                                                                          | String  |
| fraud\_status              | Detection result by Fraud Detection System (FDS). Possible values are `accept` : Approved by FDS and `challenge`: Questioned by FDS.<br />**Note**: You have to [approve](https://docs.midtrans.com/reference/approve-transaction) the transaction to accept it or transaction will get cancelled automatically during settlement.<br/>`deny`: Denied by FDS. Transaction is automatically failed. | String  |
| channel\_response\_code    | Response code from the channel.                                                                                                                                                                                                                                                                                                                                    | Integer |
| channel\_response\_message | Response message from the channel.                                                                                                                                                                                                                                                                                                                                 | String  |

***

<br />

## Redirecting Back to Finish Page

<br />

The redirection back from Kredivo to your Finish Redirect URL will be using straight-forward HTTP GET. **Please make sure the Finish Redirect URL endpoint can receive HTTP GET request.**

Also, ensure that that the specified URL is a URL of a webpage that you own.

> 🚧 Callback URL format update
>
> **Starting January 2024** Midtrans will start appending transaction information on the callback URL returned to merchant. We will do the rollout gradually so please ensure your system can support both the old and new callback URL format.

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Before January 2024
      </th>

      <th>
        After January 2024
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Callback URL from Kredivo page will only be the merchant callback URL without being append by any parameter.  

        Sample URL:
        [https://www.merchanturl.com](https://www.merchanturl.com)
      </td>

      <td>
        Callback URL from Kredivo page will be the merchant callback URL and  appended by additional parameter:  

        * Merchant order ID  
        * Transaction status  
        * Status code  

        Sample URL:\
        [https://www.merchanturl.com?order\_id=120231129030954WzDmzp1roM\&transaction\_status=expire\&status\_code=407](https://www.merchanturl.com?order_id=120231129030954WzDmzp1roM\&transaction_status=expire\&status_code=407)
      </td>
    </tr>
  </tbody>
</Table>