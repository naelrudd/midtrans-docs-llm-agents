---
updatedAt: 2025-11-10T22:59:34.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# API Headers & Idempotency

| Header Parameter | Description                                                                                                                                                                                                                                     | Required    | Example                                     |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ------------------------------------------- |
| Idempotency-Key  | Idempotency key to safely handle retry requests.                                                                                                                                                                                                | Optional    | d63ae3e0-a7c5-4733-8d81-b451168d8a2c-charge |
| X-Payment-Locale | Header provided to change language on any web pages rendered by specific payment type (Currently only for **Gopay** linking & charge). Default value is `id-ID`                                                                                 | Optional    | `en-EN` or `id-ID`                          |
| X-POP-ID         | Merchant's POP ID provided by Midtrans. This is a conditional field that may be mandatory for merchant with special integration with Midtrans. Midtrans team will inform merchant separately if merchant needs to pass X-POP-ID in the request. | Conditional | 21cc3371-4bba-4ec6-8e0d-62163e130cdc        |

<br />

***

## Idempotent Requests

`Idempotency-Key` is a unique value that is put on header on API requests. Midtrans API accepts `Idempotency-Key` on header to safely handle retry request without performing the same operation twice. This is helpful for cases where you have not received the response because of network issue or other unexpected error.

<br />

### Use case sample

If you send a request with idempotency key:A, but Midtrans doesn't send any response due to unexpected error, you can safely retry request with idempotency key:A, to get a response. It is ensured that the request is processed only once.

Midtrans handles idempotent request by saving only the successful response. Midtrans returns the same response to you, if you create a request with the same `Idempotency-Key` regardless of the request body. Please note that the key value lifetime is five minutes. After five minutes, Midtrans will process the request again. For example, second charge request might get conflict exception because it uses the same order id. It is important to note that the `Idempotency-Key` is global across any endpoints. It is recommended to generate a new `Idempotency-Key` value for every different operation on the same transaction.

There's also a special case where we handle an "on-process" request. If you retry a request while the first request is still in process and have not received a response yet, Midtrans returns a response with HTTP status code `202` until the first request finishes processing.

Midtrans API accepts `Idempotency-Key` value on all POST requests except request to `/token` and `/account` endpoint.

The maximum length of `Idempotency-Key` is **46**. Midtrans ignores the usage of `Idempotency-Key` if it is longer than the maximum length. To create random unique key, we suggest the use of UUID to avoid `Idempotency-Key` collision between requests.

> 📘 Note
>
> Currently, idempotent requests are not supported for these payment methods:
>
> 1. Permata Virtual Account
> 2. CIMB Clicks
> 3. KlikBCA
> 4. Indomaret