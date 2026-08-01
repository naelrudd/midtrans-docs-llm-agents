---
updatedAt: 2026-05-06T07:34:57.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# GoPay Tokenization

<Callout icon="📘" theme="info">
  GoPay Tokenizations mode is available for both Snap and Core API integration. To read about GoPay Tokenization in Snap checkout, go [here](/reference/gopay-tokenization-1).

  Midtrans have launched an updated version of our sandbox environment for GoPay Tokenization payment method starting from October 22nd, 2024. Fore more info on the updated sandbox, go [here](https://docs.midtrans.com/reference/testing-gopay-tokenization-on-sandbox-environment).

  To activate GoPay Tokenizations in both Production and Sandbox, please reach out to our Support team or Sales PIC.
</Callout>

> 📘 GoPay Media Kit
>
> To have a consistent and standardized GoPay branding across platform, we highly recommend merchants to refer to our media kit. Please refer to this page <https://gopay.co.id/media-kit> to access our brand guideline and image bank.

GoPay Tokenization allows you to link your customer GoPay account. The flow is similar to card tokenization where you can use the linked customer account for transaction authorization. This flow is recommended for recurring payments.

There are two flow types for GoPay Tokenization:

1. Web flow: Linking and payment verification will be done via GoPay web flow.  For this flow, use below rdirection URL:
   1. `verification-link-url` will redirect the user to a GoPay web to do OTP or PIN verification.\ <br />
2. App redirection flow: Linking and payment verification will be done via Gojek and GoPay App. For this flow, use the following two redirection URLs:
   1. `verification-link-url` is for transactions that happen in desktop browser. When the user is redirected to this URL, the user will see a QR and the customer will receive a push notification from their Gojek app to do verification. Once the customer verifies the transaction on the app, it will be automatically redirected to the merchant page.
   2. `verification-link-app` is for transactions that happen in mobile app or browser. User will be redirected to Gojek or GoPay app to do the verification.\ <br />

<Callout icon="📘" theme="info">
  For security reason, linking and payment URL on web flow can only be accessed once. Merchant who needs to reopen the web page (for example: user accidentally closed the page), need to initiate another linking or payment to generate a new URL.

  For app redirection flow, the URL can be accessed multiple times as long as the linking and payment is not expired.
</Callout>

> 📘 Redirecting to GoPay page
>
> To learn more on GoPay Tokenization redirection, please refer to these API documentations:
>
> * GoPay Tokenization web flow: <https://docs.midtrans.com/reference/faq-redirection-to-gopay-web-page>
>
> * GoPay Tokenization app redirection flow: <https://docs.midtrans.com/reference/faq-redirection-to-gojek-gopay-app>\ <br />
>
> > ❗️ GoPay may add/change GoPay redirection URL from time to time.
> >
> > To ensure merchant can always support GoPay flow at all times, we highly suggest merchant to not do explicit URL whitelisting.

<Callout icon="📘" theme="info">
  **GoPay can now support GoPay account creation on Tokenization Linking webview**

  User can now create GoPay account directly during linking steps on the merchant's app. This feature is now available on Tokenization linking webview new flow. Refer to this [link](https://docs.midtrans.com/reference/faq-redirection-to-gopay-web-page#gopay-has-revamped-its-gopay-tokenization-linking-web-page-on-the-gopay-tokenization-webview-integration-on-august-2025) to learn more!
</Callout>

**Sequence Diagram**

<details>
  <summary>Linking flow via GoPay web</summary>

  <article>
    <br />

    <Image align="center" src="https://files.readme.io/27261db-Linking_-_Webtokenization.jpg" />
  </article>
</details>

<details>
  <summary>Linking flow via Gojek / GoPay  App</summary>

  <article>
    <br />

    <Image align="center" src="https://files.readme.io/740ae5f-Linking_App_Invoke.jpg" />
  </article>
</details>

<details>
  <summary>Payment flow via GoPay web</summary>

  <article>
    <br />

    <Image align="center" src="https://files.readme.io/bdb7f72-payment_-_Tokenization_web.jpg" />
  </article>
</details>

<details>
  <summary>Payment flow via Gojek / GoPay App</summary>

  <article>
    <br />

    <Image align="center" src="https://files.readme.io/1e33d5d-Payment_-_App_invoke.jpg" />
  </article>
</details>

<details>
  <summary>Payment No Pin</summary>

  <article>
    <br />

    <Image align="center" src="https://files.readme.io/fc823d6-Payment_-_No_Pin.jpg" />
  </article>
</details>

<br />

The steps to integrate with GoPay Tokenization are given below.

1. [Link customer account](https://docs.midtrans.com/reference/create-pay-account) only if the customer's phone number is not yet linked to GoPay.
2. [Fetch customer account](https://docs.midtrans.com/reference/get-pay-account) . If the linking of customer account is successful, then the payment options available to the customer are `GOPAY_SAVINGS`, `GOPAY_WALLET`, and `PAY_LATER` with balance information. Customer can select any of these options.

<Callout icon="📘" theme="info">
  As a fallback in case linking notification is not succesfully received by merchant, **merchants are encouraged to always call this API to confirm the user's linking status.**

  **Merchants are also encouraged to always call this API before payment to make sure the merchant uses the updated token** when creating payment as the payment option token may change from time to time due to various reasons (example: customer upgrade their GoPay account to GoPay Tabungan).
</Callout>

3. Merchant can call the [Charge API](https://docs.midtrans.com/reference/gopay-tokenization#gopay-tokenization-charge-api-request) using payment option token that get from the response above to create payment. Ensure to have proper handling of various status codes that you've received from Midtrans - for example, if the `status_code` in the response is 200, then the transaction is completed. If the `status_code` is 201, then you need to open the verification URL in the `actions` to the customer. Once the verification is done, it will redirect back to the callback URL that you put in the charge call. For GoPay Tokenization, only the whitelisted domain will be accepted, hence please inform our Business team for domain that you want to used for callback URL.
4. Customer should be able to unlink GoPay account if they dont want to use GoPay anymore, ensure there's entrypoint in merchant app or web for customer to unlink their GoPay. To initiate unlinking flow, merchant can integrate with [Unbind Pay Account API](https://docs.midtrans.com/reference/unbind-pay-account).
5. Ensure to listen to the Unbind Pay Account notification for customers that unlink GoPay account from Gojek and GoPay app so the same account status between Merchant and GoPay. Customer account will be automatically unlinked if customer change phone number in Gojek/GoPay app. Please refer to this article: [Pay Account Unbind Notification](https://docs.midtrans.com/reference/unbind-pay-account#pay-account-unbind-notification)

<br />

***

<br />

## GoPay Tokenization Charge API Request

<br />

```json Sample Request - Charge API
{
  "payment_type": "gopay",
  "gopay": {
    "account_id": "00000269-7836-49e5-bc65-e592afafec14",
    "payment_option_token": "eyJ0eXBlIjogIkdPUEFZX1dBTExFVCIsICJpZCI6ICIifQ==",
    "callback_url": "https://midtrans.com/",
    "recurring": false,
    "promotion_ids": [
"CASHBACK|acbec7d4-b30b-44ac-9c42-f5d767419a72|8bb3c041-c71e-40f3-892b-688fda2ec979||2021-02-22|2021-02-23"
    ]
  },
  "transaction_details": {
    "gross_amount": 100000,
    "order_id": "order-1234"
  }
  "payment_provider_metadata" {
  	"recurring_parent_order": "merchant-recurring-parent-order",
  	"recurring_sequence": "1"
	}
}
```

The attributes to be sent to charge GoPay Tokenization are given below.

| JSON Attribute                                       | Description                                                                                                                                                                                                                                                                                                              | Type                                     | Required    |
| :--------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------- | :---------- |
| payment\_type                                        | Set GoPay payment method. Value: `gopay`.                                                                                                                                                                                                                                                                                | String                                   | Required    |
| gopay                                                | Charge details using GoPay.                                                                                                                                                                                                                                                                                              | [Object](https://docs.midtrans.com/reference/gopay-object)               | Required    |
| transaction\_details                                 | The details of the specific transaction such as `order_id` and `gross_amount`.                                                                                                                                                                                                                                           | [Object](https://docs.midtrans.com/reference/transaction-details-object) | Required    |
| callback\_url                                        | Please make sure `callback_url` is the same URL submitted during the onboarding process. <br /><br /> If callback\_url is not specified by merchant, we will use merchant's finish redirect URL that is set on Midtrans Administration Portal, please make sure these URLs are also submitted during onboarding process. | String                                   | Optional    |
| payment\_provider\_metadata                          | Object containing the payment provider’s metadata parameter. This is used whenever merchant needs to pass additional information to payment provider. Your sales representative will inform you if you need to pass information.                                                                                         | Object                                   | Conditional |
| payment\_provider\_metadata.recurring\_parent\_order | Merchant's recurring parent order ID                                                                                                                                                                                                                                                                                     | String                                   | Conditional |
| payment\_provider\_metadata.recurring\_sequence      | Recurring sequence. <br /> "0" : parent transaction <br /> "1" and so on: child transaction                                                                                                                                                                                                                              | String                                   | Conditional |

<br />

<br />

## GoPay Tokenization Charge Response and Notifications

### Response

```json Settlement
{
  "status_code": "200",
  "status_message": "Success, GoPay transaction is successful",
  "transaction_id": "00000269-7836-49e5-bc65-e592afafec14",
  "order_id": "order-1234",
  "gross_amount": "100000.00",
  "currency": "IDR",
  "payment_type": "gopay",
  "transaction_time": "2016-06-28 09:42:20",
  "transaction_status": "settlement",
  "fraud_status": "accept",
}
```
```json Pending
{
  "status_code": "201",
  "status_message": "GoPay transaction is created. Action(s) required",
  "transaction_id": "00000269-7836-49e5-bc65-e592afafec14",
  "order_id": "order-1234",
  "gross_amount": "100000.00",
  "currency": "IDR",
  "payment_type": "gopay",
  "transaction_time": "2016-06-28 09:42:20",
  "transaction_status": "pending",
  "fraud_status": "accept",
  "actions": [
    {
      "name": "verification-link-url",
      "method": "GET",
      "url": "http://api.midtrans.com/v2/gopay/redirect/gppr_6123269-1425-21e3-bc44-e592afafec14/charge"
    },
    {
      "name": "verification-link-app",
      "method": "GET",
      "url": "http://api.midtrans.com/v2/gopay/redirect/gppd_6123269-1425-21e3-bc44-e592afafec14/charge"
    }
  ]
}
```
```json Deny
{
  "status_code": "202",
  "status_message": "GoPay transaction is denied",
  "transaction_id": "a8a91ece-24f9-427d-a588-b9a2428acda0",
  "order_id": "order-1234",
  "gross_amount": "100000.00",
  "currency": "IDR",
  "payment_type": "gopay",
  "transaction_time": "2016-06-28 09:42:20",
  "transaction_status": "deny",
  "fraud_status": "accept",
}
```
```json Deny - Insufficient Balance
{
  "status_code": "202",
  "status_message": "GoPay transaction is denied",
  "transaction_id": "95581d59-f433-4803-a9e1-0d9945cb9bd4",
  "order_id": "order-1234",
  "gross_amount": "100000.00",
  "currency": "IDR",
  "payment_type": "gopay",
  "transaction_time": "2016-06-28 09:42:20",
  "transaction_status": "deny",
  "fraud_status": "accept",
  "channel_response_code": "201",
  "channel_response_message": "Insufficient Balance"
}
```

| JSON Attribute             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Type                               |
| :------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------- |
| status\_code               | Status code of transaction charge result.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | String                             |
| status\_message            | Description of transaction charge result.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | String                             |
| transaction\_id            | Transaction ID given by Midtrans.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | String                             |
| order\_id                  | Order ID specified by you.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | String                             |
| gross\_amount              | Total amount of transaction in IDR.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | String                             |
| payment\_type              | Transaction payment method.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | String                             |
| transaction\_time          | Timestamp of transaction in ISO 8601 format. Time Zone: GMT+7.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | String                             |
| transaction\_status        | Status of GoPay transaction. Possible values are<br />`pending`, `settlement`, `expire`, `deny`.                                                                                                                                                                                                                                                                                                                                                                                                                                                         | String                             |
| actions                    | Actions which can be performed with this transaction. Use `verification-link-url` or `verification-link-app` to do the verification and to redirect the customer to callback URL. <br /> These links have an expiry time of 5 minutes. <br /><br /> \*\*Merchant should no longer use`user-verification`as it will be deprecated soon. \*\* **<br /><br />GoPay may add/change GoPay redirection URL from time to time. To ensure merchant can always support GoPay flow at all times, we highly suggest merchant to not do explicit URL whitelisting.** | Array([Object](https://docs.midtrans.com/reference/action-object)) |
| currency                   | ISO-4217 representation of three-letter alphabetic currency code. Value: `IDR`.<br /> **Note**: Currently only `IDR` is supported.                                                                                                                                                                                                                                                                                                                                                                                                                       | String                             |
| channel\_response\_code    | Response code from payment channel provider.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | String                             |
| channel\_response\_message | Response message from payment channel provider.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | String                             |

<br />

### Notification

```Text Pending
{
      "transaction_time": "2025-02-10 11:10:57",
      "transaction_status": "pending",
      "transaction_id": "e1fb3680-4fab-49ce-b088-8cc94d9d1234",
      "status_message": "midtrans payment notification",
      "status_code": "201",
      "signature_key": "2d6decd3e291e37bf8a611207e4d600f0c4eda356a3d2a6bd7eb3598b685d518b999b2058533b119dbe95dbdffa8c6516263b405aa31410d654933a9847e691f",
      "payment_type": "gopay",
      "order_id": "order-id",
      "merchant_id": "G643891234",
      "gross_amount": "109000.00",
      "fraud_status": "accept",
      "expiry_time": "2025-02-10 11:26:21",
      "currency": "IDR"
    }
```
```Text Settlement
{
      "transaction_time": "2025-02-10 11:12:06",
      "transaction_status": "settlement",
      "transaction_id": "9899c9c0-ef3d-4f88-b6ae-4fdb8e1a1234",
      "status_message": "midtrans payment notification",
      "status_code": "200",
      "signature_key": "8d8ed39b540895aed06013cd63a5adf75732934bf88dd38f18782b590249ba7af2db9d5fdf1d46c1b93b97829cbb88556c1e52dcab66c5a70cec96f4d3cb113b",
      "settlement_time": "2025-02-10 11:12:06",
      "payment_type": "gopay",
      "payment_option_type": "GOPAY_WALLET",
      "order_id": "order-id",
      "metadata": {
        "description": "a metadata"
      },
      "merchant_id": "G771011234",
      "gross_amount": "14000.00",
      "fraud_status": "accept",
      "expiry_time": "2025-02-10 11:27:06",
      "currency": "IDR"
    }
```
```Text Deny
{
      "transaction_time": "2025-02-10 07:30:38",
      "transaction_status": "deny",
      "transaction_id": "8d265a4b-dcad-468d-86c4-6fe59edd1234",
      "status_message": "midtrans payment notification",
      "status_code": "202",
      "signature_key": "b15167982235fa8584d5e67c123e2c10c0fd64b5609756e3fb0b020d735442e52b87a8baff41b8ecbe7ea30cb74eff482819eeb8d9c51d4c6fe1d2205ccf98c7",
      "payment_type": "gopay",
      "order_id": "order-id",
      "merchant_id": "G616281234",
      "gross_amount": "1002500.00",
      "fraud_status": "accept",
      "expiry_time": "2025-02-10 07:45:37",
      "currency": "IDR",
      "channel_response_message": "Insufficient Balance",
      "channel_response_code": "201"
    }
```
```Text Expired
{
      "transaction_time": "2025-02-07 16:02:31",
      "transaction_status": "expire",
      "transaction_id": "3d08aa30-73fd-4788-985b-f33a8fa4abcd",
      "status_message": "midtrans payment notification",
      "status_code": "202",
      "signature_key": "e354fa93614f76fb89fb998ddba6324e77d7115fefb03b59601a999b06e1d58b569aa42dedac23b4e15b28d31258b8f4f6d8b4e439fa81f24f77c8c0321b1202",
      "payment_type": "gopay",
      "payment_option_type": "PAY_LATER",
      "order_id": "order-id",
      "merchant_id": "G643891234",
      "gross_amount": "110000.00",
      "fraud_status": "accept",
      "expiry_time": "2025-02-07 16:17:56",
      "currency": "IDR"
    }
```
```Text Cancel
{
      "transaction_time": "2025-02-10 11:01:31",
      "transaction_status": "cancel",
      "transaction_id": "1919f7fb-ebfb-4957-8158-cbe13aeca123b",
      "status_message": "midtrans payment notification",
      "status_code": "202",
      "signature_key": "627279175721bc1fa4ce157c925dd3dc57f0d6a2da9337c59dba5607862ecc611a71fa2379097a11df9f7d0a7e6968be6ab651689edf3ab2f6c581c026c1322c",
      "payment_type": "gopay",
      "payment_option_type": "GOPAY_WALLET",
      "order_id": "order-id",
      "merchant_id": "G027591234",
      "gross_amount": "2000000.00",
      "fraud_status": "accept",
      "expiry_time": "2025-02-11 11:01:31",
      "currency": "IDR"
    }
```
```Text Refund
{
      "transaction_time": "2025-02-07 16:41:19",
      "transaction_status": "refund",
      "transaction_id": "A120250123494119o1P1fiYNhZID",
      "status_message": "midtrans payment notification",
      "status_code": "200",
      "signature_key": "ec3404b274c274805ef3af520a7e75b9d86379ecb9f09e96eb7daccadb4a34dcdc6e1fbe7606a44f31e8dcae51ad392aef85364c45c96216cc2fde800847dba4",
      "settlement_time": "2025-02-07 16:41:26",
      "refunds": [
        {
          "refund_method": "online",
          "refund_key": "refund-key-123",
          "refund_chargeback_uuid": "fb030849-6b7c-3f88-b85c-25d9c0de612b",
          "refund_chargeback_id": 202502070943231234,
          "refund_amount": "27610.00",
          "created_at": "2025-02-07 16:43:23",
          "bank_confirmed_at": "2025-02-07 16:43:23"
        }
      ],
      "refund_amount": "27610.00",
      "payment_type": "gopay",
      "payment_option_type": "GOPAY_WALLET",
      "order_id": "order-id",
      "metadata": {
        "acquired_by": "GOPAY"
      },
      "merchant_id": "G449081234",
      "gross_amount": "27610.00",
      "fraud_status": "accept",
      "expiry_time": "2025-02-07 17:55:50",
      "currency": "IDR"
    }
```

<br />

| JSON Attribute             | Description                                                                                                                                                                                                                                                                                                                            | Type   |
| :------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----- |
| status\_code               | Status code of transaction charge result.                                                                                                                                                                                                                                                                                              | String |
| status\_message            | Description of transaction charge result.                                                                                                                                                                                                                                                                                              | String |
| transaction\_id            | Transaction ID given by Midtrans.                                                                                                                                                                                                                                                                                                      | String |
| order\_id                  | Order ID specified by you.                                                                                                                                                                                                                                                                                                             | String |
| gross\_amount              | Total amount of transaction in IDR.                                                                                                                                                                                                                                                                                                    | String |
| currency                   | Currency of transaction amount                                                                                                                                                                                                                                                                                                         | String |
| payment\_type              | Transaction payment method.                                                                                                                                                                                                                                                                                                            | String |
| payment\_option\_type      | Type of payment that is being used, possible values are GOPAY\_WALLET, PAY\_LATER, GO\_CICIL, GOPAY\_COINS (more possible values will be added once we launch more payment option on GoPay). Only available for GoPay payment type. <br /><br /> Will be returned on Settlement, Expired, Refund and Partial Refund notification only. | String |
| transaction\_time          | Timestamp of transaction in ISO 8601 format. Time Zone: GMT+7.                                                                                                                                                                                                                                                                         | String |
| transaction\_status        | Status of GoPay transaction. Possible values are<br />`pending`, `settlement`, `expire`, `deny`.                                                                                                                                                                                                                                       | String |
| fraud\_status              | Fraud status                                                                                                                                                                                                                                                                                                                           | String |
| channel\_response\_code    | Response code from payment channel provider.                                                                                                                                                                                                                                                                                           | String |
| channel\_response\_message | Response message from payment channel provider.                                                                                                                                                                                                                                                                                        | String |
| signature\_key             | Combination of parameters such as `order_id`, `status_code`, `gross_amount`, `server_key` to verify integrity of payload/response.                                                                                                                                                                                                     | String |

***

<br />

## GoPay Tokenization Features: Pre-Authorization

<br />

Merchant that enables GoPay Tokenization could opt to do pre-auth transactions. Pre-auth allows merchant to reserve the customer balance before the goods or services are delivered.

Pre-auth flow allows you to make a reservation to user's wallet balance. This will help for cases where you need to reserve user's balance instead of debit it directly, to initiate debit you can call [Capture API](https://docs.midtrans.com/reference/capture-transaction) afterwards. To use this feature, you can set `pre-auth` as true on [GoPay Object](https://docs.midtrans.com/reference/gopay-object). By default, reserved balance will be released after 15 minutes if there is no "capture" action for that transaction. Capturing a reservation is a process to settle the customer balance into merchant account. You can  customize reservation time limits by sending custom expiry time parameters on charge request

As of now, pre-auth flow feature only supports non PIN flow. To test in Sandbox, please make sure that the amount doesn’t exceed IDR 100,000.

<br />

***

<br />

#### GoPay Tokenization Features: Pre-Authorization Flow

<br />

The steps to integrate Gopay Tokenization Pre-Auth feature are given below.

1. The linking process is exactly same as GoPay Tokenization linking process above.
2. If the linking is already successful then the customer can proceed with the charge. The only difference is that merchant needs to pass `pre_auth`: "true" parameter. See example on the side.
3. Ensure to have proper handling of various status codes that you've received from Midtrans - for example, if the `status_code` in the response is 200, then the transaction is authorized. If the `status_code` is 201, then you need to open the verification URL in the `actions` to the customer. Once the verification is done, it will be redirected back to the callback URL that is set on your dashboard.
4. You need to call [Capture API](https://docs.midtrans.com/reference/capture-transaction). Please note that we do not accept partial amount capture for GoPay.
5. As an option, you can also cancel the authorization by calling the [Cancel API](https://docs.midtrans.com/reference/cancel-transaction).

Send a Charge API request with the details of the transaction and `pre_auth:true`. Successful request returns a `status_code:200`.

<br />

***

<br />

## Pre-Auth Charge API Request

<br />

```json Sample Request - Charge API
{
  "payment_type": "gopay",
  "gopay": {
    "account_id": "00000269-7836-49e5-bc65-e592afafec14",
    "payment_option_token": "eyJ0eXBlIjogIkdPUEFZX1dBTExFVCIsICJpZCI6ICIifQ==",
    "pre_auth": true, // the default value is false
  },
  "transaction_details": {
    "gross_amount": 100000,
    "order_id": "order-1234"
  }
}
```

| JSON Attribute       | Description                                                                    | Type                                     | Required |
| -------------------- | ------------------------------------------------------------------------------ | ---------------------------------------- | -------- |
| payment\_type        | Set GoPay payment method. Value: `gopay`.                                      | String                                   | Required |
| gopay                | Charge details using GoPay.                                                    | [Object](https://docs.midtrans.com/reference/gopay-object)               | Required |
| transaction\_details | The details of the specific transaction such as `order_id` and `gross_amount`. | [Object](https://docs.midtrans.com/reference/transaction-details-object) | Required |

<br />

***

<br />

## Pre-Auth Charge Response and Notifications

<br />

```json Success
{
  "status_code": "200",
  "status_message": "Success, GoPay transaction is successful",
  "transaction_id": "00000269-7836-49e5-bc65-e592afafec14",
  "order_id": "order-1234",
  "gross_amount": "100000.00",
  "currency": "IDR",
  "payment_type": "gopay",
  "transaction_time": "2016-06-28 09:42:20",
  "transaction_status": "authorize",
  "fraud_status": "accept",
  "channel_response_code": "0",
  "channel_response_message": "Process service request successfully."
}
```
```json Pending
{
  "status_code": "201",
  "status_message": "GoPay transaction is created. Action(s) required",
  "transaction_id": "00000269-7836-49e5-bc65-e592afafec14",
  "order_id": "order-1234",
  "gross_amount": "100000.00",
  "currency": "IDR",
  "payment_type": "gopay",
  "transaction_time": "2016-06-28 09:42:20",
  "transaction_status": "pending",
  "fraud_status": "accept",
  "actions": [
    {
      "name": "verification-link-url",
      "method": "GET",
      "url": "http://api.midtrans.com/v2/gopay/redirect/gppr_6123269-1425-21e3-bc44-e592afafec14/charge"
    },
    {
      "name": "verification-link-app",
      "method": "GET",
      "url": "http://api.midtrans.com/v2/gopay/redirect/gppd_6123269-1425-21e3-bc44-e592afafec14/charge"
    }
  ]
}
```
```json Deny
{
  "status_code": "202",
  "status_message": "GoPay transaction is denied",
  "transaction_id": "a8a91ece-24f9-427d-a588-b9a2428acda0",
  "order_id": "order-1234",
  "gross_amount": "100000.00",
  "currency": "IDR",
  "payment_type": "gopay",
  "transaction_time": "2016-06-28 09:42:20",
  "transaction_status": "deny",
  "fraud_status": "accept",
}
```

| JSON Attribute             | Description                                                                                                                                                                       | Type                               |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| status\_code               | Status code of transaction charge result.                                                                                                                                         | String                             |
| status\_message            | Description of transaction charge result.                                                                                                                                         | String                             |
| transaction\_id            | Transaction ID given by Midtrans.                                                                                                                                                 | String                             |
| order\_id                  | Order ID specified by you.                                                                                                                                                        | String                             |
| gross\_amount              | Total amount of transaction in IDR.                                                                                                                                               | String                             |
| payment\_type              | Transaction payment method.                                                                                                                                                       | String                             |
| transaction\_time          | Timestamp of transaction in ISO 8601 format. Time Zone: GMT+7.                                                                                                                    | String                             |
| transaction\_status        | Status of GoPay transaction. Possible values are<br />`pending`, `settlement`, `expire`, `deny`.                                                                                  | String                             |
| actions                    | Actions which can be performed with this transaction. Use `verification-link-url` or `verification-link-app` to do the verification and to redirect the customer to callback URL. | Array([Object](https://docs.midtrans.com/reference/action-object)) |
| channel\_response\_code    | Response code from payment channel provider.                                                                                                                                      | String                             |
| channel\_response\_message | Response message from payment channel provider.                                                                                                                                   | String                             |
| signature\_key             | Combination of parameters such as `order_id`, `status_code`, `gross_amount`, `server_key` to verify integrity of payload/response.                                                | String                             |
| currency                   | ISO-4217 representation of three-letter alphabetic currency code. Value: `IDR`.<br /> **Note**: Currently only `IDR` is supported.                                                | String                             |