---
updatedAt: 2026-06-10T10:06:08.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Setting up Callback

All of Esign products are processed asynchronously.

With that in mind, callbacks (webhook) will be the primary communication between our platform and your system to make sure integration is seamless.

## Details To Share to Us

1. Callback endpoint URL
2. HTTP method (`POST`, `PUT`, or `PATCH`)
3. Your Production IPs for us to whitelist
4. Callback authentication (Basic Auth, Bearer token, etc.) - *required if your callback API has auth*.

## Callback Endpoint Requirements

Your callback endpoint should:

* Accept JSON payloads
* Respond `200 OK` quickly
* Process business logic asynchronously
* Be idempotent by a combination of `submissionId` `status` and `result`fields.

## Recommended Callback Handling Logic

1. Verify callback authenticity based on your configured method.
2. Parse `submissionId`, `status`, `result`, `reasonCode`.
3. Return `200 OK` immediately.

## Fallback Polling

In the extremely rare case where callback is delayed or not sent, you can also poll our Submission details API.

API doc: <https://docs.midtrans.com/reference/getsubmissions>

```bash
curl -X GET \
	"https://onekyc.ky.id.sandbox.gopayapi.com/esign-partner/v1/submissions" \
	-H "x-onekyc-token: <TOKEN>" \
	-H "x-partner-user-id: user-123" \
	-H "x-partner-user-id-type: CLIENT_USER_ID" \
	-H "x-partner-session-id: session-005"
```

<br />