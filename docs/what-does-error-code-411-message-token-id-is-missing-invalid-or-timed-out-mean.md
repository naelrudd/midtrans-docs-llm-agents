---
updatedAt: 2025-11-11T00:16:20.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# What does error code 411 message “Token id is missing, invalid, or timed out” mean?

This error is related to token issues in card payment. If you encounter this error, please:

Ensure that token generation and token charging time gap short (less than 10 minutes, to be safe);\
Ensure that no '**token\_id**' is reused for another transaction, except for One Click or Two Clicks transactions.