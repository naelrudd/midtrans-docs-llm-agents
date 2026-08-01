---
updatedAt: 2025-11-11T00:24:05.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# [SNAP] How to create Snap token

```node Node
const midtransClient = require('midtrans-client');

const snap = new midtransClient.Snap({
  isProduction : false,
  serverKey : 'YOUR_SERVER_KEY'
});
 
const parameters = {
  "transaction_details": {
    "order_id": "YOUR-ORDERID-123456",
    "gross_amount": 10000
  },
};
 
snap.createTransaction(parameter).then((transaction)=>{
  const transactionToken = transaction.token;
  console.log('transactionToken:',transactionToken);
})
```

```json Response Example
{
  "token":"66e4fa55-fdac-4ef9-91b5-733b97d1b862",
  "redirect_url":"https://app.sandbox.midtrans.com/snap/v2/vtweb/66e4fa55-fdac-4ef9-91b5-733b97d1b862"
}
```

# Install the API module from NPM

<!-- node@1 -->

Install midtrans-client by running `npm install --save midtrans-client`.
[Midtrans Client - Node JS](https://github.com/Midtrans/midtrans-nodejs-client)

# Instantiate Midtrans Client with Configuration

<!-- node@3-6 -->

Use your [Server Key](https://docs.midtrans.com/en/midtrans-account/overview?id=retrieving-api-access-keys) to authenticate and set `isProduction` to true to run it on Production environment.

# Create the parameters

<!-- node@8-13 -->

Create parameters with at least the following info:
- order_id
- gross_amount

You can also send [more transaction details](/docs/snap-advanced-feature#recommended-parameters) for easier recon and reporting process.

# Create transaction

<!-- node@15-18 -->

Send the request and wait for the [response](/docs/snap-snap-integration-guide#successful-sample-response)