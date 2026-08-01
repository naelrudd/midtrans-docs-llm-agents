---
updatedAt: 2025-11-11T00:24:05.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# [SNAP] How to embed Snap UI

```javascript JavaScript

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
      // Tutorial to create snap token - https://docs.midtrans.com/reference/backend-integration
      // Also, use the embedId that you defined in the div above, here.
      window.snap.embed('TRANSACTION_TOKEN_HERE', {
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

# Import Snap code script

<!-- javascript@7-8 -->

Include snap.js library into your payment page HTML.

# Set Client Key

<!-- javascript@9 -->

Enter your Client Key as the value of data-client-key attribute in snap.js script tag.
Details for [Retrieving API Access Keys](/docs/midtrans-account#retrieving-api-access-keys).

# Prepare the container

<!-- javascript@16-17 -->

Create an empty div with the desired ID. This div is where the SNAP application will be placed.

# Call Snap script embed method

<!-- javascript@25-26 -->

instead of using `snap.pay('${snap-token}')`, you'll need to use `snap.embed('${snap-token}', { embedId: ${your div id, e.g. snap-container} })`. This will ensure that SNAP is correctly embedded and rendered within the div you previously set up.

# Utilize Callback

<!-- javascript@27-42 -->

The SNAP Embed feature also supports callbacks, similar to those available in SNAP Popup [here](https://docs.midtrans.com/recipes/snap-how-to-utilize-query-params-in-the-finish-url-for-snap-redirection). So, you don't need to worry about losing any functionality by using embedded SNAP.

# Demo Store



You can also explore and interact with the e-commerce payment SNAP Embed demo [here](https://demo.sandbox.midtrans.com/).