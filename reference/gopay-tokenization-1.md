---
updatedAt: 2026-05-06T07:33:01.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# GoPay Linking / Tokenization

GoPay Tokenization is a feature that allows customers to make seamless transaction by linking their account to the merchant's implementation of Snap. Instead of scanning QR or opening deeplink, it will enable users to pay transactions only by inputting their PIN for the already linked account within Snap checkout page without switching app.

<br />

> 📘 Activating GoPay Linking in Sandbox & Production
>
> GoPay Linking/Tokenization feature needs to be activated first in your merchant account before it can be used in Production or Sandbox. Contact your Sales PIC or Midtrans support to activate this feature.

***

<br />

## Linking Flow

<br />

1. Create `SNAP_TOKEN` with `gopay.tokenization` set to true and `user_id` filled with respective identifier. Merchant can also set `gopay.phone_number` and `gopay.country_code` to lock the linking with specific phone number.

* `user_id` is a unique identifier owned by merchant that represents a customer. Merchant can use any value in string format with a maximum length of 255. Avoid using values that could be easily linked to a customer like email, ID of records in database etc. Instead, use something like `sha512(email/record.id + salt)`. Don't expose the `user_id` to frontends like browser or mobile. To ensure that each `user_id` can only be used by the rightful customer (i.e. to prevent abuse), please make sure that there are proper measures to ensure that `user_id` is non-tamperable from the customer’s frontend, e.g. by validating through merchant’s backend.

<br />

2. `Link your GoPay account` option will be shown in the payment list.

<Image align="center" alt={500} width="50% " src="https://files.readme.io/94b6695-Screen_Shot_2023-02-06_at_16.47.44.png" title="Screen Shot 2023-02-06 at 16.47.44.png" />

<br />

3. User can then input their phone number (if phone number is not sent) or see their phone number (non modifiable) if merchant sent `phone_number` and `country_code` in create token request under `gopay` JSON object.

<br />

<Image align="center" alt={500} width="50% " src="https://files.readme.io/50babe6-Screen_Shot_2023-02-06_at_16.49.16.png" title="Screen Shot 2023-02-06 at 16.49.16.png" />

<br />

4. User will need to input OTP sent by GoPay and GoPay's PIN in order to finish linking.

<br />

<Image align="center" alt={500} width="50% " src="https://files.readme.io/c05708d-Screen_Shot_2023-02-06_at_16.49.16.png" title="Screen Shot 2023-02-06 at 16.49.16.png" />

<br />

5. Customer will then be redirected to the pay screen. After inputting PIN, transaction will be completed.

<br />

<Image align="center" alt={400} width="50% " src="https://files.readme.io/ec51e99-Screen_Shot_2023-02-07_at_08.44.50.png" title="Screen Shot 2023-02-07 at 08.44.50.png" />

<br />

***

<br />

## Sample JSON Request Body

<br />

At the bare minimum, set `tokenization` as `true` and pass `user_id` to Midtrans to enable GoPay Tokenization. See sample below.

<br />

```json Sample Request
{
  "transaction_details": {
    "order_id": "ORDER-101",
    "gross_amount": 10000
  },
  "item_details": [{
    "id": "ITEM1",
    "price": 10000,
    "quantity": 1,
    "name": "Midtrans Bear",
    "brand": "Midtrans",
    "category": "Toys",
    "merchant_name": "Midtrans"
  }],
  "customer_details": {
    "first_name": "TEST",
    "last_name": "MIDTRANSER",
    "email": "test@midtrans.com",
    "phone": "+628123456"
  },
  "enabled_payments": ["gopay"],
  "gopay": {
    "tokenization": true,
    "phone_number": "8123456789",
    "country_code": "62"
  },
  "user_id": "testuser01"
}
```

