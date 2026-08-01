---
updatedAt: 2026-06-19T02:54:48.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Testing GoPay Tokenization BI-SNAP on Sandbox

> 📘 New GoPay Tokenization BI-SNAP sandbox!
>
> Midtrans is revamping its sandbox environment for GoPay Tokenization payment method. In the new sandbox, merchant can simulate more production-like features and scenarios that cannot be simulated previously in the old sandbox. The newly supported scenarios are BI-SNAP API, GoPay promotion API, testing directly on GoPay UI, to name a few.
>
> Please note that there will be a change of behavior of the sandbox environment. The changes will be listed below.
>
> This new GoPay Tokenization sandbox will be rolled out to all merchant from **October 22nd, 2024**. Please contact your sales representative for early access.

# API domain

| Midtrans API           | API domain                                                   |
| :--------------------- | :----------------------------------------------------------- |
| Core API (non BI-SNAP) | <https://api.sandbox.midtrans.com>                           |
| BI-SNAP                | Get Auth Code API = <https://merchants-app.sbx.midtrans.com> |
|                        | Other API = <https://merchants.sbx.midtrans.com>             |

# Merchant credentials

| Merchant credentials |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| :------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| MID (Merchant ID)    | Same production MID will be used in the new sandbox<br />*Unlike in the current BI-SNAP staging where merchant will be given a separate staging MID*                                                                                                                                                                                                                                                                                                                                                                   |
| Core API server key  | For existing Core API merchant migrating to new sandbox = Server key will be the same as old sandbox, but will be kept different with production                                                                                                                                                                                                                                                                                                                                                                       |
| BI-SNAP credentials  | For existing  BI-SNAP merchant migrating to new sandbox = BI-SNAP credentials will be the same as staging, but will be kept different with production (except for a few GoPay Tokenization credentials). <br /><br /> Specific for GoPay Tokenization, merchant will need to start using these credetials below: <br /> 1. X-PARTNER-ID = Sandbox MID <br /> 2. merchantId (in Get Auth Code API) = Sandbox payment handle (UUID format). <br /> Please contact your sales representative to get both of these values. |

# Merchant eligibility

> 📘
>
> GoPay Tokenization will be automatically enabled on the new sandbox. **Merchant need to make sure that merchant phone number and email has already been filled during the registration process.**
>
> If not, merchant can easily fill in their phone number and email in Merchant dashboard <https://dashboard.midtrans.com/> through this menu Environment Sandbox > Settings > General Settings.

If GoPay Tokenization is not yet enabled, merchant can contact their sales representative for further assistance.

Specific to GoPay Tokenization BI-SNAP, merchant will still need to do credentials exchage by following these steps <https://docs.midtrans.com/reference/getting-started-1>.

# Testing user account

The table given below lists the phone numbers that can be used to test GoPay Tokenization in the new sandbox.

| Phone number  | Available payment option | Scenarios                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| :------------ | :----------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| +628215023424 | GoPay Saldo              | Happy flow                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| +628242974268 | GoPay Saldo              | Happy flow                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| +628271939753 | GoPay Saldo              | GoPay blocked                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| +628242014881 | GoPay Saldo              | Insufficient balance                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| +628237435829 | GoPay Saldo              | Promotion available                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| +380441234567 | GoPay Saldo              | Happy flow                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| +380441234568 | GoPay Saldo              | Happy flow                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| +918877661234 | GoPay Saldo              | Happy flow                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| +918877661235 | GoPay Saldo              | Happy flow                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| +628103001242 | GoPay Later              | Happy flow                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Random number | GoPay Saldo              | Not registered - GoPay will return Tokenization webview account creation flow, refer to this [link](https://docs.midtrans.com/reference/faq-redirection-to-gopay-web-page#gopay-has-revamped-its-gopay-tokenization-linking-web-page-on-the-gopay-tokenization-webview-integration-on-august-2025) . Merchant can use any unregistered random number. If the account creation flow is not triggered then it means the number is registered in GoPay, merchant can try with other number |

> 📘 Please note:
>
> * Other phone number that is not listed here cannot be used for testing GoPay Tokenization in the new sandbox
> * Merchant can use this PIN **112233** and OTP **987654** to complete linking & payment
> * Linking that is created in old sandbox or staging cannot be used in the new sandbox environment
>   * We suggest merchant to initiate freshly new linking using the provided phone number for each of the merchant's user-testing account.
> * Just like in production, merchant can also simulate production-like balance update flow. In the new sandbox, user balance will be universal accross all merchants. Balance top up and deduction will be applied universally.
>
> <Table align={["left","left"]}>
>   <thead>
>     <tr>
>       <th>
>         Sample scenario
>       </th>
>
>       <th>
>         User balance
>       </th>
>     </tr>
>   </thead>
>
>   <tbody>
>     <tr>
>       <td>
>         User 123 with phone number 123 have a balance of IDR 100K
>       </td>
>
>       <td>
>         IDR 100K
>       </td>
>     </tr>
>
>     <tr>
>       <td>
>         Merchant A create a transaction with user 123 of IDR 30K
>       </td>
>
>       <td>
>         - IDR 30K
>       </td>
>     </tr>
>
>     <tr>
>       <td>
>         Merchant B create a transaction with user 123 of IDR 20K
>       </td>
>
>       <td>
>         - IDR 20K
>       </td>
>     </tr>
>
>     <tr>
>       <td>
>         Merchant C fetch the balance of user 123
>       </td>
>
>       <td>
>         IDR 50K
>       </td>
>     </tr>
>   </tbody>
> </Table>

# Testing PIN/No PIN flow

Just like in old sandbox, merchant can simulate PIN and no PIN transaction based on the transaction amount.

| Transaction amount           | Flow   |
| :--------------------------- | :----- |
| Below IDR 100K               | No PIN |
| Above and equals to IDR 100K | PIN    |

# Testing Pre Auth flow

Just like in old sandbox, merchant can simulate pre auth flow by following the API doc here:

* Core API = <https://docs.midtrans.com/reference/gopay-tokenization#gopay-tokenization-features-pre-authorization>
* BI-SNAP = <https://docs.midtrans.com/reference/auth-payment-api-gopay-tokenization>

Please contact your sales representative to enable pre auth flow in sandbox environment.

# Testing promotion

Merchant can now test GoPay fetch promotion API on the new sandbox. Please make sure you use the testing phone number prepared for promotion (refer [here](https://docs.midtrans.com/reference/testing-on-sandbox-environment#testing-user-account) ).

Please contact your sales representative to enable promotion in sandbox environment.