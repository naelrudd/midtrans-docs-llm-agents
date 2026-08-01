---
updatedAt: 2026-04-28T11:54:01.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Postman Collection

[Postman](https://www.getpostman.com/) is a user-friendly tool that makes it easy for you to quickly send and test REST API requests without doing complex programming. Midtrans provides Postman Collection that you can import to test the Midtrans API in no time.

***

# Payment API Postman Collection

<br />

This Postman collection covers the following API:

* [Snap API](/reference/getting-started-with-snap)
* [Core API](/reference/core-api-overview)

<br />

## Usage Instructions

<br />

1. Download and open [Postman](https://www.getpostman.com).
2. Follow any of the steps given below to import Midtrans API collection.

* [Download from Postman](https://app.getpostman.com/run-collection/af068be08b5d1a422796).
* GitHub Source: [Repo Link](https://github.com/midtrans/Midtrans-Payment-API-Postman-Collections).
* Click **Run in Postman** button below, to download and import the collection.\
  [![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/af068be08b5d1a422796)

3. [Create a test account in Midtrans](https://dashboard.midtrans.com/register).
4. [Login](http://dashboard.midtrans.com) to Midtrans Merchant Administration Portal (MAP), and follow the steps given below to get the Server Key.
   1. Switch to **Sandbox** environment.
   2. On the home page, go to **SETTINGS > ACCESS KEYS**.
   3. Copy the **Server Key**.
5. In Postman, double-click to open **Midtrans Payment API** folder.
6. Click any request you want to try.
7. Select the **Auth** tab.

<br />

<Image alt={2222} caption="Postman Usage" title="technical-reference-postman-auth-1.png" src="https://files.readme.io/082305d-technical-reference-postman-auth-1.png" />

<br />

8. Select *Basic Auth* from the **TYPE** drop-down list.
9. Enter *Server Key* in the **Username** field.
10. Leave **Password** field blank.
11. Click **Send**.

<br />

<Image alt={2800} caption="Postman Usage" title="technical-reference-postman-username-2.png" src="https://files.readme.io/d7aeac7-technical-reference-postman-username-2.png" />

<br />

The server response is displayed.

<br />

## Switching to Production Mode

<br />

All endpoints used in this postman collection are for transactions on Sandbox environment. To switch to transactions in Production environment, follow the steps given below.

1. Change endpoint URL from:\
   `https://api.sandbox.midtrans.com/../..`to `https://api.midtrans.com/../..`
2. Update your *Server Key* with your production environment Server Key.

<br />

## Troubleshooting

<br />

If you encounter an error message similar to the one shown below,

<br />

```json
{
  "error_messages": [
    "Access denied due to unauthorized transaction, please check client or server key",
    "Visit https://docs.midtrans.com/reference/request-headers for more details"
  ]
}
```

<br />

Please make sure to,

* Follow the steps 4 to 11 in **[Usage Instructions](#usage-instructions)** section properly.
* Use correct *Server Key*. The *Server Keys* for the Sandbox and Production environments are different.

<br />

***

<br />