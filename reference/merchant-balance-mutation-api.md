---
updatedAt: 2026-03-31T07:24:20.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Merchant Balance Mutation API

Retrieve the balance mutation for a specific merchant over a specified period. This endpoint is useful for reconciling balances over a time period.

### HTTP Request

Endpoints: `/v1/balance/mutation`

HTTP Method: `GET`

***

### Request Headers

| Header          | Type     | Required | Description                                                     |
| :-------------- | :------- | :------- | :-------------------------------------------------------------- |
| `Content-Type`  | `string` | Required | Expected format of the request body. e.g.: `application/json`.  |
| `Accept`        | `string` | Required | Expected format of the response body. e.g.: `application/json`. |
| `Authorization` | `string` | Required | Basic Base64Encode(serverKey:)                                  |

***

## Query Parameters

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Parameter
      </th>

      <th>
        Type
      </th>

      <th>
        Required
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `currency`
      </td>

      <td>
        `string`
      </td>

      <td>
        Required
      </td>

      <td>
        The currency code for the balance mutation. Example: `IDR`.
      </td>
    </tr>

    <tr>
      <td>
        `start_time`
      </td>

      <td>
        `string`
      </td>

      <td>
        Required
      </td>

      <td>
        The start time of the mutation window in ISO 8601 format, URL encoded.  
        Example raw value: `2026-03-02T00:00:00+07:00`.  
        URL Encoded: `2026-03-02T00%3A00%3A00%2B07%3A00`
      </td>
    </tr>

    <tr>
      <td>
        `end_time`
      </td>

      <td>
        `string`
      </td>

      <td>
        Required
      </td>

      <td>
        The end time of the mutation window in ISO 8601 format, URL encoded.  
        Example raw value: `2026-03-16T23:59:59+07:00`.  
        URL Encoded: `2026-03-16T23%3A59%3A59%2B07%3A00`
      </td>
    </tr>
  </tbody>
</Table>

***

## Sample Curl

```shell
curl --location 'https://api.sandbox.midtrans.com/v1/balance/mutation?currency=IDR&start_time=2026-03-02T00%3A00%3A00%2B07%3A00&end_time=2026-03-16T23%3A59%3A59%2B07%3A00' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Basic <redacted>'
```

## Response Body

### Success

```shell 200 OK
{
    "currency": "IDR",
    "start_time": "2026-03-02T00:00:00+07:00",
    "end_time": "2026-03-16T23:59:59+07:00",
    "opening_balance_effective": 962000.01,
    "closing_balance_effective": 59312508.02,
    "opening_balance_pending": 0.01,
    "closing_balance_pending": 0.00,
    "opening_balance_overall": 962000.02,
    "closing_balance_overall": 59312508.02,
    "wallets": [
        {
            "source": "payin",
            "opening_balance_effective": 962000.00,
            "closing_balance_effective": 144.00,
            "opening_balance_pending": 0.01,
            "closing_balance_pending": 0.00,
            "opening_balance_overall": 962000.01,
            "closing_balance_overall": 144.00
        },
        {
            "source": "iris",
            "opening_balance_effective": 0.01,
            "closing_balance_effective": 59312514.01,
            "opening_balance_pending": 0.00,
            "closing_balance_pending": 0.00,
            "opening_balance_overall": 0.01,
            "closing_balance_overall": 59312514.01
        }
    ]
}
```

| Field                       | Type             | Description                                                                                                                                             |
| :-------------------------- | :--------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------ |
| currency                    | string           | The currency code for the balances returned (e.g., IDR).                                                                                                |
| start\_time                 | string           | The start time of the queried period.                                                                                                                   |
| end\_time                   | string           | The end time of the queried period.                                                                                                                     |
| opening\_balance\_effective | number           | The available funds at the beginning of the period.                                                                                                     |
| closing\_balance\_effective | number           | The available funds at the end of the period.                                                                                                           |
| opening\_balance\_pending   | number           | The pending funds at the beginning of the period.                                                                                                       |
| closing\_balance\_pending   | number           | The pending funds at the end of the period.                                                                                                             |
| opening\_balance\_overall   | number           | The total funds (effective + pending) at the beginning of the period.                                                                                   |
| closing\_balance\_overall   | number           | The total funds (effective + pending) at the end of the period.                                                                                         |
| wallets                     | array of objects | Breakdown of balances grouped by wallet source (e.g., payin for incoming payments, iris for disbursements). Contains the same balance metrics as above. |

### Failed

```shell 400 - Validation Error
{
    "error_messages": [
        "currency must not be empty"
    ]
}
```

| Field           | Type            | Description         |
| :-------------- | :-------------- | :------------------ |
| error\_messages | array of string | The list of errors. |