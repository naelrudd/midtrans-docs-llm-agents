---
updatedAt: 2025-11-11T00:31:54.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# BNI Virtual Account

The steps to integrate with BNI Virtual Account are given below.

1. Send the charge API request to Midtrans.
2. Display the virtual account number.
3. [Handle notifications](/reference/notifications-handling).

Send a Charge API request with the details of the transaction such as `payment_type`, `bank_transfer`, `transaction_details`, `item_details`, and `customer_details`. Successful request returns a VA number.

By default, default expiry time for bank transfer is 24 hours unless specified by merchant (min 20s, max 180 days).

<br />

***

<br />

## BNI Charge API Request

<br />

```json Sample Request - Charge API
{
    "payment_type": "bank_transfer",
    "transaction_details": {
        "gross_amount": 10000,
        "order_id": "{{$timestamp}}"
    },
    "customer_details": {
        "email": "budi.utomo@Midtrans.com",
        "first_name": "budi",
        "last_name": "utomo",
        "phone": "+6281 1234 1234"
    },
    "item_details": [
    {
       "id": "1388998298204",
       "price": 5000,
       "quantity": 1,
       "name": "Ayam Zozozo"
    },
    {
       "id": "1388998298205",
       "price": 5000,
       "quantity": 1,
       "name": "Ayam Xoxoxo"
    }
   ],
   "bank_transfer":{
     "bank": "bni",
     "va_number": "111111"
  }
}
```

| JSON Attribute       | Description                                                                    | Type                                     | Required |
| -------------------- | ------------------------------------------------------------------------------ | ---------------------------------------- | -------- |
| payment\_type        | Set Bank Transfer payment method. Value: `bank_transfer`                       | String                                   | Required |
| transaction\_details | The details of the specific transaction such as `order_id` and `gross_amount`. | [Object](https://docs.midtrans.com/reference/transaction-details-object) | Required |
| customer\_details    | Details of the customer.                                                       | [Object](https://docs.midtrans.com/reference/customer-details-object)    | Optional |
| item\_details        | Details of the item(s) purchased by the customer.                              | [Object](https://docs.midtrans.com/reference/item-details-object)        | Optional |
| bank\_transfer       | Charge details using bank transfer.                                            | [Object](https://docs.midtrans.com/reference/bank-transfer-object)       | Required |

<br />

***

<br />

## BNI Virtual Account Sample Responses and Notifications

<br />

```json Success
{
  "status_code": "201",
  "status_message": "Success, Bank Transfer transaction is created",
  "transaction_id": "9aed5972-5b6a-401e-894b-a32c91ed1a3a",
  "order_id": "1466323342",
  "gross_amount": "20000.00",
  "payment_type": "bank_transfer",
  "transaction_time": "2016-06-19 15:02:22",
  "transaction_status": "pending",
  "va_numbers": [
    {
      "bank": "bni",
      "va_number": "8578000000111111"
    }
  ],
  "fraud_status": "accept",
  "currency": "IDR"
}
```
```json Pending
{
  "va_numbers": [
    {
      "bank": "bni",
      "va_number": "8578000000111111"
    }
  ],
  "transaction_time": "2016-06-19 15:02:22",
  "gross_amount": "20000.00",
  "order_id": "1466323342",
  "payment_type": "bank_transfer",
  "signature_key": "74d9b6f4cc36585d74e06c9dba360331e455171bcec35df60cf28a786436f8f96e6afcc1f091d6cb61411aec246ac28ba30b76d9b2c1cdb6409c0a70fcc1fe47",
  "status_code": "201",
  "transaction_id": "a9aed5972-5b6a-401e-894b-a32c91ed1a3a",
  "transaction_status": "pending",
  "fraud_status": "accept",
  "status_message": "midtrans payment notification"
}
```
```json Settlement
{
  "va_numbers": [
    {
      "bank": "bni",
      "va_number": "8578000000111111"
    }
  ],
  "payment_amounts": [
    {
      "paid_at": "2016-06-19 20:12:22",
      "amount": "20000.00"
    }
  ],
  "transaction_time": "2016-06-19 19:12:22",
  "gross_amount": "20000.00",
  "order_id": "1466323342",
  "payment_type": "bank_transfer",
  "signature_key": "fe5f725ea770c451017e9d6300af72b830a668d2f7d5da9b778ec2c4f9177efe5127d492d9ddfbcf6806ea5cd7dc1a7337c674d6139026b28f49ad0ea1ce5107",
  "status_code": "200",
  "transaction_id": "9aed5972-5b6a-401e-894b-a32c91ed1a3a",
  "transaction_status": "settlement",
  "fraud_status": "accept",
  "status_message": "midtrans payment notification"
}
```
```json Expired
{
  "status_code": "202",
  "status_message": "midtrans payment notification",
  "transaction_id": "9aed5972-5b6a-401e-894b-a32c91ed1a3a",
  "order_id": "1466323342",
  "gross_amount": "20000.00",
  "payment_type": "bank_transfer",
  "transaction_time": "2016-06-20 15:02:23",
  "transaction_status": "expire",
  "signature_key": "e4e829a5d9a1e342daf181c5fd750afa64dd5a5c9a6e0cfb636e7966295b2613fda22b4dc52b01c30618a50ff3524f57ec661a9dced249df93f163138a0df6b0"
}
```

<Table>
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
        status\_code
      </td>

      <td>
        Status code of transaction charge result.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        status\_message
      </td>

      <td>
        Description of transaction charge result.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        transaction\_id
      </td>

      <td>
        Transaction ID given by Midtrans.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        order\_id
      </td>

      <td>
        Order ID specified by you.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        gross\_amount
      </td>

      <td>
        Total amount of transaction in IDR.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        payment\_type
      </td>

      <td>
        Transaction payment method.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        transaction\_time
      </td>

      <td>
        Timestamp of transaction in ISO 8601 format. Time Zone: GMT+7.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        transaction\_status
      </td>

      <td>
        Status of bank transfer transaction. Value:<br/>`pending` : Bank Transfer transaction is created.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        fraud\_status
      </td>

      <td>
        Detection result by Fraud Detection System (FDS). Value:<br/>`accept` : Approved by FDS.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        va\_numbers
      </td>

      <td>
        Bank name and Virtual Account number generated by Midtrans.
      </td>

      <td>
        [JSON Array](https://docs.midtrans.com/reference/va-number-object)
      </td>
    </tr>

    <tr>
      <td>
        payment\_amounts
      </td>

      <td>
        Payment histories for the transaction. RECOMMEND TO NOT USE payment\_amounts legacy field as payment\_amounts is only filled in BNI-VA and is set as empty array \[] in other banks (BCA, BRI, Permata)  

         RECOMMEND TO USE gross\_amount field field instead since gross\_amount field will always be there for all banks VA (BNI, BCA, BRI, Permata).
      </td>

      <td>
        [JSON Array](https://docs.midtrans.com/reference/payment-amount-object)
      </td>
    </tr>

    <tr>
      <td>
        currency
      </td>

      <td>
        ISO-4217 representation of three-letter alphabetic currency code. Value: `IDR`.<br /> **Note**: Currently only `IDR` is supported.
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        signature\_key
      </td>

      <td>
        Combination of parameters such as `order_id`, `status_code`, `gross_amount`, `server_key` to verify integrity of payload/response.
      </td>

      <td>
        String
      </td>
    </tr>
  </tbody>
</Table>

<br />

> 📘 Note
>
> Possible error codes are **400**, **401**, **402**, **406**, **410**