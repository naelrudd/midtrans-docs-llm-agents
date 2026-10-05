---
updatedAt: 2026-09-28T12:00:08.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Get Account Info

Use this API to retrieve and show user's account information.

<br />

Endpoints: `/api/v1/checkout/users/{{user_id}}/gopay`

HTTP Method: `GET`

<br />

## Response Body

```json Existing ENABLED account
{
  "user_id": "testww1",
  "account_id": "bb2fb8cc-d754-4390-b62f-01fb3fc1517c",
  "account_status": "ENABLED",
  "balance": "8000000.00",
  "phone_number": "8123456789",
  "country_code": "62"
}
```
```json Existing PENDING account
{
    "error_messages": [
        "account not found"
    ],
    "locale": "en"
}
```
```json Non-existing account
{
    "error_messages": [
        "account not found"
    ],
    "locale": "en"
}
```

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        JSON Attribute
      </th>

      <th>
        Description
      </th>

      <th>
        Type
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        user\_id
      </td>

      <td>
        A unique identifier owned by merchant that represents a customer
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        account\_status
      </td>

      <td>
        Status of the account.\
        Possible values are `PENDING`, `EXPIRED`, `ENABLED`, `DISABLED`
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        account\_id
      </td>

      <td>
        Customer account id to be used for payment.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        balance
      </td>

      <td>
        Current balance of the account
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        phone\_number
      </td>

      <td>
        Customer phone number, without `country_code`
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        country\_code
      </td>

      <td>
        Customer country code
      </td>

      <td>
        String
      </td>
    </tr>
  </tbody>
</Table>