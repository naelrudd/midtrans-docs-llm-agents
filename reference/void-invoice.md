---
updatedAt: 2026-07-03T08:32:26.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Void Invoice

**Endpoints:** /v1/invoices/{invoice\_id}<br />**HTTP Method:** PATCH<br />**Headers:**

Production: `https://api.midtrans.com/v1/invoices/{invoice_id}/void`

Sandbox: `https://api.sandbox.midtrans.com/v1/invoices/{invoice_id}/void`

| Key           | Description                            |
| :------------ | :------------------------------------- |
| Authorization | Basic Base64Encode(merchantServerKey:) |

<Callout icon="📘" theme="info">
  ### Eligibility

  Only invoices with PENDING and OVERDUE status can be voided. For quotations, only PUBLISHED quotations can be voided.
</Callout>

<br />

***

# Request Example

### Without cancel\_as:

```
curl --location --request PATCH 'https://api.midtrans.com/v1/invoices/{invoice_id}/void' \
--header 'Authorization: Basic Base64Encode(merchantServerKey:)'
```

### With cancel\_as:

```
curl --location --request PATCH 'https://api.midtrans.com/v1/invoices/{invoice_id}/void' \
--header 'Authorization: Basic Base64Encode(merchantServerKey:)' \
--header 'Content-Type: application/json' \
--data '{
    "cancel_as": "client"
}'
```

# Body Parameter

| Parameter                | Description                                                                                                                                                                                                                                                                                        |
| :----------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| cancel\_as<br />Optional | Specifies the cancellation mode used when voiding a quotation: providing `client` sets the status to `REJECTED`, while leaving it null, empty, or providing any other value sets the status to `CANCELLED`(note: this parameter is applicable only to Quotations and cannot be used for Invoices). |

<br />

# Response

```json 200 - OK
{
   "success": true
}

```
```json 404 - Not Found
{
   "error_messages": [
       "Not Found"
   ]
}

```
```json 409 - Conflict
{
   "error_messages": [
       "Invoice cannot be canceled"
   ]
}

```
```json 500 - Internal Server Error
{
   "error_messages": [
       "Internal server error"
   ]
}

```

<br />