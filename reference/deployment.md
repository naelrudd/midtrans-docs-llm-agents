---
updatedAt: 2026-04-28T11:57:52.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Deployment Notice

## March 16, 2026

### Card Refund Authorization

**Overview** Major card schemes, such as Visa and Mastercard, have globally mandated Refund Authorization for card transactions. Under this requirement, refund requests are processed through a real-time authorization flow with the issuing bank, similar to standard charge requests. Please note that this is an industry-wide mandate from the card networks and issuing banks, not a change to Midtrans internal logic.

**Key Changes**

* **Authorization Check**: Every refund request will now be subject to an authorization process by the card schemes.
* **Decline Possibility**: As with charge transactions, a refund request may be declined by the issuing bank.
* **Integration Impact**: Merchants should ensure their systems are prepared to handle "denied" statuses for refund API calls.

Reference on Refund Authorization as mandated by major networks:

* <Anchor label="Visa: Improve the Customer Return Process - New Purchase Return Authorization Message" target="_blank" href="https://usa.visa.com/content/dam/VCOM/global/support-legal/documents/new-purchase-return-vbs-10-apr-17.pdf">Visa: Improve the Customer Return Process - New Purchase Return Authorization Message</Anchor>
* <Anchor label="Mastercard (2.13 Refund Transactions and Corrections)" target="_blank" href="https://www.mastercard.us/content/dam/public/mastercardcom/na/global-site/documents/transaction-processing-rules.pdf">Mastercard (2.13 Refund Transactions and Corrections)</Anchor>

If you have any further questions regarding this behavior, please contact the Midtrans Support Team.

***

## September 24, 2025

### Improvement in Snap Checkout Credit Card Tokenization

We are internally improving Snap Checkout credit card tokenization process.\
Previously, tokenization requests were made using GET method. With this update, tokenization requests will now use POST method, ensuring a more standardized and consistent process.

**Impact on Merchants**

* No changes required on the merchant side.
* Existing Snap integrations will continue to work as usual.
* The update will be applied automatically and seamlessly.

**Scope of Impact**

* Applies only to payment type: credit\_card.
* No impact on other payment types.
* Currently available for Snap integration.
* Availability for Core API integration will be published soon (TBD).

**Timeline**

* Sandbox: September 24, 2025
* Production: Targeted for early-mid October 2025

<br />

**FAQ**\
Q: Do merchants need to update their integration?\
A: No, merchants don't need to make any changes. The improvement is backward compatible.

Q: Will this impact existing tokenization or payment flows?\
A: No, all existing flows will continue to work as usual.

Q: When will this be available in production environment?\
A: We plan to enable it in production environment in early-mid October 2025 after monitoring on Sandbox.

Notes:\
This enhancement is part of our ongoing efforts to improve consistency and reliability in tokenization flows.\
We will closely monitor the rollout to ensure a smooth transition.

***

## March 27, 2025

### 3DS Redirect Domain Change – Please Update Your Allowlist

As part of ongoing enhancements to ensure secure and seamless transactions. We have upcoming improvements to our 3DS (3D Secure) payment flow. **We will gradually migrate the 3DS redirect domain** from <https://api.midtrans.com> to <https://card.midtrans.com.>\
**Key Details:**

