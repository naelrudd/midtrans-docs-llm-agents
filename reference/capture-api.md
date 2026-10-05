---
updatedAt: 2026-09-28T12:00:08.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Capture API

Capture transaction is triggered to capture the transaction balance when `transaction_status:authorize`. This is only available after [Pre-Authorized Credit Card](https://docs.midtrans.com/reference/card-feature-pre-authorization) or [Pre-Authorized GoPay](/reference/gopay-tokenization#gopay-tokenization-features-pre-auth).

Endpoints: `/api/v1/core/capture`

HTTP Method: `POST`

## Request Body

```json JSON
{
  "transaction_id": "be4f3e44-d6ee-4355-8c64-c1d1dc7f4590",
  "gross_amount": 145000
}
```

| Field           | Type        | Attribute | Description                                                                                                                       |
| --------------- | ----------- | --------- | --------------------------------------------------------------------------------------------------------------------------------- |
| transaction\_id | String(255) | Required  | Transaction ID given by Midtrans.                                                                                                 |
| gross\_amount   | Long        | Optional  | Total amount of transaction in IDR. By default it captures whole transaction amount. <br /> **Note**: Decimal values are invalid. |

## Response Body

```json 200 - Success
{
  "status_code" : "200",
  "status_message" : "Success, Credit Card capture transaction is successful",
  "transaction_id" : "ca297170-be4c-45ed-9dc9-be5ba99d30ee",
  "masked_card" : "45111111-1117",
  "order_id" : "testing-0.4555-1414741517",
  "payment_type" : "credit_card",
  "transaction_time" : "2014-10-31 14:46:44",
  "transaction_status" : "capture",
  "fraud_status" : "accept",
  "bank" : "bni",
  "gross_amount" : "30000.00"
}
```
```json 200 - Error
{
  "status_code" : "412",
  "status_message" : "Merchant cannot modify the status of the transaction"
}
```

<Table>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        status\_code
      </td>

      <td>
        String
      </td>

      <td>
        Status code of transaction capture result.
      </td>
    </tr>

    <tr>
      <td>
        status\_message
      </td>

      <td>
        String
      </td>

      <td>
        Description of transaction capture result.
      </td>
    </tr>

    <tr>
      <td>
        order\_id
      </td>

      <td>
        String
      </td>

      <td>
        Order ID specified by you.
      </td>
    </tr>

    <tr>
      <td>
        transaction\_id
      </td>

      <td>
        String
      </td>

      <td>
        Transaction ID given by Midtrans.
      </td>
    </tr>

    <tr>
      <td>
        masked\_card
      </td>

      <td>
        String
      </td>

      <td>
        First 8-digits and last 4-digits of customer's card number.
      </td>
    </tr>

    <tr>
      <td>
        gross\_amount
      </td>

      <td>
        String
      </td>

      <td>
        Total amount of transaction in IDR.
      </td>
    </tr>

    <tr>
      <td>
        order\_id
      </td>

      <td>
        String
      </td>

      <td>
        Order ID specified by you.
      </td>
    </tr>

    <tr>
      <td>
        payment\_type
      </td>

      <td>
        String
      </td>

      <td>
        The payment method used by the customer.
      </td>
    </tr>

    <tr>
      <td>
        transaction\_time
      </td>

      <td>
        String
      </td>

      <td>
        Timestamp of transaction in ISO 8601 format. Time Zone: GMT+7.
      </td>
    </tr>

    <tr>
      <td>
        transaction\_status
      </td>

      <td>
        String
      </td>

      <td>
        Transaction status after capture card transaction.
      </td>
    </tr>

    <tr>
      <td>
        fraud\_status
      </td>

      <td>
        String
      </td>

      <td>
        Detection result by Fraud Detection System (FDS). Possible values are<br/>`accept` : Approved by FDS.<br/>`deny`: Denied by FDS. Transaction automatically failed.
      </td>
    </tr>

    <tr>
      <td>
        bank
      </td>

      <td>
        String
      </td>

      <td>
        The name of the acquiring bank.
      </td>
    </tr>

    <tr>
      <td>
        gross\_amount
      </td>

      <td>
        String
      </td>

      <td>
        Total amount of transaction in IDR. 
      </td>
    </tr>
  </tbody>
</Table>