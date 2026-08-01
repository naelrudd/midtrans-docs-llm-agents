---
updatedAt: 2025-11-11T00:16:29.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Why I can’t receive email from Midtrans?

Though it's a rare condition, there might be a case you didn't receive emails from Midtrans. We advise you to check your Spam folder first.

If it didn't solve the problem, your email address might be suppressed in Mailgun (the email provider used by Midtrans).

Based on the mechanism used by Mailgun, the issue of email getting suppressed happen to domains or email server that has been proven encounter issues or has a problematic history in Mailgun. Please refer to this article (official from Mailgun): <https://help.mailgun.com/hc/en-us/articles/360012287493-What-Are-Mailgun-Suppressions->, for details suppression mechanism.

We can unblock your email address, only if you have confirmed the following points has been checked on your side to prevent this problem repeated in the future:

1. The email Inbox is not full
2. The domain or email server is active and can receive email sent from domain **@midtrans.com**
3. The domain or email server in a stable condition