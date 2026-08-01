---
updatedAt: 2025-11-10T22:56:52.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Preference API

Modify your Snap look and feel & active payment methods in Snap Checkout via API

API for [Snap Preferences](https://dashboard.midtrans.com/settings/snap_preference). Modifiable features include active payment methods and look and feel customization.

***

<br />

# Get Snap Preferences

<br />

Retrieve your current Snap Preference settings.

**Endpoints:** /snap/v3/merchant-preferences\
**HTTP Method:** GET\
**Headers:**

Content-Type: application/json\
Accept: application/json

Production: `https://app.midtrans.com/snap/v3/merchant-preferences`

Sandbox: `https://app.sandbox.midtrans.com/snap/v3/merchant-preferences`

| Key           | Description                            |
| :------------ | :------------------------------------- |
| Authorization | Basic Base64Encode(merchantServerKey:) |

<br />

## Response JSON Body Details

<br />

```json 200
{
    "merchant_id": "M007743",
    "display_name": "DEMO STORE",
    "finish_payment_return_url": "https://midtrans.com/finish",
    "error_payment_return_url": "https://midtrans.com/error",
    "locale": "en",
    "other_va_processor": "bri_va",
    "allow_retry": true,
    "hide_order_id": false,
    "brand": {
        "typography": "Poppins",
        "header_color": "#ffffff",
        "button_color": "#0256A7",
        "input_border_radius": 10,
        "button_border_radius": 10,
        "hide_header": false
    },
    "payment_channels": [
        {
            "name": "credit_card",
            "enabled": true
        },
        {
            "name": "bca_va",
            "enabled": true
        }
    ]
}
```
```json 401
{
    "error_messages": [
        "Access denied, please check server key"
    ]
}
```

<br />

<Table>
  <thead>
    <tr>
      <th>
        Parameter
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        display\_name
      </td>

      <td>
        String
      </td>

      <td>
        The name of the merchant or store that will be displayed on the checkout page
      </td>
    </tr>

    <tr>
      <td>
        finish\_payment\_return\_url
      </td>

      <td>
        String
      </td>

      <td>
        The URL to which the user will be redirected after successfully completing a payment.
      </td>
    </tr>

    <tr>
      <td>
        error\_payment\_return\_url
      </td>

      <td>
        String
      </td>

      <td>
        The URL for redirecting the user in case an error occurs during the payment process
      </td>
    </tr>

    <tr>
      <td>
        locale
      </td>

      <td>
        String
      </td>

      <td>
        Specifies the language and regional settings for the checkout page
      </td>
    </tr>

    <tr>
      <td>
        other\_va\_processor
      </td>

      <td>
        String
      </td>

      <td>
        Alternative virtual account processor that the merchant can use for transactions. Corresponds to the `Other Bank/ATM Bank Processor` menu in Snap Preference > System Settings. Options: permata\_va, bni\_va, bri\_va, cimb\_va
      </td>
    </tr>

    <tr>
      <td>
        allow\_retry
      </td>

      <td>
        Boolean
      </td>

      <td>
        A boolean value that, when true, allows users to retry payments if their initial attempt fails
      </td>
    </tr>

    <tr>
      <td>
        hide\_order\_id
      </td>

      <td>
        Boolean
      </td>

      <td>
        A boolean value that, when set to false, shows the order id on the checkout page.
      </td>
    </tr>

    <tr>
      <td>
        brand.typography
      </td>

      <td>
        String
      </td>

      <td>
        Specifies the font family to be used on the checkout page. <br /><br />Options: Arial,Inter,Nunito,Open Sans,Playfair Display,Poppins,Questrial,Roboto,Source Sans Pro
      </td>
    </tr>

    <tr>
      <td>
        brand.header\_color
      </td>

      <td>
        String
      </td>

      <td>
        Hex code of header color of the checkout page
      </td>
    </tr>

    <tr>
      <td>
        brand.button\_color
      </td>

      <td>
        String
      </td>

      <td>
        Hex code of the color of buttons on the checkout page.
      </td>
    </tr>

    <tr>
      <td>
        brand.input\_border\_radius
      </td>

      <td>
        String
      </td>

      <td>
        These fields define the border radius (in pixels) for input fields, affecting their rounded corners. Max value is 10.
      </td>
    </tr>

    <tr>
      <td>
        brand.button\_border\_radius
      </td>

      <td>
        String
      </td>

      <td>
        These fields define the border radius (in pixels) for buttons, affecting their rounded corners. Max value is 10.
      </td>
    </tr>

    <tr>
      <td>
        brand.hide\_header
      </td>

      <td>
        String
      </td>

      <td>
        A boolean value that, when set to false, shows the header on the checkout page.
      </td>
    </tr>

    <tr>
      <td>
        payment\_channels
      </td>

      <td>
        Array of Object
      </td>

      <td>
        An array of objects, each representing a payment method available on the checkout page. Each object has the following properties:<br /><br />name: The identifier for the payment method (e.g., "credit\_card", "bca\_va", “gopay”).<br /><br />enabled: A boolean indicating whether the payment method is available for use.<br />
      </td>
    </tr>
  </tbody>
</Table>

***

<br />

# Update Snap Preference

<br />

Update your current Snap Preference settings.

**Endpoints:** /snap/v3/merchant-preferences\
**HTTP Method:** PATCH\
**Headers:**

Content-Type: application/json\
Accept: application/json

Production: `https://app.midtrans.com/snap/v3/merchant-preferences`

Sandbox: `https://app.sandbox.midtrans.com/snap/v3/merchant-preferences`

<br />

## Request Body

<br />

```json 200
{
    "display_name": "DEMO STORE",
    "finish_payment_return_url": "https://midtrans.com/finish",
    "error_payment_return_url": "https://midtrans.com/error",
    "locale": "en",
    "other_va_processor": "bri_va",
    "allow_retry": true,
    "hide_order_id": false,
    "brand": {
        "typography": "Poppins",
        "header_color": "#ffffff",
        "button_color": "#0256A7",
        "input_border_radius": 10,
        "button_border_radius": 10,
        "hide_header": false
    },
    "payment_channels": [
        {
            "name": "credit_card",
            "enabled": true
        },
        {
            "name": "bca_va",
            "enabled": true
        },
        {
            "name": "permata_va",
            "enabled": true
        },
        {
            "name": "other_va",
            "enabled": true
        },
        {
            "name": "echannel",
            "enabled": true
        },
        {
            "name": "indomaret",
            "enabled": true
        },
        {
            "name": "gopay",
            "enabled": true
        },
        {
            "name": "akulaku",
            "enabled": true
        },
        {
            "name": "alfamart",
            "enabled": true
        },
        {
            "name": "bri_va",
            "enabled": true
        },
        {
            "name": "bni_va",
            "enabled": true
        },
        {
            "name": "shopeepay",
            "enabled": true
        },
        {
            "name": "kredivo",
            "enabled": true
        },
        {
            "name": "other_qris",
            "enabled": true
        },
        {
            "name": "cimb_va",
            "enabled": true
        }
    ]
}
```
```json 400
{
    "error_messages": [
        "Payment type credit_card is invalid for this merchant"
    ]
}
```
```json 401
{
    "error_messages": [
        "Access denied, please check server key"
    ]
}
```

<br />

<Table>
  <thead>
    <tr>
      <th>
        Parameter
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        display\_name
      </td>

      <td>
        String
      </td>

      <td>
        The name of the merchant or store that will be displayed on the checkout page
      </td>
    </tr>

    <tr>
      <td>
        finish\_payment\_return\_url
      </td>

      <td>
        String
      </td>

      <td>
        The URL to which the user will be redirected after successfully completing a payment.
      </td>
    </tr>

    <tr>
      <td>
        error\_payment\_return\_url
      </td>

      <td>
        String
      </td>

      <td>
        The URL for redirecting the user in case an error occurs during the payment process
      </td>
    </tr>

    <tr>
      <td>
        locale
      </td>

      <td>
        String
      </td>

      <td>
        Specifies the language and regional settings for the checkout page
      </td>
    </tr>

    <tr>
      <td>
        other\_va\_processor
      </td>

      <td>
        String
      </td>

      <td>
        Alternative virtual account processor that the merchant can use for transactions. Corresponds to the `Other Bank/ATM Bank Processor` menu in Snap Preference > System Settings. Options: permata\_va, bni\_va, bri\_va, cimb\_va
      </td>
    </tr>

    <tr>
      <td>
        allow\_retry
      </td>

      <td>
        Boolean
      </td>

      <td>
        A boolean value that, when true, allows users to retry payments if their initial attempt fails
      </td>
    </tr>

    <tr>
      <td>
        hide\_order\_id
      </td>

      <td>
        Boolean
      </td>

      <td>
        A boolean value that, when set to false, shows the order id on the checkout page.
      </td>
    </tr>

    <tr>
      <td>
        brand.typography
      </td>

      <td>
        String
      </td>

      <td>
        Specifies the font family to be used on the checkout page. <br /><br />Options: Arial,Inter,Nunito,Open Sans,Playfair Display,Poppins,Questrial,Roboto,Source Sans Pro
      </td>
    </tr>

    <tr>
      <td>
        brand.header\_color
      </td>

      <td>
        String
      </td>

      <td>
        Hex code of header color of the checkout page
      </td>
    </tr>

    <tr>
      <td>
        brand.button\_color
      </td>

      <td>
        String
      </td>

      <td>
        Hex code of the color of buttons on the checkout page.
      </td>
    </tr>

    <tr>
      <td>
        brand.input\_border\_radius
      </td>

      <td>
        String
      </td>

      <td>
        These fields define the border radius (in pixels) for input fields, affecting their rounded corners. Max value is 10.
      </td>
    </tr>

    <tr>
      <td>
        brand.button\_border\_radius
      </td>

      <td>
        String
      </td>

      <td>
        These fields define the border radius (in pixels) for buttons, affecting their rounded corners. Max value is 10.
      </td>
    </tr>

    <tr>
      <td>
        brand.hide\_header
      </td>

      <td>
        String
      </td>

      <td>
        A boolean value that, when set to false, shows the header on the checkout page.
      </td>
    </tr>

    <tr>
      <td>
        payment\_channels
      </td>

      <td>
        Object
      </td>

      <td>
        An array of objects, each representing a payment method available on the checkout page. Each object has the following properties:<br /><br />name: The identifier for the payment method (e.g., "credit\_card", "bca\_va", “gopay”).<br /><br />enabled: A boolean indicating whether the payment method is available for use.<br />
      </td>
    </tr>
  </tbody>
</Table>