---
updatedAt: 2026-04-10T10:33:35.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Get Linking Token

A Linking token generated after Login with GoPay that links a user's accounts.

For you to get the linking token, you need to initiate our account linking in SNAP-based flow, merchants need to call 2 APIs as follows:

1. Initiate [access token B2B](https://docs.midtrans.com/reference/access-token-api) by calling POST v1.0/access-token/b2b
2. Initiate [binding request](https://docs.midtrans.com/reference/binding-api) by calling POST v1.0/registration-account-binding