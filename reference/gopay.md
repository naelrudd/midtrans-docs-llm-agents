---
updatedAt: 2026-06-13T04:55:49.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# GoPay & QRIS

GoPay is an e-Wallet payment method. Users will pay using the GoPay app. The user flow varies when using a Web Browser (on a computer) compared to a SmartPhone.

This API reference describes implementation of regular payment flow with GoPay and QRIS issued by GoPay. To implement GoPay Tokenizations in Snap, see this [page](/reference/gopay-tokenization-1).

You can also get a static QRIS version of your GoPay QRIS. To do so, once you have GoPay activated in your business, go to [Dashboard > + New Payment Methods,](https://dashboard.midtrans.com/new_payment_method) then proceed with the activation. Once done, in the same page, you should see a new tab called 'Manage Static QRIS', create your Static QRIS and label it with your own identifier (to help you identify the trx in your reports), then download the PDF file.

By default, GoPay Deeplink and Dynamic QRIS's transaction expiry is 15 minutes (min 20s, max 7 days).

<br />

> 📘 UI Mode
>
> We will show either QRIS or Deeplink based on customer's screen size (wide screen will get QRIS, while small screen will get deeplink). Merchant can however specify whether GoPay will be shown in deeplink or QR format persistently using `options.uiMode` in [Snap JS](/reference/snap-js). UI Mode is specified to `auto` by default.
>
> This guide will assume that the value of `uiMode` in [Snap.JS options](/reference/snap-js) is `auto`, the recommended value.

> 📘 Redirecting users to GoPay app
>
> By default,  user should be able to be redirected to GoPay app by default; no special handling needed from merchant. This applies for for QRIS link redirection to GoPay app too.&#x20;
>
> However, if you're rendering Snap Checkout from your mobile app, your WebView implementation might not allow you to redirect users to a different app by default. If that happens, please follow this <Anchor target="_blank" href="https://docs.midtrans.com/docs/technical-faq?id=ios-webview-specific#5-your-apps-webview-redirect-implementation-is-blocked-by-androidios-platform">guide </Anchor>for a possible workaround.&#x20;

> 📘 GoPay Deeplink & Tokenization redirection to GoPay app only
>
> With the launch of GoPay standalone app, **starting from 1 April 2026**, user will be redirected to GoPay app only to complete their payment (gradual rollout).
>
> **How will this impact the user experience?**
>
> 1. By default user will be redirected to GoPay app if the app is installed.
> 2. If GoPay app is not installed (even if user has Gojek app), user will see GoPay webpage and asked to download GoPay app from the play store or app store.
> 3. After downloading the app, user can continue to complete linking or payment.
>
> **How can merchant support this flow?**
>
> Just like the previous Gojek and GoPay app redirection flow, merchant just need to ensure that they have done these 3 items below:
>
> <Table align={["left"]}>
>   <thead>
>     <tr>
>       <th>
>         What merchants need to do
>       </th>
>     </tr>
>   </thead>
>
>   <tbody>
>     <tr>
>       <td>
>         1. Merchant should ensure that they can **support redirection URL in universal link format** to be able to be redirected to GoPay / Gojek app
>       </td>
>     </tr>
>
>     <tr>
>       <td>
>         2. We recommends merchant to always open our redirection URL outside of merhant's in-app webview (or directly in the user's native browser). In case merchants open the URL inside a werbview and merchant have whilisting logic, **merchants should make sure to whitelist** `gopay.co.id/*`, `*.gopay.co.id/*`, `gojek.link/*`. Please ensure that the existing URLs are also kept whitelisted on merchants' side.
>       </td>
>     </tr>
>
>     <tr>
>       <td>
>         3. In case merchants have webview implementation, merchant should ensure that the webview redirection is **not blocked by Android/iOS** platform. Fore more details on how to do this please read this FAQ page: [Android](https://docs.midtrans.com/docs/technical-faq#android)  | [iOS](https://docs.midtrans.com/docs/technical-faq#ios-webview-specific)
>       </td>
>     </tr>
>   </tbody>
> </Table>

<br />

***

<br />

## When users make a purchase using GoPay on a Web Browser(on a computer)

<br />

1. Users see a QR code on their Web Browser
2. Users open the GoPay app on their phone
3. Users tap the ***Pay*** function on the GoPay app
4. Users point their camera to the QR Code
5. Users check their payment details on the GoPay app and then tap Pay

<br />

<Image src="https://files.readme.io/79dc8af8df2314aa5f806a1b64c798faeb3fb3be50c04bfc0beac2363f83a53b-qris.png" align="center" />

<br />

6. The transaction is complete and the users' GoPay balance is deducted

7. Midtrans will **mark the payment\_type of the transaction as** `qris`. This will also impact the following:

* The JSON fields format (returned on Webhook/HTTP Notifications & Get Status API response) is `"payment_type": "qris"`

* The `"payment_type": "qris"` displayed on **Midtrans Dashboard**, and when you download transactions.

<br />

### Detailed payment Flow for GoPay on a Desktop PC/Laptop

<br />

This is the payment flow if customers process GoPay Payments on a Desktop PC/Laptop.

<br />

![](https://files.readme.io/7f52a26-gopay-qr.png "gopay-qr.png")

<br />

***

<br />

## When users make a purchase on their SmartPhone

<br />

1. Users are automatically redirected to the GoPay app when making purchases on their SmartPhone

2. Users finish the payment on the GoPay app

   <Image src="https://files.readme.io/68eceb38188727b4d4012b3b26fc0f805052c4e1b3fee39f8f4ea2eae9303c79-deeplink.png" align="center" />

3. The transaction is complete and their GoPay balance is deducted

4. Midtrans will **mark the payment\_type of the transaction as** `gopay`. This will also impact the following:

* The JSON fields format (returned on Webhook/HTTP Notifications & Get Status API response) is `"payment_type": "gopay"`

* The `"payment_type": "gopay"` displayed on **Midtrans Dashboard**, and when you download transactions.

**Note:** For a list of failure cases, please refer [here](/reference/sample-response).

<br />

### Detailed Payment Flow for GoPay on a Smartphone

<br />

This is the payment flow if customers process GoPay Payments on a smartphone.

<br />

![](https://files.readme.io/f92ebbc-gopay-deeplink.png "gopay-deeplink.png")

<br />

***

<br />

## Sample JSON Request Body

<br />

```json
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
    "enable_callback": true,
    "callback_url": "http://gopay.com"
  }
}
```

| Parameter                                                                                                         | Description                                                            |
| ----------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| transaction *details<br />*[Transaction Details](/reference/json-objects#transaction-details) Object (required)\_ | Unique transaction ID                                                  |
| item *details<br />*[Item Details](/reference/json-objects#item-details) Object (optional)\_                      | Item details will be paid by customer                                  |
| customer *details<br />*[Customer Details](/reference/json-objects#customer-details) Object (optional)\_          | Details of the customer                                                |
| enabled\_payments<br />*Array (optional)*                                                                         | Set what payment method to show in Snap's payment list. Value: `gopay` |
| gopay                 <br />*[Gopay](/reference/json-objects#gopay-object) (optional)*                            | GoPay payment options                                                  |

<br />

***

<br />

## Implementing GoPay Deeplink Callback

<br />

In addition to the standard mobile apps flow, you can implement deeplink callback to redirect customer back from GoPay to your app.

<br />

> 📘 Prerequisites
>
> E-commerce needs to prepare a deeplink which accepts two query parameters.

<br />

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Query Parameter
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
        order\_id
      </td>

      <td>
        Order ID sent on the API Request.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        result
      </td>

      <td>
        Result of the transaction to decide what kind of page to show to customer. Possible values are `success`, `failure`, or `abort`.

        - `success`: Payment successful
        - `failure`: Payment failed
        - `abort`: User cancel the payment
      </td>

      <td>
        String
      </td>
    </tr>
  </tbody>
</Table>

<br />

The steps to integrate with GoPay deeplink (Please look into the GoPay API Request for sample implementation) are given below.

<br />

1. Set `enable_callback` parameter in the api request to `true`.
2. Set `callback_url` with the deeplink URL redirecting to E-commerce apps via API request or configure it in Dashboard > Snap Preferences.
   1. **Do not** add `result` as a query param on the callback\_url as it will be conflicting with the actual query param from GoPay app.
3. Handle redirection with above parameters.

<br />

For a full list of request body parameters please refer to the [Request Body (JSON Parameter)](https://docs.midtrans.com/reference/request-body-json-parameter) section.

<br />

> 🚧
>
> It is highly recommended to avoid using value passed on `result` to update status on backend. There is [HTTP notification](/reference/handle-notifications) for this use case.

<br />