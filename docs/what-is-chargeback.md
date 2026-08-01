---
updatedAt: 2025-11-11T00:16:06.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# What is Chargeback?

Chargeback is a fund reversal request from a cardholder for their card transactions, made via their issuing bank. Bank will then forward the request to merchant via payment gateway to request for further evidences if any, before proceeding with the fund reversal, if the evidences are deemed insufficient.

Chargeback is usually requested by cardholder due to various reasons, such as cardholder never authorized the charge to their card due to fraud, product/services not rendered, product/services rendered are not as promised during the sale process, cardholder would like to ask for a refund, etc.

The process starts with a request from the cardholder to the bank for fund reversal on the disputed transactions.

After the issuing bank receives the chargeback request, the rebuttal will be forwarded by card issuing bank to acquiring bank, to be informed to the merchant via Midtrans as their payment gateway or directly to the merchant.

Merchants then will be requested to provide evidence to refute the chargeback request by providing several supporting documents, such as:

1. Transaction invoice.
2. Proof of Shipment, if any.
3. Customer details, if any.
4. Proofs of correspondence between merchant and cardholder, if any.

These supporting documents should be provided by merchants before the set deadline, usually within 7-calendar-days. Acquiring bank will process this supporting documents to answer the cardholder’s chargeback request.

It is also important to note that bank imposes a maximum chargeback threshold that has to be maintained by each merchants - hence even though 3DS protection exists, merchants are still expected to keep the number of chargebacks happening in their business to a minimum. Midtrans provides a [fraud detection service ↗](https://midtrans.com/features/fraud-detection)included by default with our payment gateway service to help merchant to reduce the potential of chargebacks from occuring in merchant's business.