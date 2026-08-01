---
updatedAt: 2025-11-11T00:16:04.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Why was my customer's transaction rejected?

You can view the rejection reason of transaction in the dashboard by :

1. Open the Merchant Administration Portal (MAP)
2. Search the transaction that was declined
3. Click the OrderID to access the transaction details page.
4. Choose button **"See Why"** in the transactions details notification.

   ![](https://files.readme.io/2dadcee-image.png)

Rejection of a transaction usually occurs due to these reasons :

1. **Deny by Bank**\
   Denied by Bank usually happened because the issuing bank did not approve the transaction.\
   We suggest to advise the customer to contact the issuing bank to clarify about the denied reason.\
   Note : It's recommended to advise the customer to ask for the reason why the transaction is rejected, not whether there are issues with their cards.

2. **Deny by Fraud Detection System (FDS)**\
   Deny by FDS means the transaction exhibits some alarming parameters which would most likely be fraudulent, so the transaction is denied for safety precaution.\
   If this customer is a valid customer and has been verified by merchant, we can [whitelist the email ↗](https://docs.midtrans.com/docs/my-customers-card-transaction-was-rejected-by-fraud-detection-system-how-can-i-whitelist-my-customers-transaction) to relax the filtering by our Fraud Detection System for customer's future transactions. We strongly advise to only request whitelist for verified customers only to prevent future disputes from the cardholder.

3. **Transactions are done by blacklisted customers**\
   The customer have been blacklisted by Midtrans for several reasons, such as fraudulent reports from Principals or banks.