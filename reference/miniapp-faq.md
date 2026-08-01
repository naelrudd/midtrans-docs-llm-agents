---
updatedAt: 2026-03-16T07:34:00.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# FAQ

This guide provides answers to common questions about GoPay MiniApps.

**Find answers to common questions about GoPay MiniApp integration:**

* [General FAQ](https://docs.midtrans.com/reference/miniapp-faq/#general-faq)
* [Seamless Login and Payment FAQ](https://docs.midtrans.com/reference/miniapp-faq/#seamless-login-and-payment-faq)
* [Backend API FAQ](https://docs.midtrans.com/reference/miniapp-faq/#backend-api-faq)
* [V2 Integration FAQ](https://docs.midtrans.com/reference/miniapp-faq/#v2-integration-faq)
* [V1 Integration FAQ](https://docs.midtrans.com/reference/miniapp-faq/#v1-integration-faq)

<br />

***

# General FAQ

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Questions
      </th>

      <th>
        Answer
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        How to start onboarding MiniApp in GoPay
      </td>

      <td>
        * Simply submit the <Anchor label="onboarding form" target="_blank" href="https://gotocompany.sg.larksuite.com/share/base/form/shrlgnBkuAhMEnphzmFxhlDFUtU">onboarding form</Anchor> to get started.
        * For detailed guidance, check the Quick Start documentation:
          * [GoPay Container V2 Quick Start](https://docs.midtrans.com/reference/miniapp-v2/#quick-start)
          * [GoPay Container V1 Quick Start](https://docs.midtrans.com/reference/miniapp-v1/#quick-start)
      </td>
    </tr>

    <tr>
      <td>
        How do I register as a merchant?
      </td>

      <td>
        If you're not yet integrated with GoPay via Midtrans, please register through the [official guide](https://docs.midtrans.com/update/reference/onboarding-v2) .
      </td>
    </tr>

    <tr>
      <td>
        Where do I find my Merchant ID?
      </td>

      <td>
        You can find your Merchant ID on your Midtrans dashboard or by contacting your Account Manager. ([docs](https://docs.midtrans.com/reference/onboarding/#existing-merchant))
      </td>
    </tr>

    <tr>
      <td>
        How long does onboarding take?
      </td>

      <td>
        Onboarding typically takes around 5–7 working days.
      </td>
    </tr>

    <tr>
      <td>
        Where will my mini app be shown in the GoPay app?
      </td>

      <td>
        You can reach out to the Midtrans sales team or GoPay business counterpart for the details
      </td>
    </tr>

    <tr>
      <td>
        Can I onboard multiple mini apps under one Merchant ID?
      </td>

      <td>
        Yes, it's possible to register multiple mini apps under the same Merchant ID. Each mini app will have a unique `GoPay_mini_app_id` and `PoP ID`.
      </td>
    </tr>

    <tr>
      <td>
        Do we have a sandbox or staging environment for testing?
      </td>

      <td>
        We don't at this moment, currently all testing is pointing at GoPay production. What we can do is update the redirectURL to point MiniApp staging or production environments.
      </td>
    </tr>

    <tr>
      <td>
        What is the payment method required for MiniApp
      </td>

      <td>
        We only support Bi-Snap payment method, which acts like a checkout redirection. MiniApp will redirect to GoPay Payment Review page and redirect back to the miniapp after transaction
      </td>
    </tr>

    <tr>
      <td>
        What do I do if the final URL doesn't load?
      </td>

      <td>
        Make sure the domain is whitelisted and matches with the one submitted. Please also check if your Mini App ID is active and all dependencies (client ID, tokens, SDK) are properly integrated.
      </td>
    </tr>

    <tr>
      <td>
        How can I check if my domain is whitelisted?
      </td>

      <td>
        If your mini app isn't loading or returns an unauthorized error, your mini-app domain may not be whitelisted yet by GoPay team. Please reach out to [GoPay-mini-app-integrations@gojek.com](mailto:GoPay-mini-app-integrations@gojek.com)  to ensure it's been reviewed and whitelisted.
      </td>
    </tr>

    <tr>
      <td>
        What should I do if I need to update my domain or URL after onboarding?
      </td>

      <td>
        You can submit the same onboarding form and select "Update existing Miniapp" <Anchor label="onboarding form" target="_blank" href="https://gotocompany.sg.larksuite.com/share/base/form/shrlgnBkuAhMEnphzmFxhlDFUtU">onboarding form</Anchor> "Whitelist Domain"
        Updating domains without whitelisting will result in connection failures.
      </td>
    </tr>

    <tr>
      <td>
        Can I update my Mini App logo, name, or metadata after launch?
      </td>

      <td>
        You can submit the same onboarding form and select "Update existing Miniapp" <Anchor label="onboarding form" target="_blank" href="https://gotocompany.sg.larksuite.com/share/base/form/shrlgnBkuAhMEnphzmFxhlDFUtU">onboarding form</Anchor> "MiniApp Icon"
      </td>
    </tr>

    <tr>
      <td>
        How to integrate with the payment API?
      </td>

      <td>
        Please use the `BI-SNAP Core API Redirection Deeplink`
      </td>
    </tr>

    <tr>
      <td>
        What’s the flow for payments?
      </td>

      <td>
        The user experience will be: FE(MiniApp) → BE → Get redirect URL→ Open payment (GoPay) → Redirect back(MiniApp).
      </td>
    </tr>

    <tr>
      <td>
        What is the incremental work in the payment if I have integrated previously with Midtrans?
      </td>

      <td>
        Merchants should share the PoP ID in the header for non-BI SNAP API or body for BI SNAP API for payment API and should trigger the API through payment SDK
      </td>
    </tr>

    <tr>
      <td>
        Can I use my existing SNAP Checkout Midtrans integration?
      </td>

      <td>
        Currently no, we're planning to support this payment method in miniapp and still in development.
      </td>
    </tr>

    <tr>
      <td>
        Can I use my existing tokenization integration?
      </td>

      <td>
        No, at the moment, tokenized payments are not supported in the mini app payment integration
      </td>
    </tr>

    <tr>
      <td>
        Are recurring payments supported?
      </td>

      <td>
        No, at the moment, recurring payments or subscriptions are not supported in the mini app payment integration.
      </td>
    </tr>

    <tr>
      <td>
        Can I send GoPay Coins/emoney?
      </td>

      <td>
        Yes, via /`v1/mini-apps/rewards`. Currently, only GoPay Coins are available for disbursement.
      </td>
    </tr>

    <tr>
      <td>
        Do I need a wallet balance?
      </td>

      <td>
        Yes, you need to top up the wallet balance before sending GoPay Coins. Please reach out to the Midtrans sales team or GoPay business counterpart to get the VA to top up.
      </td>
    </tr>

    <tr>
      <td>
        Can I send reminders?
      </td>

      <td>
        Yes, you can send a reminder via `/v1/mini-apps/reminder`. But please discuss with your Midtrans sales team or GoPay business counterpart before using it.
      </td>
    </tr>

    <tr>
      <td>
        Who do I contact for help?
      </td>

      <td>
        For any technical support, you can send out an email to [GoPay-mini-app-integrations@gojek.com](mailto:GoPay-mini-app-integrations@gojek.com)  or reach out to your Midtrans sales team or GoPay business counterpart.
      </td>
    </tr>
  </tbody>
</Table>

<br />

***

# Seamless Login and Payment FAQ

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Questions
      </th>

      <th>
        Answer
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Why i'm getting errors when calling getAuthCode?
      </td>

      <td>
        Make sure you're calling getAuthCode correctly and call getAuthCode only after deploying the mini app, not when running locally. The SDK works as a bridge between the mini app and GoPay. If you run locally, there’s no mini app container for the SDK to connect to, so getAuthCode won’t work. You may use the MiniApp Deeplink provided by GoPay to test this.
      </td>
    </tr>

    <tr>
      <td>
        Why i must call getAuthCode
      </td>

      <td>
        The authCode can only be generated when the user opens the Mini App because it serves as real-time proof that the request is from an active, authenticated GoPay session. Since it’s tied to the user’s current login state and expires quickly, it’s not possible or secure to provide it in advance. If we were to provide it in advance, there would be no real validation of the user’s session.
      </td>
    </tr>

    <tr>
      <td>
        How do I get an auth code?
      </td>

      <td>
        To retrieve the auth code, you might call `getAuthCode()` in [SDK](https://docs.midtrans.com/reference/list-of-jssdks-webkit-v4/#get-auth-code).
      </td>
    </tr>

    <tr>
      <td>
        How long is it valid?
      </td>

      <td>
        The auth code is valid for 6 minutes.
      </td>
    </tr>

    <tr>
      <td>
        What i must call getAuthToken?
      </td>

      <td>
        getAuthToken gives you token that will be used to call other GoPay BE APIs and user's account id. Make sure you get the credentials via Email to be used as the Authorization header.
      </td>
    </tr>

    <tr>
      <td>
        What value needs to be inputted into the authorization header in the request?
      </td>

      <td>
        The authorization header should include either `Bearer` or `Basic`, depending on the API and credentials required for the specific request. More details are available in the backend API documentation.
      </td>
    </tr>

    <tr>
      <td>
        Where to find the authorization header when calling getAuthToken
      </td>

      <td>
        You will receive the authCredentials via email.
      </td>
    </tr>

    <tr>
      <td>
        How do I get access token?
      </td>

      <td>
        Please use the auth code in backend API `/v1/mini-apps/authorizations/token`.
      </td>
    </tr>

    <tr>
      <td>
        Can I reuse the token?
      </td>

      <td>
        Yes, the token can be reused. Tokens do not expire and can be safely cached per user.
      </td>
    </tr>

    <tr>
      <td>
        Why am I getting a 401 Unauthorized error?
      </td>

      <td>
        This usually means your auth token is missing, expired, or incorrect. Double-check if you are sending the token in the Authorization header and that it’s valid.
      </td>
    </tr>

    <tr>
      <td>
        How payments work inside GoPay MiniApp?
      </td>

      <td>
        Payments in a GoPay MiniApp work through a one-time checkout flow. Your backend needs to call the BI-SNAP Core API to create a Payment Deeplink, then from the MiniApp you launch that deeplink using the launchPayment SDK. This will take the user to the GoPay payment page to complete the transaction, and once done, the user is automatically redirected back to your MiniApp. To confirm the result, you should always verify the payment status from your backend or via BI-SNAP notification.
      </td>
    </tr>

    <tr>
      <td>
        My payment is stuck in "pending", what should I do?
      </td>

      <td>
        Check the Midtrans dashboard for transaction status. Make sure PoP ID is included in the payment call and that redirect/callback URLs are configured correctly.
      </td>
    </tr>

    <tr>
      <td>
        What is a PoP ID?
      </td>

      <td>
        A Point of Purchase ID (PoP ID) is provided by GoPay for payment tracking. You can request this from your business or partnership contact at GoPay.
      </td>
    </tr>

    <tr>
      <td>
        When will I receive my PoP ID?
      </td>

      <td>
        You will receive your PoP ID after tokenization is completed and the Partnership team generates it. Reach out to your GoPay contact if it hasn’t been shared yet.
      </td>
    </tr>

    <tr>
      <td>
        What is the Payment E2E Flow?
      </td>

      <td>
        **1.[Integrate Payments on Sandbox](https://docs.midtrans.com/reference/core-api-snap-open-api-overview)**

        * Log in to Midtrans and open Sandbox Dashboard
        * Request GoPay team to activate generation key- [Generate Public and Private Key](https://docs.midtrans.com/reference/credential-exchange-copy)
        * Use Sandbox base URL:  
          **merchants.sbx.midtrans.com**
        * Integrate Access token b2b API
        * Integrate payment host to host API
        * Test payment deeplink on web only  
          Note: Sandbox only supports payment testing via web (not MiniApp)**  
          **2.[Migrate to Production](https://docs.midtrans.com/reference/core-api-snap-open-api-overview)**
        * Log in to Midtrans and open Production Dashboard
        * Request GoPay team to activate generation key
        * [Generate Public and Private Key](https://docs.midtrans.com/reference/credential-exchange-copy)
        * Change base URL from:  
          **merchants.sbx.midtrans.com** to **merchants.midtrans.com**
        * Add PoP ID on Payment Host to Host API
        * Use launchPayment SDK to open the payment deeplink
        * Test payment deeplink on MiniApp  
          Note: In Production, payments will redirect to GoPay App and then back to the MiniApp
      </td>
    </tr>

    <tr>
      <td>
        What happens if the user closes the app before completing payment?
      </td>

      <td>
        The transaction will remain in an incomplete state. You can monitor status on the midtrans dashboard.
      </td>
    </tr>

    <tr>
      <td>
        How can I validate that a payment has been completed?
      </td>

      <td>
        Please use the `/v1.0/debit/notify` webhook from the GoPay backend. It confirms payment success and provides reference details.
      </td>
    </tr>

    <tr>
      <td>
        How to configure redirection after payment has been completed?
      </td>

      <td>
        You dont need to configure redirection, it happens automatically after using [Launch Payment](https://docs.midtrans.com/reference/list-of-jssdks-webview-v4/#launch-payment)
      </td>
    </tr>

    <tr>
      <td>
        How do we test the payment process to the GoPay app?
      </td>

      <td>
        Currently, there’s no public GoPay Mini App staging environment. For testing purposes, we typically support merchants by funding a small amount to their account so they can test the flow in the produc
      </td>
    </tr>

    <tr>
      <td>
        How do we test the redirection to the GoPay app?
      </td>

      <td>
        We’ll provide a production deeplink to open the Mini App in the GoPay app. To test redirection, merchants must implement the payment API, which redirects users to GoPay for payment. After a successful payment, it will automatically redirect back to the Mini App, but only if **launch payment**used to open the payment deeplink.
      </td>
    </tr>

    <tr>
      <td>
        What to fill inside channel-id during payments?
      </td>

      <td>
        It's a 5 digit numeric
      </td>
    </tr>
  </tbody>
</Table>

<br />

***

# Backend API FAQ

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Questions
      </th>

      <th>
        Answer
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        What is the difference between pre-launch and post-launch consents?
      </td>

      <td>
        Some features require user consent.

        * Pre-launch consent: Shown as a popup when the mini app is first opened; can be either mandatory or optional.
        * Post-launch consent: Shown as a popup only when the getConsent SDK is called; must always be optional.
      </td>
    </tr>

    <tr>
      <td>
        Is there any limit request per second for the Push Notification API?
      </td>

      <td>
        There is no limit for sending the PN as of now
      </td>
    </tr>

    <tr>
      <td>
        Can I personalize push notifications per user behavior?
      </td>

      <td>
        Yes, as long as you manage targeting and parameters from your backend. The API supports custom fields through `template_parameters`.
      </td>
    </tr>
  </tbody>
</Table>

<br />

***

# V2 Integration FAQ

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Questions
      </th>

      <th>
        Answer
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        What is the overall E2E flow of the onboarding process?
      </td>

      <td>
        **[Merchant side to]**

        * Fill in the [MiniApp Onboarding form](https://gotocompany.sg.larksuite.com/share/base/form/shrlgnBkuAhMEnphzmFxhlDFUtU) and select "Create New MiniApp" then "GoPay Container V2"

        **[GoPay side to]**

        * QA to review and confirm the MiniApp Flow + Figma
        * Sales team to configure PoP ID
        * MiniApp tech support to generate MiniApp using submission form
        * MiniApp tech support to send MiniApp Integration Guide and AuthCredentials via Email

        **[Merchant side to]**

        * Build your MiniApp based on the Integration Guide.
        * Once you've completed development, submit MiniApp Completed using the same
          <Anchor label="onboarding form." target="_blank" href="https://gotocompany.sg.larksuite.com/share/base/form/shrlgnBkuAhMEnphzmFxhlDFUtU">onboarding form.</Anchor>

        **[GoPay side to]**

        * QA team conducts UAT and provides final sign-off
        * After QA sign-off, the rollout team will deploy the MiniApp
        * Merchant will be notified once the MiniApp is live in GoPay
      </td>
    </tr>

    <tr>
      <td>
        Where do i find the Frontend SDK for V2
      </td>

      <td>
        The GoPay Container V2 Frontend SDK is available [Here](https://docs.midtrans.com/update/reference/frontend-v2)
      </td>
    </tr>
  </tbody>
</Table>

<br />

***

# V1 Integration FAQ

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Questions
      </th>

      <th>
        Answer
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        What is the overall E2E flow of the onboarding process?
      </td>

      <td>
        **[Merchant side to]**

        * [Onboard to GoPay MiniApp Portal](https://docs.midtrans.com/reference/project-setup-v1/#1-access-to-gopay-mini-app-portal)

        **[GoPay side to]**

        * Invite Merchant to GoPay MiniApp Portal

        **[Merchant side to]**

        * Login [GoPay MiniApp Portal](https://miniapp.midtrans.com) and create workspace

        **[GoPay side to]**

        * Approve workspace

        **[Merchant side to]**

        * Refresh page/Relogin Portal
        * [Create New MiniApp Project ](https://docs.midtrans.com/reference/project-setup-v1/#2-create-new-miniapp-project) and take note your Miniapp ID
        * Fill in the [MiniApp Onboarding form](https://gotocompany.sg.larksuite.com/share/base/form/shrlgnBkuAhMEnphzmFxhlDFUtU) and select "Create New MiniApp" then "GoPay Container V1" and input Miniapp ID

        **[GoPay side to]**

        * QA to review and confirm the MiniApp Flow + Figma
        * Sales team to configure PoP ID
        * MiniApp tech support to generate MiniApp using submission form
        * MiniApp tech support to send Mini App Credentials and Integration Document via Email

        **[Merchant side to]**

        * Build your MiniApp based on the Integration Guide.
          1. [Project Initial Setup](https://docs.midtrans.com/reference/project-setup-v1/#3-project-initial-setup)
          2. [Publish your MiniApp](https://docs.midtrans.com/reference/publish-miniapp-v1)
          3. [How to Test MiniApp](https://docs.midtrans.com/reference/testing-miniapp-v1)

        * Once you've completed development,
          [Apply for Release](https://docs.midtrans.com/reference/release-miniapp-v1/#2-apply-for-release-your-miniapp)

        * Submit MiniApp Completed using the same [onboarding form](https://gotocompany.sg.larksuite.com/share/base/form/shrlgnBkuAhMEnphzmFxhlDFUtU)
          1. Select "New Release" -> First-time release, not yet rolled out to users

          2. Select "Enhancement" -> MiniApp is already live and contains updates pending release

        **[GoPay side to]**

        * QA team conducts UAT and provides final sign-off
        * After QA sign-off, Tech Support to Approve the Release

        **[Merchant side to]**

        * [Officially release the MiniApp](https://docs.midtrans.com/reference/release-miniapp-v1/#3-officially-release-your-miniapp)

        **[GoPay side to]**

        * If you've selected "New Release" during the form submission, after QA sign-off, the rollout team will deploy the MiniApp
        * Merchant will be notified once the MiniApp is live in GoPay
      </td>
    </tr>

    <tr>
      <td>
        Where do i find the Frontend SDK for V1
      </td>

      <td>
        The GoPay Container V1 Frontend SDK is available [Here](https://docs.midtrans.com/update/reference/frontend-v1)
      </td>
    </tr>
  </tbody>
</Table>

<br />

<br />

<br />