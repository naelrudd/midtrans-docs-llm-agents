---
updatedAt: 2026-09-28T12:00:08.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Get Checkout Page Preference API

This API can be used to retrieve the detail modification and configuration of merchant's checkout page, such as merchant's display name, typography, and payment channel settings.

Endpoints: `/api/v1/checkout/merchant-preferences`

HTTP Method: `GET`

## Response Body

### Success

```json 200 - Success
{
    "merchant_id": "M007743",
    "display_name": "DEMO STORE",
    "finish_payment_return_url": "https://midtrans.com/finish",
    "error_payment_return_url": "https://midtrans.com/error",
    "locale": "en",
    "other_va_processor": "bri_va",
    "allow_retry": true,
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

<Table>
  <thead>
    <tr>
      <th>
        Field
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
        Alternative virtual account processor that the merchant can use for transactions. Corresponds to the `Other Bank/ATM Bank Processor` menu in Snap Preference > System Settings. Options: `permata_va`, `bni_va`, `bri_va`, `cimb_va`
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
        brand.typography
      </td>

      <td>
        String
      </td>

      <td>
        Specifies the font family to be used on the checkout page. <br /><br />Options: `Arial`,`Inter`,`Nunito`,`Open Sans`,`Playfair Display`,`Poppins`,`Questrial`,`Roboto`,`Source Sans Pro`
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

### Failed

```json 401 - Access Denied
{
    "error_messages": [
        "Access denied, please check server key"
    ]
}
```

| Field           | Type            | Description    |
| --------------- | :-------------- | -------------- |
| error\_messages | Array of String | Error messages |

#