* New 3DS  Domain: <https://card.midtrans.com>
* Previous 3DS Redirect Domain: <https://api.midtrans.com>
* Implementation Timeline:
  * **Start Date: April 24, 2025 (Gradual rollout).**
  * **Completion Target: End of June 2025 (Complete rollout).**\
    **Action Required:**\
    If your system employs domain allowlisting, ensure that the new domain (<https://card.midtrans.com>) is added to your allowlist before April 24, 2025 to prevent disruptions. Failure to update the allowlist (if applicable) may result in transaction failures where customers cannot complete 3DS authentication and leading to declined payments.

Specifically, check all parts of your system that interact with 3DS Redirect URL, including:

* Web integrations: When performing a 3DS URL Redirect or embedding the URL in an iframe.
* Mobile apps: When handling the 3DS Webview.

***

**What’s Changing?**\
The API paths will **remain unchanged**, only 3DS Redirect domain will be updated. Below are the revised URLs for reference:\
This content is only supported in a Lark Docs\
3DS Flow Overview:

1. Redirect URL: Returned in the charge response, which (on Frontend side) you will have to redirect your customer to open 3DS URL, for them to complete 3DS process.
2. Callback URL: Automatically triggered after the Redirect URL is opened (to gather browser information data).
3. Result Completion URL: Automatically triggered or displayed after the customer completes the 3DS authentication, whether by submitting an OTP or allowing the transaction (including frictionless flows and in-app 3DS authentication).\
   For full details on the 3DS flow, refer to our documentation.

***

**Frequently Asked Questions (FAQ)**\
**Q1: When will this change take effect?**\
A: The migration will begin on April 24, 2025 and be fully completed by End of June 2025. We will notify you of any timeline adjustments.

**Q2: Do merchants need to change their integration to use the new domain?**\
A: No, merchants should continue using the existing domain for Charge, Create Token, etc. This change only affects 3DS URL (which is used to redirect customers to the 3DS web page, on the Frontend side). No action is required unless you use domain allowlisting. If so, add <https://card.midtrans.com> to your allowlist.

**Q3: Will this affect existing transactions?**\
A: No. The API paths remain identical, and the change will not disrupt current implementations.

**Q4: Is there a deadline to update our allowlist?**\
A: Yes. Ensure the new domain is allowed before April 24, 2025 to avoid service interruptions.

**Q5: What happens if we do not add the new domain to our allowlist?**\
A: If the new domain (<https://card.midtrans.com>) is not added to your allowlist, customers may experience failures when attempting to authenticate their transactions via 3DS. This can lead to increased transaction declines and potential revenue loss.

**Q6: Why is the Result Completion Page URL unchanged?**\
A: Only 3DS Redirect and Callback URLs are migrating. The Result Completion URL will remain on api.midtrans.com. However, in the future, we will also migrate this to <https://card.midtrans.com> for 3DS URL consistency. This change will be announced separately and will take place after the migration of the 3DS Redirect and Callback URLs.

***

**📢 Action Required**: If your system enforces domain allowlisting, please ensure that <https://card.midtrans.com> is added before April 24, 2025 to prevent disruptions.

## February 1, 2024

### Card Channel Response Code Improvement

In order to enhance our services, we are standardizing the API Responses Code for Midtrans payment methods with cards, which will be implemented gradually on March 1, 2024. We urge you to promptly check the latest API, now available in Sandbox mode, and make necessary configuration changes according to your needs to ensure smooth transaction processes. Please review the changes in the API response codes provided.

For more details, please refer to [Card Channel Response Code Improvement](https://docs.midtrans.com/reference/channel-response-code#card-channel-response-code-improvement)

<br />

***

## December 14, 2023

### Kredivo callback URL format update

Starting from January 8th, 2024, there will be an update on callback URL returned by Midtrans for Kredivo payment channel. Callback URL is the URL that Midtrans will return to merchant when user is redirected back to merchant's page after transaction completion in Kredivo page.

<Callout icon="📘" theme="info">
  **Staring in January 8th, 2024 we will start appending additional information on Kredivo callback URL.** We will gradually rollout the update, please make sure that your system can handle both the old and new format within the transition period.
</Callout>

The update mentioned above is as follows:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>

      </th>

      <th>

      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Before
      </td>

      <td>
        Callback URL from Kredivo page will only be the merchant callback URL without being append by any parameter.

        Sample URL:  
        [https://www.merchanturl.com](https://www.merchanturl.com)
      </td>
    </tr>

    <tr>
      <td>
        After
      </td>

      <td>
        Callback URL from Kredivo page will be the merchant callback URL and  appended by additional parameter:

        1. Merchant order ID
        2. Transaction status
        3. Status codeSample URL:  
           [https://www.merchanturl.com?order_id=120231129030954WzDmzp1roM&transaction_status=expire&status_code=407](https://www.merchanturl.com?order_id=120231129030954WzDmzp1roM\&transaction_status=expire\&status_code=407)
      </td>
    </tr>
  </tbody>
</Table>

For more details please refer to this API documentation <https://docs.midtrans.com/reference/kredivo-1>.

<br />

***

### GoPay static QRIS can only be refunded by passing Midtrans transaction ID

<Callout icon="🚧" theme="warn">
  Starting from January 14th, 2024, **refund on GoPay static QRIS transaction can only be initiated by passing Midtrans transaction ID.**

  Failure to do so may resulted in refund failures (we will return Midtrans status code 404) . We will gradually rollout the update, please make sure that your system can handle both the old and new format within the transition period.
</Callout>

The update mentioned above is as follows:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>

      </th>

      <th>

      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Before
      </td>

      <td>
        Merchant can initiate refund on GoPay static QRIS transaction by calling Midtrans refund API and passing either the merchant order ID or the Midtrans transaction ID.

        Example:  
        A static QRIS transaction has the order ID of 12345  and the transaction ID of ABCDE.

        Merchant can initiate refund by calling Midtrans refund API as follow:

        * BASE_URL/v2/12345/refund (using the merchant order ID), OR
        * BASE_URL/v2/ABCDE/refund (using the transaction ID)
      </td>
    </tr>

    <tr>
      <td>
        After
      </td>

      <td>
        Merchant can initiate refund on GoPay static QRIS transaction by calling Midtrans refund API and passing ONLY the Midtrans transaction ID.

        Example:  
        A static QRIS transaction has the order ID of 12345  and the transaction ID of ABCDE.

        Merchant can initiate refund by calling Midtrans refund API as follow:

        * BASE_URL/v2/ABCDE/refund (using the transaction ID)
      </td>
    </tr>
  </tbody>
</Table>

What is Midtrans transaction ID?

Midtrans transaction ID is a unique ID generated by Midtrans. This ID can be found as part of Midtrans charge API response as well as Midtrans HTTP post notification, also in Midtrans merchant portal as follows:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>

      </th>

      <th>
        Sample
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Charge API response
      </td>

      <td>
        \{  
        "status_code":"201",  
        "status_message":"Kredivo transaction is created",

        * * "transaction_id":"c1b4e32c-fd32-4ce3-98ed-130a6faf0fef"**,  
            …  
            }
      </td>
    </tr>

    <tr>
      <td>
        HTTP Post Notification
      </td>

      <td>
        \{  
        "transaction_time": "2023-12-07 14:51:27",  
        "transaction_status": "pending",

        * * "transaction_id": "c1b4e32c-fd32-4ce3-98ed-130a6faf0fef"**,  
            …  
            }
      </td>
    </tr>

    <tr>
      <td>
        Merchant portal
      </td>

      <td>
        ![](https://files.readme.io/6bb8758-Screen_Shot_2023-12-13_at_17.27.07.png)
      </td>
    </tr>
  </tbody>
</Table>

For more details please refer to this API documentation <https://docs.midtrans.com/reference/refund-transaction>.

<br />

***

### Midtrans status code update for GoPay blocked user scenario on GoPay Tokenization

<Callout icon="📘" theme="info">
  Starting January 14th, 2024, **there will be an update on Midtrans status code for GoPay blocked user scenario on  GoPay Tokenization linking and payment**, from the previous status code 402 to status code 410.

  We will gradually rollout the update, please make sure that your system can handle both the old and new format within the transition period.
</Callout>

The update mentioned above is as follows:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>

      </th>

      <th>

      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Before
      </td>

      <td>
        When merchant initiate a [linking](https://docs.midtrans.com/reference/get-pay-account) and [payment](https://docs.midtrans.com/reference/gopay-tokenization) on GoPay Tokenization and turns out the request failed because the user has been blocked by GoPay, we will return status_code: 402.

        Sample API response:

        \{

        * *"status_code":"402"**,  
          "status_message":"GoPay user is blocked",  
          "id":"363a8d7f-92d5-4232-9c2d-7e6de2dafa33"  
          }
      </td>
    </tr>

    <tr>
      <td>
        After
      </td>

      <td>
        When merchant initiate a [linking](https://docs.midtrans.com/reference/get-pay-account) and [payment](https://docs.midtrans.com/reference/gopay-tokenization)on GoPay Tokenization and turns out the request failed because the user has been blocked by GoPay, we will return status_code: 410.

        Sample API response:

        \{

        * *"status_code":"410"**,  
          "status_message":"GoPay user is blocked",  
          "id":"d038d0ab-6fe1-4915-b7e2-d90bb931001c"  
          }
      </td>
    </tr>
  </tbody>
</Table>

For more details please refer to this API documentation <https://docs.midtrans.com/reference/code-4xx>.

<br />

***

### Update on order id format on B2B virtual account subsequent transactions

<Callout icon="📘" theme="info">
  Starting January 14th, 2024, **we will update the format of B2B virtual account subsequent transactions** format to become a random asymmetrical value.

  We will gradually rollout the update, please make sure than your system can handle both the old and new format within the transition period.
</Callout>

The update mentioned above is as follows:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>

      </th>

      <th>

      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Before
      </td>

      <td>
        If merchant is using B2B (multi use) VA transaction, their VA can be paid multiple times. And in the subsequent transaction, the order ID will be generated by Midtrans on behalf of the merchant.

        Before, the format for these subsequent order IDs as follows:

        * Format: \<parent_order_id>-\<transaction_timestamp> <br /> - Type: Alphanumeric <br /> - Length: Upto 255Sample:  
          Given merchant initiate a multi use B2B VA with VA number 12345 and order id ABCD

        * First transaction has order id: ABCD

        * Second transaction has order id: ABCD-081223034114438
      </td>
    </tr>

    <tr>
      <td>
        After
      </td>

      <td>
        If merchant is using B2B (multi use) VA transaction, their VA can be paid multiple times. And in the subsequent transaction, the order ID will be generated by Midtrans on behalf of the merchant.

        After the change applied, the format for these subsequent order ID will be a random alphanumeric value as follow: <br /> - Format: Random <br /> - Type: Alphanumeric <br /> - Length: Upto 255

        Sample:  
        Given merchant initiate a multi use B2B VA with VA number 12345 and order id ABCD

        * First transaction has order id: ABCD
        * Second transaction has order id: A12345685989ahhdfdjID
      </td>
    </tr>
  </tbody>
</Table>

<br />

## September 12, 2023

Related to internal optimization and improvement, we would like to announce changes related to the full PAN card payment  [Card Feature - Full PAN](https://docs.midtrans.com/reference/card-feature-full-pan).

**Change on Full PAN Card Payment Endpoint**\
Full PAN simplifies the process of recurring transactions on card payment by removing the tokenization step in a normal card payment transaction. This can be used only if the Merchant is already in accordance with PCI-DSS (Payment Card Industry Data Security Standard) compliance.

**Before**\
Merchants use the same endpoint as a one-time card payment: <https://api.midtrans.com> (for sandbox <https://api.sandbox.midtrans.com>).

**Now**\
Merchants need to use a different endpoint for full PAN card payment than a one-time card payment to <https://panapi.midtrans.com> (for sandbox <https://panapi.sandbox.midtrans.com>).

**Purpose**\
Midtrans decided to provide a separate endpoint for full PAN card transactions to isolate PCI scope and mitigate any potential risks in the future related to PCI data in full PAN card transactions.

**What merchant should do**\
Merchants need to change the endpoint to <https://panapi.midtrans.com> to be able to continue using the full PAN feature after the endpoint is ready in production. If there are any concerns about these changes please let us know at <support@midtrans.com.>

**Timeline on Sandbox**\
We plan to expose the new endpoint for full PAN transactions around 18 to 22 September 2023

**Timeline on Production**\
We plan to expose the new endpoint for full PAN transactions around 3 October to 3 November 2023. After 3 November, any full PAN transactions through the old endpoint (*api.midtrans.com*) will be denied/rejected.

<br />

```json Charge API Response - Full PAN not support
{
  "status_code": "402",
  "status_message": "Please migrate to Full PAN new endpoint",
  "id": "5f907720-e9db-4aaf-8f11-8864ad5a021b"
}
```

<br />

## August 7, 2023

In the event of our internal optimization and improvement, we would like to announce some changes regarding `status_message` of credit card payment type in the [Status API](https://docs.midtrans.com/reference/get-transaction-status-card).

<Table align={[null,"left"]}>
  <thead>
    <tr>
      <th>
        transaction_status
      </th>

      <th>
        status_message
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        AUTHORIZE
      </td>

      <td>
        Success, Credit Card transaction is successful
      </td>
    </tr>

    <tr>
      <td>
        CAPTURE
      </td>

      <td>
        Success, Credit Card transaction is successful
      </td>
    </tr>

    <tr>
      <td>
        CAPTURE  
        _(capture authorize transaction)_
      </td>

      <td>
        Success, Credit Card capture transaction is successful
      </td>
    </tr>

    <tr>
      <td>
        SETTLEMENT
      </td>

      <td>
        Success, Credit Card transaction is successful
      </td>
    </tr>

    <tr>
      <td>
        DENY
      </td>

      <td>
        Deny by Bank [BCA] with code [05] and message [FAILURE]
      </td>
    </tr>

    <tr>
      <td>
        DENY  
        _(by FDS)_
      </td>

      <td>
        Denied by Veritrans Fraud Detection System
      </td>
    </tr>

    <tr>
      <td>
        DENY  
        _(by 3DS)_
      </td>

      <td>
        3DS Authentication Denied
      </td>
    </tr>

    <tr>
      <td>
        DENY  
        _(3DS timeout)_
      </td>

      <td>
        3DS Authentication Timeout
      </td>
    </tr>

    <tr>
      <td>
        FAILURE  
        _(bank timeout)_
      </td>

      <td>
        Credit Card transaction is failed
      </td>
    </tr>

    <tr>
      <td>
        PENDING
      </td>

      <td>
        Credit Card transaction is pending
      </td>
    </tr>

    <tr>
      <td>
        CANCEL
      </td>

      <td>
        Success, transaction is canceled
      </td>
    </tr>

    <tr>
      <td>
        REFUND
      </td>

      <td>
        Success, refund request is approved by the bank
      </td>
    </tr>

    <tr>
      <td>
        PARTIAL_REFUND
      </td>

      <td>
        Success, refund request is approved by the bank
      </td>
    </tr>

    <tr>
      <td>
        EXPIRE
      </td>

      <td>
        Credit Card transaction is expired
      </td>
    </tr>

    <tr>
      <td>
        CHARGEBACK
      </td>

      <td>
        Success, transaction is found
      </td>
    </tr>

    <tr>
      <td>
        PARTIAL_CHARGEBACK
      </td>

      <td>
        Success, transaction is found
      </td>
    </tr>

    <tr>
      <td>
        PARTIAL_SETTLEMENT
      </td>

      <td>
        Success, transaction is found
      </td>
    </tr>
  </tbody>
</Table>

<br />

## July 14, 2023

Midtrans would like to announce changes in credit card payment type.

**1. Addition of channel in charge and status response**\
Channel parameter in charge request is an optional field in credit card requests. If a merchant sends it on request, it helps Midtrans to create a payment to the specific channel.

**Possible values of this field:**

| No | Channel     |
| -- | :---------- |
| 1  | DRAGON      |
| 2  | MTI         |
| 3  | MIGS        |
| 4  | CYBERSOURCE |
| 5  | BRAINTREE   |
| 6  | MPGS        |

**Before**\
Midtrans only sends the channel parameter in the charge response when the merchant has provided the channel parameter in the charge request. If merchants do not send any channel parameter on the charge request, then there will be no channel parameter mentioned in the charge response from Midtrans.

**Now**\
Midtrans intends to gradually return the channel parameter in both of the charge and status response.\
**Final goal:** The end goal is to achieve consistency so that all charge and status responses contain the channel parameter, ensuring accurate channel information is provided in both types of responses.

For more details regarding [Channel](https://docs.midtrans.com/reference/feature-route-to-specific-channel)

**Benefit**\
The inclusion of the channel parameter in the charge and status response will be beneficial for merchants who utilize multiple channels. It will provide visibility into which specific channel is used for credit card transactions. This is important because the channel\_response\_code and channel\_response\_message may vary for each channel. Therefore, having the channel parameter in the response will help merchants accurately identify and handle transactions across different channels.

For more details regarding [channel\_response\_code & channel\_response\_message](https://docs.midtrans.com/reference/channel-response-code)

**What merchant should do**\
As Midtrans will gradually send the channel parameter both in the charge and status response, it may pose challenges for the merchants. The merchants need to be ready to accept or disregard the channel parameter if it is returned by Midtrans in the charge and status response.\
If this new field will break merchant implementation please let us know at <support@midtrans.com>.

**Timeline on Sandbox**\
We plan to deploy for credit card transactions with one-time token on 14th July, 2023

**Timeline on Production**\
We plan to deploy gradually on 20th July, 2023 until 20th August, 2023

**2. Addition of settlement\_time in API response\
Before**\
There is no settlement\_time parameter in the charge and status response of a captured credit card transaction.

**Now**\
Midtrans will send settlement\_time parameter in API response for any transaction\_status state.\
**Final goal:** The end goal is to achieve consistency so that all charge and status responses contain the settlement\_time parameter.

For more details regarding [settlement\_time](https://docs.midtrans.com/reference/charge-transactions-on-card)

**What merchant should do**\
As Midtrans will gradually send the settlement\_time parameter both in the charge and status response, it may pose challenges for the merchants. The merchants need to be ready to accept or disregard the channel parameter if it is returned by Midtrans in the charge and status response.\
If this new field will break merchant implementation please let us know at <support@midtrans.com>.

**Timeline on Sandbox**\
We plan to deploy for credit card transactions with one-time token on 14th July, 2023

**Timeline on Production**\
We plan to deploy gradually on 20th July, 2023 until 20th August, 2023

**3. Addition of expiry\_time charge and status response\
Before**

* There is expiry\_time in the status response of an authorized credit card transaction.
* The default expiry\_time for 3DS & non-3DS authorized transactions is 8 days.
* The default expiry\_time for 3DS pending transactions is 10 minutes.
* There is no expiry\_time for non-3DS captured transactions.
* Merchants able to set custom expiry\_time and receive the same on response.

**Now**

* Midtrans will keep the default expiry as 8 days for both 3DS and non-3DS authorized and captured transactions.
* Expiry\_time for 3DS pending transaction still 10 minutes and the transaction will expire within 10 minutes if no further action to complete 3DS process.
* Merchants still able to set custom expiry\_time and receive the same on response.
* **Final goal:** The end goal is to achieve consistency so that all charge and status responses contain the expiry\_time parameter.

For more details regarding [expiry\_time](https://docs.midtrans.com/reference/charge-transactions-1#set-custom-expiry)

**Disclaimer:**\
In the case where a merchant sends a custom expiry parameter in charge request then Midtrans will use the sent custom expiry time. (Note: please note that, for credit card transactions, the custom expiry feature is no longer supported. For more details on custom expiry, please refer to [expiry\_time](https://docs.midtrans.com/reference/charge-transactions-1#set-custom-expiry))

**What merchant should do**\
As Midtrans will gradually send the expiry\_time parameter both in the charge and status response, it may pose challenges for the merchants. The merchants need to be ready to accept or disregard the channel parameter if it is returned by Midtrans in the charge and status response.\
If this new field will break merchant implementation please let us know at <support@midtrans.com>.

**Timeline on Sandbox**\
We plan to deploy for credit card transactions with one-time token on 14th July, 2023

**Timeline on Production**\
We plan to deploy gradually on 20th July, 2023 until 20th August, 2023

**Summary**

* Merchants will be able to see channel in [charge](https://docs.midtrans.com/reference/charge-transactions-on-card), [capture](https://docs.midtrans.com/reference/capture-transaction-card), [cancel](https://docs.midtrans.com/reference/cancel-transaction-card), [refund](https://docs.midtrans.com/reference/refund-transaction-card), and [status](https://docs.midtrans.com/reference/get-transaction-status-card) responses.
* Merchants will be able to see settlement\_time in [charge](https://docs.midtrans.com/reference/charge-transactions-on-card), [capture](https://docs.midtrans.com/reference/capture-transaction-card), [cancel](https://docs.midtrans.com/reference/cancel-transaction-card), [refund](https://docs.midtrans.com/reference/refund-transaction-card), and [status](https://docs.midtrans.com/reference/get-transaction-status-card) responses.
* Merchants will be able to see expiry\_time in [charge](https://docs.midtrans.com/reference/charge-transactions-on-card), [capture](https://docs.midtrans.com/reference/capture-transaction-card), [cancel](https://docs.midtrans.com/reference/cancel-transaction-card), [refund](https://docs.midtrans.com/reference/refund-transaction-card), and [status](https://docs.midtrans.com/reference/get-transaction-status-card) responses.
* Please be noted these changes will be sent gradually for credit card payment that use a one-time token. For Full PAN and Recurring features readiness will be announced in separate announcements.
* Sandbox deployment for credit card transactions with one-time token on 14th July, 2023
* Production deployment for credit card transactions with one-time token will implement gradually on 20th July, 2023 until 20th August, 2023
* If these changes will break Merchant implementation please contact <support@midtrans.com>

<br />

<br />

## June 19, 2023

<br />

In the event of our internal optimization and improvement, we would like to announce several changes:

1. `payment_type` and `bank_transfer` value during Permata Virtual Account charge request\
   *Impacted payment channel: Permata Virtual Account*

   ```json Before
   {
     "payment_type": "bank_transfer",
     "bank_transfer": null,
     "transaction_details": {
       "order_id": "H17550",
       "gross_amount": 145000
     }
   }

   OR

   {
     "payment_type": "bank_transfer",
     "bank_transfer": {
       "permata": {
         "recipient_name": "SUDARSONO"
       }
     },
     "transaction_details": {
       "order_id": "H17550",
       "gross_amount": 145000
     }
   }

   OR

   {
     "payment_type": "bank_transfer",
     "bank_transfer": {
       "bank": "permata",
       "permata": {
         "recipient_name": "SUDARSONO"
       }
     },
     "transaction_details": {
       "order_id": "H17550",
       "gross_amount": 145000
     }
   }
   ```
   ```json After
   {
     "payment_type": "permata",
     "bank_transfer": {
       "permata": {
         "recipient_name": "SUDARSONO"
       }
     },
     "transaction_details": {
       "order_id": "H17550",
       "gross_amount": 145000
     }
   }

   OR

   {
     "payment_type": "bank_transfer",
     "bank_transfer": {
       "bank": "permata"
       "permata": {
         "recipient_name": "SUDARSONO"
       }
     },
     "transaction_details": {
       "order_id": "H17550",
       "gross_amount": 145000
     }
   }
   ```
2. New `id` field in the error response\
   *Impacted payment channels: Permata Virtual Account, Mandiri Bill Payment and Indomaret*

   ```json Before
   {
     "status_code": "402",
     "status_message": "Payment channel is not activated."
   }
   ```
   ```json After
   {
     "status_code": "402",
     "status_message": "Payment channel is not activated.",
     "id": "788e20d7-8fe7-4068-98a8-9bc4139bcd87"
   }

   ```
3. New `expiry_time` field in the charge api response\
   *Impacted payment channels: Permata Virtual Account, Mandiri Bill Payment and Indomaret*
   ```json Before
   {
     "status_code": "201",
     "status_message": "Success, PERMATA VA transaction is successful",
     "transaction_id": "4f4da2ac-4779-4a03-9ca0-577909042ab4",
     "order_id": "order03",
     "merchant_id": "G00123",
     "gross_amount": "275000.00",
     "currency": "IDR",
     "payment_type": "bank_transfer",
     "transaction_time": "2022-04-21 17:15:30",
     "transaction_status": "pending",
     "fraud_status": "accept",
     "permata_va_number": "91019021579"
   }
   ```
   ```json After
   {
     "status_code": "201",
     "status_message": "Success, PERMATA VA transaction is successful",
     "transaction_id": "4f4da2ac-4779-4a03-9ca0-577909042ab4",
     "order_id": "order03",
     "merchant_id": "G00123",
     "gross_amount": "275000.00",
     "currency": "IDR",
     "payment_type": "bank_transfer",
     "transaction_time": "2022-04-21 17:15:30",
     "transaction_status": "pending",
     "fraud_status": "accept",
     "permata_va_number": "91019021579",
     "expiry_time": "2023-01-09 09:56:44"
   }
   ```
4. Status message changes when calling Expire API for cancelled/expired transaction\
   *Impacted payment channels: Permata Virtual Account and Indomaret*

   ```json Before
   {
     "status_code": "412",
     "status_message": "Merchant cannot modify the status of the transaction"
   }
   ```
   ```json After
   {
     "status_code": "412",
     "status_message": "Transaction status cannot be updated.",
     "id": "353b3884-b1d8-4e05-a1d7-004a4e8fd183"
   }
   ```

<br />

## February 9, 2023

<br />

Card transactions that are made using a card that is still using outdated 3DS version 1 will be denied immediately on Midtrans when merchants send `/charge` API request, to prevent from proceeding it to Card Principal’s network (Visa, MasterCard, JCB, Amex). Midtrans will only proceed normally if the card supports 3DS version 2. With main benefits of improving processing time & efficiency.

<br />

As compared to before: Midtrans would still proceed with 3DS version 1 card, even though Principal no longer supports 3DS version 1 (cards that do not support 3DS version 2 will be rejected). This would often result in rejection on the Principal side instead, which is less efficient.

<br />

```json Charge API Response - Card not support 3DS version 2
{
  "status_code": "402",
  "status_message": "Cards with 3DS version 1 or lower are not supported. Please retry with another card that supports the minimum 3DS version 2.",
  "id": "dc948e9d-21c1-438d-9e4d-6ee5268b2ac7"
}
```

<br />

***

<br />

## August 30, 2022

<br />

The allowed maximum time of expiry for GoPay is now adjusted to 7 days.

<br />

***

<br />

## June 17, 2022

<br />

Starting on 22nd July, 2022, we are going to Implement 8 Digit bin.

<br />

> 📘 Note: 8 Digit Bin
>
> With the oncoming mandates from Visa and other principals, Midtrans will start supporting 8-digit BIN's for card transaction processing flows.
>
> The 8-digit bin changes on CoreAPI and will impact the length of token\_id and format of saved\_token\_id.

<br />

Changes list:

1. Change on token\_id length from 48 digit to 50 digit.

| Stage  | Sample                                             | Length | Description                                                |
| ------ | -------------------------------------------------- | ------ | ---------------------------------------------------------- |
| Before | 481111-1114-7baba36c-5698-47cf-9170-80efd6a2e973   | 48     | 6 first digit + "-" + 4 last digit + "-" + 36 random digit |
| After  | 48111111-1114-7baba36c-5698-47cf-9170-80efd6a2e973 | 50     | 8 first digit + "-" + 4 last digit + "-" + 36 random digit |

2. Change on saved\_token\_id format.

| Stage  | Sample                           | Length | Description                                    |
| ------ | -------------------------------- | ------ | ---------------------------------------------- |
| Before | 481111sHdcfSakAvHvFQFEjTivUV1114 | 32     | 6 first digit + 22 random digit + 4 last digit |
| After  | 48111111sHfSakAvHvFQFEjTivUV1114 | 32     | 8 first digit + 20 random digit + 4 last digit |

3. Change of masked\_card in response body, event, and notification.

| Stage  | Sample        | Length | Description                                      |
| ------ | ------------- | ------ | ------------------------------------------------ |
| Before | 481111-1114   | 11     | 6 first digit + 1 digit delimiter + 4 last digit |
| After  | 48111111-1114 | 13     | 8 first digit + 1 digit delimiter + 4 last digit |

4. Support 8 digit bin in Midtrans Fraud Detection System/Aegis.
5. Support 8 digit bin in [BIN API](/reference/bin-api).

<br />

***

<br />

## October 7, 2022

<br />

Starting on 7th Oct 2022, all MIGS MID has been migrated to MPGS MID.

<br />

> ❗️ Migrate MIGS to MPGS for BCA & BRI except Maybank
>
> In relation to 3DS2.0 mandate from principal, we need to migrate all of existing BCA and BRI MID from MIGS to MPGS because MIGS BCA & BRI only support 3DS 1.0<br />\
> The MID migration will affect <b>channel\_response\_code</b> and <b>channel\_response\_message</b> format.
>
> For more MPGS response details, please refer to [MPGS Response code](/reference/channel-response-code#mpgs)

<br />

Affected Banks:

<br />

| Bank | Previous Channel | New Channel |
| ---- | ---------------- | ----------: |
| BCA  | MIGS             |        MPGS |
| BRI  | MIGS             |        MPGS |

if you have any inquiry, please contact <support@midtrans.com>

<br />

## December 6, 2022

<br />

### GoPay Deny Error

<br />

Starting in January 2023 there will be an update on Midtrans deny error for GoPay payment channel. The transition phase will start in January upto April 2023, Please ensure that merchant's system can accommodate both behavior (before and after) within this period.

<br />

> 🚧 Update on behavior of Midtrans deny errors for GoPay payment channel.
>
> Midtrans will change the behavior of Midtrans deny error for GoPay payment channel - Some of GoPay error will be mapped to Midtrans error (4xx/5xx) - GoPay error that is mapped to 4xx error won’t have HTTP post notification.

<br />

```curl Status Code 202 Sample
{
"Status_code":"202",
"status_message":"GoPay transaction is denied",
"channel_response_code":"201",
"channel_response_message":"insufficient balance"
…
}
```
```curl Status code 4xx sample
{
  "status_code":"400",
  "status_message":"One or more parameters in the payload is invalid.",
  "validation_messages":[
    "Gopay.account_id is required"
  ],
  "id":"1a3fef7b-c034-4cf2-98d6-e239594976f3"
}
```
```curl Status code 5xx sample
{
  "status_code":"500",
  "status_message":"Sorry. Our system is recovering from unexpected issues. Please retry.",
  "Id":"6a782ad4-1e18-4df5-b5bd-dbf94ce15ddc"
}
```

| Terms                    | Definition                                                                                                                                                                                                                                                            |
| :----------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Deny error               | An error that Midtrans return back to merchant, if Midtrans got rejection from payment provider ([status code 202](/reference/code-2xx)). For this error Merchant can call [GET Status API](reference/get-transaction-status) to retrieve payment provider error data |
| Channel response code    | Error code that Midtrans received from payment provider                                                                                                                                                                                                               |
| Channel response message | Error message that Midtrans received from payment provider                                                                                                                                                                                                            |
| 4xx error                | [status code 4xx](/reference/code-4xx)                                                                                                                                                                                                                                |
| 5xx error                | [status code 5xx](/reference/code-5xx)                                                                                                                                                                                                                                |

<br />

**Change List :**

<br />

1. Update on behaviour for listed GoPay errors below :

<Table align={["left","left","left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        GoPay error code
      </th>

      <th>
        GoPay error message
      </th>

      <th>
        New status code
      </th>

      <th>
        New HTTP code
      </th>

      <th>
        Before
      </th>

      <th>
        After
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        310
      </td>

      <td>
        Malformed data
      </td>

      <td>
        400
      </td>

      <td>
        400
      </td>

      <td>
        \{  
        "Status_code":"202",  
        "status_message":"GoPay transaction is denied",  
        "channel_response_code":"310",  
        "channel_response_message":"Malformed data  
        …  
        }
      </td>

      <td>
        \{  
        "status_code": "400",  
        "status_message": "One or more parameters in the payload is invalid.",  
        "validation_messages": [  
        "Malformed data"  
        ],  
        "id": "f7f6463e-d46b-4b4e-9027-8d8104ac34c6"  
        }
      </td>
    </tr>

    <tr>
      <td>
        2901
      </td>

      <td>
        Duplicate transaction
      </td>

      <td>
        406
      </td>

      <td>
        200
      </td>

      <td>
        \{  
        "Status_code":"202",  
        "status_message":"GoPay transaction is denied",  
        "channel_response_code":"2901",  
        "channel_response_message":"Duplicate transaction",  
        …  
        }
      </td>

      <td>
        \{  
        "status_code":"406",  
        "status_message":"The request could not be completed due to a conflict with the current state of the target resource, please try again",  
        "id":"be929ec4-19cb-458b-85e4-43869ada0597"  
        }
      </td>
    </tr>

    <tr>
      <td>
        2701
      </td>

      <td>
        The currency is not supported for the country
      </td>

      <td>
        400
      </td>

      <td>
        400
      </td>

      <td>
        \{  
        "status_code":"202",  
        "status_message":"GoPay transaction is denied",  
        "channel_response_code":"2701",  
        "channel_response_message":"The currency is not supported for the country",  
        …  
        }
      </td>

      <td>
        \{  
        "status_code": "400",  
        "status_message": "One or more parameters in the payload is invalid.",  
        "validation_messages": [  
        "The currency is not supported for the country"  
        ],  
        "id": "f7f6463e-d46b-4b4e-9027-8d8104ac34c6"  
        }
      </td>
    </tr>

    <tr>
      <td>
        4060
      </td>

      <td>
        Fraud validation
      </td>

      <td>
        202
      </td>

      <td>
        200
      </td>

      <td>
        \{  
        "Status_code":"202",  
        "status_message":"GoPay transaction is denied",  
        "channel_response_code":"4060",  
        "channel_response_message":"Fraud validation error",  
        …  
        "fraud_status":"accept"  
        }
      </td>

      <td>
        \{  
        "status_code": "202",  
        "status_message": "GoPay transaction is rejected by FDS",  
        "transaction_id": "171dba71-6d5c-4bb8-8fd7-3ad44fdeb8fb",  
        ...  
        "fraud_status": "deny"  
        }
      </td>
    </tr>

    <tr>
      <td>
        303
      </td>

      <td>
        Field cannot be blank
      </td>

      <td>
        402
      </td>

      <td>
        200
      </td>

      <td>
        \{  
        "Status_code":"202",  
        "status_message":"GoPay transaction is denied",  
        "channel_response_code":"303",  
        "channel_response_message":"Field cannot be blank"  
        …  
        }
      </td>

      <td>
        \{  
        "status_code":"402",  
        "status_message":"Missing GoPay merchant setting data",  
        "id":"363a8d7f-92d5-4232-9c2d-7e6de2dafa33"  
        }
      </td>
    </tr>

    <tr>
      <td>
        112
      </td>

      <td>
        User Blocked
      </td>

      <td>
        402
      </td>

      <td>
        200
      </td>

      <td>
        \{  
        "Status_code":"202",  
        "status_message":"GoPay transaction is denied",  
        "channel_response_code":"112",  
        "channel_response_message":"User Blocked"  
        …  
        }
      </td>

      <td>
        \{  
        "status_code":"402",  
        "status_message":"GoPay user is blocked",  
        "id":"363a8d7f-92d5-4232-9c2d-7e6de2dafa33"  
        }
      </td>
    </tr>

    <tr>
      <td>
        1703
      </td>

      <td>
        Midtrans merchant not active
      </td>

      <td>
        400
      </td>

      <td>
        400
      </td>

      <td>
        \{  
        "Status_code":"202",  
        "status_message":"GoPay transaction is denied",  
        "channel_response_code":"1703",  
        "channel_response_message":"Midtrans merchant not active",  
        …  
        }
      </td>

      <td>
        \{  
        "status_code":"402",  
        "status_message":"GoPay merchant is not active.",  
        "id":"363a8d7f-92d5-4232-9c2d-7e6de2dafa33"  
        }
      </td>
    </tr>

    <tr>
      <td>
        153
      </td>

      <td>
        The token is invalid for the payment
      </td>

      <td>
        400
      </td>

      <td>
        400
      </td>

      <td>
        \{  
        "status_code":"202","status_message":"GoPay transaction is denied",  
        "channel_response_code":"153",  
        "channel_response_message":"The token is invalid for the payment",  
        …  
        }
      </td>

      <td>
        \{  
        "status_code": "400",  
        "status_message": "One or more parameters in the payload is invalid.",  
        "validation_messages": [  
        "GoPay token is invalid for the payment"  
        ],  
        "id": "f7f6463e-d46b-4b4e-9027-8d8104ac34c6"  
        }
      </td>
    </tr>

    <tr>
      <td>
        5009
      </td>

      <td>
        Auth token already expired
      </td>

      <td>
        400
      </td>

      <td>
        400
      </td>

      <td>
        \{  
        "Status_code":"202",  
        "status_message":"GoPay transaction is denied",  
        "channel_response_code":"5009",  
        "channel_response_message":"Auth token already expired",  
        …  
        }
      </td>

      <td>
        \{  
        "status_code": "400",  
        "status_message": "One or more parameters in the payload is invalid.",  
        "validation_messages": [  
        "GoPay challenge token is already expired"  
        ],  
        "id": "f7f6463e-d46b-4b4e-9027-8d8104ac34c6"  
        }
      </td>
    </tr>

    <tr>
      <td>
        110
      </td>

      <td>
        Unauthorized
      </td>

      <td>
        402
      </td>

      <td>
        200
      </td>

      <td>
        \{  
        "status_code":"202",  
        "status_message":"GoPay transaction is denied",  
        "channel_response_code":"110",  
        "channel_response_message":"Unauthorized",  
        …  
        }
      </td>

      <td>
        \{  
        "status_code":"402",  
        "status_message":"GoPay merchant is unauthorized.",  
        "id":"363a8d7f-92d5-4232-9c2d-7e6de2dafa33",

        }
      </td>
    </tr>

    <tr>
      <td>
        132
      </td>

      <td>
        Transaction in progress
      </td>

      <td>
        406
      </td>

      <td>
        200
      </td>

      <td>
        \{  
        "Status_code":"202",  
        "status_message":"GoPay transaction is denied",  
        "channel_response_code":"132",  
        "channel_response_message":"Transaction in progress",  
        …  
        }
      </td>

      <td>
        \{  
        "status_code":"406",  
        "status_message":"The request could not be completed due to a conflict with the current state of the target resource, please try again",  
        "id":"be929ec4-19cb-458b-85e4-43869ada0597"

        }
      </td>
    </tr>

    <tr>
      <td>
        2903
      </td>

      <td>
        Invalid Request
      </td>

      <td>
        402
      </td>

      <td>
        200
      </td>

      <td>
        \{  
        "Status_code":"202",  
        "status_message":"GoPay transaction is denied",  
        "channel_response_code":"2903",  
        "channel_response_message":"Invalid Request",  
        …  
        }
      </td>

      <td>
        \{  
        "status_code":"402",  
        "status_message":"Missing GoPay merchant setting data",  
        "id":"363a8d7f-92d5-4232-9c2d-7e6de2dafa33"  
        }
      </td>
    </tr>

    <tr>
      <td>
        902
      </td>

      <td>
        Malformed JSON
      </td>

      <td>
        413
      </td>

      <td>
        200
      </td>

      <td>
        \{  
        "Status_code":"202",  
        "status_message":"GoPay transaction is denied",  
        "channel_response_code":"902",  
        "channel_response_message":"Malformed JSON",  
        …  
        }
      </td>

      <td>
        \{  
        "status_code": "413",  
        "status_message": "The request cannot be processed due to malformed syntax in the request body"  
        }
      </td>
    </tr>

    <tr>
      <td>
        101
      </td>

      <td>
        Wallet not found
      </td>

      <td>
        404
      </td>

      <td>
        200
      </td>

      <td>
        \{  
        "Status_code":"202",  
        "status_message":"GoPay transaction is denied",  
        "channel_response_code":"101",  
        "channel_response_message":"Wallet not found",  
        …  
        }
      </td>

      <td>
        \{  
        "status_code": "404",  
        "status_message": "GoPay Wallet doesn't exist.",  
        "id": "7d17e7e6-4272-42ac-be95-f728a42c6b78"  
        }
      </td>
    </tr>

    <tr>
      <td>
        900
      </td>

      <td>
        Internal server error
      </td>

      <td>
        either 500 or 202
      </td>

      <td>
        200
      </td>

      <td>
        \{  
        "status_code":"202",  
        "status_message":"GoPay transaction is denied",  
        "channel_response_code":"900",  
        "channel_response_message":"Internal server error",  
        …  
        }
      </td>

      <td>
        * _500_*: \{  
          "status_code":"500",  
          "status_message":"Sorry. Our system is recovering from unexpected issues. Please retry.",  
          "id":"6a782ad4-1e18-4df5-b5bd-dbf94ce15ddc"  
          }\

        * _202_*: \{  
          "status_code":"202",  
          "status_message":"GoPay transaction is denied",  
          "channel_response_code":"900",  
          "channel_response_message":"Internal server error",  
          "transaction_id":"c4f05215-1044-4740-b1b9-6154a73fc433",  
          "order_id":"893016743",  
          "merchant_id":"G253339736",  
          "gross_amount":"61499.00",  
          "currency":"IDR",  
          "payment_type":"gopay",  
          "transaction_time":"2022-11-22 09:30:29",  
          "transaction_status":"deny","fraud_status":"accept"  
          }
      </td>
    </tr>
  </tbody>
</Table>

<br />

2. GoPay error that is mapped to 4xx error won’t have HTTP post notification.

<br />

### Expiry Threshold

<br />

Starting on January 16th 2023, we will apply minimum and maximum expiry time threshold.

<br />

> 🚧 New minimum and maximum expiry time threshold
>
> Midtrans will apply minimum and maximum expiry time threshold on all payment channels. - Transaction with expiry time less than 20 seconds will be rejected. - Transaction with expiry time more than 180 days will be accepted, but expiry time will be trimmed to 180 days\*
>
> \*except for GoPay transaction. GoPay have maximum expiry time of 7 days

<br />

| Terms                 | Definition                                                                                     |
| :-------------------- | :--------------------------------------------------------------------------------------------- |
| Transaction timestamp | Timestamp at which transaction is initiated via [Charge AP](/reference/charge-transactions-1)I |
| Expiry timestamp      | Timestamp at which the order will be expired                                                   |
| Expiry time           | Time between transaction timestamp and expiry timestamp                                        |

<br />

**Change list:**

<br />

1. Added field `expiry_time` on charge response, get status response and notification. `expiry_time` field will be returned in API response (charge and status API) and also HTTP notification

```curl expiry_time in charge & status API response
{
   "transaction_time":"2023-01-16 10:00:00",
   "Transaction_status":"pending",
   "transaction_id":"ce0a3584-5a0c-4049-ad88-5590a96be4fe",
   …
   "expiry_time":"2023-07-16 10:00:00"
}
```
```curl expiry_time in HTTP Notification
{
   "transaction_time": "2023-01-16 10:00:00",
   "transaction_status": "pending",
   "transaction_id": "ce0a3584-5a0c-4049-ad88-5590a96be4fe",
   "status_message": "midtrans payment notification",
   …
   "expiry_time":"2023-07-16 10:00:00"
}
```

<br />

2. Transaction with expiry time less than 20 seconds will be rejected

Sample scenario of Charge API with [Custom Expiry object](/reference/custom-expiry-object) :

a. charge request without order time\
If merchant send the sample request (seen on right side) without `order_time` at 10:00:30 GMT+7, then the calculated expiry time is 10 seconds, as follow:

* `order_time`: not specified hence will follow transaction time
* `transaction_time`: 10:00:30 GMT+7
* `expiry_duration` : 10 seconds
* Expiry timestamp: 10:00:40 GMT+7
* **Expiry time: 10 seconds**

Therefore the transaction will be **rejected.**

b. charge request with order time\
If merchant send the sample request (seen on right side) with order\_time at 10:00:30 GMT+7, then the calculated expiry time is 10 seconds, as follow:

* `order_time`: 10:00:00 GMT+7
* `transaction_time`: 10:00:30 GMT+7
* `expiry_duration`: 40 seconds
* Expiry timestamp: 10:00:40 GMT+7
* **Expiry time: 10 seconds**

Therefore the transaction will be **rejected**.

<br />

```curl Custom expiry without order_time sample
"custom_expiry": {
  "expiry_duration": 10,
  "unit": "second"
}
```
```curl Custom expiry with order_time sample
"custom_expiry": {
  "order_time": "2023-01-16 10:00:00 +0700",
  "expiry_duration": 40,
  "unit": "second"
}
```
```curl Charge response for rejected transaction
{
   "status_code": "400",
   "status_message": "One or more parameters in the payload is invalid.",
   "id": "1a1a66f7-27a7-4844-ba1f-d86dcc16ab27",
   "validation_messages": 
       [
           "custom_expiry is below minimum threshold"
        ]
}
```

<br />

3. Transaction with expiry time more than 180 days will be accepted but expiry time will be trimmed to 180 days (except for GoPay transaction which is 7 days)

Sample scenario of Charge API with [Custom Expiry object](/reference/custom-expiry-object) :

a. charge request without order time\
If merchant send the sample request (seen on right side) request at 2023-01-16, then the calculated expiry time is 210 days, as follow:

* `order_time`: not specified hence will follow transaction time
* `transaction_time`: 2023-01-16 10:00:00 GMT+7
* `expiry_duration` : 210 days (approx 7 months)
* Expiry timestamp withouth trim should be: 2023-08-16 10:00:00 GMT+7

We will trim the expiry time to 180 days with **new expiry timestamp: 2023-07:16 10:00:00 GMT+7.**

b. charge request with order time

If merchant send the sample request (seen on right side) request at 2023-01-16, then the calculated expiry time is 209 days, as follow:

* `order_time`: 2023-01-15 10:00:00 GMT+7
* `transaction_time`: 2023-01-16 10:00:00 GMT+7
* `expiry_duration`: 210 days (approx 7 months)
* Expiry time: 209 days
* Expiry timestamp withouth trim should be: 2023-08-15 10:00:00 GMT+7

Therefore we will trim the expiry time to 180 days with **new expiry timestamp: 2023-07:16 10:00:00 GMT+7.**

<br />

```curl Custom expiry without order_time sample
"custom_expiry": {
  "expiry_duration": 210,
  "unit": "day"
}
```
```curl Custom expiry with order_time sample
"custom_expiry": {
  "order_time": "2023-01-15 10:00:00 +0700",
  "expiry_duration": 210,
  "unit": "day"
}
```
```curl Charge response with trimmed expiry_time
{
  "transaction_time":"2023-01-16 10:00:00",
  "transaction_status":"pending",
  "transaction_id":"ce0a3584-5a0c-4049-ad88-5590a96be4fe",
  ....
  "expiry_time":"2023-07-16 10:00:00" 
}
```