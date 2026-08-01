---
updatedAt: 2026-01-26T11:59:39.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Promo Management

> 📘 What's new
>
> * Daily budget / redemption limit can now be implemented on top of the overall campaign budget.
> * Voucher code redemption is now supported.
> * Support for all payment methods - now you can create promo for not just card payments, but also for all payment methods supported by Midtrans.
> * SKU based promotion - run promotions that's applicable if your customer purchases a specific item(s) only.

<br />

# Introduction

<br />

Midtrans Promo Engine is an exclusive feature of hosted checkout page (Snap and Payment Link) integration, where merchant can easily run promotion without any additional code or technical development. From promo campaign creation to implementation in the checkout page can be set via dashboard without any technical capabilities needed.

Promo Engine makes it easy for merchant to perform the following operations :

* Implement promotion directly in the checkout flow\
  If promotion is active and customer is eligible, customer will see a promo sticker next to the payment method selection in Snap's payment list. Customer then can choose which promotion they want to apply to their transaction, and final amount will be deducted before customer clicks pay. Note that user can only choose 1 promotion within a transaction.

<br />

<Image border={false} src="https://files.readme.io/40a3fc2-midtrans_promo_engine.gif" title="midtrans promo engine.gif" />

<br />

* Budget control\
  Set maximum budget (max IDR budget, trx cap, or both) per campaign. Once the budget runs out, campaign will be automatically deactivated, ensuring that merchant will not spend more then the allocated budget.

* User maximum transaction cap\
  Limit the number of time a user (defined by either email, phone number or card number) can transact using a promotion according to the campaign rules to prevent promo abuse or fraud.

* Implement BIN based campaign\
  For card payment specific promotions, limit which card BINs would be eligible to receive promotion, according to partner bank's terms and conditions.

* Set campaign active period\
  Set the time period when the campaign will be active - once campaign has passed the set date, campaign will automatically deactivate.

