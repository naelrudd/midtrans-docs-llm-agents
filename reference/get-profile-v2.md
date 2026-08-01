---
updatedAt: 2026-07-27T08:12:44.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Get Profile

This method retrieves the phone number of the user. It returns a promise that resolves with the phone number or rejects it if there is an error.

| **Path**    | **/v1/mini-apps/users/profile**                  |
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
| error             | object        | This object will be non-null only in case of failures                          |
| error.code        | string        | The error code                                                                 |
| error.description | string        | The description of the error                                                   |

## Sample Response:

Success Response:

```Text Javascript
{
  "success": true,
  "error": {},
  "data": {
    "phone_number": "+628210072773",
    "email": "example@gmail.com",
    "username": "example",
  }
}
```

Error Response: With appropriate HTTP status codes. Only 5xx would be retriable

```Text Javascript
{
  "success": false,
  "error": {
    "code": "105",
    "description": "User not found"
  }
}
```

Error codes:

| **Error code** | **Description**         |
| :------------- | :---------------------- |
| 105            | User not found          |
| 303            | Malformed Authorization |
| 900            | Unable to process       |

Error Codes

| Code   | Error                           | When                                                   |
| ------ | ------------------------------- | ------------------------------------------------------ |
| 303    | FIELD\_CANNOT\_BE\_BLANK        | Missing Authorization header                           |
| 310    | MALFORMED\_DATA                 | Malformed auth header or malformed reward type parsing |
| 110    | UNAUTHORIZED                    | Invalid/inactive token, missing scope, forbidden scope |
| 5003   | INVALID\_AUTHORISATION          | Authorization service rejects introspection            |
| 900    | GENERIC\_SERVICE\_ERROR         | Generic fallback/exception                             |
| 105    | USER\_NOT\_FOUND                | User service / profile not found                       |
| 40001  | MINI\_APP\_NOT\_FOUND           | Mini app lookup by merchant cross-ref fails            |
| 400001 | CONSENT\_PROFILE\_NOT\_FOUND    | CMS cannot find consent profile/config                 |
| 400002 | INVALID\_CONSENT\_CATALOG\_ID   | CMS consent catalog config invalid                     |
| 400004 | USER\_CONSENT\_DOES\_NOT\_EXIST | User does not have consent record/details              |

<br />