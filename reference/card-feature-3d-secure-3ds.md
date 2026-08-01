---
updatedAt: 2025-11-11T13:16:45.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Feature: 3D Secure (3DS)

Three Domain Secure (3DS) is a security feature which requires the customer to complete an additional verification step while making payments using card. 3DS can be enabled/disabled for specific transactions. Always enable 3DS, to prevent unnecessary security and chargeback risks.\
Successful request returns `redirect_url` to redirect customer to the authentication page. After completing the authentication process, you will receive notification containing the transaction details and 3DS result.

<br />

***

<br />

## 3DS Charge Request

```json Sample Request - 3DS Charge
{
  "payment_type": "credit_card",
  "transaction_details": {
    "order_id": "C17550",
    "gross_amount": 145000
  },
  "credit_card": {
    "token_id": "< your token ID >",
    "authentication": true,
    "callback_type": "js_event"
  }
}
```

The `credit_card` object in Charge request to configure 3DS feature is identical with [Card Charge Request](/reference/charge-transactions-on-card#card-charge-request), with the additional attributes given below.

| JSON Attribute | Description                                                                                                                                                                                                                                   | Type    | Required |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- |
| token\_id      | Token ID represents customer's card information acquired from [Get Card Token](/reference/get-token#getting-card-token) response.                                                                                                             | String  | Required |
| authentication | Flag to enable the 3D secure authentication. Default value is `false`.                                                                                                                                                                        | Boolean | Optional |
| callback\_type | Determines how the transaction status is updated to the merchant frontend. Possible values are `js_event` (default) and `form`. For more details, refer [Handling 3DS Callback](/reference/card-feature-3d-secure-3ds#handling-3ds-callback). | String  | Optional |

<br />

***

<br />

## 3DS Charge Response and Notifications

### Sample Response

```json Success
{
  "status_code": "201",
  "status_message": "Success, Credit Card transaction is successful",
  "transaction_id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
  "order_id": "C17550",
  "redirect_url": "https://api.veritrans.co.id/v2/3ds/redirect/451249-2595-e14aac7f-cfb3-4ab2-98ab-5cc5e70f4b2c",
  "gross_amount": "145000.00",
  "currency": "IDR",
  "payment_type": "credit_card",
  "transaction_time": "2018-09-12 22:10:23",
  "transaction_status": "pending",
  "masked_card": "48111111-1114",
  "card_type": "credit",
  "three_ds_version": "2",
  "on_us": true
}
```
```json Pending after submit OTP 3DS 2.0
{
  "status_code": "201",
  "status_message": "Success, Credit Card transaction is successful",
  "transaction_id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
  "order_id": "C17550",
  "redirect_url": "https://api.veritrans.co.id/v2/3ds/redirect/451249-2595-e14aac7f-cfb3-4ab2-98ab-5cc5e70f4b2c",
  "gross_amount": "145000.00",
  "currency": "IDR",
  "payment_type": "credit_card",
  "transaction_time": "2018-09-12 22:10:23",
  "transaction_status": "pending",
  "masked_card": "48111111-1114",
  "card_type": "credit",
  "three_ds_version": "2",
  "three_ds_challenge_completion": false
}
```
```json Error Response
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
  "on_us": true
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
  "status_message": "midtrans payment notification",
  "channel_response_code": "00",
  "channel_response_message": "Approved",
  "card_type": "credit",
  "three_ds_version": "2"
}
```

The 3DS response is identical with [Card Payment Charge Response](/reference/charge-transactions-on-card#card-charge-response-and-notifications), with the additional attributes given below.

| JSON Attribute | Description                                                      | Type   |
| -------------- | ---------------------------------------------------------------- | ------ |
| redirect\_url  | The URL to redirect the user to 3D Secure authentication page.   | String |
| eci            | The 3D secure ECI Code indicating the result of the 3DS process. | String |

<br />

***

<br />

## Handling 3DS Callback

By default, 3DS callback scheme is set as `js_event`. It is optimized for merchants who prefer to open the 3DS page without leaving from their page.

Midtrans JavaScript library provides functions to handle the redirect URL and its callback response.

```javascript Authenticate function from the JavaScript Library to handle the redirect URL and callback response
var redirect_url = '<redirect_url Retrieved from Charge Response>';

// callback functions
var options = {
  performAuthentication: function(redirect_url){
    // Implement how you will open iframe to display 3ds authentication redirect_url to customer
    popupModal.openPopup(redirect_url);
  },
  onSuccess: function(response){
    // 3ds authentication success, implement payment success scenario
    console.log('response:',response);
    popupModal.closePopup();
  },
  onFailure: function(response){
    // 3ds authentication failure, implement payment failure scenario
    console.log('response:',response);
    popupModal.closePopup();
  },
  onPending: function(response){
    // transaction is pending, transaction result will be notified later via 
    // HTTP POST notification, implement as you wish here
    console.log('response:',response);
    popupModal.closePopup();
  }
};

// trigger `authenticate` function
MidtransNew3ds.authenticate(redirect_url, options);

/**
 * Example helper functions to open Iframe popup, you may replace this with your own 
 * method of open iframe. In this example, PicoModal library is used by including 
 * this script tag on the HTML:
 * <script src="https://cdnjs.cloudflare.com/ajax/libs/picomodal/3.0.0/picoModal.js"></script>
 */
var popupModal = (function(){
  var modal = null;
  return {
    openPopup(url){
      modal = picoModal({
        content:'<iframe frameborder="0" style="height:90vh; width:100%;" src="'+url+'"></iframe>',
        width: "75%",
        closeButton: false,
        overlayClose: false,
        escCloses: false
      }).show();
    },
    closePopup(){
      try{
        modal.close();
      } catch(e) {}
    }
  }
}());

/**
 * Alternatively, instead of opening 3ds authentication redirect_url using iframe,
 * you can also redirect customer using:
 * MidtransNew3ds.redirect( redirect_url, { callbackUrl : 'https://mywebsite.com/finish_3ds' });
 **/
```

```javascript Sample Callback Function Implementation
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sample</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/picomodal/3.0.0/picoModal.js"></script>
    <script id="midtrans-script" type="text/javascript" src="https://api.midtrans.com/v2/assets/js/midtrans-new-3ds.min.js" data-environment="sandbox" data-client-key="<INSERT YOUR CLIENT KEY HERE>"></script>
</head>
<body>
    <script>
        /**
         * Example helper functions to open Iframe popup, you may replace this with your own 
         * method of open iframe. In this example, PicoModal library is used by including 
         * this script tag on the HTML:
         */
        var popupModal = (function(){
            var modal = null;
            return {
                openPopup(url){
                modal = picoModal({
                    content:'<iframe frameborder="0" style="height:90vh; width:100%;" src="'+url+'"></iframe>',
                    width: "75%",
                    closeButton: false,
                    overlayClose: false,
                    escCloses: false
                }).show();
                },
                closePopup(){
                try{
                    modal.close();
                } catch(e) {}
                }
            }
        }());
    </script>

    <script>
        var redirect_url = '<redirect_url Retrieved from Charge Response>';

        // callback functions
        var options = {
            performAuthentication: function(redirect_url){
                // Implement how you will open iframe to display 3ds authentication redirect_url to customer
                popupModal.openPopup(redirect_url);
            },
            onSuccess: function(response){
                // 3ds authentication success, implement payment success scenario
                console.log('response:',response);
                popupModal.closePopup();
                // // Simulate an HTTP redirect:
                window.location.replace("http://midtrans.com?status=success");
            },
            onFailure: function(response){
                // 3ds authentication failure, implement payment failure scenario
                console.log('response:',response);
                popupModal.closePopup();
            },
            onPending: function(response){
                // transaction is pending, transaction result will be notified later via 
                // HTTP POST notification, implement as you wish here
                console.log('response:',response);
                popupModal.closePopup();
            }
        };

        // trigger `authenticate` function
        MidtransNew3ds.authenticate(redirect_url, options);
    </script>   
</body>
</html>
```

Callback via `form` is a simple web redirection. From the merchant website, the customer is redirected to 3DS page and then back to merchant website. For callback via `js-event` open 3DS page in an iFrame, and the callback happens as a JSON.

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
        The payment method used by the customer. <br /> Value: `credit_card`.<br />**Note**: For any transactions using payment card (credit or debit), `payment_type` is `credit_card`.
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
        Transaction status after charge card transaction. Possible values are<br/>`capture`: Transaction is accepted by the bank and ready for settlement. <br/>`deny`: transaction is denied by the bank or FDS.<br/>`authorize`: card is authorized in Pre-authorization feature.<br/>`pending`: Credit card is pending and you will need to rely on the http notification webhook to receive the final transaction status.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        fraud\_status
      </td>

      <td>
        Detection result by Fraud Detection System (FDS). Possible values are<br/>`accept`: Approved by FDS.<br/>`challenge`: Questioned by FDS.<br /> **Note**: [Approve transaction](https://docs.midtrans.com/reference/approve-transaction) to accept it or transaction will get cancelled automatically during settlement.<br/>`deny`: Denied by FDS. Transaction automatically failed.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        masked\_card
      </td>

      <td>
        First 8-digits and last 4-digits of customer's card number.
      </td>

      <td>
        String
      </td>
    </tr>

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
        bank
      </td>

      <td>
        The name of the *Acquiring Bank*.
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
        Status message describing the result of the API request.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        approval\_code
      </td>

      <td>
        Approval code. It can be used for refund. This does not exist on denied transaction.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        eci
      </td>

      <td>
        The 3D secure ECI Code indicating the result of the 3DS process.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        channel\_response\_code
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
        channel\_response\_message
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
        card\_type
      </td>

      <td>
        Type of payment card used for the transaction. Possible values are `credit`, `debit`.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        three\_ds\_version
      </td>

      <td>
        3DS Version that used for transaction (This field only present for 3DS Transaction). Possible values are `1`, `2`
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        three\_ds\_challenge\_completion
      </td>

      <td>
        3DS Challenge completion state to indicate the customer has been submitted the OTP or not(it doesn't matter if the OTP is valid or not). Possible values are `true`, `false`
      </td>

      <td>
        Boolean
      </td>
    </tr>
  </tbody>
</Table>

> 📘 Note
>
> If you receive pending transaction\_status, you will need to rely on the http notification webhook to receive the final transaction status

<br />

***

<br />

# Redirecting to 3DS Page (3DS 2.0 Compatible)

After proceeding card transaction to Charge API request, if the transaction needs 3DS authentication, you will receive `redirect_url` in the response. You can optionally use built-in `MidtransNew3ds.redirect` function to redirect the customer.

After 3DS process is completed, the customer is redirected back to the website specified in `callbackUrl` or the *Finish Redirect URL* configured on your MAP account.\
This final redirect is HTTP POST method. It contains JSON string encapsulated as value of `response` key of the POST form-data.

Callback response object attributes are listed below.

```javascript Redirect Function
var options = {
    // In case, Merchant needs to override for each transactions
    callbackUrl = "<ANY LINK>"
}

MidtransNew3ds.redirect(redirect_url, options);
```
```html How Midtrans redirects customer via HTML form (POST Method)
<form id="veritrans" method="post" action="<callbackUrl>">
    <input type="hidden" name="response" value="<JSON FORMAT CALLBACK OBJECT>"/>
</form>
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
        The payment method used by the customer.
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
        Transaction status after charge credit card transaction. Possible values are<br/>`capture` : Transaction is accepted by the bank and ready for settlement. <br/>`deny`: transaction is denied by the bank or FDS.<br/>`authorize`: Credit card is authorized in pre-authorization feature.<br/>`pending`: Credit card is pending and you will need to rely on the http notification webhook to receive the final transaction status..
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        fraud\_status
      </td>

      <td>
        Detection result by Fraud Detection System (FDS). Possible values are<br/>`accept` : Approved by FDS.<br/>`challenge`: Questioned by FDS. **Note:** [Approve transaction](/reference/approve-transaction) to accept it or transaction gets automatically canceled during settlement.<br/>`deny`: Denied by FDS. Transaction automatically failed.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        masked\_card
      </td>

      <td>
        First 8-digits and last 4-digits of customer's credit card number.
      </td>

      <td>
        String
      </td>
    </tr>

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
        bank
      </td>

      <td>
        The name of the acquiring bank.
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
        Status message describing the result of the API request.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        approval\_code
      </td>

      <td>
        Approval code. It can be used for refund. This does not exist on denied transaction.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        eci
      </td>

      <td>
        The 3D secure ECI Code.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        channel\_response\_code
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
        channel\_response\_message
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
        card\_type
      </td>

      <td>
        Type of card used for the transaction. Possible values are `credit`, `debit`.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        three\_ds\_version
      </td>

      <td>
        3DS Version that used for transaction (This field only present for 3DS Transaction). Possible values are `1`, `2`
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        three\_ds\_challenge\_completion
      </td>

      <td>
        3DS Challenge completion state to indicate the customer has submit the OTP or not(it doesn't matter if the OTP is valid or not). Possible values are `true`, `false`
      </td>

      <td>
        Boolean
      </td>
    </tr>
  </tbody>
</Table>

> 📘 Note
>
> If you receive pending transaction\_status, you will need to rely on the http notification webhook to receive the final transaction status

<br />

Optional parameter is given below.

| Name        | Description                                                                      | Required |
| ----------- | -------------------------------------------------------------------------------- | -------- |
| callbackUrl | To override where the customer gets redirected after 3DS authentication is done. | Optional |

<br />

***

<br />

## 3DS Redirect Page – Gather Browser Information

As mentioned earlier, after 3DS transaction is charged successfully, the response includes a redirect\_url, which directs the customer to an authentication page. At this stage, Midtrans returns an HTML page that collects browser information via JavaScript. This Midtrans redirect page automatically gathers the following browser details:

```Text Sample: browser information
"BrowserInfo": {
	"browserAcceptHeader": "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8",
	"browserColorDepth": "24",
	"browserIP": "103.84.5.252",
	"browserJavaEnabled": false,
	"browserJavascriptEnabled": true,
	"browserLanguage": "en-GB",
	"browserScreenHeight": 932,
	"browserScreenWidth": 430,
	"browserTZ": -420,
	"browserUserAgent": "Mozilla/5.0 (iPhone; CPU iPhone OS 18_1_1 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.1.1 Mobile/15E148 Safari/604.1",
	"challengeWindowSize": "05"
}
```

<br />

> 📘 Important
>
> Please do not override `BrowserInfo` parameters when redirecting to Midtrans page. This browser information will be forwarded to Midtrans Server in Base64 format as parameters.

```Text Sample: JavaScript Gather Browser Information
function setBrowserInformation(browserInfo) {
    var browserJavascriptEnabled = true;
    if (browserInfo === undefined || browserInfo == null || browserInfo.length <= 0) {
        browserInfo={};
        browserJavascriptEnabled = false;
        Object.assign(browserInfo, {browserUserAgent: window.navigator.userAgent});
    }

    Object.assign(browserInfo, {browserJavascriptEnabled: browserJavascriptEnabled});
    document.getElementById('BrowserInfo').value = window.ThreedDS2Utils.base64Url.encode(JSON.stringify(browserInfo));
}

<form id="veritrans" method="post" action="{{threeDSCallbackUrl}}">
    <input type="hidden" name="BrowserInfo" id="BrowserInfo"/>
</form>
```

<br />

3D Secure 2.0 (3DS 2.0) introduces more advanced authentication mechanism designed to improve security and reduce fraud while minimizing friction for customers. One of the key improvements in 3DS 2.0 is risk-based authentication (RBA), where the issuer evaluates multiple factors, including browser and device information, to determine whether additional authentication is needed.

To support this process, the browser information collected in the redirect page plays a critical role in helping banks and card networks assess the legitimacy of a transaction. Incorrect or missing browser details may lead to authentication failures, requiring additional verification or causing the transaction to be declined.

Potential Issues and Best Practices:

* Avoid modifying `BrowserInfo` parameters
  * Any alterations to` browserUserAgent, browserIP, browserScreenWidth, or other fields` may lead to transaction failures.
* Do not rename `BrowserInfo` object
  * The 3DS system expects a standardized format. Any renaming or structural changes could disrupt the authentication process.
* Using a VPN may cause transaction failures

> 📘 Using VPN for 3DS Transaction
>
> We strongly recommend that customers do not use VPN during a 3DS transaction.\
> The `browserIP` field is a key data point sent to the 3DS Servers, which is used for risk evaluation. If the detected IP does not match the customer's typical location, it may trigger high-risk alerts, potentially leading to authentication failure or rejection by the 3DS servers (Bank, Card Network, ACS).

By following these guidelines, merchants and customers can ensure smooth authentication and minimize transaction disruptions when using 3DS 2.0.

***

## Opening 3DS Page via iFrame (3DS 2.0 Compatible)

Optionally, you can use `MidtransNew3ds.performAuthentication` function to open `redirect_url` as iFrame. It is a substitute to the redirection scheme.

After 3DS process is completed by a customer, your website receives JSONP callback containing the transaction result.

Callback response object attributes are listed below.

```javascript Sample code to open redirect_url on iFrame (JQuery - FancyBox)
// Open 3DSecure dialog box
function openDialog(url) {
    // make sure to load fancybox in a script tag
    $.fancybox.open({
        href: url,
        type: 'iframe',
        autoSize: false,
        width: 400,
        height: 420,
        closeBtn: false,
        modal: true
    });
}

// Close 3DSecure dialog box
function closeDialog() {
    $.fancybox.close()
}

var options = {
  performAuthentication: function(url) {
    openDialog(url)
  },
  onSuccess: function(response) {
    // Successful handling
    closeDialog()
  },
  onPending: function(response) {
    // Pending handling
    closeDialog()
  },
  onFailure: function(response) {
    // Failure handling
    closeDialog()
  }
}

MidtransNew3ds.authenticate(redirect_url,options)
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
        The payment method used by the customer.
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
        Transaction status after charge credit card transaction. Possible values are<br/>`capture` : Transaction is accepted by the bank and ready for settlement. <br/>`deny`: transaction is denied by the bank or FDS.<br/>`authorize`: Credit card is authorized in pre-authorization feature.<br/>`pending`: Credit card is pending and you will need to rely on the http notification webhook to receive the final transaction status.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        fraud\_status
      </td>

      <td>
        Detection result by Fraud Detection System (FDS). Possible values are<br/>`accept` : Approved by FDS.<br/>`challenge`: Questioned by FDS. **Note:** [Approve transaction](/reference/approve-transaction) to accept it or transaction gets automatically canceled during settlement.<br/>`deny`: Denied by FDS. Transaction automatically failed.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        masked\_card
      </td>

      <td>
        First 8-digits and last 4-digits of customer's credit card number.
      </td>

      <td>
        String
      </td>
    </tr>

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
        bank
      </td>

      <td>
        The acquiring bank of the transaction.
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
        approval\_code
      </td>

      <td>
        Approval code. It can be used for refund. This does not exist on denied transaction.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        eci
      </td>

      <td>
        The 3D secure ECI Code.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        channel\_response\_code
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
        channel\_response\_message
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
        card\_type
      </td>

      <td>
        Type of card used for the transaction. Possible values are `credit`, `debit`.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        three\_ds\_version
      </td>

      <td>
        3DS Version that used for transaction (This field only present for 3DS Transaction). Possible values are `1`, `2`
      </td>

      <td>
        String
      </td>
    </tr>
  </tbody>
</Table>

> 📘 Note
>
> If you receive pending transaction\_status, you will need to rely on the http notification webhook to receive the final transaction status

<br />

Available options are given below.

| Name                  | Description                                                                                    |
| --------------------- | ---------------------------------------------------------------------------------------------- |
| performAuthentication | Implementation to open redirect URL in iFrame.                                                 |
| onSuccess             | Handle to receive successful callback response.                                                |
| onPending             | Handle to receive callback response. Only applicable when merchant applied for async endpoint. |
| onFailure             | Handle to receive failure response.                                                            |

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "info": {
    "title": "core-api-credit-card-3ds",
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
        "summary": "Feature: 3D Secure (3DS)",
        "description": "",
        "operationId": "card-feature-3d-secure-3ds",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "required": [
                  "payment_type",
                  "credit_card"
                ],
                "properties": {
                  "payment_type": {
                    "type": "string",
                    "default": "credit_card"
                  },
                  "transaction_details": {
                    "properties": {
                      "gross_amount": {
                        "type": "string",
                        "default": "145000.00"
                      },
                      "order_id": {
                        "type": "string",
                        "default": "mid-1234567"
                      }
                    },
                    "required": [
                      "gross_amount"
                    ],
                    "type": "object"
                  },
                  "credit_card": {
                    "type": "object",
                    "required": [
                      "token_id"
                    ],
                    "properties": {
                      "token_id": {
                        "type": "string",
                        "default": "token_id"
                      },
                      "authentication": {
                        "type": "boolean",
                        "default": true
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
                    "value": "{\n  \"status_code\": \"201\",\n  \"status_message\": \"Credit Card transaction is in progress\",\n  \"transaction_id\": \"1a1a66f7-27a7-4844-ba1f-d86dcc16ab27\",\n  \"order_id\": \"C17550\",\n  \"redirect_url\": \"https://api.veritrans.co.id/v2/token/rba/redirect/451249-2595-e14aac7f-cfb3-4ab2-98ab-5cc5e70f4b2c\",\n  \"gross_amount\": \"145000.00\",\n  \"currency\": \"IDR\",\n  \"payment_type\": \"credit_card\",\n  \"transaction_time\": \"2018-09-12 22:10:23\",\n  \"transaction_status\": \"pending\",\n  \"masked_card\": \"48111111-1114\",\n  \"card_type\": \"credit\",\n  \"three_ds_version\": \"2\",\n  \"on_us\": true\n}"
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
                      "example": "Credit Card transaction is in progress"
                    },
                    "transaction_id": {
                      "type": "string",
                      "example": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27"
                    },
                    "order_id": {
                      "type": "string",
                      "example": "C17550"
                    },
                    "redirect_url": {
                      "type": "string",
                      "example": "https://api.veritrans.co.id/v2/token/rba/redirect/451249-2595-e14aac7f-cfb3-4ab2-98ab-5cc5e70f4b2c"
                    },
                    "gross_amount": {
                      "type": "string",
                      "example": "145000.00"
                    },
                    "currency": {
                      "type": "string",
                      "example": "IDR"
                    },
                    "payment_type": {
                      "type": "string",
                      "example": "credit_card"
                    },
                    "transaction_time": {
                      "type": "string",
                      "example": "2018-09-12 22:10:23"
                    },
                    "transaction_status": {
                      "type": "string",
                      "example": "pending"
                    },
                    "masked_card": {
                      "type": "string",
                      "example": "48111111-1114"
                    },
                    "card_type": {
                      "type": "string",
                      "example": "credit"
                    },
                    "three_ds_version": {
                      "type": "string",
                      "example": "2"
                    },
                    "on_us": {
                      "type": "boolean",
                      "example": true,
                      "default": true
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