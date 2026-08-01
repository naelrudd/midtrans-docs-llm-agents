---
updatedAt: 2026-07-27T08:11:10.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Push Notification

This method explains how merchants can send push notifications to users in the GoPay app using this API. This API currently supports sending only one notification at a time. The user for push notification will be identified from the Authorization token.

<Callout icon="📝" theme="default">
  ### Note

  To enable the Push Notification API for non-marketing purposes, please request a submission form. Include the title and description, and our team will respond with the appropriate template name for merchant use.
</Callout>

| **Path**    | **/v1/mini-apps/notifications/push**             |
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

| **Property**         | **Data type** | **Required** | **Description**                                                                   |
| :------------------- | :------------ | :----------- | :-------------------------------------------------------------------------------- |
| template\_name       | string        | Yes          | The name of the template that is registered in GoPay                              |
| template\_parameters | object        | Yes          | The object which contains notification parameters such as title, description, etc |

## Response:

| **Property**      | **Data type** | **Description**                                                                |
| :---------------- | :------------ | :----------------------------------------------------------------------------- |
| success           | boolean       | It will be **true** if API call is successful and **false** in case of failure |
| error             | object        | This object will be non-null only in case of failures                          |
| error.code        | string        | The error code                                                                 |
| error.description | string        | The description of the error                                                   |

## Sample Request:

```Text JSON
{
  "template_name": "HK_PDS_NOTIFY",
  "template_parameters": {
    "amount": "100000",
    "currency": "IDR"
  }
}
```

## Sample Response:

Success Response:

```Text Javascript
{
  "success": true
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

Error Codes

| Code  | Error                                     | When                                                   |
| ----- | ----------------------------------------- | ------------------------------------------------------ |
| 303   | FIELD\_CANNOT\_BE\_BLANK                  | Missing Authorization header                           |
| 310   | MALFORMED\_DATA                           | Malformed auth header or malformed reward type parsing |
| 110   | UNAUTHORIZED                              | Invalid/inactive token, missing scope, forbidden scope |
| 5003  | INVALID\_AUTHORISATION                    | Authorization service rejects introspection            |
| 900   | GENERIC\_SERVICE\_ERROR                   | Generic fallback/exception                             |
| 305   | ILLEGAL\_LENGTH\_FOR\_FIELD               | MAA schema validation                                  |
| 902   | MALFORMED\_JSON                           | MAA JSON parsing                                       |
| 40003 | MINI\_APP\_REMINDER\_TEMPLATE\_NOT\_FOUND | Notification template/reminder template not found      |
| 2903  | INVALID\_REQUEST\_ERROR                   | Unable to deserialize notification request             |

<br />