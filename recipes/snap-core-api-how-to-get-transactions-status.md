---
updatedAt: 2025-11-11T00:24:06.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# [Snap & Core API] How to get transaction's status

```curl cURL
curl --location --request GET '	https://api.sandbox.midtrans.com/v2/[ORDER_ID]/status' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic TWlkLXNlcnZlci1vZkRrWnNYaGdHd0psdTMxaTNnRjBuOHc6'
```

```json Response Example
{"success":true}
```

# Get status of transaction

<!-- curl@1 -->

To get the status of a transaction, you can send a request to Midtrans API. It will then send back the transaction status. This method requires the transaction `order_id` or `transaction_id` as an identifier.

# Set HTTP Header

<!-- curl@2-4 -->

Midtrans API validates HTTP request by using Basic Authentication method. The username is your Server Key while the password is empty. The authorization header value is represented by AUTH_STRING. AUTH_STRING is base-64 encoded string of your username and password separated by colon symbol (:). For more details, refer to [API Authorization and Headers](/docs/api-authorization-headers).

# Handle Response



The actual API response may have slight variations (more/less JSON fields), depending on conditions (like different payment methods will have different fields, etc.).

In the future, Midtrans can also add new JSON fields to enhance this API with more useful information.

Please refer to [Sample Response](/docs/get-status-api-requests).