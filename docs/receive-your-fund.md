---
updatedAt: 2025-11-11T00:09:49.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Receiving Your Fund as Payout

Guide on how to withdraw your fund

## Billings Page Overview

<br />

Billings page displays the financial information between merchant and Midtrans.

This pages displays

* The amount of funds that can be withdrawn
* The bank account information to which the funds are disbursed
* The history of payouts

<br />

***

<br />

## Configure Billing Information

<br />

Midtrans will only payout funds to the account configured on the MAP. Please ensure that the account listed on MAP is in accordance with the Agreement (PKS). Make sure to fill out your Billing Information properly. You can change the destination account on the bank account information. You can change billing account from **BILLINGS** menu or **SETTINGS > BILLING**

<br />

To configure the billing information, follow the steps given below.

<br />

1. Login to your Midtrans Account Portal.

2. Click **SETTINGS** (1) > **BILLING** (2)

3. Click **Change Billing Information** (3) to change the Billing Information.<br />

<Image align="center" src="https://files.readme.io/75e4efa-Untitled_design_7.png" />

<br />

*Current Billing Information* screen is displayed.

4. Enter the **Account Name**.

5. Enter the **Account No**.

6. Select the **Bank Name** from the drop-down.

7. Enter the **Branch Name**.

8. Click **Save**.<br />

   ![](https://files.readme.io/5168a6a-after-payment-dash-usage-12.png)

   <br />
   A confirmation message is displayed.

9. Click **OK** to update the billing information.

   Upon successful update, *Success saved* message is displayed on the Billing screen.

<br />

If you want to configure the billing information from the **BILLINGS** menu, you can click **Change Bank Account** then you will be redirected to **Settings > Billing** menu to follow the same steps above.

<br />

***

<br />

## Scheduled Payout

<br />

Midtrans provides feature to schedule automated payout, that can be set as daily, weekly or monthly.

<br />

![](https://files.readme.io/d6d6ad5-after-payment-dash-usage-13.png)

<br />

> 📘 Minimum Amount for Auto Payout
>
> There is a minimum amount for automated payout to work, it will be shown on the page (e.g. IDR 50.000). If the amount of funds to disburse has not reached the specified limit, the system waits until the minimum is reached. If the amount is reached before the next schedule, the disbursement is processed on the next schedule. Other limitation(s) will also be shown on the page.

<br />

***

<br />

## Manual Payout

<br />

You can manually withdraw funds from Midtrans. To withdraw funds, follow the steps given below.

<br />

1. From the Dashboard, go to **Billings** menu (1).\
   Summary of the funds is displayed.
2. Click **Transfer** (2).

   ![](https://files.readme.io/2f6ad75-after-payment-dash-usage-14.png)

   The amount is transferred to the specified account.<br />

### Detail Field Description

<br />

| Field                 | Description                                                                           |
| --------------------- | ------------------------------------------------------------------------------------- |
| Total Settlement      | Amount of transaction funds that have been settled.                                   |
| Payable               | Amount of funds that can be withdrawn excluding pending-refund.                       |
| Refund                | The amount of approved refund.                                                        |
| Total MDR             | Total transaction fee (bank) for credit card payment methods.                         |
| Total Transaction Fee | Total transaction fee (Midtrans) for all payment methods, excluding MDR.              |
| Bank Transfer Fee     | Transfer fee if the payout account is on a different bank than Midtrans.              |
| Total Fee             | Total amount of fee of transactions.                                                  |
| Payable (Nett)        | The amount of funds that can be disbursed after deducting the transaction fee.        |
| Cut off Date          | You can only withdraw funds from the transactions received before the displayed date. |

<br />

***

<br />

## Transaction Fund Details Per Payment Method

<br />

To see transactions fund break down by certain payment method, follow the steps given below.

1. Go to **BILLINGS**.
2. Switch to **Select Payment Type** tab.
3. Select the particular payment method from the options provided.

<br />

![](https://files.readme.io/85cb366-after-payment-dash-usage-15.png)

<br />

The summary of transaction is displayed as shown in the figure below.

<br />

![](https://files.readme.io/c843668-after-payment-dash-usage-16.png)

<br />

***

<br />

## Payout History

<br />

Midtrans keeps a history of payout. If you click on the amount of funds, a detailed list of transactions (as source of fund) of that particular payout, is displayed.

<br />

![](https://files.readme.io/7220f19-after-payment-dash-usage-17.png)

<br />

* **Payout by Bank**: Amount of payout funds sent directly by the bank (for the facilitator business model).
* **Transfer History**: History of payout funds transfer sent by Midtrans (for the aggregator business model).