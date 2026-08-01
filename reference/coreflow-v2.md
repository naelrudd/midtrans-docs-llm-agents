---
updatedAt: 2026-03-16T07:32:13.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Core Flows

This guide explains end-to-end MiniApp flows, which may involve a combination of frontend SDKs and backend APIs.

# [Seamless Login](https://docs.midtrans.com/reference/seamless-login-v2)

This is mandatory for all miniapps, this allows users to open the miniapp without any login requirements. You will receive gopay\_account\_id (user unique identifier) and authToken (authorization header for other GoPay BE API)

| Name                                                                                                   | Description                                                     | Mandatory | Prerequisite                                                                                                                                                                    |
| :----------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------- | :-------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **[FE SDK Script](https://docs.midtrans.com/reference/seamless-login-v2/#1-initialize-sdk-script)**    | Initiate SDK Script                                             | M         |                                                                                                                                                                                 |
| **[Get Auth Code](https://docs.midtrans.com/reference/seamless-login-v2/#2-get-authorization-code)**   | Use this SDK to get auth code (Active GoPay User session)       | M         | [SDKScript](https://docs.midtrans.com/reference/seamless-login-v2/#1-initialize-sdk-script)                                                                                     |
| **[Get Auth Token](https://docs.midtrans.com/reference/seamless-login-v2/#3-get-authorization-token)** | Use this API to retrieve user's access token for authentication | M         | [AuthCode](https://docs.midtrans.com/reference/seamless-login-v2/#2-get-authorization-code)<br />[AuthCredentials](https://docs.midtrans.com/reference/miniapp-v2/#quick-start) |

# [Seamless Payments](https://docs.midtrans.com/reference/seamless-payment-v2)

This is mandatory if you use payments on your miniapp, this allows users to do payments seamlessly inside GoPay App. The journey once user initiate payments, users will redirect to GoPay Payment review page and will redirect back to the miniapp after transactions.

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Name
      </th>

      <th>
        Description
      </th>

      <th>
        Mandatory
      </th>

      <th>
        Prerequisite
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **[Get B2B Access Token](https://docs.midtrans.com/reference/seamless-payment-v2#1-access-token-b2b)**
      </td>

      <td>
        Initiate order with Super App Backend Merchant access token is needed for verification purposes
      </td>

      <td>
        O
      </td>

      <td>
        [Bi Snap Activation](https://docs.midtrans.com/reference/credential-exchange-copy)<br />[IP Whitelisting](https://docs.midtrans.com/reference/register-ip-address)
      </td>
    </tr>

    <tr>
      <td>
        **[Initiate Host to Host Payment](https://docs.midtrans.com/reference/seamless-payment-v2#2-payment-host-to-host)**
      </td>

      <td>
        Create Payment Deeplink with Super App backend
      </td>

      <td>
        O
      </td>

      <td>
        [B2BAccessToken](https://docs.midtrans.com/reference/seamless-payment-v2#1-access-token-b2b)<br />[PointofPurchaseID](https://docs.midtrans.com/reference/miniapp-v2/#quick-start)
      </td>
    </tr>

    <tr>
      <td>
        **[Launch Payment](https://docs.midtrans.com/reference/seamless-payment-v2#3-launch-payment)**
      </td>

      <td>
        Use this SDK to automatically redirect users to the GoPay app to complete the payment, then return them to your Mini App.

        This is the FE Payment Response
      </td>

      <td>
        O
      </td>

      <td>
        [Initiate Host to Host Payment](https://docs.midtrans.com/reference/seamless-payment-v2#2-payment-host-to-host)
      </td>
    </tr>

    <tr>
      <td>
        **[Notify](https://docs.midtrans.com/reference/seamless-payment-v2#4-notify)**
      </td>

      <td>
        Use this API to get transaction status.

        This is the BE Payment Response.
      </td>

      <td>
        O
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        **[Refund](https://docs.midtrans.com/reference/refund-api)**
      </td>

      <td>
        Initiating refund for GoPay and GoPay Tokenization (non Pre-Auth) transaction
      </td>

      <td>
        O
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        Order History URL Configuration
      </td>

      <td>
        GoPay to Configure the URL allowing users redirect to the merchant's order history page from GoPay's order history page. If no URL is configured, users are redirected to the merchant's home page.
      </td>

      <td>
        O
      </td>

      <td>
        [Seamless Login](https://docs.midtrans.com/reference/seamless-login-v2) (if not implemented globally)
      </td>
    </tr>
  </tbody>
</Table>

Note:

* Payments only works in production host, currently it will NOT work on sandbox host (it will only redirect to browser only)
* Please ensure that seamless login is enabled globally, as we will add deeplink redirection from the user's order history for all transactions. "Once UAT sign off in staging, please request another modify request and select payments to share your "Order History URL" as informed in the project tracker on miniapp workbook"

***

# [Other GoPay Frontend SDKs](https://docs.midtrans.com/reference/frontend-v2)

***

# [Other GoPay Backend APIs](https://docs.midtrans.com/reference/backend-v2)

<br />

<br />

<br />