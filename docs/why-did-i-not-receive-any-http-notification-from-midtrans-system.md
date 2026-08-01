---
updatedAt: 2025-11-11T00:16:18.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Why did I not receive any HTTP notification from Midtrans’ system?

Merchant typically fails to receive HTTP notification from us because of many reasons, most commonly are network disturbances and merchant’s endpoint URL is unavailable. If you are whitelisting IP address for any incoming messages, please include the following IP block:

**Production Environment:**\
**103.208.23.0/24\
103.208.23.6/32\
103.127.16.0/23\
103.127.17.6/32**

**Sandbox Environment:**\
**103.58.103.177**

For more details please [click here ↗.](https://docs.midtrans.com/en/technical-reference/ip-address)