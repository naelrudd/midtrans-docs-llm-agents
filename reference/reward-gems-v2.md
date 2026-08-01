---
updatedAt: 2026-07-27T08:09:03.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Reward Gems (Ruby)

This API is used to fetch the user's latest gems balance and to issue gems to the user. It returns a promise that resolves with the result or rejects if an error occurs.

<Callout icon="📝" theme="default">
  ### Note

  Prior to the API call

  1. please ensure that you have an active merchant wallet, you may contact the sales team to activate the merchant wallet.
  2. In order to top up the wallet balance, please visit the midtrans portal and you may see the Virtual Account as a top up destination.
</Callout>

# Fetch Gems Balance

| **Path**    | **/v1/mini-apps/gems/balance**                   |
| :---------- | :----------------------------------------------- |
| Host        | <https://public-mini-app-merchants.gopayapi.com> |
| Http Method | GET                                              |

## Request Headers:

| **Property**  | **Data type** | **Required** | **Description**                                                                             |
| :------------ | :------------ | :----------- | :------------------------------------------------------------------------------------------ |
| Debug-Id      | string        | No           | This is an identifier that is used for debugging purposes                                   |
| Request-Id    | string        | Yes          | This is an identifier that is used for maintaining idempotency                              |
| Authorization | string        | Yes          | Bearer Authorization header<br />This is the token you would receive in the apply token API |

## Response:

| **Property**      | **Data type** | **Description**                                                                |
| :---------------- | :------------ | :----------------------------------------------------------------------------- |
| success           | boolean       | It will be **true** if API call is successful and **false** in case of failure |
| data.balance      | integer       | User's gems balance. If success is false, this will be omitted                 |
| error             | object        | This object will be non-null only in case of failures                          |
| error.code        | string        | The error code                                                                 |
| error.description | string        | The description of the error                                                   |

## Sample Response:

Success Response:

```Text Javascript
{
    "data": {
        "balance": 1000000
    },
    "success": true
}
```

Error Response: With appropriate HTTP status codes. Only 5xx would be retriable

```Text Javascript
{
    "success": false,
    "error": {
        "code": "159",
        "description": "Payment option not found"
    }
}
```

Error codes:

| **Error code** | **Description**         |
| :------------- | :---------------------- |
| 105            | User not found          |
| 303            | Malformed Authorization |
| 900            | Unable to process       |

<br />

# Issue Gems Rewards

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

        Possible values :<br />**GOPAY_GEMS**
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
        Any map of string, string that merchant
        wants to reference in the order. But there
        are some required metadata to be passed.
        Required some mandatory metadata:
        • mini_app_name
        • activity_name
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
  "reward_type": "GOPAY_GEMS",
  "metadata": {
    "mini_app_name": "GoPay Pet"
  }
}
```

## Sample Response:

Success Response:

```Text Javascript
{
  "success": true
  "data": {
     "payment_id": "order-id"
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

# Collect Gems

| **Path**    | **/v1/mini-apps/gems/collect**                   |
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
        metadata
      </td>

      <td>
        object
      </td>

      <td>
        No
      </td>

      <td>
        Any map of string, string that merchant
        wants to reference in the order. But there
        are some required metadata to be passed.
        Required some mandatory metadata:
        • mini_app_name
        • activity_name
      </td>
    </tr>
  </tbody>
</Table>

## Sample Request:

```Text JSON
{
    "amount": {
        "currency": "IDR",
        "value": 1000
    },
    "description": "Gopay gems collect tesing",
    "metadata": {
        "mini_app_name": "GoPay Pet"
    }
}
```

## Sample Response:

Success Response:

```Text Javascript
{
  "success": true
  "data": {
     "payment_id": "order-id"
   }
}
```

Error Response: With appropriate HTTP status codes. Only 5xx would be retriable

```Text Javascript
{
    "success": false,
    "error": {
        "code": "900",
        "description": "Internal server error"
    }
}
```

<br />

Error Codes

| Code  | Error                               | When                                                   |
| ----- | ----------------------------------- | ------------------------------------------------------ |
| 303   | FIELD\_CANNOT\_BE\_BLANK            | Missing Authorization header                           |
| 310   | MALFORMED\_DATA                     | Malformed auth header or malformed reward type parsing |
| 110   | UNAUTHORIZED                        | Invalid/inactive token, missing scope, forbidden scope |
| 5003  | INVALID\_AUTHORISATION              | Authorization service rejects introspection            |
| 900   | GENERIC\_SERVICE\_ERROR             | Generic fallback/exception                             |
| 305   | ILLEGAL\_LENGTH\_FOR\_FIELD         | MAA schema validation                                  |
| 902   | MALFORMED\_JSON                     | MAA JSON parsing                                       |
| 19007 | DATASOURCE\_NOT\_FOUND              | No gems eligibility config found                       |
| 43001 | REQUEST\_VALUE\_EXCEEDS\_MAX\_LIMIT | Gems request value exceeds configured limit            |

<br />