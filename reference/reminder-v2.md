---
updatedAt: 2026-07-27T08:09:53.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Reminder System (GoPay Genie Card)

This method explains how merchants can display reminders on the GoPay app homepage for time-sensitive actions like bill payments or returns. This feature is limited to selected merchants. To request access, contact the GoPay team with your business use case and provide the reminder template details.

<Image src="https://files.readme.io/b4d17c51d3c295f387dbdc6c36288c3e04fc72b98c892e9680a10d31ab5615a7-image.png" align="center" width="200px" />

| Template    | Details                                                                                                           |
| :---------- | :---------------------------------------------------------------------------------------------------------------- |
| Title       | This is a mini app name                                                                                           |
| Description | This is a field to spec out what the reminder is , max char 50 - 70 char                                          |
| Due         | This is a field to inform when is the due date for the user to do certain action                                  |
| CTA         | This is the copy to indicate the action that a user can do , i.e. Top up , pay, return , etc. Max char 7 - 8 char |
| URL         | This is the URL to redirect the user somewhere within the GoPay app , i.e. Your mini app                          |

# Create Reminder:

![](https://files.readme.io/1be7c80b69dd1e75b9632a684b9f50232ea20162b7999a8e76ac0e30d9390ee0-image.png)

This API can be called by the Mini App backend service to create reminders in the GoPay app.

* GoPay backend will return a reminder\_id that can be used later to remove the reminder once the task is completed.
* The merchant should store the reminder\_id at their end so they can use it later to delete the reminder if required.

| **Integration Needed** | **Details**                             |
| :--------------------- | :-------------------------------------- |
| Mini App Backend       | Create a reminder for user in GoPay app |

| **Path**    | **/v1/mini-apps/reminder**                       |
| :---------- | :----------------------------------------------- |
| Host        | <https://public-mini-app-merchants.gopayapi.com> |
| Http Method | PUT                                              |

## Request Headers:

| **Property**  | **Data type** | **Required** | **Description**                                                                             |
| :------------ | :------------ | :----------- | :------------------------------------------------------------------------------------------ |
| Debug-Id      | string        | No           | This is an identifier that is used for debugging purposes                                   |
| Request-Id    | string        | No           | This is an identifier that is used for maintaining idempotency                              |
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
| error.description | string        | The description of the error                                                   |
| data              | object        | The object containing the reminder details                                     |
| data.reminder\_id | string        | The ID of the reminder                                                         |

## Sample Request:

```Text JSON
{
  "template_name": "<template_name>", // can be obtained from GoPay team
  "reminder_id": "<reminder_id>",
  // these parameters are not fixed and may vary based on usecase
  "template_parameters": {
    "message": "Food is ready",
    "cta_label_en": "Track",
    "cta_label_id": "Track",
    "amount": 12000
  }
}
```

## Sample Response:

Success Response:

```Text Javascript
{
  "success": true,
  "data": {
    "reminder_id": "<reminder_id>"
  }
}
```

Error Response: With appropriate HTTP status codes. Only 5xx would be retriable

```Text Javascript
{
  "success": false,
  "error": {
    "description": "NotificationTemplate not found"
  }
}
```

# Remove Reminder:

![](https://files.readme.io/2fe559500e8a3809cfc4e7010ef5b09468d72851f2ec71f84a8c4f57fd1fbfab-image.png)

<Callout icon="📝" theme="default">
  ### Note

  This API access will give you access to remove the created reminder for GoPay users on the GoPay app homepage. It is strictly limited to specific merchants. Please discuss with the GoPay team if you want to use it
</Callout>

This API can be called by the Mini App backend to delete a reminder in the GoPay app.

* The id that is obtained from Create Reminder API needs to be passed as part of the path param for that reminder to be removed from GoPay app
* API returns true if the reminder got removed successfully

| **Integration Needed** | **Details**                     |
| :--------------------- | :------------------------------ |
| Mini App Backend       | Remove reminder on user's phone |

| **Path**    | **/v1/mini-apps/reminder/\<reminder\_id>**       |
| :---------- | :----------------------------------------------- |
| Host        | <https://public-mini-app-merchants.gopayapi.com> |
| Http Method | DELETE                                           |

## Request Headers:

| **Property**  | **Data type** | **Required** | **Description**                                                                             |
| :------------ | :------------ | :----------- | :------------------------------------------------------------------------------------------ |
| Debug-Id      | string        | No           | This is an identifier that is used for debugging purposes                                   |
| Request-Id    | string        | No           | This is an identifier that is used for maintaining idempotency                              |
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
  "success": true
}
```

Error Response: With appropriate HTTP status codes. Only 5xx would be retriable

```Text Javascript
{
  "success": false,
  "error": {
    "description": "Reminder not found"
  }
}
```

<br />

Error Codes

| Code  | Error                                     | When                                                   |
| ----- | ----------------------------------------- | ------------------------------------------------------ |
| 303   | FIELD\_CANNOT\_BE\_BLANK                  | Missing Authorization header                           |
| 310   | MALFORMED\_DATA                           | Malformed auth header or malformed reward type parsing |
| 110   | UNAUTHORIZED                              | Invalid/inactive token, missing scope, forbidden scope |
| 5003  | INVALID\_AUTHORISATION                    | Authorization service rejects introspection            |
| 900   | GENERIC\_SERVICE\_ERROR                   | Generic fallback/exception                             |
| 40003 | MINI\_APP\_REMINDER\_TEMPLATE\_NOT\_FOUND | Reminder template not found in mini-app-service        |

<br />