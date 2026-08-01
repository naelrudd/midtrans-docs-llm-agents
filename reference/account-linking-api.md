---
updatedAt: 2026-04-20T03:22:50.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Account Linking API

> 📘 GoPay Media Kit
>
> To have a consistent and standardized GoPay branding across platform, we highly recommend merchants to refer to our media kit. Please refer to this page <https://gopay.co.id/media-kit> to access our brand guideline and image bank.

GoPay Tokenization allows merchants to link customer's GoPay account to their platform to be used for subsequent transactions.

## Initiate account linking

To initiate account linking in SNAP-based flow, merchants need to call 3 APIs as follows:

1. Initiate [access token B2B](https://docs.midtrans.com/reference/access-token-api) by calling POST v1.0/access-token/b2b
2. Initiate [get oauth URL request](https://docs.midtrans.com/reference/get-auth-code-api) by calling GET v1.0/get-auth-code
3. Initiate [binding request](https://docs.midtrans.com/reference/binding-api) by calling POST v1.0/registration-account-binding

<Image align="center" src="https://files.readme.io/619874e-SNAP_based_account_linking_flow.png" />

<br />

> 📘 Redirecting to GoPay page during linking
>
> To learn more on GoPay Tokenization redirection, please refer to these API documentations:
>
> * GoPay Tokenization web flow: <https://docs.midtrans.com/reference/faq-redirection-to-gopay-web-page>
>
> * GoPay Tokenization app redirection flow: <https://docs.midtrans.com/reference/faq-redirection-to-gojek-gopay-app>
>
> > ❗️ GoPay may add/change GoPay redirection URL from time to time.
> >
> > To ensure merchant can always support GoPay flow at all times, we highly suggest merchant to not do explicit URL whitelisting.

> 📘 What to do when merchant lost the customer-authorization token?
>
> Peviously merchant cannot initiate another linking of the same phone number as it is already linked in Midtrans/GoPay side. Midtrans will return an error to merchant.
>
> Now, to accommodate the scenario where due to various reasons merchant lost customer-authorization token after completing linking, Midtrans has made an improvement whereby instead of throwing an error (like before), Midtrans will:
>
> 1. Let merchant do relinking of the same phone number
> 2. Midtrans will return GoPay PIN/OTP page as part of the Get Auth Code API
> 3. User will need to redo the user authorization by inputting their PIN/OTP
> 4. Once authorized, Midtrans will send an authCode to merchant
> 5. Merchant will then need to confirm the linking by calling the Binding API and passing the authCode.
> 6. Midtrans will return the same customer-authorization token for that particular user account (phone number).
>
> Please contact your Midtrans sales representative to enable this feature.

> 📘 Receiving notification on account linking and unlinking
>
> Midtrans will also be sending HTTP post notification on account linking and unlinking in BI-SNAP flow. Refer to this diagram below to see how it works!
>
> **Account Linking notification**
>
> <Image align="center" src="https://files.readme.io/fb5d197583b5f7768d3d3aac8d193fbc32aafc6b5eed686a9aa1c0fc42fbabc2-SNAP_based_account_linking_flow-Copy_of_linking.drawio.png" />
>
> **Account Unlinking notification**
>
> <Image align="center" src="https://files.readme.io/8465118d95868c6a1454eba7120f8885487d432a8b9389a83b7d1814dc756d0a-SNAP_based_account_linking_flow-Copy_of_linking.jpg" />
>
> To start accepting notification, merchants will need to integrate to our **Account Linking Notification API**. To learn how to set this up, merchant can refer to this [API documentation](https://docs.midtrans.com/reference/account-linking-unlinking-notification).
>
> As a fallback in case linking notification is not succesfully received by merchant, **merchants are encouraged to always call the Binding Inquiry API to confirm the user's linking status.**

<Callout icon="📘" theme="info">
  **GoPay can now support GoPay account creation on Tokenization Linking webview**

  User can now create GoPay account directly during linking steps on the merchant's app. This feature is now available on Tokenization linking webview new flow. Refer to this [link](https://docs.midtrans.com/reference/faq-redirection-to-gopay-web-page#gopay-has-revamped-its-gopay-tokenization-linking-web-page-on-the-gopay-tokenization-webview-integration-on-august-2025) to learn more!
</Callout>

## Additional APIs

1. To fetch account information such as account status, balance and payment option token, merchant need to initiate[ Binding Inquiry API](https://docs.midtrans.com/reference/binding-inquiry-api) call. **Merchants are encouraged to always call this API before payment to make sure the merchant uses the updated token when creating payment as the payment option token may change from time to time due to various reasons (example: customer upgrade their GoPay account to GoPay Tabungan).**
2. To initiate account unbinding, merchant need to call [Unbinding API](https://docs.midtrans.com/reference/unbind-api)
3. To accept account linking and unlinking  HTTP post notification from Midtrans, refer to this [account linking and unlinking notification API](https://docs.midtrans.com/reference/account-linking-unlinking-notification)

<Callout icon="📘" theme="info">
  As a fallback in case linking notification is not succesfully received by merchant, **merchants are encouraged to always call the Binding Inquiry API to confirm the user's linking status.**
</Callout>