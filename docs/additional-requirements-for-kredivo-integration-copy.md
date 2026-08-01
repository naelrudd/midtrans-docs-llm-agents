---
updatedAt: 2025-11-11T00:13:03.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Additional Requirements for Kredivo Integration (COPY)

By default, Kredivo requires **item\_details** ([click here ↗](https://docs.midtrans.com/reference/json-objects#item-details-object)) and **customer\_details** ([click here ↗](https://docs.midtrans.com/reference/json-objects#customer-details-object)) on top of **payment\_type** and **transaction\_details** to be sent by merchants as **MANDATORY PARAMETERS.**

To ensure that merchants comply with Kredivo requirements, all merchants will need to conduct **transaction testing** with the Kredivo team before accepting real Kredivo transactions from customers. Kredivo will check the completeness of the parameters during the testing process.