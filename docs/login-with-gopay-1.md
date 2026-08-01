---
updatedAt: 2026-05-21T06:20:11.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Login with GoPay

A flow where users authenticate using their GoPay account via phone number.

# What is Login with GoPay?

Login with GoPay allows users to sign in to a your application using their GoPay account. Authentication is handled by GoPay, including OTP, PIN, and face verification.

<Image align="center" src="https://files.readme.io/70791070649ba2d87d5af0bf46d6e59fe042f35dafae742c6c6b576d0d74a328-My_Jam_Frame_2.png" />

Once the flow is completed, a **Linking Token** is returned — a permanent token that links the user's GoPay account to your platform. Store this token securely as it will be used for subsequent GoPay interactions on behalf of the user.

> **Note:** The Linking Token is issued only upon successful completion of the required verification steps. Incomplete or failed flows will not produce a token.