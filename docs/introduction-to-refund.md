---
updatedAt: 2025-11-11T00:15:11.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Introduction to Refund

# About Refund

Refund means returning the funds back to the customer. It is caused by double order, products/services not available, cancelled flight, etc.

To process refund, or to return the funds back to customer, we need to make sure that the money has been successfully transferred from customer to merchant; or operationally, the payment status has been changed to “Settlement”. In Midtrans, refund request is mostly applicable in Card Payment transactions, and it works by restoring the Card limit. Refund for other payment methods can be processed by the merchant itself, usually by transferring the money back.

Refund process for Credit Card normally takes 7-14 working days. Refund for Debit Card might take longer, up to two months; and customer needs to contact their Issuing Bank as well.

Refund request took couple of days because it needs to be coordinated with various parties, such as acquiring and issuing bank. If customer complained that their limit has not been returned, merchant should ask the Acquiring Banks and customer should ask the Issuing Bank as well. It usually need data of: orderID, merchants details, customer details, and approval code.

# Credit Card - Aggregator

If you are a merchant who uses Midtrans aggregator agreement for Card payment, refund request should be done via Midtrans. You can open Merchant Administration Portal, look for the specific orderID you need to refund, and click Refund button. After pressing the button, please fill in the refund amount and refund reason then press Submit. We will process your request to banks on the next working days. You will still got the funds, but we will deduct the funds from your next payout request.

If your refund button has not been activated, you can activate it by filling out the form at [this link ↗.](https://midtrans.com/contact-us/transaction-information/prosedur-refund-pengembalian-dana)

# Credit Card - Facilitator

If you are a merchant who uses Midtrans facilitator agreement for Card payment, refund request should be done directly via Banks. Please contact our team through [this link ↗](https://midtrans.com/contact-us/transaction-information/prosedur-refund-pengembalian-dana), fill the form and submit it to provide you the refund request templates.