---
updatedAt: 2026-01-08T05:27:58.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Overview

This section will explain about Payment Link API BETA. Merchant can create & manage Payment Link using the API. Payment Link is a web-based link (URL) which can be shared to Customer to receive payments from them – like an invoice. The link will redirect them to Midtrans hosted payment web page.

<br />

Have a feature request / feedback for Payment Link? Submit it directly to our product team's inbox or upvote other feature requests <Anchor label="here" target="_blank" href="https://midtrans.canny.io/featurerequest">here</Anchor>.

***

<br />

## Pre-requisite

<br />

Midtrans merchant account & Midtrans API Keys.

<br />

***

<br />

## Steps

<br />

1. Merchant's backend sends [request to Create Payment Link API](/reference/create-payment-link), in order to retrieve payment URL.
2. Share the payment URL to Customer (e.g. via system, messaging app, or Midtrans automated email), and then wait for them to proceed to payment.
3. Merchant [gets notified of payment status changes & handles](/reference/handle-notifications) accordingly.

***

<br />

<b>Questions?</b> [Contact our support team.](https://midtrans.com/contact-us)

<b>Not ready to integrate?</b> [Create a test account first.](https://dashboard.midtrans.com/register)

<b>Help us improve this docs & our solutions </b> - [let us know your feedback.](/page/report-issues)