---
updatedAt: 2026-03-16T07:32:06.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# UI/UX Guidelines

This guide outlines the mandatory UI/UX standards for Mini Apps to ensure a seamless, secure, and consistent user experience within the GoPay App environment.

## UI Guidelines

Please refer to the following UI/UX guideline resources in \[[Mac](https://gotocompany.sg.larksuite.com/drive/folder/P4c3f5iZmlKAjhdErGRlOHgXgSh?from=from_copylink)|[Windows](https://gotocompany.sg.larksuite.com/drive/folder/P4c3f5iZmlKAjhdErGRlOHgXgSh?from=from_copylink)]

1. Typography & Color Tokens
2. Font Files
3. Figma Components

## UX Guidelines

1. **User Login & Personal Data Restrictions**
   1. Mini Apps must not require users to log in (i.e., request phone numbers, emails, or any personal identity such as KTP, passport, etc.) with authentication methods like OTP, PIN, or password for accessing the overall experience.
   2. If a Mini App requires a user’s phone number, email, or personal identity, it is only permitted for booking or payment-related purposes.
   3. Mini App partners must consult and share the user experience flow with the GoPay team before implementation. GoPay reserves the right to approve or reject the request.\ <br />
2. **Credentials, PII and Device Permission**
   1. Mini Apps should provide a strong reason why Mini Apps required the PII and device information
   2. If the PII purposes for seamless login for the GoPay app users to cut the registration processes, hence;
      1. When the PII is provided under user consent, please check and ensure the capability to map to Mini App account is there
      2. When the PII is provided under user consent, and if the PII information , i.e. mobile number is not exist under the Mini App account - please generate the Mini Apps account with those particular provided mobile number for seamless login
3. **Restrictions on External Redirection**
   1. Mini Apps must not redirect users to external websites or apps outside the GoPay App environment.
   2. If the Mini App contains advertisements, the user should only be able to view the ad without being redirected to an external app or website. Any redirection outside the GoPay App is strictly prohibited as it creates a broken journey.\ <br />
4. **Prohibited Content & Activities**\
   Mini Apps must not include any form of content, promotions, or materials related to:
   1. Tobacco, cigarettes, vaping, or alcohol-related content.
   2. Sexually explicit content, adult entertainment, or escort services.
   3. Gambling, betting, lottery, or any financial speculation that is illegal or unregulated.
   4. Crime, violence, drugs, or any activities prohibited by Indonesian law.
   5. Any activities targeted exclusively for users aged 18 and above without prior approval from GoPay.\ <br />
5. **Security & Performance Compliance**
   1. Mini Apps must comply with GoPay's security and performance standards, ensuring that the app runs smoothly within the GoPay environment without impacting user experience.
   2. Any third-party SDKs, trackers, or scripts integrated into the Mini App must be disclosed to GoPay for approval.
   3. Mini Apps should not request excessive permissions (e.g., camera, microphone, location) unless strictly required for the core functionality. Any request should be informed, approved, and use GoPay consent service.\ <br />
6. **Payments & Transactions**
   1. All payments within the Mini App must be processed exclusively through GoPay as the primary payment method.
   2. Mini Apps must not implement direct bank transfers, cash payments, or external third-party payment processors without GoPay’s explicit approval.
   3. Mini Apps should use GoPay Payment Redirection Core API that compliant with SNAP BI.
   4. Partners offering digital goods or services, GoPay is aligning with platform policies regarding in-app payments. You may still proceed with in-app payment integration using GoPay. We'll notify you of any payment related adjustments if required.\ <br />
7. **Compliance & Enforcement**
   1. GoPay reserves the right to review, modify, or remove any Mini App that violates these guidelines.
   2. Non-compliance with these guidelines may result in suspension or termination of the Mini App within the GoPay ecosystem.
   3. GoPay may update these guidelines periodically, and partners are required to comply with the latest version.\ <br />
8. **Others**
   1. Mini Apps should at least provide Bahasa Indonesia and set it as default language