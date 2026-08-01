---
updatedAt: 2025-11-10T23:00:32.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Payment Method: Card

Using *Card* payment method, customers can make payments using a credit card or any online-transaction-capable debit card within Visa, MasterCard, JCB, American Express (Amex) or China Union Pay (CUP) network. Midtrans sends real-time notification when the customer completes the payment.

The steps to integrate with Midtrans are given below.

1. Get [token](https://docs.midtrans.com/reference/get-token).
2. Send [Charge request](https://docs.midtrans.com/reference/charge-transactions-on-card) using the token.
3. For 3D secure transactions, redirect the customer to the address specified in the response. (Optional)
4. [Handle notifications](https://docs.midtrans.com/reference/notifications-handling).

<br />

<br />

> 📘 Note
>
> Not all acquiring banks support JCB, Amex, or CUP cards. Please contact us for more information or assistance with activation of JCB, Amex, or CUP acceptance.