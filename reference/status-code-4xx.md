---
updatedAt: 2025-11-11T00:26:58.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Code 4xx

List of Midtrans specific status codes starting with 4XX.

<Table>
  <thead>
    <tr>
      <th>
        <b>Status</b>
      </th>

      <th>
        <b>Description</b>
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **400**
      </td>

      <td>
        Validation Error, merchant sends bad request data example; validation error, invalid transaction type, invalid credit card format, etc.
      </td>
    </tr>

    <tr>
      <td>
        **401**
      </td>

      <td>
        Access denied due to unauthorized transaction, please check client key or server key
      </td>
    </tr>

    <tr>
      <td>
        **402**
      </td>

      <td>
        Merchant doesn't have access for this payment type
      </td>
    </tr>

    <tr>
      <td>
        **403**
      </td>

      <td>
        The requested resource is only capable of generating content not acceptable according to the accepting headers that sent in the request
      </td>
    </tr>

    <tr>
      <td>
        **404**
      </td>

      <td>
        The requested resource is not found
      </td>
    </tr>

    <tr>
      <td>
        **405**
      </td>

      <td>
        HTTP method is not allowed
      </td>
    </tr>

    <tr>
      <td>
        **406**
      </td>

      <td>
        Duplicate order ID. Order ID has already been utilized previously
      </td>
    </tr>

    <tr>
      <td>
        **407**
      </td>

      <td>
        Expired transaction
      </td>
    </tr>

    <tr>
      <td>
        **408**
      </td>

      <td>
        Merchant sends the wrong data type
      </td>
    </tr>

    <tr>
      <td>
        **410**
      </td>

      <td>
        Merchant account is deactivated. Please contact Midtrans support
      </td>
    </tr>

    <tr>
      <td>
        **411**
      </td>

      <td>
        Token id is missing, invalid, or timed out
      </td>
    </tr>

    <tr>
      <td>
        **412**
      </td>

      <td>
        Merchant cannot modify status of the transaction
      </td>
    </tr>

    <tr>
      <td>
        **413**
      </td>

      <td>
        The request cannot be processed due to malformed syntax in the request body
      </td>
    </tr>
  </tbody>
</Table>