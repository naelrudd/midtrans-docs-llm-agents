---
updatedAt: 2025-11-11T00:12:14.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Introduction to Static QRIS

Quick Response Code Indonesian Standard, commonly abbreviated as QRIS (read KRIS) is the unification of QR types from various Payment System Service Providers (PJSP) using QR codes. QRIS was developed by the payment system industry together with Bank Indonesia to make the transaction process with QR codes easier, faster, and more secure.

Merchants only need to create an account with one of the QRIS providers [licensed by BI ↗](https://www.bi.go.id/PJSPQRIS/Default.aspx), one of which is [Midtrans ↗](https://midtrans.com/).

Furthermore, merchants can accept payments from customers using QR from any application. What are you waiting for? let's register and use QRIS!​​​

<br />

# Content List

## What is the difference between static QRIS and dynamic QRIS?

| **Static QRIS**                                                                                                                                    | **Dynamic QRIS**                                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------- |
| QR code for static QRIS will **always be the same**, merchants only need **1 QR code** for every transaction.                                      | The QR code for dynamic QRIS will **always be different** for each transaction.                                         |
| The payment amount in static QRIS is not determined in advance by the merchant, **the customer can input the nominal** after scanning the QR code. | The payment amount in dynamic QRIS is **determined in advance by the merchant** and cannot be changed by your customer. |
| Order ID for static QRIS transactions is **determined by the system**, with the format QRIS-xxx.                                                   | Order ID for dynamic QRIS transactions **can be determined by the merchant** freely.                                    |
| Transactions will be formed for static QRIS **after payment is made**.                                                                             | Transactions will be formed for dynamic QRIS **before payment** is made.                                                |
| Refunds for static QRIS are currently **not available**.                                                                                           | Refunds for dynamic QRIS **can be made** via the dashboard and API.                                                     |

<br />

<Image
  alt="An example of a **static QRIS** that can be displayed in your offline store. The QR code will **always be the same** for every transaction.  
[Image Source](https://qris.online/homepage/qris-news-detail?page=3-7-alasan-mengapa-bisnis-anda-wajib-pakai-qris-sekarang-juga)"
  align="center"
  src="https://files.readme.io/693e486-image_14.png"
>
  An example of a **static QRIS** that can be displayed in your offline store. The QR code will **always be the same** for every transaction.\
  [Image Source](https://qris.online/homepage/qris-news-detail?page=3-7-alasan-mengapa-bisnis-anda-wajib-pakai-qris-sekarang-juga)
</Image>

<br />

<Image alt="An example of a **dynamic QRIS**. The QR code will **always be different** for each transaction." align="center" src="https://files.readme.io/1644ec3-QRIS_dinamis.png">
  An example of a **dynamic QRIS**. The QR code will **always be different** for each transaction.
</Image>

***

<br />

## For what purpose do merchants use static QRIS?

In general, static QRIS can be used for:

* The need to accept payments via QRIS without an EDC/POS machine in offline stores or bazaars where a very fast payment flow is required.
* Accepting donations/open amount transactions, the QRIS code can be displayed by merchants on the website or social media.
* Payment of transactions via social media/chat app, as an alternative to Payment Link.
* Payments for transactions whose amount is unknown before the end of the transaction/may change, such as down payments, service payments, or others.

***

<br />

## How to receive payments using static QRIS

<Image align="center" src="https://files.readme.io/16550c4-mceclip1.png" />

***

<br />

## How to activate static QRIS for GoPay

By registering for GoPay products at Midtrans, merchants will get static QRIS products as well as dynamic QRIS.\
Static QRIS will be received within **3-7 working days** after completing [the registration process ↗](https://dashboard.midtrans.com/register?language=en) and filling out [the GoPay QRIS registration form ↗](https://www.tfaforms.com/5019792).

***

<br />

## Does the merchant need a different account (MID) for static GoPay activation if the dynamic GoPay is already active?

No need, merchants can use the same account (MID).

***

<br />

## How merchants get a static QR code

Midtrans will send a **digital image** file (a digital image of a static QR code) to **the merchant's email** and **WhatsApp**.

***

<br />

## What does the merchant need to do after the file is sent?

* Prints a static QRIS code to install in the shop/bazaar.
* Sharing digitally (for example, for transactions via WhatsApp, or can be posted on the website for open amount donations, social media, sent via newsletters, and others).

***

<br />

## How to check static QRIS transactions

You need to be a Midtrans merchant to be able to use Midtrans static QRIS.\
Static QRIS transactions can be checked on [the Midtrans dashboard (MAP) ↗](https://dashboard.midtrans.com/login?language=en). Please note that static QRIS transactions **cannot be checked** via **the GoBiz app/dashboard**.\
Follow these steps to check your transaction:

1. [Login ↗](https://dashboard.midtrans.com/login?language=en) with your registered email.
2. Select **the Transaction** menu.

   <Image align="center" src="https://files.readme.io/252b42e-mceclip0.png" />
3. You can find a list of successful transactions on this page.
   1. A transaction with **SETTLEMENT** status means that the funds have been received from the customer, and **can be withdrawn within 2 working days**.
   2. Transactions with **FAILURE, DENY, CANCEL, or EXPIRE** status means the transaction failed and **money was not received**.

***

<br />

## How to withdraw static QRIS funds

Withdrawals can be made within **2 working days** after payment from the customer is received (**SETTLEMENT** status).\
There are 2 methods to be able to withdraw your funds, namely **Manual Payout** and **Automatic Payout**.\
Please [click here ↗](https://docs.midtrans.com/docs/how-can-i-have-my-money-in-my-account-payout) to find out how to withdraw your funds with the method you need.

***

<br />

## Is static QRIS already available on the Payment Link?

Currently not available, merchants can simply use a **digital image** file (digital image of a static QR code) that Midtrans sends to the **merchant's email and WhatsApp**.

***

<br />

## Can a static QRIS be created via the API?

Currently not available, merchants can simply use a **digital image** file (digital image of a static QR code) that Midtrans sends to the **merchant's email and WhatsApp**.

***

<br />

## The transaction is successful but it's not reflected on the Midtrans dashboard

Have you ever registered for QRIS at a provider other than Midtrans?\
If **yes**, then please check first with the provider whether the transaction exists or not.\
If **not**, then please send the evidence below through [this link ↗](https://midtrans.com/contact-us/transaction-information/Pertanyan-lain).

1. Proof of a successful transaction (a photo containing proof of transaction, merchant name and nominal) - Example of [proof of transaction ↗](https://drive.google.com/file/d/1NX4CweILhhx9yWBpcUnIRp-VA3URi5vz/view).
2. Nominal transaction, payment using which e-wallet/bank and the transaction hours (if it's not in the screenshot. If it's in the screenshot, you can ignore point number 2).

***

<br />

## What if you have registered for QRIS at a provider other than Midtrans?

The current PTEN regulations require the concept of 1 QRIS for all, with priority on processing QRIS transactions on an **on-us basis (same issuer-acquirer)**. Due to the 1 QRIS concept for all of these, if the KTP/Entity has previously been registered with PTEN for QRIS products outside Midtrans, then the static QRIS code provided by Midtrans will automatically apply to QRIS acquirers registered outside Midtrans.\
This means that **there is a possibility that certain transactions will go to another acquirer outside of the acquirer supported by Midtrans**, even though this QRIS code is sent to you by Midtrans. In this case, **please check with the acquirer whether the transaction exists or not**.

***

> 📘 Info 💡
>
> **Acquirer** is a bank or non-bank institution whose function is to receive transaction funds from merchant banks (issuers).
>
> Example: GoPay, ShopeePay, OVO, DANA, etc.
>
> **Issuer** is a bank or non-bank institution whose function is to send transaction funds to acquirers.
>
> Example: BCA, BNI, BRI, Mandiri, etc.

> 🚧 Notes 📝
>
> Midtrans **cannot see transactions processed by other acquirers**. In this case, Midtrans acts as a distributor of the QRIS code generated by PTEN, but Midtrans does not have the right to regulate which acquirer will process the transaction.
>
> If you want that all transactions are processed by Midtrans, you can submit a request to another provider to **request termination of cooperation with other providers** so that the provider is no longer registered with PTEN as your acquirer.

***