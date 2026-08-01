---
updatedAt: 2026-03-16T07:32:33.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Backend APIs (Shared)

This guide explains the technical specifications of APIs that can be called from your application's backend.

These APIs are meant to be called from your application's backend after receiving the authCode from the frontend. The backend uses this code to retrieve a user-specific access token, which is then used to securely call GoPay services such as reminders, payments, disbursements, and more. This ensures sensitive operations are handled securely on the server side.

GoPay APIs are now accessible via a public domain, Simply use the provided host for all API calls.

| **Path**    | \<api-path>                                      |
| :---------- | :----------------------------------------------- |
| Host        | <https://public-mini-app-merchants.gopayapi.com> |
| Http Method | \<api-method>                                    |

<br />

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Name
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>

      <th style={{ textAlign: "left" }}>
        Mandatory
      </th>

      <th style={{ textAlign: "left" }}>
        Prerequisite
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        **[Get Auth Token](https://docs.midtrans.com/reference/seamless-login-v2/#3-get-authorization-token)**
      </td>

      <td style={{ textAlign: "left" }}>
        Retrieve user's access token for authentication
      </td>

      <td style={{ textAlign: "left" }}>
        M
      </td>

      <td style={{ textAlign: "left" }}>
        [AuthCode](https://docs.midtrans.com/reference/seamless-login-v2/#2-get-authorization-code)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **[Reward GoPay Coins/eMoney](https://docs.midtrans.com/reference/reward-coins-emoney-v2)**
      </td>

      <td style={{ textAlign: "left" }}>
        Send GoPay coins/eMoney to user's account
      </td>

      <td style={{ textAlign: "left" }}>
        O
      </td>

      <td style={{ textAlign: "left" }}>
        [AuthToken](https://docs.midtrans.com/reference/seamless-login-v2/#3-get-authorization-token)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **[Reward GoPay Gems (Ruby)](https://docs.midtrans.com/reference/reward-gems-v2)**
      </td>

      <td style={{ textAlign: "left" }}>
        Send GoPay gems (Ruby) to user's account
      </td>

      <td style={{ textAlign: "left" }}>
        O
      </td>

      <td style={{ textAlign: "left" }}>
        [AuthToken](https://docs.midtrans.com/reference/seamless-login-v2/#3-get-authorization-token)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **[Reminder](https://docs.midtrans.com/reference/reminder-v2)**
      </td>

      <td style={{ textAlign: "left" }}>
        Configure a reminder for scheduled actions
      </td>

      <td style={{ textAlign: "left" }}>
        O
      </td>

      <td style={{ textAlign: "left" }}>
        [AuthToken](https://docs.midtrans.com/reference/seamless-login-v2/#3-get-authorization-token)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **[Push Notification](https://docs.midtrans.com/reference/push-notification-v2)**
      </td>

      <td style={{ textAlign: "left" }}>
        Send notifications to user
      </td>

      <td style={{ textAlign: "left" }}>
        O
      </td>

      <td style={{ textAlign: "left" }}>
        [AuthToken](https://docs.midtrans.com/reference/seamless-login-v2/#3-get-authorization-token)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **[Get Profile](https://docs.midtrans.com/reference/get-profile-v2)**
      </td>

      <td style={{ textAlign: "left" }}>
        Retrieve user's information such as mobile number, email, username
      </td>

      <td style={{ textAlign: "left" }}>
        O
      </td>

      <td style={{ textAlign: "left" }}>
        [AuthToken](https://docs.midtrans.com/reference/seamless-login-v2/#3-get-authorization-token)  
        [ConsentApproval](https://docs.midtrans.com/reference/frontend-v2/#get-user-consent)
      </td>
    </tr>
  </tbody>
</Table>

<br />