---
updatedAt: 2026-05-04T02:23:51.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Convert Invoice

**Endpoints:** /v1/invoices/\{invoice\_id}/convert\
**HTTP Method:** PATCH\
**Headers:**

Production: `https://api.midtrans.com/v1/invoices/{invoice_id}/convert`

Sandbox: `https://api.sandbox.midtrans.com/v1/invoices/{invoice_id}/convert`

| Key           | Description                            |
| :------------ | :------------------------------------- |
| Authorization | Basic Base64Encode(merchantServerKey:) |

> 📘 Eligibility
>
> Only invoice documents with document\_type = `quotation` can be converted.\
> Quotation must not be expired (current time must be before `quotation_validity_date`) and must not have been converted before (`converted_at` is null)
>
> Client fields are optional and can be sent to override existing client values if needed during conversion. Only fields provided in the request will be updated.

## Request Body

```
{
    "client": {
        "id": "Midtrans123",
        "name": "midtrans user",
        "email": "email@midtrans.com",
        "phone": "628129912838"
    }
}
```

## Request JSON Body Details

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Parameter
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        client  
        Optional
      </td>

      <td>
        Client information associated with the invoice.
      </td>
    </tr>

    <tr>
      <td>
        client.id  
        Optional
      </td>

      <td>
        Number of the invoice
      </td>
    </tr>

    <tr>
      <td>
        client.name  
        Optional
      </td>

      <td>
        Client name.
      </td>
    </tr>

    <tr>
      <td>
        client.email  
        Optional
      </td>

      <td>
        Client email address.
      </td>
    </tr>

    <tr>
      <td>
        client.phone  
        Optional
      </td>

      <td>
        Client phone number.
      </td>
    </tr>
  </tbody>
</Table>