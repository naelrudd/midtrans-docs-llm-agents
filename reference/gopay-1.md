---
updatedAt: 2026-05-20T08:46:48.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# GoPay

> 📘 GoPay Media Kit
>
> To have a consistent and standardized GoPay branding across platform, we highly recommend merchants to refer to our media kit. Please refer to this page <https://gopay.co.id/media-kit> to access our brand guideline and image bank.

GoPay is an *E-Wallet* . Users can pay using the Gojek app, GoPay app or any QRIS compatible app. The user flow is different for web browser (on a computer or a tablet) and mobile phone:

1. **QRIS Code** - This is the user flow on a web browser (on a computer or a tablet). User is shown a QRIS code and asked to scan using any QRIS compatible app, such as Gojek app or GoPay app. (Sequence Diagram for QR Code)
2. **Deeplink** - This is the user flow on a mobile device. User gets redirected to the GoPay app to finish payment. (Sequence Diagram Deeplink). For more details related to redirection to GoPay app, please read [this article](https://docs.midtrans.com/reference/faq-redirection-to-gojek-gopay-app).

By default, GoPay Deeplink and QRIS's transaction expiry is 15 minutes (min 20s, max 7 days). For custom expiry, please refer to [this section](https://docs.midtrans.com/reference/custom-expiry-object).

<br />

<b>Sequence Diagram for QR Code</b>

<Image align="center" src="https://files.readme.io/7322595-midtrans_api_doc-Page-1_1.jpg" title="gopay-qr (1).png" />

<br />

<b>Sequence Diagram for Deeplink</b>

<Image align="center" src="https://files.readme.io/6d09be9-midtrans_api_doc-Page-2.jpg" title="gopay-deeplink (1).png" />

<br />

The steps to integrate with GoPay are as follows:

1. Create payment instructions for users (see example below).
2. Send the charge API request to Midtrans.
3. Alter payment flow depending on the device used:

* On a computer or tablet: Show QRIS code image (on a computer or a tablet).
* On a mobile device: Redirect user with the deeplink URL that given from the response.

4. [Handle notifications](/reference/notifications-handling) from Midtrans.

<br />

> 📘 Instruction Example For QRIS Code
>
> 1. Tap Pay using GoPay.
> 2. Click Pay Now. QRIS code will be displayed.
> 3. Open Gojek app or GoPay app on your mobile phone.
> 4. Scan the QRIS code.
> 5. Verify your payment details and then click Pay.
> 6. Verify your Security PIN and finish your transaction.

<br />

<Image align="center" src="https://files.readme.io/d56f4a3-Screenshot_2023-12-15_at_15.36.29.png" />

<br />

> 📘 Instruction Example For Deeplink
>
> 1. Tap Pay using GoPay.
> 2. You will be redirected to GoPay App.
> 3. Verify your payment details and then click Pay.
> 4. Verify your Security PIN and finish your transaction.

<br />

<Image align="center" src="https://files.readme.io/a1c7373-Screenshot_2023-12-15_at_13.44.16.png" />

<br />

**In summary:**

Send a Charge API request with the details of the transaction such as `payment_type`:`gopay`, `transaction_details`, `item_details`, and `customer_details`. Successful request returns a deeplink redirect URL or QR code image URL.

<br />

***

<br />

## GoPay Charge API Request

<br />

```json Sample Request - Charge API
{
  "payment_type": "gopay",
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
  "gopay": {
    "enable_callback": true,
    "callback_url": "someapps://callback"
  }
}
```

| JSON Attribute       | Description                                                                    | Type                                     | Required |
| -------------------- | ------------------------------------------------------------------------------ | ---------------------------------------- | -------- |
| payment\_type        | Set GoPay payment method. Value: `gopay`.                                      | String                                   | Required |
| transaction\_details | The details of the specific transaction such as `order_id` and `gross_amount`. | [Object](https://docs.midtrans.com/reference/transaction-details-object) | Required |
| item\_details        | Details of the item(s) purchased by the customer.                              | [Object](https://docs.midtrans.com/reference/item-details-object)        | Optional |
| customer\_details    | Details of the customer.                                                       | [Object](https://docs.midtrans.com/reference/customer-details-object)    | Optional |
| gopay                | Charge details using GoPay.                                                    | [Object](https://docs.midtrans.com/reference/gopay-object)               | Required |

<br />

***

<br />

## GoPay Charge Response and Notifications

<br />

```json Success
{
	"status_code": "201",
	"status_message": "GO-PAY billing created",
	"transaction_id": "e48447d1-cfa9-4b02-b163-2e915d4417ac",
	"order_id": "SAMPLE-ORDER-ID-01",
	"gross_amount": "10000.00",
	"payment_type": "gopay",
	"transaction_time": "2017-10-04 12:00:00",
	"transaction_status": "pending",
	"actions": [{
			"name": "generate-qr-code",
			"method": "GET",
			"url": "https://api.midtrans.com/v2/gopay/e48447d1-cfa9-4b02-b163-2e915d4417ac/qr-code"
  	},
		{
			"name": "generate-qr-code-v2",
			"method": "GET",
			"url": "https://api.midtrans.com//v4/qris/gopay/A120250818053027lQ9S1FXLIHID/qr-code"
		},
    {
			"name": "deeplink-redirect",
			"method": "GET",
			"url": "gojek://gopay/merchanttransfer?tref=1509110800474199656LMVO&amount=10000&activity=GP:RR&callback_url=someapps://callback?order_id=SAMPLE-ORDER-ID-01"
		},
		{
			"name": "get-status",
			"method": "GET",
			"url": "https://api.midtrans.com/v2/e48447d1-cfa9-4b02-b163-2e915d4417ac/status"
		},
		{
			"name": "cancel",
			"method": "POST",
			"url": "https://api.midtrans.com/v2/e48447d1-cfa9-4b02-b163-2e915d4417ac/cancel",
			"fields": []
		}
	],
	"channel_response_code": "200",
	"channel_response_message": "Success",
  "currency": "IDR"
}
```
```json Pending
{
  "status_code": "201",
  "status_message": "midtrans payment notification",
  "transaction_id": "1c28dbbb-8596-48e4-85d7-9f1382db8a1f",
  "order_id": "order03",
  "gross_amount": "275000.00",
  "payment_type": "gopay",
  "transaction_time": "2016-06-19 15:50:12",
  "transaction_status": "pending",
  "signature_key": "40747f7f8f489c423c8ed72879ca8cb28dcd0c03fc9a192138667c4588f91486ae46094a6695d9fddbce0abab8055fd483b65ecf59e3c43d4a22cc024326993a"
}
```
```json Settlement
{
  "status_code": "200",
  "status_message": "midtrans payment notification",
  "transaction_id": "1c28dbbb-8596-48e4-85d7-9f1382db8a1f",
  "order_id": "order03",
  "gross_amount": "275000.00",
  "payment_type": "gopay",
  "payment_option_type": "GOPAY_WALLET",
  "transaction_time": "2016-06-19 15:54:42",
  "transaction_status": "settlement",
  "signature_key": "973d175e6368ad844b5817882489e6b22934d796a41a0573c066b1e64532dc0001087b87d877a3eac37cba20a733e1305f5e62739e65ff501d5d33c5ac62530f"
}
```
```json Expired
"status_code": "202",
  "status_message": "midtrans payment notification",
  "transaction_id": "1c28dbbb-8596-48e4-85d7-9f1382db8a1f",
  "order_id": "order03",
  "gross_amount": "275000.00",
  "payment_type": "gopay",
  "transaction_time": "2016-06-20 15:50:12",
  "transaction_status": "expire",
  "signature_key": "53c6e2e3639a6b5c09b9103aa343f00cfd0168c6a69a2d4f2203bdc58072531ad7b340ea01725538996a7827c4ce091fb94d0aa70778a20c69d3f9991e0f65eb"
}
```

<Table align={["left","left","left"]}>
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
        status_code
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
        status_message
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
        transaction_id
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
        order_id
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
        gross_amount
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
        payment_type
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
        payment_option_type
      </td>

      <td>
        Type of payment that is being used, possible values are GOPAY_WALLET, PAY_LATER, GO_CICIL, GOPAY_COINS (more possible values will be added once we launch more payment option on GoPay). Only available for GoPay payment type. <br /><br /> Will be returned on Settlement, Refund and Partial Refund notification only.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        transaction_time
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
        transaction_status
      </td>

      <td>
        Status of GoPay transaction. Possible values are<br />`pending`, `settlement`, `expire`, `deny`.
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

        Use `generate-qr-code` action to render the QR code image (PNG format).

        Use `generate-qr-code-v2` action to render the QR code image with ASPI's border (PNG format, _see reference on the callout below_).

        Use `deeplink-redirect` action to redirect to Gojek apps.
      </td>

      <td>
        Array([Object](https://docs.midtrans.com/reference/action-object))
      </td>
    </tr>

    <tr>
      <td>
        channel_response_code
      </td>

      <td>
        Response code from payment channel provider.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        channel_response_message
      </td>

      <td>
        Response message from payment channel provider.
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
        signature_key
      </td>

      <td>
        Combination of parameters such as `order_id`, `status_code`, `gross_amount`, `server_key` to verify integrity of payload/response.
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

  We are introducing a new method for merchants to generate QR codes. In the response’s actions array, we have added a new object containing a URL that merchants can use to generate a QR code in ASPI’s format. You can use the URL inside the new object named _generate-qr-code-v2_ to create the QR code.

  Reference

  <Image align="center" width="200px" src="https://files.readme.io/8b4ab6e37458ceecfdb71b323ef641796d84cc0dffd0641d53258c3b05c246fd-image.png" />
</Callout>

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

| Query Parameter | Description                                                                                                            | Type   |
| --------------- | ---------------------------------------------------------------------------------------------------------------------- | ------ |
| order\_id       | Order ID sent on the Charge Request.                                                                                   | String |
| result          | Result of the transaction to decide what kind of page to show to customer. Possible values are `success` or `failure`. | String |

<br />

> 🚧 Note
>
> It is highly recommended to avoid using value passed on `result` to update status on backend. There is [HTTP notification](https://docs.midtrans.com/reference/notifications-handling) for this use case.

<br />

The steps to integrate with GoPay deeplink (Please look into the GoPay Charge API Request for sample implementation) are given below.

1. Set `enable_callback` parameter in the charge request to `true`.
2. Set `callback_url` with the deeplink URL redirecting to E-commerce apps (via API request / configure in Dashboard > Settings > Payments)
3. Handle redirection with above parameters.