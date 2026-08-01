---
updatedAt: 2026-02-03T07:36:51.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# FAQ: Redirection to Gojek / GoPay app

> 📘 GoPay Deeplink & Tokenization redirection to GoPay app only
>
> With the launch of GoPay standalone app, **starting from 1 April 2026**, user will be redirected to GoPay app only to complete their payment (gradual rollout).
>
> **How will this impact the user experience?**
>
> 1. By default user will be redirected to GoPay app if the app is installed.
> 2. If GoPay app is not installed (even if user has Gojek app), user will see GoPay webpage and asked to download GoPay app from the play store or app store.
> 3. After downloading the app, user can continue to complete linking or payment.
>
> **How can merchant support this flow?**
>
> Just like the previous Gojek and GoPay app redirection flow, merchant just need to ensure that they have done these 3 items below:
>
> <Table align={["left"]}>
>   <thead>
>     <tr>
>       <th>
>         What merchants need to do
>       </th>
>     </tr>
>   </thead>
>
>   <tbody>
>     <tr>
>       <td>
>         1. Merchant should ensure that they can **support redirection URL in universal link format** to be able to be redirected to GoPay / Gojek app
>       </td>
>     </tr>
>
>     <tr>
>       <td>
>         2. We recommends merchant to always open our redirection URL outside of merhant's in-app webview (or directly in the user's native browser). In case merchants open the URL inside a werbview and merchant have whilisting logic, **merchants should make sure to whitelist** `gopay.co.id/*`, `*.gopay.co.id/*`, `gojek.link/*`. Please ensure that the existing URLs are also kept whitelisted on merchants' side.
>       </td>
>     </tr>
>
>     <tr>
>       <td>
>         3. In case merchants have webview implementation, merchant should ensure that the webview redirection is **not blocked by Android/iOS** platform. Fore more details on how to do this please read this FAQ page: [Android](https://docs.midtrans.com/docs/technical-faq#android)  | [iOS](https://docs.midtrans.com/docs/technical-faq#ios-webview-specific)
>       </td>
>     </tr>
>   </tbody>
> </Table>

<br />

On GoPay deeplink, GoPay Tokenization linking, and some GoPay Tokenization transactions (the ones that require PIN challenge), users will be redirected to Gojek or GoPay app to input their GoPay PIN. Previously (before August 2023), users will only be redirected to Gojek app. However, GoPay has launched GoPay standalone app since August 2023. With the launch of GoPay standalone app, there are few changes on the payment experience as per detailed below:

| User flow                    | Before August 2023               | August 2023 - November 2025                      | November 2025 - 31 March 2026                             | 1 April 2026 onwards (Gradual rollout) |
| :--------------------------- | :------------------------------- | :----------------------------------------------- | :-------------------------------------------------------- | :------------------------------------- |
| User has Gojek and GoPay app | Redirected to Gojek app          | Redirected to GoPay app                          | Redirected to GoPay app                                   | Redirected to GoPay app                |
| User has GoPay app only      | Redirected to download Gojek app | Redirected to GoPay app                          | Redirected to GoPay app                                   | Redirected to GoPay app                |
| User has Gojek app only      | Redirected to Gojek app          | Redirected to Gojek app                          | Redirected to download GoPay app or continue in Gojek app | Redirected to download GoPay app       |
| User doesn't have any app    | Redirected to download Gojek app | Redirected to download either Gojek or GoPay app | Redirected to download either Gojek or GoPay app          | Redirected to download GoPay app       |

<br />

**How will this impact the user experience?**

Previously, by default users will be redirected to Gojek app to complete linking and payments. Now with the launch of GoPay app, users who have GoPay App will be automatically redirected to GoPay app.

### August 2023 - November 2025

<Image align="center" border={false} width="500px" src="https://files.readme.io/f52df75-GoPay_app_redirection_flow-Copy_of_Copy_of_Copy_of_Page-1.png" />

1. By default, users will be redirected to GoPay app if the app is installed
2. If GoPay app is not installed, users will be redirected to Gojek app if Gojek app is installed on user's phone
3. If Gojek app is not installed, user will see the Gojek webpage and user can choose which app (Gojek/GoPay) they want to use to continue the linking/payment

   <Image align="center" border={false} width="200px" src="https://files.readme.io/d77120e-IMG_9693.jpg" />
4. User need to click the CTA button to be redirected to Gojek/GoPay app play store / app store
5. Once user downloaded Gojek/GoPay app, user can continue linking/payment

<br />

### November 2025 - 31 March 2026

<Image align="center" border={false} width="500px" src="https://files.readme.io/bd225e3053adc604884ff8793739852ad69a6f271d86745a66a3eb7c52b549db-image.png" />

<br />

1. By default, users will be redirected to GoPay app if the app is installed
2. If GoPay app is not installed, user will see the Gojek webpage and user can choose which app (Gojek/GoPay) they want to use to continue the linking/payment

   <Image align="center" border={false} width="200px" src="https://files.readme.io/0ea10f1765dcba33bad23123ce9a0f4d70d28b1e7f0719dab8b2d4d2ce2d223a-Screenshot_2025-11-21_at_10.27.25_AM.png" />

   1. If they have Gojek app and choose to continue in Gojek app, then user will be redirection to Gojek app to continue linking/payment
   2. If user choose to continue in GoPay app, user will be redirected to download GoPay app. Once user downloaded GoPay app, user can continue linking/payment.

   <br />

<Callout icon="📘" theme="info">
  **Starting 1 February 2026, all users will be redirected to complete payment on the GoPay app only.** Refer to the top section of this page (gradual rollout).
</Callout>

### 1 April 2026 onwards (Gradual rollout)

<Image align="center" border={false} width="500px" src="https://files.readme.io/4d4cfc3c6f5787c13f78d588f0e3127338fc81be664358b05a6684e818551e15-image.png" />

**How can merchants support this flow?**

Since August 2023, we are returning a new link for redirection as follows:

| Flow                               | Redirection link                                                 | Remarks |
| :--------------------------------- | :--------------------------------------------------------------- | :------ |
| GoPay deeplink (one time payment)  | gojek://gopay/merchanttransfer?tref=xyz>                         | Old     |
|                                    | <https://gojek.link/gopay/merchanttransfer?tref=xyz>             | Old     |
|                                    | <https://gopay.co.id/app/merchanttransfer?tref=xyz>              | New     |
| GoPay Tokenization linking via app | <https://gojek.link/gopay/tokenization/linking?reference_id=xyz> | Old     |
|                                    | <https://gopay.co.id/app/tokenization/linking?reference_id=xyz>  | New     |
| GoPay Tokenization payment via app | <https://gojek.link/gopay/tokenization/payment?reference_id=xyz> | Old     |
|                                    | <https://gopay.co.id/app/tokenization/payment?reference_id=xyz>  | New     |
| All Flow                           | <https://gopayapp.page.link>                                     | New     |
|                                    | <https://gojek.page.link>                                        | New     |
|                                    | <https://gojek.link/>                                            | New     |
|                                    | <https://app.gopay.co.id/>                                       | New     |

**To support the new redirection to GoPay App, merchants need to do the following items:**

<Table align={["left"]}>
  <thead>
    <tr>
      <th>
        What merchants need to do
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        1. Merchant should ensure that they can **support redirection URL in universal link format** to be able to be redirected to GoPay / Gojek app
      </td>
    </tr>

    <tr>
      <td>
        2. We recommends merchant to always open our redirection URL outside of merhant's in-app webview (or directly in the user's native browser). In case merchants open the URL inside a werbview and merchant have whilisting logic, **merchants should make sure to whitelist** `gopay.co.id/*`, `*.gopay.co.id/*`, `gojek.link/*`. Please ensure that the existing URLs are also kept whitelisted on merchants' side.
      </td>
    </tr>

    <tr>
      <td>
        3. In case merchants have webview implementation, merchant should ensure that the webview redirection is **not blocked by Android/iOS** platform. Fore more details on how to do this please read this FAQ page: [Android](https://docs.midtrans.com/docs/technical-faq#android) | [iOS](https://docs.midtrans.com/docs/technical-faq#ios-webview-specific)
      </td>
    </tr>
  </tbody>
</Table>

For more information on GoPay redirection, please read our [technical FAQ page](https://docs.midtrans.com/docs/technical-faq?id=ios-webview-specific#failure-to-redirect-the-customer-to-gojek-gopay-shopee-pay-and-other-e-wallet-payment-provider-app-what-should-i-do) or directly contact your Midtrans Sales representative so we can assist you further.