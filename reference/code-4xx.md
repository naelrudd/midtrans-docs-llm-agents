---
updatedAt: 2025-11-11T00:28:33.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Code 4xx

List of Midtrans specific status codes starting with 4XX.

| Status | Description                                                                                                             |
| ------ | ----------------------------------------------------------------------------------------------------------------------- |
| `400`  | Validation Error. You have sent bad request data like invalid transaction type, invalid payment card format, and so on. |
| `401`  | Access denied due to unauthorized transaction. Please check *Client Key* or *Server Key*.                               |
| `402`  | No access for this payment type.                                                                                        |
| `403`  | The requested resource is not capable of generating content in the format specified in the request headers.             |
| `404`  | The requested resource/transaction is not found. Please check `order_id` or other details sent in the request.          |
| `405`  | HTTP method is not allowed.                                                                                             |
| `406`  | Duplicate order ID. `order_id` has already been utilized previously.                                                    |
| `407`  | Expired transaction.                                                                                                    |
| `408`  | Wrong data type.                                                                                                        |
| `410`  | GoPay user is blocked                                                                                                   |
| `411`  | `token_id` is missing, invalid, or timed out.                                                                           |
| `412`  | Transaction status cannot be updated.                                                                                   |
| `413`  | The request cannot be processed due to syntax error in the request body.                                                |
| `414`  | Refund request is rejected due to merchant insufficient funds.                                                          |
| `429`  | API rate limit exceeded. The global rate limit is applied to Create Pay Account API and Charge API                      |