---
updatedAt: 2025-11-11T00:16:01.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# What is ECI on 3DS protocol?

Electronic Commerce Indicator (ECI) is a value returned by Directory Servers (namely Visa, MasterCard, JCB, and American Express) indicating the outcome of authentication attempted on transactions enforced by 3DS.

Possible value returned by **[Visa ↗](https://usa.visa.com/dam/VCOM/download/merchants/verified-by-visa-acquirer-merchant-implementation-guide.pdf)**, **American Express**, and **JCB** and its interpretation:

* **ECI 05:** 3DS authentication was successful; transactions are secured by 3DS.
* **ECI 06:** authentication was attempted but was not or could not be completed; possible reasons being either the card or its Issuing Bank has yet to participate in 3DS.
* **ECI 07:** 3DS authentication is either failed or could not be attempted; possible reasons being both card and Issuing Bank are not secured by 3DS, technical errors, or improper configuration.

<br />

Possible value returned by **[MasterCard ↗](https://www.mastercard.us/content/dam/mccom/en-us/documents/SMI_Manual.pdf)** and its interpretation:

* **ECI 02:** 3DS authentication is successful; both card and Issuing Bank are secured by 3DS.
* **ECI 01:** 3DS authentication was attempted but was not or could not be completed; possible reasons being either the card or its Issuing Bank has yet to participate in 3DS, or cardholder ran out of time to authorize.
* **ECI 00:** 3DS authentication is either failed or could not be attempted; possible reasons being both card and Issuing Bank are not secured by 3DS, technical errors, or improper configuration.