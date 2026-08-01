---
updatedAt: 2026-05-20T05:53:28.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Snap JS

Show Snap UI in your website/app by embedding Snap JS within a page or loading it as an overlay in your website/app.

There are two ways to display Snap's UI modal in your web/app, first is by embedding Snap modal within your web/app's page (**Embedded mode**) or by displaying the modal as an overlay on your web/app's page (**Pop up mode**).

Alternatively, you can call Snap's checkout page in a new page via window redirection method. See the guide [here](/reference/window-redirection).

Sample implementation of [Embedded mode](https://demo.sandbox.midtrans.com/) and [Pop up mode](https://demo.midtrans.com).

<br />

***

<br />

# Snap Pop Up

`snap` pop up mode has 3 public functions: `pay`, `show` & `hide` .

<br />

## pay(snapToken, options)

<br />

Start Snap payment page. You can also implement callback to trigger your custom JavaScript implementation on each event.

<br />

```javascript
snap.pay('YOUR_SNAP_TOKEN', {
  onSuccess: function(result){console.log('success');console.log(result);},
  onPending: function(result){console.log('pending');console.log(result);},
  onError: function(result){console.log('error');console.log(result);},
  onClose: function(){console.log('customer closed the popup without finishing the payment');}
})
```

| Name                                                   | Description                                                                                                                                                                                                |
| ------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| snapToken <br /> *String (required)*                   | Snap token acquired from backend integration                                                                                                                                                               |
| enabledPayments <br /> *Array (optional)*              | List of payment types to be displayed. This will filter out enabled payments from backend integration.                                                                                                     |
| options.onSuccess <br /> *Function (optional)*         | Payment success callback (200 `status_code`)                                                                                                                                                               |
| options.onPending <br /> *Function (optional)*         | Payment pending callback (201 `status_code`)                                                                                                                                                               |
| options.onError <br /> *Function (optional)*           | Payment error callback (NOT `200` or `201` `status_code`)                                                                                                                                                  |
| options.onClose <br /> *Function (optional)*           | Called if customer has closed the payment popup prematurely without finishing the payment                                                                                                                  |
| options.language <br /> *String (optional)*            | Sets the language. This will override language setting on Merchant Administration Portal. Supported values are `en` (English) and `id` (Bahasa Indonesia). Defaults to `id`                                |
| options.autoCloseDelay <br /> *Integer (optional)*     | Auto closes the last page of Indomaret and Bank Transfer payments after the specified time delay. The time delay is specified in seconds. Setting it to `0` will disable this feature. Defaults to `0`.    |
| options.selectedPaymentType <br /> *String (optional)* | Skips order summary and select payment page to directly select a specific payment type. Supported values are `credit_card`, `echannel`, `permata_va`, `other_va`, `bca_va`, `bni_va`.                      |
| options.uiMode <br /> *String (optional)*              | Choose the UI mode for [GoPay](/reference/json-objects#gopay-object), [ShopeePay](/reference/json-objects#shopeepay-object) . Supported values are `deeplink`, `qr`, and `auto`. Set to `auto` by default. |

`onSuccess`, `onPending`, & `onError` function accept one parameter which is [Transaction Result](/reference/js-callback#transaction-result) object.

<br />

***

<br />

## show()

<br />

Show snap loading page. Helper function if you want to show instant loading feedback while getting `SNAP_TOKEN` using AJAX.

If AJAX success, call `snap.pay` to continue payment process. Else, call `snap.hide` to end loading page.

<br />

***

<br />

## hide()

<br />

Hide active snap page. Complementary function of `snap.show`. Helper function if you want to show instant loading feedback while getting `SNAP_TOKEN` using AJAX.

<br />

```javascript
function ajaxGetToken(transactionData, callback){
    var snapToken;
    // Request get token to your server & save result to snapToken variable

    if(snapToken){
      callback(null, snapToken);
    } else {
      callback(new Error('Failed to fetch snap token'),null);
    }
}

payButton.onclick(function(){
  snap.show();
  ajaxGetToken(transactionData, function(error, snapToken){
    if(error){
      snap.hide();
    } else {
      snap.pay(snapToken);
    }
  });
});
```

<br />

***

<br />

# Snap Embedded

<br />

Embed Snap modal within your page using this method. See how it will look like below.

<br />

<Image align="center" alt="Snap Embedded" caption="Snap Embedded - Web Implementation" src="https://files.readme.io/9b87685-Snap_Embedded.gif" width="% " />

<br />

<Image align="center" alt="Snap Embedded - Mobile Implementation via Mobile Webview" caption="Snap Embedded - Mobile Implementation via Mobile Webview" src="https://files.readme.io/39c1768-Snap_embedded_-_mobile.gif" width="40% " />

<br />

`snap` embedded mode has 3 functions; `embed`, `show`, and `hide`. `show` and `hide` works exactly the same as in Pop Up implementation.

<br />

## Embed Snap Modal

<br />

Steps to implement :

1. Create an empty div with the desired ID, e.g. `<div id="snap-container"></div>`. This div is where the SNAP application will be placed.
2. Add **snap.embed('$\{snap-token}', \{ embedId: $\{your div id, for example snap-container} })**. This will ensure that SNAP is correctly embedded and rendered within the div you previously set up.

<br />

```html html
<html>

<head>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <!-- @TODO: replace SET_YOUR_CLIENT_KEY_HERE with your client key -->
  <script type="text/javascript"
		src="https://app.sandbox.midtrans.com/snap/snap.js"
    data-client-key="SET_YOUR_CLIENT_KEY_HERE"></script>
  <!-- Note: replace with src="https://app.midtrans.com/snap/snap.js" for Production environment -->
</head>

<body>
  <button id="pay-button">Pay!</button>

  <!-- @TODO: You can add the desired ID as a reference for the embedId parameter. -->
  <div id="snap-container"></div>

  <script type="text/javascript">
    // For example trigger on button clicked, or any time you need
    var payButton = document.getElementById('pay-button');
    payButton.addEventListener('click', function () {
      // Trigger snap popup. @TODO: Replace TRANSACTION_TOKEN_HERE with your transaction token.
      // Also, use the embedId that you defined in the div above, here.
      window.snap.embed('YOUR_SNAP_TOKEN', {
        embedId: 'snap-container'
      });
    });
  </script>
</body>

</html>
```

<br />

To make the modal blends more seamlessly to your website, is it possible to hide Snap's modal header that shows your merchant/display name. To do so, go to Dashboard > [Snap Preference](https://dashboard.midtrans.com/settings/snap_preference) > Theme and Logo > then untick `Use Header`.

<br />

## Adjusting Snap Modal Dimension

<br />

* The default width and height are set to 320px and 560px, which are the minimum sizes that meet our application standards.
* Size of snap-container div can be adjusted by adding height and width via CSS. Note that Snap-container size can only be enlarged, but not make it smaller than the default width and height to ensure that customers can easily make payments and ensure all functionality works properly.
* We also ensure responsiveness by using flexbox, which sets the width to 100% and follows the flex behavior of its parent. This ensures that the Snap content is appropriately displayed and preserved on smaller devices.

<br />

![](https://files.readme.io/a713534-Snap_Flexbox.gif)

<br />

## Implementing Callback JS

<br />

Utilize callback JS to trigger your custom JavaScript implementation on each event. See sample implementation below. Note that callback implementation between Embedded and Pop Up modes are identical.

<br />

```html
<html>

<head>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <!-- @TODO: replace SET_YOUR_CLIENT_KEY_HERE with your client key -->
  <script type="text/javascript"
		src="https://app.sandbox.midtrans.com/snap/snap.js"
    data-client-key="SET_YOUR_CLIENT_KEY_HERE"></script>
  <!-- Note: replace with src="https://app.midtrans.com/snap/snap.js" for Production environment -->
</head>

<body>
  <button id="pay-button">Pay!</button>

  <!-- @TODO: You can add the desired ID as a reference for the embedId parameter. -->
  <div id="snap-container"></div>

  <script type="text/javascript">
    // For example trigger on button clicked, or any time you need
    var payButton = document.getElementById('pay-button');
    payButton.addEventListener('click', function () {
      // Trigger snap popup. @TODO: Replace TRANSACTION_TOKEN_HERE with your transaction token.
      // Also, use the embedId that you defined in the div above, here.
      window.snap.embed('YOUR_SNAP_TOKEN', {
        embedId: 'snap-container',
        onSuccess: function (result) {
          /* You may add your own implementation here */
          alert("payment success!"); console.log(result);
        },
        onPending: function (result) {
          /* You may add your own implementation here */
          alert("wating your payment!"); console.log(result);
        },
        onError: function (result) {
          /* You may add your own implementation here */
          alert("payment failed!"); console.log(result);
        },
        onClose: function () {
          /* You may add your own implementation here */
          alert('you closed the popup without finishing the payment');
        }
      });
    });
  </script>
</body>

</html>
```

| Name                                                   | Description                                                                                                                                                                                                                                                                                                                              |
| ------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| embedID <br /> *String (required)*                     | Embed ID for Snap container.                                                                                                                                                                                                                                                                                                             |
| snapToken <br /> *String (required)*                   | Snap token acquired from backend integration                                                                                                                                                                                                                                                                                             |
| enabledPayments <br /> *Array (optional)*              | List of payment types to be displayed. This will filter out enabled payments from backend integration.                                                                                                                                                                                                                                   |
| options.onSuccess <br /> *Function (optional)*         | Payment success callback (200 `status_code`)                                                                                                                                                                                                                                                                                             |
| options.onPending <br /> *Function (optional)*         | Payment pending callback (201 `status_code`)                                                                                                                                                                                                                                                                                             |
| options.onError <br /> *Function (optional)*           | Payment error callback (4xx or 5xx `status_code`)                                                                                                                                                                                                                                                                                        |
| options.onClose <br /> *Function (optional)*           | Called if customer has closed the payment popup prematurely without finishing the payment                                                                                                                                                                                                                                                |
| options.language <br /> *String (optional)*            | Sets the language. This will override language setting on Merchant Administration Portal. Supported values are `en` (English) and `id` (Bahasa Indonesia). Defaults to `id`                                                                                                                                                              |
| options.autoCloseDelay <br /> *Integer (optional)*     | Auto closes the last page of Indomaret and Bank Transfer payments after the specified time delay. The time delay is specified in seconds. Setting it to `0` will disable this feature. Defaults to `0`.                                                                                                                                  |
| options.selectedPaymentType <br /> *String (optional)* | Skips order summary and select payment page to directly select a specific payment type. Supported values are `credit_card`, `cimb_clicks`, `bca_klikbca`, `bca_klikpay`, `bri_epay`, `telkomsel_cash`, `echannel`, `indosat_dompetku`, `permata_va`, `other_va`, `bca_va`, `bni_va`, `kioson`, `indomaret`, `gci`, and `danamon_online`. |
| options.uiMode <br /> *String (optional)*              | Choose the UI mode for [GoPay](/reference/json-objects#gopay-object), [ShopeePay](/reference/json-objects#shopeepay-object) . Supported values are `deeplink`, `qr`, and `auto`. Set to `auto` by default.                                                                                                                               |

<br />

***

<br />

# Additional Implementation Notes

<br />

* Unlike in Pop Up mode; in Embedded mode, X button in the modal is intentionally removed to prevent users from accidentally exiting after making a payment. However, merchant can still close the Snap window by using the hide() method covered in Snap Pop Up guide.
* It is not possible to have two different types of Snap instances open simultaneously. If Snap Popup is currently active, Snap Embed cannot be displayed. To switch between the two methods, you will need to hide the active instance using the hide method.
* It is possible to hide the header section in Snap modal that shows your merchant/display name. To do so, go to Dashboard > [Snap Preference](https://dashboard.midtrans.com/settings/snap_preference) > Theme and Logo > then untick `Use Header`.
* If the snap.js callback is not implemented, SNAP will redirect the user to the finish URL configured in the Midtrans Dashboard.