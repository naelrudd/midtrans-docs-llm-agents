---
updatedAt: 2025-11-11T00:24:05.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# [SNAP] How to open Snap through redirection

```javascript JavaScript
{
  "token":"66e4fa55-fdac-4ef9-91b5-733b97d1b862",
  "redirect_url":"https://app.sandbox.midtrans.com/snap/v2/vtweb/66e4fa55-fdac-4ef9-91b5-733b97d1b862"
}

```

# Use `redirect_url` from response

<!-- javascript@3 -->

Alternatively, you can use `redirect_url` retrieved from backend in [this step](/docs/snap-snap-integration-guide#1-acquiring-transaction-token-on-backend) to redirect customer to payment page hosted by Midtrans. This is useful if you do not want or can not display payment page on your web page via snap.js.

# Configure redirection after payment



You can [configure](/docs/snap-advanced-feature#configuring-redirect-url) where customer will be redirected to after payment by setting the Redirect URL in Midtrans's dashboard : 
- Login to your MAP/Midtrans Dashboard account
- Go to Settings > Configuration
- Configure the Finish, Unfinish, Error Redirection URLs.