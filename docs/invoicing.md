---
updatedAt: 2026-05-21T18:19:02.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Invoicing (NEW!)

Streamline your invoice creation flow from start to finish with Midtrans Invoicing.

<Callout icon="🚀" theme="default">
  ### What's new in Invoicing

  * Creating a sales quotation is now supported! You can then accept and convert the quotation into a payable invoice.
  * Tax exclusive and inclusive, along with custom tax schemes are now supported.
  * Markdown is now supported in Notes section.
  * Product ID max char is now expanded to 40 char - now you can use it for info such as Product name, etc.

  Send us your feedback and request via the product board [here](/page/feature-request).
</Callout>

<br />

You can now streamline your account receivable collection process with Midtrans Invoicing - from creating a custom branded invoice, generating a payment link or a Virtual Account number to digitally collect payments, automatically send  reminders, and programmatically reconcile payments with invoice.

Invoicing can be accessed from [Dashboard > Invoicing](https://www.google.com/url?q=https://dashboard.midtrans.com/invoices\&sa=D\&source=docs\&ust=1701848454752647\&usg=AOvVaw0V8H1QpvzCBnQjhKCHdIIQ) menu, Production environment only. No manual activation is needed to use Invoicing.

Want to integrate Invoicing to your system? Use our [Invoicing API](/reference/overview-2) instead.

<br />

<Image align="center" width="50% " src="https://files.readme.io/5a55888-RenderedInvoice.png" />

<br />

***

<br />

# Set up Invoicing

Before you create a new invoice or quotation, set up your document settings first. This will not just help reduce the number of fields that you need to fill when creating a document, but also is required to ensure that your invoice and quotation looks professional, and works properly. You can immediately see how it will look like in your PDF via the preview pane in the right side of the page.

You can change most of the values in the Settings when creating a document - Settings will just help you to prefill repetitive information into your document draft.

Do note that if you use Payment Link, some settings e.g. logo, branding and payment method default expiry needs to be configured in [Snap Preference](https://dashboard.midtrans.com/settings/snap_preference) settings, so ensure your Snap Preference settings are updated as well.

<br />

> 🚧 Setup your invoice before creating your first invoice
>
> While it's possible to create an invoice without setting up anything, we strongly advise to finish configuring your invoice settings first. Otherwise, some aspects might not work properly.
>
> Any changes to Invoice settings will apply to newly created invoices.

<br />

To start configuring your settings, click the `Start set up` button. Otherwise you can also access the setting from the `Setting` button in the top right side of the page that will appear when at least 1 invoice has been created.

<br />

<Image align="center" alt="Invoice settings" caption="Invoice settings" src="https://files.readme.io/b5445a4-Empty_State.png" />

<br />

## Set up default document type

![](https://files.readme.io/59ff70d7bd4190f0c756a16fae67b9fb0f60071191a8fe36467cfb911a165255-image.png)

Here, you can set the default document type that will be selected when you create a new document, either as Sales Quotation or Invoice. Quotation contains no payment methods, but can be converted into Invoice, which will contain the payment methods. Invoice will directly have the payment methods.

<br />

## Set up branding

<br />

Set up your business branding in your invoice and quotation to make it look professional and helpful for your customer to understand and verify your business. Upload your business logo and fill in your business details such as Official Merchant Name in Midtrans's [General Settings](https://dashboard.midtrans.com/settings/general_info) page - Invoicing will use said information to populate your business information that will be shown in Invoice PDF and email.

Note : you can also customize your Invoice and Quotation title before and after payment here - e.g. set the title as Sales Order before payment, and let our system automatically update it to Invoice if the payment has been made to said invoice.

<br />

<Image align="center" alt="Branding settings" caption="Branding settings" src="https://files.readme.io/53cda94-image.png" width="50% " />

<br />

## Set up payment method default settings (optional)

<br />

You can choose from two ways to get paid; by generating a Payment Link, or a Virtual Account number ( that will be attached directly to your Invoice PDF - henceforth will be referred as **Direct VA**). The former has the benefit where your customers can pay using a wide array of payment methods; while the latter make it easy for your customers whose workflow requires paying via bank account to streamline the payment e.g. saving the VA number to their transfer list, get the VA number without having to open a link everytime, etc.

Payment Link's configuration is optional and can only be done when creating an invoice. For Direct VA, you can configure what would be your default acquiring bank that will issue the VA (e.g. BCA VA, BRI VA, etc). You can also configure the default expiry time - either it will match the invoice due date (rendering invoice unpayable once invoice's due date has passed), or x hours/days after `Invoice date`.

<br />

<Image align="center" alt="Payment method default settings" caption="Payment method default settings" src="https://files.readme.io/17e92d6-Payment_Method.PNG" width="50% " />

<br />

<br />

## Configure default tax mode

![](https://files.readme.io/9d4bbdc14d86652d2fe6269429807191cd1a86da89159e91148debc529206750-image.png)

Here, you can configure your default tax mode :

* No tax : no tax will be added by default
* Tax exclusive : tax will be calculated after the inputted product price subtotal
* Tax inclusive : tax will be back calculated based on the provided product price

You can also configure your default tax type and set up custom tax scheme here.

<br />

## Add additional information (optional)

You can add the default value for optional additional information such as T\&C, Notes, Signature, and Signatory information in this section. You can still modify Notes directly within the invoice creation form.

<br />

<Image align="center" width="50% " src="https://files.readme.io/de8ca6c-Additional_Information.PNG" />

<br />

## Set up reminder schedule

<br />

> 📘 Sending a reminder
>
> Reminders can only be sent to customers via emails at the moment. In order to user the reminder feature, ensure that Client email is filled when creating an invoice. Otherwise, reminder will not be sent.
>
> Reminder that's scheduled to be sent after the Invoice status has changed to Expired will be skipped. This also applies for any invalid reminder schedule.
>
> Reminder will only be sent for an Invoice, not a Quotation.

<br />

Set the toggle to On in order to user the reminder feature. Once toggled on, reminders will sent to customers/recipient via email - you must set at least 1 reminder schedule.

You can set up to 3 reminders. Reminder will then be sent to customer **x hours/ days after the date invoice is published (posting date)**.

<br />

<Image align="center" alt="Reminder settings" caption="Reminder settings" src="https://files.readme.io/8cfd8af-Reminder.PNG" width="50% " />

<br />

## Set up custom text template

<br />

In the scenario where you want to share your Invoice PDF or payment method to customers manually, Midtrans will generate a text containing the PDF download link and Payment Link URL / Direct VA number that you can copy and share to your customers via any of your preferred channel. You can modify the header section of the template in this section. Note that text template for both Quotation and Invoice will be different; Quotation text template is non modifiable.

<br />

<Image align="center" alt="Text template" caption="Text template" src="https://files.readme.io/3797cf7-Text_Invoice_Template.PNG" width="50% " />

<br />

***

<br />

# Creating a document

<br />

## Create a new invoice or sales quotation

<br />

> 🚧 B2B / Open Amount Virtual Account
>
> Invoicing does not yet support using B2B / Open Amount VA. If you still choose to use it; payment will still be accepted as usual, but invoice will never be marked as `Paid`.

When creating an invoice from a new fresh form, some of the information will be auto populated from the Settings. Midtrans will also auto generate some value for you (e.g. Invoice No, Order ID) in fields that are mandatory to be filled in order to publish an invoice - but you are free to change the value as per your needs. You can see an approximate preview of how your invoice would look like from the preview pane on the right; the final preview will be shown when you click `Preview and Send`.

You can choose to create a Sales Quotation that can be converted into an Invoice, or directly create an Invoice. Sales quotation will not show methods to pay to customers before you convert the quotation into an invoice.

<br />

<Image align="center" width="75% " src="https://files.readme.io/a4dffe7-Create_FOrm.PNG" />

Below are some explanation of the invoice fields :

* **Customer details** ***(Required)*** : Your client information that is the subject to receive the information. At least **Name** needs to be filled. If you plan to use the Reminder feature, then Email must be filled as well.
* **Invoice information** ***(Required)*** : Invoice properties. At least **Invoice date, Invoice due date, Invoice no, and Order ID** are mandatory to be filled. By default we will prepopulate these fields for you; the dates using today's date, IDs using random UUID. Several notes :\ <br />
  * *Invoice no* : Your invoice number. Number needs to be unique among paid invoices; however you can reuse any invoice number if previous invoice's status is expire. This no will be shared with Sales Quotation
  * *Invoice date* : Date of your invoice. Backdate and future date is allowed, up to 2 years prior / after.
  * *Invoice due date* : The date when your invoice will be marked as `Overdue`  in Midtrans. Overdue invoice can still be paid by customers as long as the payment method hasn't expired yet. Invoice due date must be at least or later than today's date. Invoice due date can be set up to 2 years after today's date.\ <br />
* **Payment method\_(Required)\_** : Define how do you want to get paid for that particular invoice. Payment method will not be shown in Sales Quotation, until the quotation is converted into Invoice.\
  Payment link is selected by default - customer can attempt to pay again until 1 pending/successful payment is generated.\
  If you choose Virtual account (Direct VA) instead - Invoice will generate a VA number that will be automatically shown in the Invoice PDF and email. The default bank from Settings will be automatically selected here, however you can change it in this section. Expiry time will be by default configured as `Same as due date`.\ <br />\
  **You can only choose between Payment Link and Direct VA, not both.** If you choose Payment Link, you can still accept VA payment, however customer will need to open the Payment Link URL first and choose to pay using Virtual Accounts.\ <br />\
  To accept VA payment in either Payment Link or Direct VA, you need to have at least one VA payment method active in your merchant account.\ <br />
  * Payment link settings **(Optional)**:\
    This is an optional configuration to modify what payment method you want to show, and specific payment settings for VA and Card Payment. Some settings (e.g. payment method expiry time or Payment Link logo/branding) needs to be set in Snap Preference so ensure your Snap Preference is updated as well. You can choose to skip modifying this section if not needed. If you want to set the expiry time to be specific time period after Posting date / at a specific date, choose Expiry Date as custom.
  * Virtual Account settings **(Optional)** :\
    By default, VA bank will be chosen from the default bank set in Invoice settings. You can also optionally define the Custom VA number here (e.g. in case where you want to assign a static VA number to each customer). Please do note all typical custom VA behaviour and limitation applies here; such as if VA number has been used in a Pending transaction within Midtrans's system, Midtrans will automatically generate a random VA number instead during Invoice generation - or that VA number with short number length will automatically be appended with trailing zeros.\ <br />
* **Product List** ***(Required*)** :  Products being sold and billed using Invoicing. **Price, quantity and Descriptions are mandatory to be filled**. You can add up to 30 products here.
* **Discount, tax and shipping fee** ***(Optional)*** : Add discount, tax and shipping amount in this section. This section is optional - if filled, they will be shown before the final Total amount in the Invoice PDF.

<br />

## Sales Quotation

Streamline your B2B negotiations by sending professional proposals and seamlessly converting them into payable invoices once your customers approve.

* Unified Creation Flow: Select Sales Quotation as your document type directly from the standard "Create Document" page.
* Custom Validity: Define a quotation date and a validity period (expiry date) to ensure your offers are time-bound. If the date passes, the quote automatically transitions to an Expired status.  Quotation date and validity can be different from Invoice date and expiry date.
* Status Tracking: Monitor your deal pipeline with built-in statuses: Draft, Published, Accepted, Rejected, Expired, and Voided.
* Terms & Condition : provide a custom T\&C for your Quotation. T\&C will be different from the T\&C provided for Invoice.
* One-Click Conversion: When a customer approves a Published quotation, simply select Accept to automatically generate a Pending invoice. All relevant details, including customer info and line items, carry over to eliminate duplicate data entry.
* Easy Sharing: Generate unique, shareable URLs or download PDFs to send quotes directly to your leads via their preferred communication channel.

After publishing, you can either Accept, Void, or Reject a quotation from the three dots action menu in the landing page, or from the Document Details page.

* Accept : indicates customer has accepted the quotation. The document then will be updated and converted automatically into an invoice - an email then will be sent to customer (or you can manually share the text template / PDF files) containing the invoice PDF and payment methods
* Void : choose this to void or cancel the quotation for any reason.
* Reject : choose this if customer rejects your quotation.

By choosing the correct action between Void and Reject, you can record which quotations are rejected, and which quotations are cancelled due to non rejection reasons (e.g. needing to change some details etc).

<br />

## Tax modes

Match your invoices to your internal pricing models and Indonesian tax compliance requirements effortlessly. You can configure default tax settings in your dashboard, which will automatically apply to new invoices, or you can manually adjust them on a per-invoice basis.

Tax Modes :

* No Tax : no tax will be added to your pricing.
* Tax Exclusive : Enter your base product prices. The system calculates the selected tax amount and adds it on top of your subtotal to determine the final amount due.
* Tax Inclusive: Enter your final product prices. We automatically back-calculate the tax portion embedded within each item. Your customers will clearly see the calculated tax amount broken down on their PDF ("Includes \[Tax Name]"), while the total amount due reflects the exact prices you entered.

Custom Tax Settings :

* Preset Options: Quickly apply standard Indonesian tax rates, such as PPN (11%) or PPh 23 (2%), using our pre-filled dropdown options.
* Custom Taxes: If your business requires a different tax structure, you can create a custom tax profile. Simply define a custom tax name and specify the rate as either a percentage or an exact nominal amount.

<br />

## Creating and deleting a draft

<br />

You can save your progress and save it as draft by clicking the `Save draft` button in the top right side of the Create Invoice form. You can also delete the draft by going to the Draft details (click the specific Invoice number in the Invoice list page), then click the `Delete` button in the top right.

Draft information can be filled with incomplete information, but do note that all information needs to be valid and complete once it's ready to be published.

<br />

## Duplicating a document

<br />

<Image align="center" alt="Duplicate an invoice" caption="Duplicate an invoice" src="https://files.readme.io/3c7a196-Duplicate.PNG" />

<br />

You can duplicate from a published invoice to create a new draft already populated with all of the previous information. Some important things to note :

* **Order ID and Invoice Number** will be generated with a new random UUID, as Order ID and Invoice Number cannot be duplicate with any pending transaction or open invoice, respectively.
* **Invoice date** will be duplicated as it is. That means, an Invoice date can potentially change into a backdate, if said invoice is duplicated later than today's date.
* **Invoice due date** will be adjusted to today's date if the original Invoice due date is earlier than today's date.

<br />

## Publishing and sharing your invoice or quotation

<br />

Once ready, publish your document by clicking the `Preview and send` button in the top right side of Create invoice page. If your inputted data is valid, you will see the final preview of the PDF. Click the `X` button if you want to go back and edit your document, otherwise click Send.

**If you input your customer's email when creating the document,** an email will be sent to your customer notifying of an outstanding invoice or a new quotation offering, containing the PDF as attachment, and link to pay / direct VA number in the email body for Invoice.

**If you do not input your customer's email when creating the document,** you will need to download the PDF and share the PDF to your customers manually, either by sharing the PDF file directly, or sharing the template text generated via the preferred channel of your choice..

To download the PDF, there are two ways to do this :

* Download from the Document List page : go to the rightmost side of the table row, click the `...` button in the actions column, then click `Download PDF`.\ <br />

  <Image align="center" alt="Download PDF from Quick Actions" caption="Download PDF from Quick Actions" src="https://files.readme.io/d548a3f-Download_PDF.PNG" />

  <br />
* Download from the Document detail page : from Document List page, click the Document No to be redirected to Document Detail page, then click the   `Download PDF`  button in the top right side of the page.

  <Image align="center" alt="Download PDF from Invoice Detail Page" caption="Download PDF from Invoice Detail Page" src="https://files.readme.io/dda3fbc-Download_PDF_from_Detail.PNG" />

<br />

**You can also share a template text containing the PDF download link and Payment Link URL or Direct VA number** by copying the text from Document Details. Then share said text to your customer via your preferred channel.

<br />

***

<br />

# After publishing an invoice or quotation

<br />

It's highly recommended to input your customer's email when creating an invoice or quotation in order to fully utilize Invoicing's features designed to streamline your collection process and increase the chance of your invoice to be paid.

In the event when an email address is inputted, Midtrans will send the following emails to your customers  :

1. **Notification of an open invoice / offered quotation** will be emailed to your customer. Said email will contain invoice /quotation information, payment link URL or direct VA number (for Invoice only), and an attachment of your PDF.
2. Midtrans will programmatically send additional emails to your customers whenever the **document status is updated**. This way, your customer will be updated in regard of the invoice or quotation status.
3. Additionally, your customer will be notified every time **the transaction status changes**, in the event where customer has started a payment via Payment Link, or is expected to pay via a Direct VA. This is useful to notify customers in case there are problems with their payments (e.g. payments get rejected) or when there are changes to their successful payments (e.g. payment gets refunded or cancelled).
4. **Invoice Reminders** will also be sent to your customers according to the reminder schedule specified in the Invoice settings.

If needed, you can also retrieve the PDF files and copying the payment link URL/direct VA number via the quick actions in the Document List page, or Document Details page. Text template can be copied from the Document Detail page only.

<br />

***

<br />

# Getting paid

<br />

There are two methods of getting paid via Midtrans's invoicing - one is via a virtual account number generated for the sole purpose of this invoice, and the other is via Payment Link.  You can only choose either one of the two method for each invoice created.

Please do note that you need the relevant payment methods to be active in your merchant accounts in order to use it to accept payments for your invoices.

**Important note : B2B/Open amount VA type as a payment method is not yet properly supported in this beta phase. Please refrain from using it, otherwise invoices using B2B/Open amount VA will not properly marked as paid.**

<br />

## Direct Virtual Account

<br />

<Image align="center" alt="Direct VA Number as shown in Invoice PDF" caption="Direct VA Number as shown in Invoice PDF" src="https://files.readme.io/35a11e0-VA_PDF.PNG" width="70% " />

<br />

You can opt to generate a virtual account number and attach it directly to your Invoice PDF - that way your **customer can copy and pay the VA number directly without having to navigate through a payment link each time**, and potentially even save the VA number in their transfer list if the VA number is customized for each client via the custom VA number feature. This is useful for customers that you know only wants to pay bank transfer.

Some acquiring banks support open loop virtual account such as BRI, Permata, BNI and CIMB - open loop means that said VA number can be paid using any banks in Indonesia. You can choose with acquirer to generate the VA number for you when creating an invoice via the Bank dropdown field; do ensure that you have the corresponding banks active in your Midtrans's merchant account in order to use it. If not, you can apply to activate your desired banks via the Payment Method menu in Midtrans's dashboard.

Do note that once a direct VA number has expired; payment can no longer be done to the associated invoice and invoice subsequently will be marked as `Expired`. In cases where customer wants to attempt repaying again, we recommend to duplicate and issue a new invoice instead. Otherwise, you can also set the VA expiry time in Invoice settings to be longer (up to 180 days) than the Invoice due date, so that customer can still pay even if the invoice is already `Overdue`.

<br />

> 🚧 Notable Custom VA Number Behaviour
>
> VA number needs to be unique within Midtrans's system; that means there could not be any transactions with `Pending` status with identical VA number. As such, if you're creating an invoice with a custom VA number per client; ensure the previous open invoice has been paid first before issuing a new invoice with the same custom VA number; otherwise VA number for the newer invoice will be randomly generated due to the conflicts.
>
> If you need to use the custom VA number feature and have multiple open invoices at the same time, we recommend to create multiple custom VA numbers reserved for said clients instead.
>
> If you're creating a VA number with shorter number length than the provided instruction, trailing zeros will automatically be appended to said number.
>
> For merchants using Permata VA `pretty VA number` feature, as it only supports phone number as a custom VA, reinput your client phone number into the custom VA number; otherwise a random VA number will be generated.

<br />

## Payment Link

<br />

Create a payment link for your customers to pay. With payment links, you can offer and accept a wide array of payment methods (e.g. cards) to your customers. To pay, customer simply need to click on the link provided, choose a payment method, then follow the instruction to pay.

In Invoicing, payment link generated will be a single use payment link, closed amount payment link only. Single use here means that customer can reattempt to pay multiple times using the same link, until 1 transaction in Pending/Capture/Settlement state is generated - in which case payment link can no longer be used to pay. If payment does not succeed, said link can be reused again by customers to pay.

Just like VA, payment link has an expiry time, which can be set even longer than the invoice's due date (up to 2 years). Each payment method expiry time however will follow the expiry settings in Snap Preference settings page. In the scenario where customer has generate a payment (e.g. payment code) but soon after payment link URL expires, invoice status will only be updated to `Expired` if the generated payment code has expired.

<br />

***

<br />

# Track and automatically reconcile your invoices with payments

<br />

Invoice created via Midtrans Invoicing will have its status be programmatically updated according to the payment status as long as the payment is made via Midtrans (see below for more information on Invoice statuses). You can track the status of an invoice from the [Invoice List](https://dashboard.stg.midtrans.com/invoices) page. Additionally, you can also download the tables as a CSV report via the `Export CSV` button in the top right side of the page.

In order to download the report, ensure to Filter the page first to narrow down the date range of at least one of the date filter to be under 31 days.

You can also search for invoice using specific properties of the invoice e.g. customer details, invoice no etc using the Custom Filter. Up to 3 keywords can be searched - Invoicing will then return the list of invoices that matches all 3 keywords.

<br />

***

<br />

# Understanding Invoice status and dates

<br />

## Invoice status

<br />

Invoices move through different statuses from the time they’re created to when they’re paid. Below is the explanation of each statuses :

* `Draft` : Invoice form is already filled and saved as draft, but hasn't been published yet. At this state, invoice can still be edited.
* `Pending` : invoice has been published and currently awaiting payment. Pending invoice cannot be edited anymore.
* `Paid` : a payment has been successfully received for the associated invoice. You can still refund/cancel the payment via Transaction page, however Invoice status will stay as `Paid`.
* `Expired` : all means of payment has expired, hence Invoice is no longer possible to be paid. This status can be triggered if either a) Direct VA has expired, or b) Payment Link URL has expired and there's no pending payments generated by Payment Link. In the event where Payment Link URL has expired but there's a pending payment (e.g. pending QRIS payment generated from Payment Link), Invoice will only change status to `Expire` once said payment has expired.
* `Overdue` : invoice will change status to `Overdue` if invoice has passed the invoice's due date. Invoice can still be paid however - there are no notable effect of an invoice being marked as `Overdue` other than for merchant's tracking purposes. Automated reminder will still be sent as per the schedule.

<br />

## Important `dates` in Invoice

There are several dates shown in Invoices that mark the different stages of an invoice's lifecycle. Below is the explanation of each dates  :

1. Quotation date : the date that the quotation starts to be valid. This will only show up if you choose to create a Sales Quotation
2. Quotation validity / valid until : Quotation validity date. Once passed, the quotation will expire and can no longer be used.
3. Invoice date : the date of the invoice; can be used to represent the date on which the goods have been billed and the transaction officially recorded. This date is fillable by merchant; accepts both backdate and future date (up to 2 years of forward/backward looking).
4. Due date : date where the invoice is expected to be paid by customer at the latest. This date is fillable by merchant and accepts any date later than today's date up to 2 years. If due date is passed, invoice will be marked as `Overdue`.
5. Creation date : non modifiable, system generated date that represents the invoice creation date (either as a draft or a published invoice). Creation date is used to sort the invoices from newest to oldest in the Invoice List page.
6. Posting date : non modifiable, system generated date that represents the date when invoice is published, and subsequently marked as `Pending`.

<br />

***

<br />

# Adding e-Meterai to Invoice

<br />

Now you can add e-Meterai to your invoice that will enhance legal validation to your invoice, ensure compliance with tax regulations, and prevents fraud.

To use, tick the e-Meterai box to use e-Meterai. Fee (Rp13.000) will be reserved from your pending payable amount (can be viewed via [Balance ](https://dashboard.midtrans.com/beta/balance)page) the moment your invoice is posted and deducted from your pending payable amount by the end of the day. Your reserved amount might not be reflected in your remaining pending payable amount before the end of the day, so make sure to also take into account your e-Meterai purchases on that day to calculate your available pending payable amount to purchase e-Meterai, otherwise your purchase might fail.

Pending payable amount is calculated from your successful transactions that haven't been settled to your Withdrawable Balance yet. If for some reasons you don't have enough balance, you can increase your balance by having new successful transactions with amount > Rp13.000. The simplest way to do this is by creating and completing a transactions via Payment Link - to do so, follow below steps :

1. Create a Payment Link and input enough amount to purchase e-Meterai (Rp 13.000/e-Meterai + your Midtrans fee).
2. Open the created link and complete the payment.
3. Return to the invoice page and click refresh balance if the balance is not updated.

<br />

Afterwards, you'll be able to see a preview of the e-Meterai in your invoice preview. You will then be charged once the Invoice has been successfully published.

***

# Formatting Notes and T\&C via Markdown

<br />

<Callout icon="📘" theme="info">
  **Upcoming feature**

  This is an upcoming feature - watch out for this space or our docs's landing page once the feature is released!
</Callout>

Midtrans supports Markdown, a lightweight way to add formatting to your notes, descriptions, and internal logs. This helps you organize information - like payment terms or internal instructions - so they are easy for your team to read at a glance.

**Quick Syntax Guide**

Use these simple characters to style your text instantly:

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Style
      </th>

      <th>
        Syntax
      </th>

      <th>
        Result
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **Bold**
      </td>

      <td>
        `**Text**`
      </td>

      <td>
        **Text**
      </td>
    </tr>

    <tr>
      <td>
        _Italic_
      </td>

      <td>
        `*Text*`
      </td>

      <td>
        _Text_
      </td>
    </tr>

    <tr>
      <td>
        Lists
      </td>

      <td>
        `- Item`
      </td>

      <td>
        * Item
      </td>
    </tr>

    <tr>
      <td>
        Links
      </td>

      <td>
        `[Label](URL)`
      </td>

      <td>
        [Item]()
      </td>
    </tr>
  </tbody>
</Table>

<br />