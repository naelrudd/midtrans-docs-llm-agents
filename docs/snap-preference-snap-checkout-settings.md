---
updatedAt: 2025-11-10T22:53:31.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Snap Preference (Snap Checkout Settings)

Configure your Midtrans's Snap Checkout look and feel and system settings here.

In this page, you can configure your Snap Preference themes and system settings such as Redirection URL here. Note that some values e.g. Redirection URL and expiry time can also be specified as part of parameter in the create token requests; when specified, Snap Checkout will prioritize those values instead of the values specified in the dashboard.

<br />

# Theme and Logo

***

<br />

In this section, you can tailor the look and feel of your Snap Checkout here.

<br />

## Header (Embedded and Pop Up Mode only)

<br />

This section controls the header displayed on your Snap payment page when using the embedded or pop-up integration methods.

* Use header: Check this box to display a header on your Snap payment page. This is only applicable for Pop Up and Embedded integrations only.
* Display Branding\
  You can specify whether you want to show your business name as a text or upload the logo file here.
  * Display Name: Enter the name you want to be displayed on the payment page (e.g., your store name).
  * Brand Logo: Click Upload to upload your brand logo. Supported Formats: png, jpeg -  maximum size: 200 KB

<br />

## Font

<br />

This section lets you choose the font used for the text elements on your Snap payment page.

<br />

## Colors

<br />

This section allows you to customize the color scheme of your Snap payment page to match your brand. This will target the header and primary buttons e.g. Pay button. You can specify the hex code or choose from the color palette picker.

<br />

## Style

<br />

This section provides options to adjust the visual style of certain elements on your Snap payment page.

* Input Field: Choose the shape of the input fields (e.g., Square, Rounded).
* Button: Choose the shape of the buttons (e.g., Square, Rounded).

<br />

## Preview

<br />

On the right side of the page, you'll find a real-time preview of how your Snap payment page will look based on the configurations you've set. This allows you to see the changes as you make them. The preview shows both the expanded view and a view of the credit card input fields.

<br />

## Actions

<br />

* Reset to default: Click this button to revert all settings on the page back to their original default values.
* Save: Click this button at the bottom left of the page to apply and save all the changes you've made to your Snap Preferences.

<br />

# Payment Channels

***

<br />

You can drag and drop which payment methods do you want to show to your customers here. You will only see a list of payment methods that are already activated in your business. If you specify the available payment methods via the `enabled_payments` param when creating a Snap Token, the payment methods shown up will be a subset of the payment methods specified in the `enabled_payments` but still follow the sortings as specified in the dashboard.

Scroll down the right side of the preview screen to use our Recommended Payment Method sorting; this will sort out the payment methods based on the sorting that is optimized for checkout conversion rate based on our data. This sorting will be updated dynamically.

<br />

# Bank List

***

<br />

Bank list behaves identically to the payment channel section where you can sort the Virtual Account bank options here via the drag and drop panel. In here, you can also specify the default virtual account bank processor for Other Banks here.

<br />

# System Settings

***

<br />

You can set up key system settings here :

* **Google Analytics** : if you're using Google Analytics, specify the code here.
* **Page expiry settings** : specify the max expiry time of Snap Checkout page here (you can specify up to 7 days). For select payment methods like GoPay, Bank Transfers, and Over the Counter, once users have generated the payment code / QR code, the expiry time counter for code will start and follow the expiry time specified for each payment method in below's section.  You can also specify this page expiry value when creating a Snap token.
* **Payment expiry settings** : specify the expiry time for each payment methods here. If not specified, Snap Checkout will use the default values.
* **Redirection URL** : specify the webpage URL that customer will see after completing a payment flow here. Finish URL will be shown if customer has completed or successfully generate a payment code; likewise Error URL will be shown if customer failed to complete the payments (e.g. transaction is denied or expired).
* **Language** : set the default Snap Checkout language here. Customer will still be able to change the language selection when they open the Snap Checkout page.
* **Hide order ID** : toggle this as true if you want to hide your order ID from your customers.

<br />

Click save in order to apply your changes.

<br />

# Card Payment Settings

***

<br />

Card payment settings tab will only appear if you have card payment method activated for you.  You can configure settings pertaining to installments here. You can specify the config either via API request or via Snap Preference.

<br />

![](https://files.readme.io/c4df7c712c60aacaddbc4a085bb3b856d7ffc70b1033fa138b47397cd1e469eb-image.png)

<br />

See more details on how to configure this [here](/docs/snap-advanced-feature#configuring-installment-via-snap-preference).