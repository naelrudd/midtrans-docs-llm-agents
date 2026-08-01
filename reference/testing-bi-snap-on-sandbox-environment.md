---
updatedAt: 2025-11-11T00:48:27.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Testing Core API BI-SNAP on Sandbox Environment

Sandbox Environment can be used to create "testing" transactions (usually performed from your development/testing environment). All transaction made within this environment mode is not "real", and does not require "real payment/fund". This environment is created automatically when you are signing up, and free to use.

> 📘 Merchant can now test CoreAPI BI-SNAP flow on Sandbox!
>
> This includes account linking and payment flow.
>
> This new sandbox will be rolled out to all merchant from **October 22nd, 2024**. Please contact your sales representative for early access.

# API domain

| Midtrans API           | API domain                                                   |
| :--------------------- | :----------------------------------------------------------- |
| Core API (non BI-SNAP) | <https://api.sandbox.midtrans.com>                           |
| BI-SNAP                | Get Auth Code API = <https://merchants-app.sbx.midtrans.com> |
|                        | Other API = <https://merchants.sbx.midtrans.com>             |

# Merchant credentials

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Merchant credentials
      </th>

      <th>

      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        MID (Merchant ID)
      </td>

      <td>
        Same production MID will be used in the new sandbox\
        *Unlike in the current BI-SNAP staging where merchant will be given a separate staging MID*
      </td>
    </tr>

    <tr>
      <td>
        Core API server key
      </td>

      <td>
        For existing Core API merchant migrating to new sandbox = Server key will be the same as old sandbox, but will be kept different with production
      </td>
    </tr>

    <tr>
      <td>
        BI-SNAP credentials
      </td>

      <td>
        For existing  BI-SNAP merchant migrating to new sandbox = BI-SNAP credentials will be the same as staging, but will be kept different with production (except for a few GoPay Tokenization credentials). <br /><br /> Specific for GoPay Tokenization, merchant will need to start using these credetials below: <br /> 1. X-PARTNER-ID = Sandbox MID <br /> 2. merchantId (in Get Auth Code API) = Sandbox payment handle (UUID format). <br /> Please contact your sales representative to get both of these values.
      </td>
    </tr>
  </tbody>
</Table>

# Merchant eligibility

> 📘
>
> Sandbox environment will be enabled to the merchants once they have registered to Midtrans. Merchant need to make sure that merchant phone number and email has already been filled during the registration process.
>
> If not, merchant can easily fill in their phone number and email in Merchant dashboard <https://dashboard.midtrans.com/> through this menu Environment Sandbox > Settings > General Settings.
>
> Specific to BI-SNAP flow, merchant will still need to do credentials exchange by following these steps <https://docs.midtrans.com/reference/getting-started-1>.

If any of the payment method is not yet enabled, merchant can contact their sales representative for further assistance.

# Testing GoPay/ShopeePay/DANA deeplink

Merchant can test GoPay/ShopeePay/DANA deeplink in sandbox environment by calling the sandbox API endpoint.

1. Merchant create payment by calling the Direct Debit Payment API to the sandbox API endpoint.
2. As part of the API response, Midtrans will return redirect URL with Midtrans sandbox simulator
3. Merchant to open the URL and complete the payment directly on the simulator. Merchant can input PIN 123456 to complete the payment.
4. Merchant will then be redirected to the merchant page as stated in the merchant's API request

# Testing QRIS

Merchant can test QRIS in sandbox environment by calling the sandbox API endpoint.

1. Merchant create payment by calling the Generate QR MPM API to the sandbox API endpoint.
2. As part of the API response, Midtrans will return QRIS image URL
3. Merchant needs to open the Midtrans sandbox simulator for QRIS payment <https://simulator.sandbox.midtrans.com/openapi/qris/index>
4. Merchant then needs to paste the QRIS image URL to the simulator, then click "Scan QR"
5. Merchant to complete the payment. Merchant can choose to pay with GoPay or other QRIS player.
6. Merchant will then be redirected to the merchant page as stated in the merchant's API request

# Testing Virtual Account (Bank transfer)

Merchant can test virtual account in sandbox environment by calling the sandbox API endpoint.

1. Merchant create payment by calling the Create VA API to the sandbox API endpoint.
2. As part of the API response, Midtrans will return virtual account number or (for Mandiri) biller code and bill key
3. Merchant needs to open the Midtrans sandbox simulator for virtual account payment

| Bank type | Simulator link                                                         |
| :-------- | :--------------------------------------------------------------------- |
| BCA       | <https://simulator.sandbox.midtrans.com/bca/va/index>                  |
| BRI       | <https://simulator.sandbox.midtrans.com/openapi/va/index?bank=bri>     |
| BNI       | <https://simulator.sandbox.midtrans.com/bni/va/index>                  |
| Permata   | <https://simulator.sandbox.midtrans.com/openapi/va/index?bank=permata> |
| CIMB      | <https://simulator.sandbox.midtrans.com/openapi/va/index?bank=cimb>    |
| Mandiri   | <https://simulator.sandbox.midtrans.com/openapi/va/index?bank=mandiri> |

4. Merchant then needs to paste the virtual account number or biller code and bill key to the simulator, then click "Inquire"
5. Merchant to complete the payment in the simulator
6. Merchant will then be redirected to the merchant page as stated in the merchant's API request

# Testing GoPay Tokenization

Merchant can simulate GoPay Tokenization transaction on sandbox environment, they can test various production-like features such as GoPay promotion API, pre-auth, and recurring flows. With the new sandbox, merchant can also test directly using GoPay UI instead of using Midtrans mock UI.

<Image align="center" src="https://files.readme.io/069091e1682522e2d45fe72506ae834d9a4ae3c9333124d28be0cc22c578dc5d-midtrans_GoPay_Tokenization_Sandbox.gif" />

**Please note, there will be new behavior on the sandbox environment:**

1. Merchant can only test using phone number that has been provided by Midtrans
2. User balance will be applied universally
3. Previous linking made in the staging environment or old sandbox environment (for non BI-SNAP flow), cannot be used in the new sandbox. We suggest merchant to do fresh linking when testing on new sandbox.

For more details, please refer to this page <https://docs.midtrans.com/reference/testing-gopay-tokenization-bi-snap-on-sandbox>.