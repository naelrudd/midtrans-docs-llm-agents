---
updatedAt: 2025-11-11T00:24:05.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# [SNAP] How to open Snap through pop-up

```javascript JavaScript
<html>
  <head>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script type="text/javascript"
      src="https://app.sandbox.midtrans.com/snap/snap.js"
      data-client-key="SET_YOUR_CLIENT_KEY_HERE"></script>
  </head>
 
  <body>
    <button id="pay-button">Pay!</button>
 
    <script type="text/javascript">
      var payButton = document.getElementById('pay-button');
      payButton.addEventListener('click', function () {
        window.snap.pay('TRANSACTION_TOKEN_HERE');
      });
    </script>
  </body>
</html>
```

# Import Snap code script

<!-- javascript@4-5 -->

Include snap.js library into your payment page HTML.

# Set Client Key

<!-- javascript@6 -->

Enter your Client Key as the value of data-client-key attribute in snap.js script tag. 
Details for [Retrieving API Access Keys](/docs/midtrans-account#retrieving-api-access-keys)

# Call Snap script pay method

<!-- javascript@15 -->

Call `window.snap.pay` method with transaction token you retrieved from [Snap backend.](/docs/snap-snap-integration-guide#1-acquiring-transaction-token-on-backend).

# Include the viewport meta tag inside your <head>

<!-- javascript@3 -->

To ensure that Snap popup modal is displayed correctly on a mobile device, please include the viewport meta tag inside your <head> tag.