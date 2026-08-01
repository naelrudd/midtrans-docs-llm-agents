---
updatedAt: 2025-11-11T00:12:31.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# How do I migrate my account from Sandbox to Production?

Before migrating your account to Production mode, you need to complete the [onboarding process ↗](https://passport.midtrans.com/) for submit the legal documents, get your application approved, and have your production credentials (i.e. Bank Merchant ID or Merchant Key) with you. Please also ensure you have integrated our system by following this [step-by-step guide ↗](https://docs.midtrans.com/).

If all the above are done, please complete these extra steps to finally migrate your account to Production mode:

* In your Merchant Administration Portal, ensure that your [General Setting ↗](https://dashboard.midtrans.com/settings/general_info) is completed;
* Ensure that your [Configuration ↗](https://dashboard.midtrans.com/settings/vtweb_configuration) is completed, and the Payment URL Notification testing sends '200';
* Change your environment to 'Production';
* Change your [Access Keys ↗](https://dashboard.midtrans.com/settings/config_info) (these two points are important to avoid [this error ↗](https://docs.midtrans.com/docs/what-does-the-error-code-401-message-access-denied-due-to-unauthorized-transaction-please-check-client-key-or-server-key-mean));
* Test an actual real transaction of minimal value IDR 10,000.

If the test transaction is successful, you are ready to go live and accept payments with Midtrans.