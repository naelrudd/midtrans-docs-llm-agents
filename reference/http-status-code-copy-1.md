---
updatedAt: 2026-09-28T12:00:08.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# HTTP Status Code

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        HTTP Code
      </th>

      <th style={{ textAlign: "left" }}>
        HTTP Status
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        200
      </td>

      <td style={{ textAlign: "left" }}>
        OK
      </td>

      <td style={{ textAlign: "left" }}>
        Everything is working as expected
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        400
      </td>

      <td style={{ textAlign: "left" }}>
        Bad Request
      </td>

      <td style={{ textAlign: "left" }}>
        The request is not accepted due to missing parameter or wrong parameter format
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        401
      </td>

      <td style={{ textAlign: "left" }}>
        Unauthorized
      </td>

      <td style={{ textAlign: "left" }}>
        No valid API key provided
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        403
      </td>

      <td style={{ textAlign: "left" }}>
        Forbidden
      </td>

      <td style={{ textAlign: "left" }}>
        The API key does not have permission to perform the request
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        404
      </td>

      <td style={{ textAlign: "left" }}>
        Not Found
      </td>

      <td style={{ textAlign: "left" }}>
        The requested resource is not valid
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        405
      </td>

      <td style={{ textAlign: "left" }}>
        Method Not Allowed
      </td>

      <td style={{ textAlign: "left" }}>
        The request method is not supported for the requested resource
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        409
      </td>

      <td style={{ textAlign: "left" }}>
        Conflict
      </td>

      <td style={{ textAlign: "left" }}>
        The request conflicted with another request (possibly due to having the same idempotency key)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        429
      </td>

      <td style={{ textAlign: "left" }}>
        Too Many Requests
      </td>

      <td style={{ textAlign: "left" }}>
        Too many requests hit the API too quickly. We recommend limiting the request amount or implementing exponential backoff
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        5xx
      </td>

      <td style={{ textAlign: "left" }}>
        Server Errors
      </td>

      <td style={{ textAlign: "left" }}>
        Something went wrong on Midtrans' end. To handle this:  

        1. Reach out to [our support team](https://midtrans.com/contact-us)  for clarification on whether it's safe to retry the request. Explain the issue you encountered.

        2. Ensure you include all relevant request details. This could involve the specific API endpoint, payload, and any relevant parameters used.

        3. If your request used an idempotency key, make sure to provide it. The idempotency key helps ensure that the same request is not processed multiple times if retried.By following these steps, you can get the necessary guidance on whether retrying is safe and how to proceed.
      </td>
    </tr>
  </tbody>
</Table>