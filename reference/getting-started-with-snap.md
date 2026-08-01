---
updatedAt: 2025-11-11T00:24:17.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Getting Started

## Payment Flow

<br />

![](https://files.readme.io/bc8912c-payment-flow_1.svg "payment-flow (1).svg")

<br />

> 1. User performs the checkout operation
> 2. Merchant server makes an [API request](https://docs.midtrans.com/reference/backend-integration) to the Snap backend to get the `SNAP_TOKEN`
> 3. Snap backend responds to the API call with the `SNAP_TOKEN`
> 4. Merchant server constructs the [html](https://docs.midtrans.com/reference/frontend-integration) page and sends it back to the browser
> 5. User verifies the details and clicks the pay button. Merchant's Javascript code calls [`snap.pay(SNAP_TOKEN, options)`](https://docs.midtrans.com/reference/snap-js). User then fills up the payment details and clicks the confirm button.
> 6. Snap JS sends the payment details to the Snap backend
> 7. Snap backend processes the details and responds with the charge status. Snap JS then calls the corresponding [callback](https://docs.midtrans.com/reference/snap-js) provided by the merchant's Javascript code.
> 8. Snap backend notifies the merchant server about the charge status

<br />