---
updatedAt: 2025-11-11T00:13:32.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Can I cancel a transaction that has been settled?

Canceling transactions can only be done for card transactions with **CAPTURE / SUCCESS** status and other payment methods with **PENDING** status. You can do so from the [transaction page ↗](https://dashboard.midtrans.com/payments) on our portal, or via our [API ↗](https://api-docs.midtrans.com/#expire-transaction). To cancel from the portal, simply search the specific transaction, go into its details and click the **CANCEL** button.

For credit card transactions, if the status is Capture/Success and canceled, the customer limit will automatically return to a maximum of H+1 working days.

For other payment methods, there is no refund process from the Midtrans side to merchants or merchant consumers, because the transaction status has not yet reached Settlement.

Note: transactions that status is Settlement cannot be canceled, however [refunds ↗](https://docs.midtrans.com/docs/how-can-i-refund-transaction) can be made, but only for the credit card, GoPay, QRIS, Shopeepay, and Akulaku transactions.