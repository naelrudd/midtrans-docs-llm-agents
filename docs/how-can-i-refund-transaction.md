---
updatedAt: 2025-11-10T22:45:09.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# How can I refund transaction?

Transactions that can be refunded through Midtrans are only credit card, e-wallet, QRIS, Shopeepay and Akulaku payment methods. For other payment methods, the process of refunding funds to customers is completely left to the merchant.

The conditions for a successful refund are:

1. Refund only applies to credit card, e-wallet, QRIS, Shopeepay and Akulaku.
2. Refund can be processed if the status is **Settlement**.
3. There are funds that can be disbursed (Payable Amount).

The refund process for transactions can be done using the refund button via the Midtrans dashboard (MAP) or through the [refund API ↗](https://api-docs.midtrans.com/#direct-refund-transaction).

<br />

For refund using Midtrans Dashboard (MAP) it can be done with following step:

1. Login to Midtrans Dashboard (MAP).

   ![](https://files.readme.io/79151ca-image.png)
2. Select menu Transactions.

   ![](https://files.readme.io/f142bc6-image.png)
3. Select the transaction wants to refunded, it can searched by Order Id or else.

   ![](https://files.readme.io/7adf52f-image.png)
4. Select refund button on Detail Transaction.

   ![](https://files.readme.io/3140e9c-image.png)
5. Input the amount wants to refunded on **Refund Amount** column, as additional information for refund can be done with partially from total transaction or can be refunded with full amount.

   ![](https://files.readme.io/6c7bf12-image.png)
6. Input the reason on **Reason for Refund** column.\
   Example: Cancel Transaction, Double Order, Out of stock, etc

   ![](https://files.readme.io/5dcdfe8-image.png)
7. Click button **Refund**.

If your refund button has not been activated, you can activate it by filling out the form at [this link ↗](https://midtrans.com/contact-us/transaction-information/prosedur-refund-pengembalian-dana).