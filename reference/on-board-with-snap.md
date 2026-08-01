---
updatedAt: 2025-11-11T00:24:18.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# On Board with Snap

To start using Snap, you have to register for Midtrans Sandbox/Production account [here](https://dashboard.midtrans.com/register). Once you have registered, Midtrans will provide all available payment channels in sandbox mode that you can start to integrate with.

<br />

***

<br />

## <b> Existing Merchant </b>

<br />

For existing merchants (merchants already live in Production), only one step need to be taken to enable a specific payment method.

<br />

### Set Activate Payment Option in Snap Payment List

<br />

Merchants can pick to activate a payment method through the Merchant Administration Portal (MAP) in menu [Settings -> Snap Preferences Settings](https://dashboard.sandbox.midtrans.com/settings/snap_preference) on Tab ‘Payment Channels’. Merchant can drag the a desired payment channels into which payment channel’s order. Consider the following figure.

<br />

![](https://files.readme.io/640bb1f-payment-list.png "payment-list.png")

<br />

Just drag a desired payment channels option to the active list of payment list. Through this option, the merchant no longer need to do any code adjustment in their end, just set a desired payment channel on and that payment will be live.

<br />

> 👍 Apply Recommended Sorting
>
> It is highly recommended to apply recommended sorting to sort your payment list presentment - Recommended Sorting will sort out your payment method based on popular payment methods which will help to increase your payment conversion rate.

<br />

***

<br />

## <b>New Merchant</b>

<br />

There are a few pre-requisites before integrating with Midtrans:

<br />

### 1. Register to Midtrans Sandbox/Production account

<br />

Midtrans has one central login to access both production and sandbox account. Sandbox is utilized for development period while production is utilized when the merchant has completed the integration process and want to go live. Data and transaction made on sandbox account will not trigger an actual purchase while in production account will trigger an actual process. Register for Midtrans Sandbox/Production account [here](https://dashboard.midtrans.com/register).

Once logged in, there will be a small button on the header of the dashboard that shows you on whether you are in the production or sandbox environment. The color of the navigation sidebar are also set differently between Production (light blue) and Sandbox (dark blue) for further clarity.

<br />

### 2. Fill in the required information in Merchant Administration Portal (MAP)

<br />

The required fields can be found under [Settings - General Settings](https://dashboard.sandbox.midtrans.com/settings/general_info).

<br />

### 3. Take note of your account Access Keys

<br />

Your account keys can be found under [Settings - Access Keys](https://dashboard.sandbox.midtrans.com/settings/config_info).

<br />

### 4. Configure Redirection URL

<br />

Customer will be returned to your website after payment process is completed.

Go to [Snap Preference - System Settings](https://dashboard.midtrans.com/settings/snap_preference) menu to manage the redirection URL.

<br />

### 5. Configure Checkout Page Branding

<br />

Merchants can configure Snap's checkout page branding via [Snap Preference > Theme and Logo](https://dashboard.midtrans.com/settings/snap_preference). The following aspects are available to be customized :

* Brand name :  max 25 char to fit in Snap's window width
* Use header : choose to display Snap header (that shows brand name / display name). Applicable for Snap Pop Up and Embedded mode only.
* Logo : If merchant does not want to show brand name, a logo file can be uploaded instead.
* Header and button color : specify the hex code or choose from the color picker to change header and Pay/Back To Merchant button color.
* Font : choose from available typeface choices
* Button and input field roundness : choose from Square, Pill, or Round (roundness value can be customized)
* Language : set the default language of Snap payment page. Specifically for language settings, access it from System Settings tab in Snap Preference menu.

<br />

### 6. Manage Payment List Display and Sorting

<br />

Merchants can configure which specific payment options to show and manage the sorting via [Settings - Snap Preferences Settings](https://dashboard.sandbox.midtrans.com/settings/snap_preference) on Tab ‘Payment Channels’. To do so, drag the particular payment into Snap window in desired order (or drag from Snap window to payment list to hide), or apply Recommended Sorting to make use of Midtrans's payment method sorting optimized to increase payment conversion rate.

If you have an open loop virtual account payment method active, you can also manage your [Other Bank](/reference/other-banks)'s VA assignment in Bank List tab.

<br />

### 7. Set Session Expiry and Google Analytics

Merchant can also customize [various expiry](/reference/expire-a-snap-session) (payment methods & page) and integrate Google Analytics via [Snap Preference](https://dashboard.midtrans.com/settings/snap_preference) > System Settings.

<br />

### 8. Configure Card Payment Settings

This is an optional settings if you have card payment installment feature is activated on your merchant account. To activate card payment installment feature, contact your Sales PIC first or Midtrans support team for the required procedure.

Once card payment installment feature is activated, you can specify the config either via API request or via Snap Preference. See more details on how to configure it via Snap Preference [here](/docs/snap-advanced-feature#configuring-installment-via-snap-preference).