| Parameter                                                                                                            | Description                                                                                        |
| -------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| transaction\_details     <br /> [Transaction Details](/reference/json-objects#transaction-details) Object (required) | Unique transaction ID                                                                              |
| item\_details                 <br /> [Item Details](/reference/json-objects#item-details) Object (optional)          | Item details will be paid by customer                                                              |
| customer\_details   <br /> [Customer Details](/reference/json-objects#customer-details) Object (optional)            | Details of the customer                                                                            |
| enabled\_payments <br /> Array (optional)                                                                            | Set GoPay payment method. Value: `gopay`                                                           |
| user\_id <br /> String(255) (optional)                                                                               | The id of user that will be bind to the GoPay account                                              |
| gopay            <br /> [GoPay](/reference/json-objects#gopay-object) (optional)                                     | GoPay payment options - pass the tokenization param, user\_id and target linked phone number here. |

<br />

***

<br />

## Linking and Payment Process Flowchart

<br />

Refer to the following chart as a reference for GoPay Tokenization linking and payment flow.

<br />

<Image align="center" alt={946} width="80%" src="https://files.readme.io/e0afa28-Untitled.png" title="Untitled.png" />

<br />

***

<br />

## Unlink Account

<br />

Merchant can provide the capability for users to unlink the account outside of Snap by sending DELETE request for a specific `user_id`.

<br />

```curl
curl --request DELETE \
  --url https://app.midtrans.com/snap/v3/users/{user_id}/gopay \
  --header 'Authorization: {merchant_server_key}' \
  --header 'Content-Type: application/json' \
  --header 'Accept: application/json'
```

Alternatively, customer can also perform unlinking from GoPay app by tapping Explore at home page > Settings > Apps linked to GoPay.

<br />

## Get Account Info

<br />

Use this API to retrieve and show user's account information.

<br />

### Sample Request

```curl
curl --request GET \
  --url https://app.midtrans.com/snap/v3/users/{user_id}/gopay \
  --header 'Authorization: Basic {merchant_server_key -> in base64}' \
  --header 'Content-Type: application/json' \
  --header 'Accept: application/json'
```

### Sample Response

```json Existing ENABLED account
{
  "user_id": "testww1",
  "account_status": "ENABLED",
  "balance": "8000000.00",
  "phone_number": "8123456789",
  "country_code": "62",
  "account_id": "bb2fb8cc-d754-4390-b62f-01fb3fc1517c"
}
```
```json Existing PENDING account
{
    "error_messages": [
        "account not found"
    ],
    "locale": "en"
}
```
```json Non-existing account
{
    "error_messages": [
        "account not found"
    ],
    "locale": "en"
}
```

<br />

## Supporting Recurring

<br />

> 📘 Activating Recurring Feature
>
> Recurring needs to be configured on your account first before usage. Contact Midtrans Support team or your Sales PIC to request for activation.

<br />

Snap also supports recurring payments via GoPay Tokenization. To support it, your account will need to be configured first by Midtrans team to support both Recurring and No Pin flow.

The flow will be as follows :

1. Perform the first charge as usual, following the linking flow above. Customer will then have to link their GoPay account to Snap first.
2. Merchant will then need to capture customer's GoPay `account_id` post first successful payment charge via HTTP notifications.
3. Using said `account_id`, fetch the account `token` using [Get Pay Account API](https://docs.midtrans.com/reference/get-pay-account).
4. Use our Subscription API to create a subscription and define the subsequent charge schedule. You will need to pass the `account_id` and `token` fetched from the previous steps when creating a subscription.
5. Finally, utilize the [Subscription API](/reference/create-subscription) to update, delete, or modify ongoing subscriptions as needed.

<br />

### Sample HTTP Notification with `account_id`

<br />

This info will be passed via HTTP notification after the first successful transaction charge using GoPay Linking. Once merchant has received this information, call Subscription API to convert it into recurring payments.

```json
{
      "transaction_time": "2023-09-04 14:10:30",
      "transaction_status": "settlement",
      "transaction_id": "57fxxxxxx-5f96-xxx0-xxxx-xxxxxx",
      "status_message": "midtrans payment notification",
      "status_code": "200",
      "signature_key": "f5xxxxxxxxxx",
      "settlement_time": "2023-09-04 14:10:30",
      "payment_type": "gopay",
      "order_id": "testrecurring",
      "metadata": {
        "extra_info": {
          "user_id": "aaaa-aaaa-aaaa-aaaa-aaaaaaaaaa",
          "account_id": "aaaa-aaaa-4e4f-aaaa-e81fc4f640a5"
        }
      },
      "merchant_id": "G01xxxxxxxx",
      "gross_amount": "100000.00",
      "fraud_status": "accept",
      "expiry_time": "2023-09-04 14:25:30",
      "currency": "IDR"
}
```

<br />

## Fallback Payment Flow

When `gopay` is the only enabled payment method and `gopay.tokenization` is set to true, users will be provided with alternative ways to complete their payment in the events they do not want to link their account yet to complete payments: GoPay Deeplink on mobile devices, or QRIS on desktop.

<br />

<Image align="center" alt="Pay with QRIS on desktop view" caption="Pay with QRIS on desktop view" src="https://files.readme.io/b6fbb07575724c16d27420275a6db00fe3a02b9ffa69e85c2842721744175517-image.png" width="50% " />

<Image align="center" alt="Pay without linking on mobile view" caption="Pay without linking on mobile view" src="https://files.readme.io/5807a4b912f21f959643141571b6587ed1f8fd117279ee5be22f42c58c3e9fd5-image.png" width="50% " />

<br />

<br />

You can disable this fallback mechanism by setting `gopay.enforce_tokenization` to `true`.

```json Sample Request
{
  "transaction_details": {
    "order_id": "ORDER-101",
    "gross_amount": 10000
  },
  "enabled_payments": ["gopay"],
  "gopay": {
    "tokenization": true,
    "enforce_tokenization": true,
    "phone_number": "8123456789",
    "country_code": "62"
  },
  "user_id": "testuser01"
}
```