---
updatedAt: 2025-11-11T00:12:33.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Midtrans' notification features

Midtrans has 2 types of notifications that are used to send information to you as a merchant or customer merchant, namely email notification and HTTP notification.

# Email Notification

Midtrans will automatically send a notification in the form of an email containing information regarding the payment method, VA number, order ID, and also payment status.

You can activate the Email Notification feature on your Midtrans dashboard.

* To send notifications to merchants, you can activate it in the Settings menu - Email Notification - (tick) Send email to me - Save.
* To send notifications to customers, you can activate it in the Settings menu - Email Notification - (tick) Send email to customer - Save.

> 🚧 Notes 📝
>
> The email template cannot be changed.

<Image
  alt="Example the email notification

***"
  align="center"
  src="https://files.readme.io/2b9cd3d-mceclip0_3.png"
>
  Example the email notification

  ***
</Image>

# HTTP Notification

Midtrans also sends notifications via HTTP format to the merchant's backend, where the merchant can use the notification to update transaction status on the merchant's database side or for other internal purposes.

To set the page URL that customers will see after completing a transaction, you can do it via the **Settings - Payment - Finish Redirect URL**.

<Image align="center" src="https://files.readme.io/008a351-6f5f6cc1-c1a0-4679-bd0b-b4edadeeaa31.png" />

<Image align="center" src="https://files.readme.io/e4ae18d-df4f5ed2-6390-4b37-82f1-ad369c7a7fbf.png" />

Please ensure the following when setting the Payment Notification URL:

1. Please do not use unusual ports in your notification URL endpoint (e.g: do not use <https://tokoecomm.com:**20070**/notification>), Midtrans notification service cannot send notifications to unusual ports.
2. The URL you use can receive HTTP notifications that Midtrans sends and not be redirected to another URL when accessed.
3. Do not use the IP Address format. (For example, don't use <https://172.168.111.111/notification>).\
   You can do HTTP notification settings via the Settings - Payment - Notification URL menu.

<Image align="center" src="https://files.readme.io/e55af88-8bba1a7c-513e-4c63-8831-8b5f13480688.png" />

<Image align="center" src="https://files.readme.io/a777c19-ad964e03-6f57-45f5-9912-a010f328d30e.png" />

Please ensure the following when setting the Notification URL:

1. Please do not use unusual ports in your notification URL endpoint (e.g: do not use <https://tokoecomm.com:**20070**/notification>), Midtrans notification service cannot send notifications to unusual ports.
2. The URL you use can receive HTTP notifications that Midtrans sends and not be redirected to another URL when accessed.
3. Do not use the IP Address format. (For example, don't use <https://172.168.111.111/notification>).
4. If you use an IP Whitelist to communicate with Midtrans API, please whitelist the Midtrans domain and IP address at [this link ↗](https://docs.midtrans.com/en/technical-reference/ip-address).
5. If you use certain plugins, please adjust the payment notification URL settings for each plugin you use [here ↗](https://docs.midtrans.com/en/technical-reference/library-plugin).

<br />

You can see an example of the JSON sent for each payment method at [this link ↗](https://docs.midtrans.com/en/after-payment/http-notification?id=sample-for-various-payment-methods).