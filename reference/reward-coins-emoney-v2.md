---
updatedAt: 2026-07-27T08:07:11.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Reward GoPay Coins/eMoney

This method explains how merchants can disburse GoPay Saldo or GoPay Coins to users using this API. The user who receives the disbursement will be identified from the Authorization token.

<Callout icon="📝" theme="default">
  ### Note

  Prior to the API call

  1. please ensure that you have an active merchant wallet, you may contact the sales team to activate the merchant wallet.
  2. In order to top up the wallet balance, please visit the midtrans portal and you may see the Virtual Account as a top up destination.
</Callout>

| **Path**    | **/v1/mini-apps/rewards**                        |
| :---------- | :----------------------------------------------- |
| Host        | <https://public-mini-app-merchants.gopayapi.com> |
| Http Method | POST                                             |

## Request Headers:

| **Property**  | **Data type** | **Required** | **Description**                                                                             |
| :------------ | :------------ | :----------- | :------------------------------------------------------------------------------------------ |
| Debug-Id      | string        | No           | This is an identifier that is used for debugging purposes                                   |
| Request-Id    | string        | Yes          | This is an identifier that is used for maintaining idempotency                              |
| Authorization | string        | Yes          | Bearer Authorization header<br />This is the token you would receive in the apply token API |

## Request Body:

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        **Property**
      </th>

      <th>
        **Data type**
      </th>

      <th>
        **Required**
      </th>

      <th>
        **Description**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        amount
      </td>

      <td>
        object
      </td>

      <td>
        Yes
      </td>

      <td>
        It will be **true** if API call is successful and **false** in case of failure
      </td>
    </tr>

    <tr>
      <td>
        amount.value
      </td>

      <td>
        integer
      </td>

      <td>
        Yes
      </td>

      <td>
        A positive integer representing how much to charge in the smallest currency unit
      </td>
    </tr>

    <tr>
      <td>
        description
      </td>

      <td>
        string
      </td>

      <td>
        Yes
      </td>

      <td>
        Merchant given description for this cashback, string upto 256 characters.
      </td>
    </tr>

    <tr>
      <td>
        amount.currency
      </td>

      <td>
        string
      </td>

      <td>
        Yes
      </td>

      <td>
        Three-letter ISO 4127 currency code.smallest possible denomination Should be IDR for Indonesia.
      </td>
    </tr>

    <tr>
      <td>
        reward_type
      </td>

      <td>
        string
      </td>

      <td>
        Yes
      </td>

      <td>
        Identifies whether reward should be provided as emoney cashback or coins cashback

        Possible values :<br />**EMONEY**<br />**GOPAY_COINS**
      </td>
    </tr>

    <tr>
      <td>
        metadata
      </td>

      <td>
        object
      </td>

      <td>
        No
      </td>

      <td>
        The object containing the reminder details
      </td>
    </tr>
  </tbody>
</Table>

## Response:

| **Property**     | **Data type** | **Description**                                                                |
| :--------------- | :------------ | :----------------------------------------------------------------------------- |
| success          | boolean       | It will be **true** if API call is successful and **false** in case of failure |
| error            | object        | This object will be non-null only in case of failures                          |
| data             | object        | The object containing the reminder details                                     |
| data.payment\_id | string        | The ID of the payment for reference                                            |
| data.code        | string        | The error code                                                                 |
| data.description | string        | The description of the error                                                   |

## Sample Request:

```Text JSON
{
  "amount": {
    "currency": "IDR",
    "value": 10000
  },
  "description": "Cashback for daily check-in",
  "reward_type": "GOPAY_COINS",
  "metadata": {
    "reference_id": "123"
  }
}
```

## Sample Response:

Success Response:

```Text Javascript
{
  "success": true
  "data": {
     "payment_id": "0120250107121627eTRXfvlCZ6ID"
   }
}
```

Error Response: With appropriate HTTP status codes. Only 5xx would be retriable

```Text Javascript
{
  "success": false,
  "error": {
    "description": "User not found"
  }
}
```

Error Response: 4060. It's non-retriable error.

```Text Javascript
{
  "success": false,
  "error": {
    "code": "4060",
    "description": "Fraud validation error"
  }
}
```

<Callout icon="📝" theme="default">
  ### Note

  Error code 4060 — Cashback feature is temporarily disabled for this user. Please inform the user that they can’t receive cashback for the time being and suggest them to reach GoPay Help page for further information.
</Callout>

<br />

Error Codes

| Code  | Error                                 | When                                                   |
| ----- | ------------------------------------- | ------------------------------------------------------ |
| 303   | FIELD\_CANNOT\_BE\_BLANK              | Missing Authorization header                           |
| 310   | MALFORMED\_DATA                       | Malformed auth header or malformed reward type parsing |
| 110   | UNAUTHORIZED                          | Invalid/inactive token, missing scope, forbidden scope |
| 5003  | INVALID\_AUTHORISATION                | Authorization service rejects introspection            |
| 900   | GENERIC\_SERVICE\_ERROR               | Generic fallback/exception                             |
| 40006 | MINI\_APP\_REWARD\_CONFIG\_NOT\_FOUND | Reward config not found in mini-app-service            |

<br />