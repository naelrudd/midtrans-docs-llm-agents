---
updatedAt: 2025-11-10T22:58:25.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Google Pay™

## Google Pay™ via Hosted Checkout (Midtrans Snap)

Google Pay™ offers a fast, secure way for customers to pay using their Google accounts. By adding Google Pay™, you can:

* Streamline the checkout process
* Increase conversion rates
* Offer a trusted payment method

Midtrans Snap is a hosted checkout solution that simplifies the integration process for you. With Snap, you don't need to handle the complexities of integrating Google Pay™ directly. Midtrans takes care of the technical implementation, making it easier for you to offer Google Pay™ to your customers.

<br />

<Image align="center" className="border" width="450px" border={true} src="https://files.readme.io/4e4c53eed4d001a6a4744729cefa4ad6a89d52266e4fc999931e07a70725fe34-Screenshot_2024-10-14_at_13.46.54.png" />

<br />

## Using Google Pay™ with Snap

When you use Midtrans Snap, the integration of Google Pay™ is handled automatically. Here's what you need to know:

* **Snap Checkout**: When you initiate a Snap transaction, Google Pay™ will be included as a payment option if it's enabled in your Midtrans Dashboard, activated in your Snap Preferences, and the Card payment channel is active.
* **Customer Experience**: Customers will see the Google Pay™ option in the Snap checkout interface. When selected, they'll complete the payment using their Google Pay™ account with a linked card.
* **Transaction Handling**: Midtrans will process the Google Pay™ transaction as a card transaction. This means the transaction will be handled through the credit card payment channel in Midtrans.
  * All card-related settings, such as 3D Secure, fraud detection, and any credit card-specific rules, will apply to Google Pay™ transactions.
  * In your transaction reports and dashboard, Google Pay™ transactions will appear under the card payment method.
* **Notifications**: You'll receive transaction notifications through your existing Snap integration setup. No additional configuration is needed for Google Pay™ transactions. These notifications will indicate that the payment was made via Google Pay™, but the transaction itself will be processed as a card payment.
* **Refunds and Disputes**: As Google Pay™ transactions are processed as card payments, any refunds or disputes will follow the same process as regular credit card transactions in Midtrans.

<br />

## Prerequisites

To start using Google Pay™ with Midtrans Snap, ensure the following requirements are met:

* Midtrans Account:
  * An active Midtrans account
  * Card payment channel activated in your Midtrans account
  * To enroll, contact [Midtrans Support](support@midtrans.com) to enable Google Pay™ for your Midtrans account.
* Hosting Clarification:\
  Midtrans exclusively supports Google Pay™ through the Snap hosted checkout solution. Merchants are not required to:
  * Embed or host the Google Pay button on their websites.
  * Modify their website's Content-Security-Policy (CSP) settings.
* Merchant Actions:\
  Merchants must ensure:
  * Google Pay™ is enabled in Snap Preferences via the Midtrans Dashboard or Enable Google Pay™ in Transaction Request.
  * Compliance with the [Google Pay APIs Acceptable Use Policy](https://payments.developers.google.com/terms/aup).
  * Acceptance of the [Google Pay API Terms of Service](https://payments.developers.google.com/terms/sellertos).

<br />

## Configure Google Pay™ in Snap Preferences

If you have the Google Pay™ feature available, you can control its availability in your Snap checkout:

* In your Midtrans Dashboard, go to Settings > Snap Preferences
* Look for the Google Pay™ option
* Use the toggle switch to enable or disable Google Pay™ for your Snap transactions

<br />

<Image align="center" width="700px" src="https://files.readme.io/f6dd5baccec5a8c33b7064ac4ca117cbb79f18f1b381c4685017f3a9facef6cb-Screenshot_2024-10-14_at_13.46.04.png" />

<br />

## Important Requirements

* 3DS and PAN\_ONLY Support:
  * Midtrans ensures that all Google Pay™ transactions are processed with 3D Secure (3DS).
  * Midtrans supports only PAN\_ONLY credentials, and 3DS is automatically applied for every transaction.
* Merchant Configuration:
  * `secure` must be set to true in credit\_card object
  * Google Pay™ will NOT appear in checkout if:
    * `secure` is set to `false`
    * Currently Google Pay™ does not support installment payments or Installment is configured as required\ <br />
  * Merchants do not need to take additional steps to enable 3DS for Google Pay™ transactions. By setting `"secure": true` in the credit\_card object of the transaction request, 3DS is automatically enforced for all card transactions, including Google Pay™.

<br />

> ## Security Assurance for Merchants:
>
> Google Pay™ transactions processed via Midtrans hosted checkout (Snap) always include 3D Secure (3DS) for enhanced security. Midtrans' integration ensures compliance with the latest payment security standards.

<br />

## Enable Google Pay™ in Transaction Request

```
{
  "transaction_details": {
    "order_id": "order-id",
    "gross_amount": 10000
  },
  "credit_card": {
    "secure": true  // Must be true for Google Pay
  },
  "enabled_payments": ["google_pay"]
}
```

<br />

## Test

<br />

Perform these tasks to test Midtrans Snap integration with Google Pay™ transactions:

1. Join Google Pay™ test environment:

   1. Visit: [test-card-group](https://groups.google.com/g/googlepay-test-mode-stub-data)
   2. Register as member of Google Pay™ API Test Cards

   <br />

   <Image align="center" src="https://files.readme.io/ee0b340fb1ebb7fd126ce7a97bcdfa8a819efbde0eb353ea0440337b3fa107c7-Screenshot_2024-11-12_at_17.50.52.png" />
2. After joining the test environment, Test cards will automatically appear in your Google Pay™ wallet
   1. These test cards will ONLY appear when you're signed in with your registered Google Account in test environment
   2. Test cards will NOT appear in production environment
3. Choose Google Pay™ at Snap Checkout
4. Sign in using the same Google Account that you registered in test environment
5. Test cards will automatically appear in your Google Pay™ wallet
6. Select test card from wallet
7. Complete payment
8. Check transaction status in Midtrans dashboard

<br />

### Success Cards

Visa: 4811 1111 1111 1114

Mastercard: 5211 1111 1111 1117

<br />

### Decline Cards

Visa: 4911 1111 1111 1113

Mastercard: 5111 1111 1111 1118

<br />

<Image align="center" src="https://files.readme.io/265645f6ebbff206ad9cdd130e6fb19f8b18a80b4b66d65a7d2cb2f610bbd9fc-google-pay-gif.gif" />