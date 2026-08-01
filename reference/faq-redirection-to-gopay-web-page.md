---
updatedAt: 2026-04-20T03:10:42.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# FAQ: Redirection to GoPay web page (GoPay Tokenization webview)

On GoPay Tokenization webview flow, users will be redirected to GoPay web page to confirm their linking and payments.

# Linking

When merchant initiate linking by calling the [Create Pay Account API](https://docs.midtrans.com/reference/create-pay-account) (Legacy flow) or [Get Auth Code & Registration Account Binding API](https://docs.midtrans.com/reference/account-linking-api) (BI SNAP flow), Midtrans will return GoPay web page URL. Merchant is expected to open the page so that user can input the OTP and GoPay PIN. After completion, user will be redirected back to merchant's page.

## GoPay has revamped its GoPay Tokenization linking web page on the GoPay Tokenization webview integration on August 2025\*\*

**What is new?**

GoPay Tokenization linking web page will have new a new look and UI design.

**Before**

<Image align="center" width="300px" src="https://files.readme.io/a0b0be853010b035906f88a758e7d370247a51c072dd962d70604ef33fdba23d-Screenshot_2025-05-16_at_13.48.06.png" />

<Image align="center" width="300px" src="https://files.readme.io/f5b4a337ca0e950a357924c275fb22afecc16f3e6f21545608089b66ac955974-Screenshot_2025-05-16_at_13.48.16.png" />

**After**

<Image align="center" width="300px" src="https://files.readme.io/1ddf18fb5c17efde2a35cc9e92d04820ca02d99df038710b66c8bff8599a134c-Screenshot_2025-05-16_at_11.19.39.png" />

<Image align="center" width="300px" src="https://files.readme.io/134e7532e254ebda00490cb1666127fab932b7852dc53a7d9b857d55aff11f8c-Screenshot_2025-05-16_at_11.20.01.png" />

<Image align="center" width="300px" src="https://files.readme.io/4e8b47cd68afc760f6630e8c26339626781af4432fc8fe29997838276128f0ce-Screenshot_2025-05-16_at_14.16.59.png" />

<br />Please note that there will be a change of behavior of the GoPay Tokenization linking web page. The changes will be listed below.

**What are the changes in the behavior?**

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Change
      </th>

      <th>
        Description
      </th>

      <th>
        What merchants need to do
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Additional GoPay web page domain
      </td>

      <td>
        We will have 2 domains for the GoPay web pages.

        **Merchant will need to whitelist both domains**

        to support the new linking flow.

        The full domain list for linking flow is as listed below:
      </td>

      <td>
        **To ensure merchant is able to support GoPay flow on all times, we highly suggest merchant to not do whitelisting as GoPay might add/change the URL from time to time.** <br /><br />If merchants apply whitelisting logic, merchant should whitelist both of the domains.
      </td>
    </tr>

    <tr>
      <td>

      </td>

      <td>
        Production:

        1.

        [https://merchants-gws-app.gopayapi.com](https://merchants-gws-app.gopayapi.com)

        (this domain is used for the linking consent page, OTP page, and success page)

        2.

        [https://pin-web-client.gopayapi.com](https://pin-web-client.gopayapi.com)

        (this domain is used for the PIN page)
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>

      </td>

      <td>
        Sandbox:

        1.

        [https://sandbox-gws-app.gopayapi.com](https://sandbox-gws-app.gopayapi.com)

        (this domain is used for the linking consent page, OTP page, and success page)

        2.

        [https://pin-web-client-sandbox.gopayapi.com](https://pin-web-client-sandbox.gopayapi.com)

        (this domain is used for the PIN page)
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        Removal of inner iframe
      </td>

      <td>
        In the old linking flow, the linking form was rendered within an inner iframe on the GoPay Web Page.

        As part of our ongoing efforts to enhance the user experience and improve the performance of our web pages, the inner iframe will be removed, and the form will now be rendered directly on the main page.
      </td>

      <td>
        If merchant's integration includes custom handling that relies on the presence of the inner iframe - such as reading status or errorCode after redirection from within GoPay’s iframe - merchants may need to update their implementation to support this revised structure.
      </td>
    </tr>
  </tbody>
</Table>

<br />**GoPay Tokenization linking web page will be gradually rolled out to all GoPay Tokenization webview merchants from August 2025**. Newly onboarded merchant will only be onboarded to new flow.

Please make sure that your integration have supported these changes to prevent issue on the linking flow.

> 👍 New linking flow is now available in Sandbox!
>
> Merchant can try the new linking flow via Midtrans Sandbox. To understand more about testing GoPay Tokenization in Sandbox please refer to this [API documentation](https://docs.midtrans.com/reference/testing-gopay-tokenization-on-sandbox-environment).

> 📘 GoPay account creation - new feature available on the new linking flow!
>
> User can now create a GoPay account during linking steps right from the merchant's app.
>
> #### Account creation steps
>
> 1. User initiate GoPay linking on merchant's app
> 2. When user's phone number is not registered on GoPay, user will be asked to create a GoPay account & linking
> 3. User will be asked to input their name for the GoPay account creation
> 4. User then needs to confirm their account creation by inputting OTP sent by GoPay and set up GoPay PIN.
> 5. Once done, user's GoPay account will be created and is directly linked to the merchant.
>
> **This feature is now available on GoPay Tokenization webview revamped (new) flow**. Make sure you have migrated to the linking new flow to be able to enjoy this feature. You can reach out to your Midtrans representative to start the migration process.

<br />

# Payments

After completing linking, merchant can initiate payments by calling the [Charge API](https://docs.midtrans.com/reference/gopay-tokenization) (Legacy flow), [Direct Debit Payment API](https://docs.midtrans.com/reference/direct-debit-api-gopay-tokenization) (GoPay Tokenization non Pre Auth - BI SNAP), or [Auth Payment API](https://docs.midtrans.com/reference/auth-payment-api-gopay-tokenization) (GoPay Tokenization Pre Auth - BI SNAP). If transaction requires user to do PIN authorization, Midtrans will return GoPay web page URL. Merchant is expected to open the web page so user can input their GoPay PIN and complete payment.

<Image align="center" width="300px" src="https://files.readme.io/16748e60819ba8af03959d53389f655d2447c9f3f47f6bed3e4d8f4dbc86a34c-Screenshot_2025-05-16_at_15.06.37.png" />

<Image align="center" width="300px" src="https://files.readme.io/05fd4904da12e31982d6dab846846bd081c87a03855d378c8e2b013460fbda83-Screenshot_2025-05-16_at_15.06.43.png" />

After payment completion, user will be redirected back to merchant's page

For more information on GoPay redirection, please read our [technical FAQ page](https://docs.midtrans.com/docs/technical-faq?id=ios-webview-specific#failure-to-redirect-the-customer-to-gojek-gopay-shopee-pay-and-other-e-wallet-payment-provider-app-what-should-i-do) or directly contact your Midtrans Sales representative so we can assist you further.