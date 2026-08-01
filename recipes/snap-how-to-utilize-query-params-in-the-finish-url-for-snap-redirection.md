---
updatedAt: 2025-11-11T00:24:06.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# [SNAP] How to utilize query params in the finish url for Snap redirection

```javascript JavaScript

```

# Configure Redirect URL for complete payment process



You can [configure](https://dashboard.sandbox.midtrans.com/settings/vtweb_configuration) where customer will be redirected after after the payment process is complete through Snap with these following steps:
- Login to your MAP/Midtrans Dashboard account.
- Go to Settings > Configuration.
- Configure the Finish, Unfinish, Error Redirection URLs.

# Handle appended query parameters



The final redirect URL is appended with query parameter like `?order_id=xxx&status_code=xxx&transaction_status=xxx`.

For example the final redirect URL may look like this: `https://tokoecommerce.com/finish_payment/?order_id=CustOrder-102123123&status_code=200&transaction_status=capture`.

You may use this information to display custom message to your customer on your finish URL.

# Success Redirect URL



- Check the `transaction_status` in the query params.
- For success payment status, the `transaction_status` will be either `capture` or `settlement`.
- You may use that value to display `Thank you` message.

# Error Redirect URL



- Check the `transaction_status` in the query params.
- For error payment status, the `transaction_status` will always be `deny`.
- You may use that value to display `We could not receive your payment` message. 
- Note that you will get `?transaction_status=deny` if the transaction failed more than 3 times.

# Pending Redirect URL



- Check the `transaction_status` in the query params.
- For pending payment status, the `transaction_status` will always be `pending`.
- You may use that value to display `Proceed payment as instructed` message.

# Handle Payment Notification



if the payment method is Credit Card & processed via [3DS 2](/reference/card-feature-3d-secure-20-emv-3ds) (when the acquiring bank and the MID support), there's small possibility of the transaction is still waiting for the card's 3DS provider to process/verify it, which then Snap will trigger redirect with `?transaction_status=pending`.

To handle the payment success update, as usual you should [handle HTTP Notification](/docs/snap-snap-integration-guide#4-handling-after-payment)