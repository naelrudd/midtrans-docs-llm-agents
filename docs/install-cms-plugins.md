---
updatedAt: 2025-11-11T00:09:23.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Install a CMS Plugins

Integrating Midtrans Snap to E-commerce Content Management System (CMS)

Content Management System (CMS) allows you to easily have a website or web store without building from scratch. CMS does not require programming knowledge. You just need to install the CMS and customize according to your requirement. Then you can focus on managing the content, without much technical work. In the context of Ecommerce CMS, it means you can easily manage your ecommerce website. Some of the examples of CMS are **WordPress**, **Magento 2**, **PrestaShop**, **WHMCS**, and so on.

Midtrans provides easy to use & install plugins for popular Ecommerce CMS, which will enable your website to accept payments from your customers. All [payment methods](https://midtrans.com/payments) available on [Snap](/docs/snap) that are activated on your Midtrans Account will become available for your website’s customers.

<br />

> 📘
>
> Want to **try Midtrans CMS payment plugins, without/before installing?** We have some demo web-stores that you can use to try the payment journey directly, [follow this section.](/docs/install-cms-plugins#bmidtrans-payment-plugin-live-demonstration-b)

<br />

***

# <b> Preparation</b>

<br />

[Sign Up for Midtrans Account](/docs/midtrans-account#register-midtrans-account-here)\
Sign up for a Midtrans Merchant Administration Portal (MAP) account, to get your API Keys for *Sandbox* environment and to test integration.

<br />

[Retrieve API Keys](/docs/midtrans-account#retrieving-api-access-keys)\
Retrieve API Keys for *Sandbox* environment that will be used for this guide.

<br />

> 📘 Note
>
> Follow the [preparation section](#preparation) to retrieve *Client Key* and *Server Key*, before proceeding to the section given below.

<br />

***

# <b>CMS Plugins and Extensions Supported by Midtrans</b>

<br />

Browse the navigation on the left for list of Content Management System (CMS) supported by Official Midtrans plugins and extensions. Step-by-step guide to install Snap integration plugin to your CMS of choice will also be explained.

Note: (un-official) 3rd party plugins from outside developer may exists out there and may support more CMSes than those being listed here. Feel free to use/try them, as most of them is useful and genuine, but Midtrans will not be able to offer support, or held responsible for the implementation of them.

<br />

***

# <b>WordPress - WooCommerce</b>

<br />

Midtrans ❤️ WooCommerce! This plugin allows secure online payment on your WooCommerce store, without ever needing your customer to leave your WooCommerce store! It has a beautiful built-in responsive payment interface. Midtrans strives to make payments simple for you and your customers. It supports various online payment channels. Midtrans supports WooCommerce v2 and v3.

Midtrans-WooCommerce plugin is also available on [WordPress plugins store](https://wordpress.org/plugins/midtrans-woocommerce/). If you cannot find it listed there, you can always download and install it manually. For more details, refer to Manual Installation.

<br />

> 📘 Note
>
> Wordpress is generally known as a generic CMS used for blogging, news, etc. But it also can easily become Ecommerce by installing WooCommerce plugin on top of it. Please ensure to install WooCommerce plugin first on your Wordpress site, so that payment feature is enabled.

<br />

## Requirements

<br />

Some of the requirements to continue with the integration process, are listed below.

* WordPress v3.9 or later **|** Tested up to v5.x
* WooCommerce v2 or later **|** Tested up to v3.5.2
* PHP version v5.4 or later
* MySQL version v5.0 or later
* PHP CURL enabled server/host
* Download Midtrans plugin for WooCommerce: [Zip file](https://github.com/veritrans/SNAP-Woocommerce/archive/master.zip) (Open source on [GitHub](https://github.com/veritrans/SNAP-Woocommerce))

<br />

## WooCommerce Plugin Installation

<br />

Select **any one** of the installation options given below.

<br />

### A. Simple Installation

To install Midtrans-WooCommerce plugin, follow the steps given below.

1. Login to your WordPress administration panel.
2. Go to **Plugins** menu.
3. Click **add new**.
4. Search for **Midtrans-WooCommerce plugin**.
5. Click **Install Now** and follow on-screen instructions.

The plugin is installed successfully. Proceed to [WooCommerce Plugin Configuration](#wooCommerce-plugin-configuration).

If you are unable to install, proceed to Manual Installation.

<br />

### B. Manual Installation

If you are unable to install using simpler method above, to install Midtrans-WooCommerce plugin manually, follow the steps given below.

1. Download the plugin file from the link given above.
2. Extract the plugin, then rename the modules folder as **midtrans-woocommerce**.
3. Upload the unzipped plugin folder to your WordPress installation's `./wp-content/plugins/` directory.
4. On WordPress administration panel, click **Install and activate** the plugin from plugins menu.

The plugin is installed successfully. Proceed to [WooCommerce Plugin Configuration](#wooCommerce-plugin-configuration).

<br />

## WooCommerce Plugin Configuration

<br />

To configure Midtrans-WooCommerce plugin, go to **WooCommerce > Settings > Payments > Midtrans** menu and follow the steps given below.

* Enter **Merchant ID**.
* In the **Environment** list, click the appropriate environment. `Sandbox` for testing transaction and `Production` for real transaction.
* Enter **Client Key**.
* Enter **Server key**.
* For more details, refer to [Preparation](/docs/snap-preparation).

Optionally configure **Button Title**. This text appears on the WooCommerce payment button displayed to the customer. Also you can configure **Button Description** too, if you wish.

> 📘 Note
>
> Other fields are optional. You may leave it as default.

The plugin is configured successfully.

<br />

## WooCommerce Plugin Notification Configuration

<br />

To configure the Midtrans-WooCommerce plugin notification URL, follow the steps given below.

1. Login to [Midtrans Dashboard portal](https://account.midtrans.com/).
2. In the **Environment** list, click the appropriate environment.
3. On the Home page, go to **SETTINGS > CONFIGURATION**.\
   *Configuration* page is displayed. Follow the steps given below.
   * Enter **Payment Notification URL**.
   * Enter **Finish Redirect URL**.
   * Enter **Error Redirect URL**.
   * Enter **Unfinish Redirect URL**.
4. Click **Update**. A confirmation message is displayed.

The plugin notification URL is configured successfully.

The table given below shows the fields and the URL.

| Field                    | URL                                            |
| ------------------------ | ---------------------------------------------- |
| Payment Notification URL | \[your-site-url]/?wc-api=WC\_Gateway\_Midtrans |
| Finish Redirect URL      | \[your-site-url]/?wc-api=WC\_Gateway\_Midtrans |
| Unfinish Redirect URL    | \[your-site-url]/?wc-api=WC\_Gateway\_Midtrans |
| Error Redirect URL       | \[your-site-url]/?wc-api=WC\_Gateway\_Midtrans |

> 📘 Note
>
> WordPress is installed in `your-site-url`. It can be the domain root directory such as `https://myshop.com` or `https://shop.myshop.com`or within a sub directory such as `https://myshop.com/wordpress/`.
>
> Please make sure to input **http\://** or **https\://** when filling Notification URL and Redirect URL, according to your web-server configuration.
>
> If you are not sure, try opening your web URL in a browser, and check the URL is **http** or **https** on the address bar.
>
> You can also test the validity of the URL by opening it (`[your-site-url]/?wc-api=WC_Gateway_Midtrans`) on your web browser, if you see the following message, then the URL is correct and valid. You can copy this current URL on your browser address bar.

![](https://files.readme.io/242d5a0-woocommerce-notif-url-0.png "woocommerce-notif-url-0.png")

<br />

## Transaction Test

1. Perform successful transaction on your online store by entering the card details given below. For more details, refer to [Testing Payment on Sandbox](/docs/testing-payment-on-sandbox).

* **Card Number**: 4811 1111 1111 1114
* **CVV**: 123
* **Exp. Month**: 01
* **Exp. Year**: 2025

2. To ensure the proper installation and performance of the plugin, examine few points given below.

| Check Point                 | Error                                     | Troubleshooting                                                                                                                                                            |
| --------------------------- | ----------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Order status in CMS backend | Order status not recorded in the backend. | Check endpoint or the *Payment Notification URL* setting on MAP.<br/> Check if your CMS or notification URL is publicly accessible.                                        |
| Merchant email notification | Notification not received.                | Check *Email Notifications* settings on MAP. For more details, refer to [Configuring Email Notifications](/docs/midtrans-dashboard-usage#configuring-email-notifications). |
| Customer email notification | Notification not received.                | Check *Email Notifications* settings on MAP. For more details, refer to [Configuring Email Notifications](/docs/midtrans-dashboard-usage#configuring-email-notifications). |

<br />

## Payment Example

<br />

![](https://files.readme.io/b09b601-woo-pay-show.gif "woo-pay-show.gif")

<br />

For more details and configurations, refer to [Midtrans WooCommerce wiki documentation](https://github.com/veritrans/SNAP-Woocommerce/wiki).

<br />

## Possible Issue: Midtrans Payment Options Isn’t Displaying on Latest Version of WooCommerce

You may encounter issue of Midtrans Payment Options isn’t displaying on Checkout Page of latest version of WooCommerce, with a message of "There are no payment methods available." like so.

<Image align="center" src="https://files.readme.io/4036aa7-Screenshot_2024-02-05_at_17.01.21.png" />

In this case, please [follow this additional steps](https://docs.midtrans.com/docs/technical-faq?id=ios-webview-specific#woocommerce-midtrans-payment-options-isnt-displaying-on-checkout-page-of-latest-version-of-woocommerce-v83).

<br />

## Advanced: Specific Payment Buttons

<br />

\[Optional] Follow these steps **if you prefer to have each payment method displayed individually in your WooCommerce checkout page**. See example below :

<br />

<Image title="woocommerce-specific-0.png" alt={1131} align="center" src="https://files.readme.io/3d54c0f-woocommerce-specific-0.png">
  WooCommerce Specific
</Image>

1. Go to **WooCommerce > Settings > Payments**, you will see **Midtrans Specific:\[Payment Method Name]**.
2. You can choose which payment methods you want to show to your customers by toggling the on-off switch. The toggle will only work for payment methods that you have activated in Midtrans. See below:

<br />

<Image title="woocommerce-specific-1.png" alt={2295} align="center" src="https://files.readme.io/7c86c07-woocommerce-specific-1.png">
  WooCommerce Specific Config Toggle
</Image>

<br />

3. \[Optional] Click each payment method's **Manage** button to configure the payment method's appearance, such as the displayed Payment Method Name & Description text.
4. Once you've finished configuring the settings, you're all set. Each of the specific buttons will use the same configurations as "Midtrans – All Supported Payment"'s [configuration](#woocommerce-plugin-configuration).
5. If you choose to display each payment method individually, it is advised to toggle off the main "Midtrans – All Supported Payment" button.

Note: This feature is only available in plugin version v2.30.0 or above - please ensure you have updated your plugin to the latest version.

<br />

## Advanced: Customize WooCommerce Order Status upon Payment Paid

<br />

\[Optional] You can configure the status that WooCommerce Order should become when an order is successfully paid. This can be useful if you want, for example, order status to become `completed` once paid (instead of `processing` as default behaviour).

Configure it from **WooCommerce > Settings > Payment > Midtrans > Manage** under configuration field **WC Order Status on Payment Paid**. Select your preferred value from the drop down.

<br />

<Image title="woocommerce-custom-status-1.png" alt={1352} align="center" src="https://files.readme.io/96f7174-woocommerce-custom-status-1.png">
  WooCommerce Custom Order Status on Paid
</Image>

<br />

## WooCommerce Midtrans Plugin Advanced features

<br />

If you have Woocommerce Subscription feature, and want to integrate it with Midtrans, please [follow this guide](https://github.com/veritrans/SNAP-Woocommerce/wiki/02---Credit-card-online-and-offline-installment).

For installment feature (when you have completed the business agreeement), you can [follow this guide to configure installment](https://github.com/veritrans/SNAP-Woocommerce/wiki#payment-methods-featured).

Further resources:

* <https://github.com/veritrans/SNAP-Woocommerce/wiki>
* <https://github.com/veritrans/SNAP-Woocommerce#readme>

<br />

## WooCommerce Midtrans Plugin FAQ

<br />

Available [on this page](/docs/technical-faq#cms-plugins).

<br />

***

# <b>Magento</b>

<br />

Midtrans ❤️ Magento! Midtrans takes customer experience (UX) seriously and tries to make payments simple for you and the customers. With this plugin you can make your Magento store using Midtrans payment. This extension is also available on [Magento Marketplace](https://marketplace.magento.com/midtrans-snap.html).

<br />

> 📘 Note
>
> This section explains the installation and the configuration for Magento 2. For Magento 1, please refer to [Snap Plugin for E-commerce CMS](/docs/midtrans-api-libraries-plugins#snap-plugin-for-e-commerce-cms).

<br />

## Requirements

<br />

Some of the requirements to continue with the integration process, are listed below.

* An online store with Magento infrastructure
* Magento 2 version 2.1.0, 2.2.0, 2.3.4 and later **|** Tested up to v2.3.4
* PHP v5.6 or later
* MySQL v5.7 or later
* Download Midtrans plugin for Magento (Please choose accordingly):
  * For Magento v2.x: [Zip file](https://github.com/Midtrans/Midtrans-Magento2/archive/master.zip) (Open source on [GitHub](https://github.com/Midtrans/Midtrans-Magento2))
  * For Magento v1.9: [Zip file](https://github.com/veritrans/SNAP-Magento/archive/master.zip) (Open source on [GitHub](https://github.com/veritrans/SNAP-Magento))

<br />

## Midtrans Snap Plugins Installation

<br />

To install Magento Snap plugin, select **any one** of the installation options given below.

<br />

### A. Installation through Magento Marketplace

You can install Midtrans Snap plugin through Magento Marketplace. Please visit Midtrans on [Magento Marketplace](https://marketplace.magento.com/midtrans-snap.html) and follow step-by-step installation instructions from the [Official Magento extension docs](https://docs.magento.com/user-guide/system/web-setup-extension-manager.html). Proceed to [Magento 2 Plugin Configuration](#magento-2-plugin-configuration) section.

<br />

### B. Installation through Composer

Install Composer and create Magento Marketplace account before installing Midtrans Snap plugin through Composer.

On your terminal, go to the Magento folder and run the commands given below.

1. Install the plugins: `composer require midtrans/snap`.
2. Enable the plugin: `bin/magento module:enable Midtrans_Snap`.
3. Execute upgrade script : `bin/magento setup:upgrade`.
4. Flush cache storage : `bin/magento cache:flush`.
5. Login to your Magento administration Panel.

The plugin is installed successfully. Proceed to [Magento 2 Plugin Configuration](#magento-2-plugin-configuration) section.

<br />

### C. Installation from GitHub project

To customize Midtrans Magento plugin to handle your business model, follow the steps given below.

1. Download the plugin file from the link given above.
2. Extract the plugin and rename the folder as Snap.
3. Make a directory structure as shown below.

<br />

![](https://files.readme.io/9597881-magento-folder-structure.png "magento-folder-structure.png")

<br />

4. Locate the root Magento directory of your shop via FTP connection.
5. Copy the app folders into the Magento root folder.
6. Run the following commands on terminal.
   * `bin/magento module:enable Midtrans_Snap`
   * `bin/magento setup:upgrade`
   * `bin/magento cache:flush`
7. Login to your Magento administration panel.

The plugin is installed successfully. Proceed to [Magento 2 Plugin Configuration](#magento-2-plugin-configuration) section.

<br />

<br />

## Magento 2 Plugin Configuration

<br />

Before you begin, install and enable Midtrans Snap plugin.\
To configure the Midtrans-Magento 2 plugin in your Magento administration panel, follow the steps given below.

1. Login to your Magento administration panel.
2. Go to **Stores(1)** > **Configuration(2)**.
3. Go to **Sales(3)** > **Payment Methods(4)**.

<br />

![](https://files.readme.io/4e88383-Magento2-7.png "Magento2-7.png")

4. In the **Midtrans - Accept Online Payment** section, click **Basic Settings** and fill out the fields given below.

| Field                  | Description                                                                                                                                                                |
| :--------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Is Production          | Select whether you want to use a *Sandbox* or *Production* environment.                                                                                                    |
| Merchant ID            | Unique id of your Midtrans account for which the payments will be processed.                                                                                               |
| Sandbox - ClientKey    | Used as an API key to be used for authorization *Sandbox* environment on frontend API request/configuration. So, it is safe to put in your HTML / client code publicly.    |
| Sandbox - ServerKey    | Used as an API key to be used for authorization *Sandbox* environment while calling Midtrans API from the backend. So, keep it stored confidentially.                      |
| Production - ClientKey | Used as an API key to be used for authorization *Production* environment on frontend API request/configuration. So, it is safe to put in your HTML / client code publicly. |
| Production - ServerKey | Used as an API key to be used for authorization *Production* environments while calling Midtrans API from the backend. So, keep it stored confidentially.                  |
| Enable Snap redirect   | Change to Snap redirect mode, the default value is **No**.                                                                                                                 |

> 📘 Note
>
> *Access Key* and *Server Key* are unique for every merchant. Always keep *Server Key* confidential.

<br />

## Storing Log Files

<br />

The plugin will store log files in directory `/var/log/midtrans`. By default, the log files are enabled for request, notification and error log. *Enable Throw Exception* is disabled by default.

![](https://files.readme.io/09a9f77-magento-log-options.png "magento-log-options.png")

<br />

## Payment Integration Configuration

<br />

The options to use Snap payment method, for Midtrans-Magento plugins are given below.

**Snap payment integration**\
This is the default option for Midtrans Magento plugin. Snap payment is enabled automatically when Midtrans plugin is installed. Midtrans shows the available payment method on the Snap payment screen.

**Specific payment integration | Optional**\
Enabling this option displays additional payment options to the customer. For specific payment that is specified in the **Allowed Payment Method** field, Midtrans Snap will show only the listed payment method on the Snap screen.

**Online Installment payment integration | Optional**\
Enabling this option displays additional payment options to the customer, for *Online Installment* payment where the *Card Issuer* and *Acquiring Bank* is the same entity. For example, if a customer makes an installment payment using BNI Card and the *Acquiring Bank* is also BNI.

**Offline Installment payment integration | Optional**\
Enabling this option displays additional payment options to customer, for *Offline Installment* where the *Card Issuer* and *Acquiring Bank* don't have to be same entity. For example, if a customer makes an installment payment using BNI Card and the *Acquiring Bank* is Mandiri.

> 📘 Note
>
> You can use different Midtrans Account for every Snap model payment method. To do so, configure the *Access Key* in Optional section `“Use different Midtrans account”`.
>
> If the optional *Access Key* is empty, the plugin will automatically use *Access Key* on Basic Settings.

<br />

## Customizing Configuration

<br />

The table given below describes the fields to customize configurations.

<br />

| Field                  | Description                                                                                                                                                                                                                                                                                                 |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Enable                 | Payment snap section enable.                                                                                                                                                                                                                                                                                |
| Title                  | The title for the payment method in the checkout page.                                                                                                                                                                                                                                                      |
| Custom Expiry          | This field will allow you to set a custom duration on how long the transaction is available to be paid.                                                                                                                                                                                                     |
| Allowed Payment Method | Customize allowed payment method, separate payment method code with a comma. For example, bank\_transfer, credit\_card. Leave it as default if you are not sure.                                                                                                                                            |
| Acquiring Bank         | You can specify which Acquiring Bank they prefer to use for a specific transaction. The transaction fund will be routed to that specific acquiring bank. Leave it blank if you are not sure.                                                                                                                |
| BIN Number             | It is a feature that allows the merchant to accept only Credit Cards within a specific set of BIN numbers. Separate BIN number with comma. For example, `4,5,4811,bni,mandiri`. Leave it blank if you are not sure.<br />***Note***: Please ensure that there is no empty space separating the BIN numbers. |
| Installment Terms      | An arrangement for payment by installments.                                                                                                                                                                                                                                                                 |
| 3D Secure              | You must enable 3D Secure for secure card transactions. Please contact us if you wish to disable this feature in the *Production* environment.                                                                                                                                                              |
| Save Card              | This will allow your customer to save their card on the payment popup, for faster payment flow on future transactions.                                                                                                                                                                                      |

<br />

## Magento 2 Plugin Notification Configuration

<br />

To configure the Magento 2 plugin notification URL, follow the steps given below.

1. Login to [Midtrans Dashboard portal](https://account.midtrans.com/).
2. In the **Environment** list, click the appropriate environment.
3. On the Home page, go to **SETTINGS > CONFIGURATION**.\
   *Configuration* page is displayed. Follow the steps given below.
   * Enter **Payment Notification URL**.
   * Enter **Finish Redirect URL**.
   * Enter **Error Redirect URL**.
   * Enter **Unfinish Redirect URL**.
   * Click **Update**.
4. On the Home page, go to **SETTINGS > SNAP PREFERENCES > System settings**. Follow the steps given below.
   * Enter **Finish Redirect URL**.
   * Enter **Error Redirect URL**.
   * Enter **Unfinish Redirect URL**.
   * Click **Save**. A confirmation message is displayed.\ <br />The plugin notification URL is configured successfully.

The table given below shows the fields and the URL.

| Field                    | URL                                        |
| ------------------------ | ------------------------------------------ |
| Payment Notification URL | \[your-site-url]/snap/payment/notification |
| Finish Redirect URL      | \[your-site-url]/snap/index/finish         |
| Error Redirect URL       | \[your-site-url]/snap/index/finish         |
| Unfinish Redirect URL    | \[your-site-url]/snap/index/finish         |

> 📘 Note
>
> Please make sure to input **http\://** or **https\://** when filling Notification URL and Redirect URL, according to your web-server configuration.
>
> If you are not sure, try opening your web URL in a browser, and check the URL is **http** or **https** on the address bar.

<br />

## Refunding Transactions Online

<br />

You can request refunds either from the Midtrans Dashboard or from the Magento administration. After a refund is issued, it cannot be cancelled or undone. So, before you trigger a refund request, make sure to check the refund amount and any other details. The online refund feature is available for GoPay and credit card payment methods.

If you make refund from the Midtrans *Dashboard*, refund notification is sent to Magento, transaction state is set to *CLOSED* and credit memo is not created.

<br />

### Requesting Refund from Magento Administration

To request a refund for a transaction from Magento administration, follow the steps given below.

1. Log in to your Magento administration panel.
2. In the menu, go to **Sales** > **Orders**. The order overview page is displayed.
3. Click the specific **order** you want to refund.
4. Click **Invoices** tab on **Order list View** navigation sidebar.
5. Go to **Invoice List Page** > **Order**, click **View** on invoice you need to request online refund.
6. Click **Credit Memo** on the top-right corner of the page.
7. In the **New Memo for Invoice** page, scroll down to the **Refund Totals** section.
8. In this section, you can request for refund online or offline.
   * **Refund:** This option is used to request refund online to Midtrans. Midtrans automatically sends refund notification and changes the order status to **Closed**.
   * **Refund Offline**: An offline refund does not trigger request refund to Midtrans. It is only refund in Magento side. You need to take action and carry out the refund manually from Midtrans dashboard. After a refund operation, the order status changes to **Closed**. This order status change is controlled by the Magento system.<br />The status change may not mean that the refund has carried out successfully on Midtrans side. When the refund is processed successfully, the transaction status in Midtrans dashboard changes to REFUND.

<br />

## Transaction Test

<br />

1. Perform successful transaction on your online store by entering the card details given below. For more details, refer to [Testing Payment on Sandbox](/docs/testing-payment-on-sandbox).

* **Card Number**: 4811 1111 1111 1114
* **CVV**: 123
* **Exp. Month**: 01
* **Exp. Year**: 2025

2. To ensure the proper installation and performance of the plugin, examine few points given below.

| Check Point                 | Error                                     | Troubleshooting                                                                                                                                                            |
| --------------------------- | ----------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Order status in CMS backend | Order status not recorded in the backend. | Check endpoint or the *Payment Notification URL* setting on MAP.<br /> Check if your CMS or the *Notification URL* is publicly accessible.                                 |
| Merchant email notification | Notification not received.                | Check *Email Notifications* settings on MAP. For more details, refer to [Configuring Email Notifications](/docs/midtrans-dashboard-usage#configuring-email-notifications). |
| Customer email notification | Notification not received.                | Check *Email Notifications* settings on MAP. For more details, refer to [Configuring Email Notifications](/docs/midtrans-dashboard-usage#configuring-email-notifications). |

<br />

## Payment Example

<br />

![](https://files.readme.io/40a58bd-mag2-pay-show.gif "mag2-pay-show.gif")

<br />

***

# <b>PrestaShop</b>

<br />

Midtrans ❤️ PrestaShop! Integrate your PrestaShop store with Midtrans Snap payment gateway. Midtrans strives to make payments simple for you and the customers. This plugin will allow online payment on your PrestaShop store using various online payment channels.

<br />

## Requirements

<br />

Some of the requirements to continue with the integration process, are listed below.

* PrestaShop 1.6 and 1.7 or later **|** Tested up to v1.7
* PHP version 5.4 or later
* MySQL version 5.0 or later
* Download Midtrans plugin for PrestaShop: [Zip file](https://github.com/veritrans/SNAP-Prestashop/archive/master.zip) (Open source on [GitHub](https://github.com/veritrans/SNAP-Prestashop))

<br />

## PrestaShop Plugin Installation and Configuration

<br />

To install and configure the Midtrans-PrestaShop plugin, follow the steps given below.

1. Download the plugin file from the link given above.
2. Extract the plugin and rename the folder as **midtranspay**. Then Zip the folder back into **midtranspay.zip**.
3. Go to **IMPROVE > Modules > Modules Manager** on PrestaShop administration page.
4. Click **Upload a module**.
5. Locate the **midtranspay.zip** file, click **Open**.\ <br />The plugin is installed successfully. A message to confirm the action is displayed.
6. Click **Configure**.
7. Find the **Midtrans Pay** module in the module manager and click **Configure**. Configure *Midtrans Pay* page is displayed. Follow the steps given below.
   * Enter **Payment Option Display Text**. This text appears on the button displayed to the customer.
   * In the **Environment** list, click the appropriate environment. *Development* for testing transaction, *Production* for real transaction.
   * Enter **Merchant ID**.
   * Enter **Client key.**
   * Enter **Server key**.
   * Select desired order status for successful payments, from **Map payment SUCCESS status to** list.
   * Select desired order status for payment failure, from **Map payment FAILURE status to** list.
   * Select desired order status for challenge payment, from **Map payment PENDING/CHALLENGE status to** list.

<br />

> 📘 Note
>
> Other fields are optional. You may leave it as is

<br />

The plugin is installed and configured successfully.

<br />

## PrestaShop Plugin Notification Configuration

<br />

To configure Midtrans-PrestaShop plugin notification URL, follow the steps given below.

1. Login to [Midtrans Dashboard portal](https://account.midtrans.com/).
2. In the **Environment** list, click the appropriate environment.
3. On the Home page, go to **SETTINGS > CONFIGURATION**.\
   *Configuration* page is displayed. Follow the steps given below.
   * Enter **Payment Notification URL**.
   * Enter **Finish Redirect URL**.
   * Enter **Error Redirect URL**.
   * Enter **Unfinish Redirect URL**.
4. Click **Update**.\
   A confirmation message is displayed. The plugin notification URL is configured successfully.

<br />

The table given below shows the fields and the URL.

| Field                    | URL                                                                               |
| ------------------------ | --------------------------------------------------------------------------------- |
| Payment Notification URL | \[your-site-url]/index.php?fc=module\&module=midtranspay\&controller=notification |
| Finish Redirect URL      | \[your-site-url]/index.php?fc=module\&module=midtranspay\&controller=success      |
| Error Redirect URL       | \[your-site-url]/index.php?fc=module\&module=midtranspay\&controller=failure      |
| Unfinish Redirect URL    | \[your-site-url]/index.php?fc=module\&module=midtranspay\&controller=success      |

> 📘 Note
>
> Please make sure to input **http\://** or **https\://** when filling Notification URL and Redirect URL, according to your web-server configuration.
>
> If you are not sure, try opening your web URL in a browser, and check the URL is **http** or **https** on the address bar.

<br />

## Transaction Test

1. Perform successful transaction on your online store by entering the card details given below. For more details, refer to [Testing Payment on Sandbox](/docs/testing-payment-on-sandbox).

* **Card Number**: 4811 1111 1111 1114
* **CVV**: 123
* **Exp. Month**: 01
* **Exp. Year**: 2025

2. To ensure the proper installation and performance of the plugin, examine few points given below.

| Check Point                 | Error                                     | Troubleshooting                                                                                                                                                            |
| --------------------------- | ----------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Order status in CMS backend | Order status not recorded in the backend. | Check endpoint or the *Payment Notification URL* setting on MAP.<br />Check if your CMS or the *Notification URL* is publicly accessible.                                  |
| Merchant email notification | Notification not received.                | Check *Email Notifications* settings on MAP. For more details, refer to [Configuring Email Notifications](/docs/midtrans-dashboard-usage#configuring-email-notifications). |
| Customer email notification | Notification not received.                | Check *Email Notifications* settings on MAP. For more details, refer to [Configuring Email Notifications](/docs/midtrans-dashboard-usage#configuring-email-notifications). |

<br />

## Payment Example

<br />

![](https://files.readme.io/9488d57-presta-pay-show.gif "presta-pay-show.gif")

<br />

***

# <b> OpenCart </b>

<br />

Midtrans ❤️ OpenCart! This is official Midtrans extension for the OpenCart E-commerce platform.

<br />

## Requirements

<br />

Some of the requirements to continue with the integration process, are listed below.

* OpenCart minimal 2.0 or later **|** Tested up to v3.0
* PHP version 5.4 or later
* MySQL version 5.0 or later
* Download Midtrans plugin for OpenCart (Please choose accordingly):
  * For OpenCart v3.0: [Zip file](https://github.com/Midtrans/Midtrans-Opencart3/archive/master.zip) (Open source on [GitHub](https://github.com/Midtrans/Midtrans-Opencart3))
  * For OpenCart v2.3: [Zip file](https://github.com/Midtrans/SNAP-Opencart-2.3/archive/master.zip) (Open source on [GitHub](https://github.com/Midtrans/SNAP-Opencart-2.3/))
  * For OpenCart v2.0, OpenCart v2.1 or OpenCart v2.2: [Zip file](https://github.com/veritrans/SNAP-Opencart/archive/master.zip) (Open source on [GitHub](https://github.com/veritrans/SNAP-Opencart))

<br />

## OpenCart Plugin Installation and Configuration

<br />

To install and configure Midtrans-OpenCart plugin, follow the steps given below.

1. Download the plugin file from the link given above.
2. Locate the root OpenCart directory of your shop through FTP connection.
3. Copy the `admin`, `catalog`, and `system` folders into your OpenCart root folder, and merge it.
4. On your OpenCart administration page, go to **Extensions** > **Extensions**.
5. Select **Payment** Filter.
6. Select **Midtrans**.
7. Click **Install**.\
   OpenCart plugin is installed successfully.
8. To configure merchant details, follow the steps given below.
   * Click **Edit**.\
     *Configure Midtrans* page is displayed.
   * Click **Enable** in **Status** list.
   * Enter **Display name**. This text is displayed on button displayed to the customer.
   * Enter **Merchant ID** with your Merchant ID on [Midtrans account](https://dashboard.midtrans.com/settings/config_info/).
   * Select **Environment** dropdown list; *Sandbox* is for testing transaction, *Production* is for real transaction.
   * Enter **Client Key**.
   * Enter **Server Key**.
   * In **SUCCESS Order Status** list, select your desired order status for a successful payment (recommended: `Processing`).
   * In **PENDING Order Status** list, select your desired order status for a payment failure (recommended: `Pending`).
   * In **FAILURE Order Status** list, select your desired order status for a pending payment (recommended: `Canceled`).

<br />

> 📘 Note
>
> *Client Key* and *Server Key* for *Sandbox* environment and *Production* environment are different. For more details, refer to [Retrieve API Access Keys](/docs/midtrans-account#retrieving-api-access-keys).
>
> Other fields are optional. You may leave it as is.

The plugin is installed and configured successfully.

<br />

## OpenCart Plugin Notification Configuration

<br />

To configure the Midtrans-OpenCart plugin notification URL, follow the steps given below.

1. Login to [Midtrans Dashboard portal](https://account.midtrans.com/).
2. In the **Environment** list, click the appropriate environment.
3. On the Home page, go to **SETTINGS > CONFIGURATION**.\
   *Configuration* page is displayed. Follow the steps given below.
   * Enter **Payment Notification URL**.
   * Enter **Finish Redirect URL**.
   * Enter **Unfinish Redirect URL**.
   * Enter **Error Redirect URL**.
4. Click **Update**. A confirmation message is displayed.

<br />

The plugin notification URL is configured successfully.

<br />

The table given below shows the fields and the URL.

| Field                    | URL                                                                 |
| ------------------------ | ------------------------------------------------------------------- |
| Payment Notification URL | \[your-site-url]/index.php?route=payment/snap/payment\_notification |
| Finish Redirect URL      | \[your-site-url]/index.php?route=payment/snap/landing\_redir&       |
| Unfinish Redirect URL    | \[your-site-url]/index.php?route=payment/snap/landing\_redir&       |
| Error Redirect URL       | \[your-site-url]/index.php?route=payment/snap/landing\_redir&       |

> 📘 Note
>
> Please make sure to input **http\://** or **https\://** when filling Notification URL and Redirect URL, according to your web-server configuration.
>
> If you are not sure, try opening your web URL in a browser, and check the URL is **http** or **https** on the address bar.

<br />

## Transaction Test

<br />

1. Perform successful transaction on your online store by entering the card details given below. For more details, refer to [Testing Payment on Sandbox](/docs/testing-payment-on-sandbox).

* **Card Number**: 4811 1111 1111 1114
* **CVV**: 123
* **Exp. Month**: 01
* **Exp. Year**: 2025

2. To ensure the proper installation and performance of the plugin, examine few points given below.

| Check Point                 | Error                                     | Troubleshooting                                                                                                                                                            |
| --------------------------- | ----------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Order status in CMS backend | Order status not recorded in the backend. | Check endpoint or the *Payment Notification URL* setting on MAP.<br/> Check if your CMS or the notification URL is publicly accessible.                                    |
| Merchant email notification | Notification not received.                | Check *Email Notifications* settings on MAP. For more details, refer to [Configuring Email Notifications](/docs/midtrans-dashboard-usage#configuring-email-notifications). |
| Customer email notification | Notification not received.                | Check *Email Notifications* settings on MAP. For more details, refer to [Configuring Email Notifications](/docs/midtrans-dashboard-usage#configuring-email-notifications). |

<br />

## Payment Example

<br />

![](https://files.readme.io/0844d8d-opencart-pay-show.gif "opencart-pay-show.gif")

<br />

***

# <b>WHMCS</b>

<br />

Midtrans ❤️ WHMCS! This plugin allows secure online payment on your WHMCS! With sleek built-in responsive payment interface (Snap). Midtrans strives to make payments simple for you and your customers. It supports various online payment channels.

<br />

## Requirements

<br />

Some of the requirements to continue with the integration process, are listed below.

* WHMCS v5.3.12 - v7.x or later **|** Tested up to WHMCS v7.6
* PHP version 5.4 or later
* MySQL version 5.0 or later
* Download Midtrans plugin for WHMCS: [Zip file](https://github.com/veritrans/SNAP-whmcs/archive/master.zip) (Open source on [GitHub](https://github.com/veritrans/SNAP-whmcs))

<br />

## WHMCS Plugin Installation and Configuration

<br />

To install and configure Midtrans-WHMCS plugin, follow the steps given below.

1. Download the plugin file from the link given above.
2. Extract **Whmcs-master.zip** file.
3. Upload and merge module folder that you have extracted into your WHMCS directory, **Installation and Configuration**.
4. Access your WHMCS administration page.
5. Go to **Setup** > **Payments** >**Payment Gateways**.
6. Click **Midtrans** payment method.\
   *Configuration* page is displayed.
7. Perform the following actions on *Configuration* page.
   * Enter **Display Name**.
   * Enter **Midtrans Client Key**.
   * Enter **Midtrans Server Key**.
   * For *Production* environment, select the **Production Mode** check box. For *Sandbox* environment, clear the **Production Mode** check box.
   * Click **Save Changes**.

<br />

![](https://files.readme.io/ba1ec4a-snap-whmcs1.png "snap-whmcs1.png")

<br />

The plugin is installed and configured successfully.

<br />

## WHMCS Plugin Notification Configuration

<br />

To configure the Midtrans-WHMCS plugin notification URL, follow the steps given below.

1. Login to [Midtrans Dashboard portal](https://account.midtrans.com/).
2. In the **Environment** list, click the appropriate environment.
3. On the Home page, go to **SETTINGS > CONFIGURATION**.\
   *Configuration* page is displayed.
4. Enter **Payment Notification URL**.
5. Enter **Finish Redirect URL**.
6. Enter **Unfinish Redirect URL**.
7. Enter **Error Redirect URL**.
8. Click **Update**. A confirmation message is displayed.

<br />

The plugin notification URL is configured successfully.

<br />

The table given below shows the fields and the URL.

| Field                    | URL                                                      |
| ------------------------ | -------------------------------------------------------- |
| Payment Notification URL | \[your-site-url]/modules/gateways/callback/veritrans.php |
| Finish Redirect URL      | \[your-site-url]                                         |
| Unfinish Redirect URL    | \[your-site-url]                                         |
| Error Redirect URL       | \[your-site-url]                                         |

> 📘 Note
>
> Please make sure to input **http\://** or **https\://** when filling Notification URL and Redirect URL, according to your web-server configuration.
>
> If you are not sure, try opening your web URL in a browser, and check the URL is **http** or **https** on the address bar.

<br />

## Transaction Test

<br />

1. Perform successful transaction on your online store by entering the card details given below. For more details, refer to [Testing Payment on Sandbox](/docs/testing-payment-on-sandbox).

* **Card Number**: 4811 1111 1111 1114
* **CVV**: 123
* **Exp. Month**: 01
* **Exp. Year**: 2025

2. To ensure the proper installation and performance of the plugin, examine few points given below.

| Check Point                 | Error                                     | Troubleshooting                                                                                                                                                            |
| --------------------------- | ----------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Order status in CMS backend | Order status not recorded in the backend. | Check endpoint or the *Payment Notification URL* setting on MAP.<br/> Check if your CMS or the *Notification URL* is publicly accessible.                                  |
| Merchant email notification | Notification not received.                | Check *Email Notifications* settings on MAP. For more details, refer to [Configuring Email Notifications](/docs/midtrans-dashboard-usage#configuring-email-notifications). |
| Customer email notification | Notification not received.                | Check *Email Notifications* settings on MAP. For more details, refer to [Configuring Email Notifications](/docs/midtrans-dashboard-usage#configuring-email-notifications). |

<br />

***

# <b>Drupal</b>

<br />

Midtrans ❤️ Drupal! This is the official Midtrans module for the Drupal E-commerce platform. You can easily integrate your Drupal commerce store with Midtrans payment gateway.

Also Available on [Drupal Project Module](https://www.drupal.org/project/midtrans_commerce)

<br />

## Requirements

<br />

Some of the requirements to continue with the integration process, are listed below.

* Drupal v8.x/v9.x **|** Tested up to drupal v8.x and drupal v9.x
  * Note: this guide is for Drupal 8 & 9. Drupal 7 [check here](/docs/midtrans-api-libraries-plugins#snap-plugin-for-e-commerce-cms).
* Drupal Commerce 8.x-2.xx **|** Tested up to v8.x - 2.x
* PHP v5.6.x or later
* MySQL version 5.0 or later
* Download Midtrans module for Drupal: [Zip file](https://github.com/Midtrans/Midtrans-Drupal8/archive/master.zip) (Open source on [GitHub](https://github.com/Midtrans/Midtrans-Drupal8))

<br />

## Composer Installation

<br />

If you are using [Composer](https://getcomposer.org), you can install via composer CLI

1. Open terminal
2. Move to your drupal site folder: `cd /[drupal site folder]/`
3. Run: `composer require drupal/midtrans_commerce`

<br />

## Manual Installation

<br />

To install and configure Drupal Commerce Midtrans payment module, follow the steps given below.

1. Download the module file from the link given above.
2. Extract the file and rename the folder to **midtrans\_commerce**.
3. Using a FTP client, or your hosting control panel, upload the unzipped module folder to your Drupal modules installation's **\[Drupal folder]/modules/contrib/** directory.

<br />

## Plugin Configuration

<br />

1. Open Drupal administration page, click **Extend**.
2. Under **COMMERCE (CONTRIB)** group, click **Commerce Midtrans**.

<br />

![](https://files.readme.io/a8266db-drupal8_1.png "drupal8_1.png")

<br />

3. Click **Install**.\
   Drupal 8 module is installed successfully.
4. Go to **Commerce** > **Configuration** > **Payment** > **Payment gateways**.

<br />

![](https://files.readme.io/5ce8701-drupal8_2.png "drupal8_2.png")

<br />

5. Click **Add payment gateway**.

<br />

![](https://files.readme.io/7597cc2-drupal8_3.png "drupal8_3.png")

<br />

**Add payment gateway page** is displayed.

6. Perform the following actions on *Payment gateways* page.

* Enter **Name**. This text appears on the button displayed to the customer.
* Select **Plugins** radio button.
* Select **Mode**; *Sandbox* for testing transaction and *Production* for real transaction.
* Enter **Merchant ID**.
* Enter **Server key**.
* Enter **Client key**.

> 📘 Note
>
> Other fields are optional. You may leave it as is.<br />You can retrieve *Merchant ID, Server key,* and *Client key* on Midtrans MAP Dashboard.

<br />

7. Click **Save**. A confirmation message is displayed.

<br />

![](https://files.readme.io/5d9fb1e-drupal8_4.png "drupal8_4.png")

<br />

The module is installed and configured successfully.

<br />

## Drupal Module Notification Configuration

<br />

To configure the Midtrans-Drupal module notification URL, follow the steps given below.

1. Login to [Midtrans Dashboard portal](https://account.midtrans.com/).
2. In the **Environment** list, click the appropriate environment.
3. On the Home page, go to **SETTINGS > CONFIGURATION**.\
   *Configuration* page is displayed.
4. Enter **Payment Notification URL**.
5. Enter **Finish Redirect URL**.
6. Enter **Unfinish Redirect URL**.
7. Enter **Error Redirect URL**.
8. Click **Update**. A confirmation message is displayed.

The module notification URL is configured successfully.

The table given below shows the fields and the URL.

| Field                    | URL                                      |
| ------------------------ | ---------------------------------------- |
| Payment Notification URL | \[your-site-url]/payment/notify/midtrans |
| Finish Redirect URL      | \[your-site-url]/payment/finish/midtrans |
| Unfinish Redirect URL    | \[your-site-url]/payment/finish/midtrans |
| Error Redirect URL       | \[your-site-url]/payment/finish/midtrans |

> 📘 Note
>
> Please make sure to input **http\://** or **https\://** when filling Notification URL and Redirect URL, according to your web-server configuration.
>
> If you are not sure, try opening your web URL in a browser, and check the URL is **http** or **https** on the address bar.

<br />

## Transaction Test

<br />

1. Perform successful transaction on your online store by entering the card details given below. For more details, refer to [Testing Payment on Sandbox](/docs/testing-payment-on-sandbox).

* **Card Number**: 4811 1111 1111 1114
* **CVV**: 123
* **Exp. Month**: 01
* **Exp. Year**: 2025

2. To ensure the proper installation and performance of the plugin, examine few points given below.

| Check Point                 | Error                                     | Troubleshooting                                                                                                                                                            |
| --------------------------- | ----------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Order status in CMS backend | Order status not recorded in the backend. | Check endpoint or the *Payment Notification URL* setting on MAP.<br /> Check if your CMS or the notification URL is publicly accessible.                                   |
| Merchant email notification | Notification not received.                | Check *Email Notifications* settings on MAP. For more details, refer to [Configuring Email Notifications](/docs/midtrans-dashboard-usage#configuring-email-notifications). |
| Customer email notification | Notification not received.                | Check *Email Notifications* settings on MAP. For more details, refer to [Configuring Email Notifications](/docs/midtrans-dashboard-usage#configuring-email-notifications). |

<br />

## Payment Example

<br />

![](https://files.readme.io/ff06780-drupal8-pay-show.gif "drupal8-pay-show.gif")

<br />

***

# <b>WordPress - Easy Digital Download</b>

<br />

Midtrans ❤️ EDD! Integrate your Easy Digital Download (EDD) store with Midtrans Snap payment gateway. Midtrans strives to make payments simple for both the merchant and the customers. This plugin will allow online payments on your EDD store using various online payment channels.

Midtrans-EDD plugins also available on [WordPress plugins store](https://wordpress.org/plugins/edd-midtrans-gateway/).

<br />

## Requirements

<br />

Some of the requirements to continue with the integration process, are listed below.

* WordPress 3.9.1 or later **|** Tested up to v5.x
* Easy Digital Downloads 2.0 or later **|** Tested up to v2.x
* PHP version 5.4 or later
* MySQL version 5.0 or later
* PHP CURL enabled server/host
* Download Midtrans plugin for WordPress EDD: [Zip file](https://github.com/Midtrans/midtrans-edd/archive/master.zip) (Open source on [GitHub](https://github.com/Midtrans/midtrans-edd))

<br />

## WordPress EDD Plugin Installation

<br />

To install Midtrans-WordPress EDD plugin, select any **one** of the installation methods given below.

<br />

### A. Simple Installation

To install Midtrans-EDD plugin, follow the steps given below.

1. Login to your WordPress administration panel.
2. Go to **Plugins** > **Add New**.
3. Enter **Midtrans-Easy-Digital-Downloads** in the search bar.
4. Click **Install Now**.
5. Click **Activate**.

The plugin is installed successfully. Proceed to [WordPress EDD Plugin Configuration](#wordpress-edd-plugin-configuration).

<br />

### B. Manual Installation

The manual installation method involves downloading feature-rich plugin and uploading it to your Webserver through your favorite FTP application. To install WordPress EDD manually, follow the steps given below.

1. Download the plugin file from the link given above and unzip it.
2. Extract the plugin, and rename the folder modules as **edd-midtrans-gateway**.
3. Using an FTP program, or your hosting control panel, upload the unzipped plugin folder to your WordPress installation wp-content/plugins/ directory.
4. Install and Activate the plugin from the **Plugins** menu on the WordPress administration panel.
5. Activate Easy Digital Downloads - Midtrans Gateway plugin from **Plugin** menu in your WordPress administration page.

The plugin is installed successfully. Proceed to [WordPress EDD Plugin Configuration](#wordpress-edd-plugin-configuration).

<br />

## WordPress EDD Plugin Configuration

<br />

To configure Midtrans-EDD plugin, follow the steps given below.

1. On Dashboard, go to **Downloads(1) > Settings(2)**.\
   *Easy Digital Downloads Settings* page is displayed.
2. Select **Payment Gateways(3)** tab.
3. Select **General**.
4. For *Sandbox* environment, select the **Test mode** check box. For *Production* environment, click to clear the **Test mode** check box.
5. Under **Payment Gateways**, click **Midtrans (4)**.
6. In the **Default Gateway(5)** list, click **Midtrans**.
7. Click **Save Changes(6)**.

<br />

![](https://files.readme.io/23e9ed7-EDD-Config-1.png "EDD-Config-1.png")

<br />

8. Click **Midtrans(7)**.
9. On *Midtrans Settings* page, follow the steps given below.
   * Enter **Checkout Label**.
   * Enter **Merchant ID**.
   * For *Production* Environment, enter **Production Server Key** and **Production Client Key**. For *Sandbox* Environment, enter **Sandbox Server Key** and **Sandbox Client Key**.
10. Click **Save Changes**.

<br />

![](https://files.readme.io/0e5eab0-EDD-Config-2.png "EDD-Config-2.png")

<br />

The plugin is configured successfully.

<br />

## EDD Plugin Notification Configuration

<br />

To configure the Midtrans-EDD plugin notification URL, follow the steps given below.

1. Login to [Midtrans Dashboard portal](https://account.midtrans.com/).
2. In the **Environment** list, click the appropriate environment.
3. On the Home page, go to **SETTINGS > CONFIGURATION**.\
   *Configuration* page is displayed.
4. Enter **Payment Notification URL**.
5. Enter **Finish Redirect URL**.
6. Enter **Unfinish Redirect URL**.
7. Enter **Error Redirect URL**.
8. Click **Update**. A confirmation message is displayed.

The plugin notification URL is configured successfully.

The table given below shows the fields and the URL.

| Field                    | URL                                     |
| ------------------------ | --------------------------------------- |
| Payment Notification URL | \[your-site-url]/?edd-listener=midtrans |
| Finish Redirect URL      | \[your-site-url]                        |
| Unfinish Redirect URL    | \[your-site-url]                        |
| Error Redirect URL       | \[your-site-url]                        |

> 📘 Note
>
> Please make sure to input **http\://** or **https\://** when filling Notification URL and Redirect URL, according to your web-server configuration.
>
> If you are not sure, try opening your web URL in a browser, and check the URL is **http** or **https** on the address bar.

<br />

## Transaction Test

<br />

1. Perform successful transaction on your online store by entering the card details given below. For more details, refer to [Testing Payment on Sandbox](/docs/testing-payment-on-sandbox).

* **Card Number**: 4811 1111 1111 1114
* **CVV**: 123
* **Exp. Month**: 01
* **Exp. Year**: 2025

2. To ensure the proper installation and performance of the plugin, examine few points given below.

| Check Point                 | Error                                     | Troubleshooting                                                                                                                                                            |
| --------------------------- | ----------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Order status in CMS backend | Order status not recorded in the backend. | Check endpoint or the *Payment Notification URL* setting on MAP.<br/> Check if your CMS or the notification URL is publicly accessible.                                    |
| Merchant email notification | Notification not received.                | Check *Email Notifications* settings on MAP. For more details, refer to [Configuring Email Notifications](/docs/midtrans-dashboard-usage#configuring-email-notifications). |
| Customer email notification | Notification not received.                | Check *Email Notifications* settings on MAP. For more details, refer to [Configuring Email Notifications](/docs/midtrans-dashboard-usage#configuring-email-notifications). |

<br />

## Payment Example

<br />

![](https://files.readme.io/4aa2721-edd-show-pay.gif "edd-show-pay.gif")

<br />

***

# <b>Midtrans Payment Plugin Live Demonstration </b>

<br />

Want to see Midtrans CMS payment plugins in action? We have some demo web-stores that you can use to try the payment journey directly, visit these [sample stores](https://plugins-demo.midtrans.com/).

<br />

***

# <b>Feedback And Request</b>

<br />

If you have any kind of feedback, feature-request, new CMS that you want us to support, etc. related to Midtrans' CMS payment plugin, please [do let us know by filling this form](https://forms.gle/m3nJC1SNUDCw8Hmq9).

# Other Notes

* if you are looking for Shopify, please refer to [Midtrans' Shopify Payment App guide](/docs/ecommerce-platform#bshopifyb), as it is included in Ecommerce Platform section.