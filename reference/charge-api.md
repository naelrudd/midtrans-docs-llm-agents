---
updatedAt: 2026-09-28T12:00:08.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Charge API

Endpoints: `/api/v1/core/charge`

HTTP Method: `POST`

## Request Body

```json JSON
{
  "payment_type": "bank_transfer",
  "bank_transfer": {
    "bank": "permata"
  },
  "transaction_details": {
    "order_id": "C17550",
    "gross_amount": 145000
  }
}
```

More information regarding list of parameters on request body can be seen on [here](https://docs.midtrans.com/reference/charge-transactions-1)

## Response Body

```json 200 - Success
{
    "status_code": "201",
    "status_message": "Success, PERMATA VA transaction is successful",
    "transaction_id": "a3b75ca9-8b52-445b-99c8-c2cc742a0991",
    "order_id": "C17550",
    "merchant_id": "G772349112",
    "gross_amount": "145000.00",
    "currency": "IDR",
    "payment_type": "bank_transfer",
    "transaction_time": "2024-07-04 10:53:53",
    "transaction_status": "pending",
    "fraud_status": "accept",
    "permata_va_number": "8778000002332015",
    "expiry_time": "2024-07-05 10:53:53"
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