* Set campaign recurrence\
  Set when campaign will be applicable (certain day of the week, certain date of the month) or the frequency (reset campaign's user cap every day, every week, or every month).

* Promotion reporting\
  Easily download promotion reports for merchant's own recon activities or to be shared with bank/payment's partners, via Midtrans's dashboard or Promo Engine's dashboard.

<br />

***

<br />

# Activating and Logging in to Promo Engine

<br />

To activate Promo Engine on your merchant account, activate first via [Midtrans's Dashboard's Payment Methods](https://dashboard.midtrans.com/new_payment_method) page for feature activation. Once done, you will be able to see the Promo menu in your Midtrans's dashboard.

Promo Engine is automatically activate in Sandbox. If you didn't see the menu in your dashboard, contact our support team and request for feature activation in Sandbox.

<br />

***

<br />

# Creating Promo Campaigns

<br />

> 🚧 Transaction counted as successful transaction in Promo Engine
>
> Transaction with the status `PENDING`, `CAPTURE`, or `SETTLEMENT` with the promo applied during checkout in Snap's page is counted as a successful transaction and will deduct the allocated budget/user cap set in the campaign. If the transaction's status is `CANCEL`,  `EXPIRE`, or `FAILURE` however, the campaign's promo limit from said transactions will be replenished.
>
> Example :\
> A promo campaign is set with a budget limit of 1,000,000 IDR. If a transaction with a 10,000 IDR discount applied was made by customer and transaction status is `CAPTURE`, budget will be deducted and 990,000 IDR is left. However if transaction is cancelled later on; 10,000 IDR will be returned back to the budget limit, making the budget limit of said campaign back to 1,000,000 IDR.

<br />

Promo campaigns can be created by going to Midtrans Dashboard > Promo > Create Promo.  You can save the campaign as draft first by ensuring that the **Promo will be automatically active during the promo period** tickbox in the **Promo Period** section is left unticked when clicking the **Submit Promo** button. It's very important to note that **campaigns' budget and terms cannot be modified once set to active**.

To deactivate a campaign, go to the Promo List, click the `...` menu on the right side of the table, then click Deactivate.

<br />

<Image border={false} src="https://files.readme.io/02f6008-image.png" />

<br />

To create a campaign; set your promo details, discount terms, promotion's budget, customer's max transaction limit, and promo period within the promo creation page.

<br />

## Promo Details

***

<br />

Fill in the following promotion details upon creating a campaign :

* Name\
  Promotion name. This will appear as the promotion name that customer can choose in Snap's checkout page.

* Sponsor Name\
  Input the provider who sponsors this campaign. This will be available as filterable information in the Promo page.

* Promo code\
  Promotion unique code, used as promo identifier within Promo Engine. Promo code needs to be unique for every campaign.

* Payment method\
  Specify the payment methods eligible for this campaign. Multiple selection is supported.

* Promo period\
  Tick the **Promo will be automatically active during the promo period** checkbox in the **Promo Period** section if you want to activate the campaign which will run on the defined date, otherwise it will be saved as draft and needs to be activated manually. You will also need to specify at least the promo start date. If no end date is specified, promo will run indefinitely.

<br />

## Discount Terms

***

<br />

### Discount Type

Set the discount type between Fixed Amount, Percentage or Combo (Fixed Amount & Percentage). This section is mandatory to be filled.

* **Fixed**

<br />

<Image border={false} src="https://files.readme.io/8b5d36c-image.png" />

<br />

Fixed discount will discount the transaction over a fixed amount. If discount amount exceeds the total transaction amount, final transaction amount will be zero - be careful as this might cause the transaction to fail as some payment method/banks do not support transaction below a certain amount.

Example :\
If you set the fixed discount amount to 10,000, and total transaction amount prior to discount is 100,000 - once applied by customer, final transaction amount that will be charged to Midtrans and customer will be 90,000 IDR.

<br />

* **Percentage**

<br />

<Image border={false} src="https://files.readme.io/5478185-image.png" />

<br />

Percentage discount will discount the transaction based on % set in the `Discount Amount` field..  If discount IDR amount exceeds the total transaction amount, final transaction amount will be zero, same caution above applies.

Example :\
If Discount Percentage is set to 10%, and total transaction amount prior to discount is 100,000 - once applied by customer, final transaction amount that will be charged to Midtrans and customer will be 90,000 IDR.

<br />

* **Fixed Amount & Percentage (Combo)**

<br />

<Image border={false} src="https://files.readme.io/ec2c1b6-image.png" />

<br />

Combo discount will apply % based discounts with maximum IDR amount of discount, whichever IDR discount amount is lower (either the % based discount or maximum IDR amount) will be applied to the transaction.

Example :\
If discount percentage is set to 10% and fixed discount amount is set to 10,000 - if a transaction with basket size of 1,000,000 is made by customer and promotion is applied; IDR 10,000 will be discounted from the transaction (making the final amount charged to Midtrans 990,000) as 10% of the transaction amount is greater than the maximum discount amount (IDR 100,000 vs IDR 10,000).

<br />

### Minimum transaction amount

<br />

Set the minimum transaction amount (basket size) eligible to receive promo and discount type in this section.

<br />

<Image align="center" border={false} width="70% " src="https://files.readme.io/b8055e8-image.png" />

<br />

Tick the `Minimum transaction amount` in the Advanced Settings section if you want to enable promo for transaction with basket size (before discount is applied) to be at least a certain amount. Customers who makes transactions with gross amount below the set minimum amount will not be shown this promo.

<br />

<br />

## Promo Budget

***

<br />

**Promo Budget** section in the promo creation page allows you to set a maximum budget for your promo campaign. Untick it to set the promo campaign to run without regard of campaign budget until the end of specified promo period. If set to Yes, your campaign will only run until the set limit is reached, then campaign will automatically deactivate. Budget limit can be set by transaction amount, transaction count, or a combination of both.

<br />

<Image border={false} src="https://files.readme.io/107981f-image.png" />

<br />

### Budget amount

<br />

<Image border={false} src="https://files.readme.io/58aee82-image.png" />

<br />

`Budget amount` will limit the promotion up to your total allocated IDR budget for the whole campaign. If the `budget amount` is exceeded, the promo can no longer be used.

Example :\
If you set the `Budget amount` as 100,000,000 - and then you have 1000 transactions which have redeemed the promotion amount accumulated to a total of 100,000,000 - the 1001st transaction going forward will not see any promotion option in Snap checkout page and be processed as normal.

<br />

### Promo quota

<br />

<Image border={false} src="https://files.readme.io/8b374b6-image.png" />

<br />

Limit the promotion for x number of transactions only. If the transaction count is exceeded within the promo period, the promo can no longer be used by customer.

Example :\
If `promo quota` is set to 100, and 100 transactions from various customers have successfully used the promotion, the 101th transaction going forward will not see any promotion option in Snap and be processed as normal.

<br />

### Budget amount & promo quota

<br />

<Image border={false} src="https://files.readme.io/eb83db6-image.png" />

<br />

Combine both `Budget amount` and `Promo quota`. Whichever condition is met first will deactivate the campaign.

Example :\
If you set the `Budget amount` as 1,000,000 and count to 10 - and then you have 10 transactions which have redeemed in total 900,000 IDR worth of discount before the campaign ends - the 11th transaction going forward will not see any promotion option in Snap and be processed as normal.

<br />

### Daily Budget

<br />

<Image border={false} src="https://files.readme.io/930e055f6335ebc31cb4630047f3f623b61e204ed6cba363fdcb75485ccbf9f0-image.png" />

<br />

<br />

You can also implement a daily redemption limit on top of the overall campaign budget, to prevent premature over redemptions.  How it works :

* Once the daily redemption limit (e.g. 100 transactions) is reached, no more promo redemptions will be allowed that day
* Limits reset automatically at the start of each new day
* Daily budget limit type can differ from the overall budget limit (e.g. overall budget limit in IDR, daily limit in count of trx and IDR)

***Sample Scenario***\
Merchant can set a budget for the overall campaign and introduce an overall daily redemption limit (shared across all customers) to prevent budget being spent too prematurely. For example :

Campaign overall budget : 100 mil\
Max daily redemption  : 10trx and 10mil

After there are 10 trx with promo redeemed or discounts redeemed up to 10 mil on a particular day, no promo will be available anymore for that day.

<br />

## Promo Period

***

<br />

This section governs how long the campaign will be active (and with it, the budget calculation time).

Tick the **Promo will be automatically active during the promo period** checkbox in the **Promo Period** section if you want to activate the campaign which will run on the defined date, otherwise it will be saved as draft and needs to be activated manually. You will also need to specify at least the promo start date and time. If no end date is specified, promo will run indefinitely.

<br />

## Promo Schedule

***

<br />

This section governs when promotion will be available for customers.

<br />

* `Daily - at selected time` : campaign will be active everyday within the specified hour. Outside of specified hour, promo will deactivate and be automatically reactivated again on the next calendar day within the specified hour.

<br />

<Image border={false} src="https://files.readme.io/4f0147f-image.png" />

<br />

* `On selected days` : campaign will be active on certain days of the week (multiple days selection are supported), within the specified hour.

<br />

<Image border={false} src="https://files.readme.io/8d2d60c-image.png" />

<br />

* `On specific dates` : campaign will be active on a certain date of the month (range between 1-31, multiple inputs are allowed separated by comma) and specified hour. Example : if you want to set up a payday period campaign that occurs every month on 25-27th day, type `25,26,27` into the `Enter specific dates` field.

<br />

<Image border={false} src="https://files.readme.io/19b608a-image.png" />

<br />

> 🚧 Budget calculation
>
> `Promo schedule` does not affect budget calculation - say that if you set it to `Daily - at selected time`, budget calculation will not be reset daily. Instead, it will follow the start date and end date set in the `Promo Period` fields (or never reset if on End Date is specified in Promo Period).

<br />

<br />

## Promotional Product

<br />

> **Note** :
>
> SKU based promotion might not work with Shopify, as it's a Shopify's known limitation where Shopify might not forward SKU information to payment gateway's extensions. Please verify your integration first before proceeding.

<Image border={false} src="https://files.readme.io/2814cb9-image.png" />

<br />

Set up cart level promotions in this section. This feature can be combined with other promo criteria, e.g. credit card specific rules. Promo engine will check the eligibility of the cart based on information passed on Snap Checkout's [`item_details` object.](/reference/json-objects#item-details-object) or Payment Link's `Items` information.

To set up, specify the following information :

a. **Promo Eligibility**

Specify how a cart will qualify for the promotion. There are two variants supported :

* *Cart only contains the selected product*\
  Transaction will only be eligible for promotion if cart (or item information passed in Snap Checkout's `item_details`) has only promoted items, nothing else.\
  E.g. if promo is set up to qualify for `phone cables` only but user purchases `phone cables` and `mobile phone`, said transaction will not qualify for promotion.
* *Cart contains at least 1 selected product*\
  Transaction will eligible for promotion if cart has at least 1 of the specified items in the campaign. Only qualified items will be discounted.\
  E.g. if promo is set up to qualify for `tea`, `coffee` and `juice`, and user purchases `tea`, `coffee` and `water`, the transaction will still qualify for promotion, with only `tea` and `coffee` getting discounted.

b. **Product Identifier**

Specify how Promo Management will identify eligible product within the cart / `item_details` object. You can choose between 4 types of parameters provided in the `item_details` object in Snap Checkout, which is SKU ID (corresponds to `id`), Product Name (corresponds to `name`), Product Category (corresponds to `category`), and `Brand` (corresponds to `brand`). See the `item_details` object docs to check what kind of inputs are accepted.

Additionally, Promo Management will check eligibility based on case insensitive exact match, e.g. if you specified `Tea` when creating the campaign, only `Tea` or `tea` passed in the `item_details` will be considered as; but variations such as `teacups` or `green tea` will not be considered as eligible.

Once you have selected which identifier to use, you can specify the list of eligible values - separate each value with comma without space in between of values. Note that transaction/cart needs to contain at least 1 of the specified product in order to be eligible for the promotions.

c. **Min & max quantity of SKU**

An optional limitation that you can set to check the minimum and maximum quantity of the product that’s eligible for promo. See example below for further details.\
E.g : Say that you specify a campaign of discount 10%, eligible for cart containing products of `tea` and `coffee`, with min quantity of 1, and max quantity of 2. A user then purchases 2 teas @ 10k IDR each and 3 coffees @ 15k IDR each. As such, only the 2 cups of teas are eligible for the discount, hence the total discount will be 2 x 1k IDR = 2K IDR total.

<br />

## Voucher Code Redemption

<br />

You can now create a voucher code based promotion where customers will need to input a certain promo code in order to be able to use the promo. This feature can be combined with all other features (e.g. Budget, Credit Card Rules, SKU Based Promotion, etc).

There are two types of voucher code redemption available, single voucher and bulk vouchers.

<br />

### Single Voucher Code

<br />

Single voucher code feature will allow you to create a promotion campaign where user can redeem 1 generic voucher code. This is useful to for evergreen or thematic campaigns e.g. newsletter subscription campaigns, new user campaigns, theme specific campaigns (e.g. Anniversary promo) where there's only 1 generic code that can be used by all users.

In order to limit usage per customer, you will need to specify the customer limit at the Promo Usage Limit section.

<br />

<Image align="center" border={false} width="75% " src="https://files.readme.io/98f76d0-image.png" />

<br />

If single voucher code method is used, promo will use the previously defined Promo Code (in the General Settings section) as the voucher code.

**OPTIONAL** - You can also perform a check to make sure the voucher code redeemed is eligible for said transaction (e.g. for event promotion campaigns, you'll want user to enter the correct event code within the relevant Snap Checkout transaction page. If you checklist the `Allow redemptions if matches custom fields` option, Snap Checkout page will check that the promo code redeemed matches the value provided in any of the [custom fields](https://docs.midtrans.com/reference/request-body-json-parameter).

<br />

### Bulk Voucher Code

<br />

Bulk voucher code feature will allow you to generate multiple voucher codes within 1 campaign that can be redeemed once per purchase. This is useful for campaigns e.g. user specific campaigns.

There are two ways to generate the codes, one is where Midtrans auto generate it for you, or you upload a CSV containing the codes.

* **Auto generate code**

  <Image align="center" alt="Create promo with multi voucher codes" border={false} caption="Create promo with multi voucher codes" src="https://files.readme.io/56c33a3-image.png" width="70% " />

  If you let Midtrans auto generate the code for you, you can define the properties such as the length (excluding prefix), quantity of codes, prefix (optional), and whether you want to include a separator between prefix and code. Check the preview first to see whether the sample code looks right, then submit the promo.\
  Afterwards, you can go to the promo details (by clicking anywhere within the table row of the campaign in the Promo landing page) to download the voucher codes, see the # of used promo, and top up the generated codes.

  <Image align="center" alt="Voucher code usage in Promo Details" border={false} caption="Voucher code usage in Promo Details" src="https://files.readme.io/cf06e7a-image.png" width="60% " />

<br />

* **Bulk upload CSV**

  <Image align="center" alt="Upload result" border={false} caption="Upload result" src="https://files.readme.io/92edf94-image.png" />

  If you already have your own codes, you can choose to upload it as a CSV file instead. Download the provided template and fill in your codes according to the template, then upload the file.\
  Afterwards you will see the result - if there are mistakes with the template (e.g. invalid codes) you will be able to see the result in CSV format, and then to either choose to proceed with the correct codes only, or fix the file by reuploading.

  Afterwards you can check in the promo detail by clicking anywhere within the table row area of the campaign. You can check the voucher codes redemption, download the list of the redeemed codes, or top up the codes stock by reuploading more vouchers.

  <Image align="center" alt="Redemption statistics" border={false} caption="Redemption statistics" src="https://files.readme.io/b3fe05b-image.png" width="70% " />

<br />

## Credit Card Rules

***

<br />

<Image border={false} src="https://files.readme.io/3556a55-image.png" />

<br />

You can set promo limitation specific to card payment properties in the `Credit Card BIN and installment` section. Setting this section is **optional**; if not needed, then leave the checkbox unticked or leave it as empty.

<br />

### Credit Card Bin

Activate promo only for transactions using card with specific BIN number. BIN number typically comprises of 6-8 digits, but here you can specify the BIN digit up to 8 digits For example, if you want the promo to be activated only for Mandiri cards, simply adding 46170069 in the input field will enable the promo option only for customers who use cards beginning with 46170069. If you want to make this applicable for all Visa cards - you can simply input 4 into the field.

You can also input multiple BINs by separating them with commas such as 46170069,52642210,45992078 (no space).

Please note that we highly recommend filling in 8 digits Card Bin in this input field.

<br />

### Installment

Tick all the eligible the Installment Terms options. If not set, promo will be applicable for all type of transactions.

<br />

## Promo usage limit

***

<br />

<Image border={false} src="https://files.readme.io/675e2a5-image.png" />

<br />

### Setting the max count per customer

You can set how many times a customer can use the promotion within a certain time period. If customer exceeds the cap set here, the subsequent transaction made by said customer will proceed as normal without promotion applied.

A customer is defined by a unique card number, phone number or email address - promo engine will count transactions made by each card, phone number and email. If all three limitation fields (shown in above picture) are filled and customer is using the same credentials across three fields, whichever limit is met first will deactivate the promotion for said customer's transaction. These fields are **optional**.

Example :\
If you set the max trx limit as follows,\
a. 1 trx per card\
b. 2 trx per email\
c. 3 trx per mobile phone number.

If customer using card A, email B, and phone number C across all of their transactions, the first transaction will be eligible for promo, but 2nd transaction going forward will no longer be eligible for promotion since max cap per card has already been met, even though cap per email or phone number hasn't been met yet.

If customer however changes card for their second transaction, customer will be eligible for promotion on their second transaction as no max cap is met as of 2nd transaction.

<br />

### Setting the timeframe of customer's limitation

<br />

<Image border={false} src="https://files.readme.io/c7116fb-image.png" />

<br />

The previously set customer's limitation period can be set in the `Reset cycle of promo usage` section. Once the timeframe has been exceeded, customer's limit will be reset and customer can use the promo again. If not set, each customer's quota will not be reset until the end of campaign.

Example :\
If limitation timeframe is set as `End of day` and max transaction cap is set as 1, if customer has made a transaction and used promo today on 11PM GMT+7, customer can only use the promo again from said campaign as early as 00:00:01 GMT+7 the following day.

<br />

There are 3 types of timeframe :

* End of promo period\
  Customer's limitation will last as long as the campaign is active. Once customer's transaction limit is met, customer can no longer use the promo until the campaign ends.

* End of day\
  Customer's limitation will last per transaction's date (GMT+7). Once the day changed, the limitation will be reset.

* End of week\
  Customer's limitatation will last per week cycle (Monday - Sunday). Once the week is over, the limitation will be reset.

* End of month\
  Customer's limitation will last per transaction's month (GMT+7). Once the month changed, the limitation will be reset.

* Custom interval\
  Define how many days (1 day is defined as 24 hour) after transaction until the limitation will be reset. Days will be calculated from the date and time when customer made a transaction. Max days that can be set is 30 days. E.g. if you set is as 2 days and customer transact at 2023-02-14 03:00:00, then customer can use promo again on 2023-02-16 03:00:00.

<br />

<br />

***

<br />

# Downloading Reports

<br />

Download transaction as usual via Midtrans's Dashboard > Transactions. When downloading, tick the `Promo Details` checkbox which will add two columns in the report, the Promo Code (campaign unique identifier as set in the Promo Creation page), and Promo Original Amount (original transaction amount as sent by merchant prior to discount).