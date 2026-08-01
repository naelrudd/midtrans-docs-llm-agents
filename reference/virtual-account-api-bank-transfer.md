---
updatedAt: 2026-06-12T01:52:20.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Payment Method : Bank Transfer

This section will explain how merchants can initiate bank transfer (virtual account) transactions using BI-SNAP-based CoreAPI specification.

# Creating bank transfer (virtual account) transaction

| Path              | /{version}/transfer-va/create-va |
| :---------------- | :------------------------------- |
| HTTP Method       | POST                             |
| Version           | v1.0                             |
| SNAP version code | 27                               |

## Request Header

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field Name
      </th>

      <th>
        Field Type
      </th>

      <th>
        Mandatory
      </th>

      <th>
        Field Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Content-Type
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Media type of the resource, i.e. application/json
      </td>
    </tr>

    <tr>
      <td>
        X-TIMESTAMP
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Client’s current local time in ISO-8601 format
      </td>
    </tr>

    <tr>
      <td>
        Authorization
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Represents access\_token of a request; string starts with keyword “Bearer ” followed by access\_token. Can get this from Access Token B2B API response.
      </td>
    </tr>

    <tr>
      <td>
        X-SIGNATURE
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Created using symmetric signature HMAC\_SHA512 algorithm
      </td>
    </tr>

    <tr>
      <td>
        X-PARTNER-ID
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Unique identifier for caller (merchant\_id)
      </td>
    </tr>

    <tr>
      <td>
        CHANNEL-ID
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Mandatory field from Bank Indonesia that can take any value with correct format 5 digits numeric string
      </td>
    </tr>

    <tr>
      <td>
        X-EXTERNAL-ID
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Alphanumeric string. We suggest merchant to use UUID format. The value should be unique. In case of timeout, merchant can do:

        1. Use this value in get status API to get status transaction
        2. Retry this request with the same X-EXTERNAL-ID and request body to avoid creating duplicate transaction <br /><br /> The value should also be the same as _request\_body.trxId_
      </td>
    </tr>
  </tbody>
</Table>

```
Content-type:application/json
X-TIMESTAMP:2020-01-01T00:00:00+07:00
X-SIGNATURE:da1fa417c72d6b91c257e01e54fac824
Authorization:Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
X-PARTNER-ID:G12345678
X-EXTERNAL-ID:midtrans-testing-001
CHANNEL-ID:12345
```

## Request Body

<br />

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field Name
      </th>

      <th>
        Field Type
      </th>

      <th>
        Mandatory
      </th>

      <th>
        Field Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        partnerServiceId
      </td>

      <td>
        String(8)
      </td>

      <td>
        M
      </td>

      <td>
        This field will be shared by Midtrans during the onboarding process. This will be associated with the bank's company code.<br />The value should be left-padded with spaces until it’s 8 characters long.
      </td>
    </tr>

    <tr>
      <td>
        customerNo
      </td>

      <td>
        String(20)
      </td>

      <td>
        M
      </td>

      <td>
        Merchant-defined number. The value will be used to generate the VA number.
      </td>
    </tr>

    <tr>
      <td>
        virtualAccountNo
      </td>

      <td>
        String(28)
      </td>

      <td>
        M
      </td>

      <td>
        This field will be the combination of _partnerServiceId_ + _customerNo_

        Please refer to the "Custom VA Number" below this section if you're looking to define your own VA number for your customers.

        If you want to randomize your VA number, please refer to the `additionalInfo.flags.shouldRandomizeVaNumber` field
      </td>
    </tr>

    <tr>
      <td>
        virtualAccountName
      </td>

      <td>
        String(255)
      </td>

      <td>
        M
      </td>

      <td>
        The customer name
      </td>
    </tr>

    <tr>
      <td>
        virtualAccountEmail
      </td>

      <td>
        String(255)
      </td>

      <td>
        O
      </td>

      <td>
        The customer’s email
      </td>
    </tr>

    <tr>
      <td>
        virtualAccountPhone
      </td>

      <td>
        String(30)
      </td>

      <td>
        O
      </td>

      <td>
        The customer’s phone number
      </td>
    </tr>

    <tr>
      <td>
        trxId
      </td>

      <td>
        String(36)
      </td>

      <td>
        M
      </td>

      <td>
        Alphanumeric string. Preferably UUID. Reference number that should be unique across 3 months. This value should be filled with the same value as **X-EXTERNAL-ID**<br />**Note:** Allowed Symbols are dash(-), underscore(\_), tilde (\~), and dot (.). Any request containing unauthorized symbols will be automatically declined.
      </td>
    </tr>

    <tr>
      <td>
        totalAmount
      </td>

      <td>
        Object
      </td>

      <td>
        M
      </td>

      <td>
        For **Multi-use** VA with flexible amount, merchant should fill the totalAmount field with a totalAmount.value of at least **1.00**
      </td>
    </tr>

    <tr>
      <td>
        totalAmount.value
      </td>

      <td>
        String (16, 2)
      </td>

      <td>
        M
      </td>

      <td>
        The numeric string of the amount up to two decimal places
      </td>
    </tr>

    <tr>
      <td>
        totalAmount.currency
      </td>

      <td>
        String (3)
      </td>

      <td>
        M
      </td>

      <td>
        The currency of the value paid. Should be **IDR**
      </td>
    </tr>

    <tr>
      <td>
        expiredDate
      </td>

      <td>
        String (25)
      </td>

      <td>
        O
      </td>

      <td>
        Indicate the deadline the virtual account should be paid at the latest. Beyond the specified time it will be marked as expired.

        The default expiry time is **24 hours**.

        For **Multi-use VA, this value will be ignored** and the expiry time will always be **6 months after creation** for the first payment and indefinite for the next payments
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo
      </td>

      <td>
        Object
      </td>

      <td>
        M
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.bank
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Indicates the bank chosen to create the VA at. The banks that can be used will differ based on the banks chosen by the merchant during the onboarding process. Possible values are

        - Permata (`permata`)
        - BCA (`bca`)
        - Mandiri (`mandiri`)
        - CIMB (`cimb`)
        - BNI (`bni`)
        - BRI (`bri`)
        - Danamon (`danamon`)
        - BSI (`bsi`)
        - SeaBank (`seabank`)
        - Saqu (`saqu`)
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.merchantId
      </td>

      <td>
        String(10)
      </td>

      <td>
        M
      </td>

      <td>
        This will be the _merchantId_ shared during the onboarding process
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.subCompanyCode
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        This field can be used if the VA being created is BCA. It can filled with BCA’s sub company code value

        - _Note:_\* Default is 00000.
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.freeText
      </td>

      <td>
        Array of Objects
      </td>

      <td>
        O
      </td>

      <td>
        Will be used by the bank to show to the consumer in the bank app

        - _Note:_\* Right now only used for BCA VA.
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.freeText.inquiry
      </td>

      <td>
        Object
      </td>

      <td>
        O
      </td>

      <td>
        Will be used by the bank to show to the consumer at the inquiry process
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.freeText.inquiry.english
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        English description of the inquiry text
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.freeText.inquiry.indonesia
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Bahasa Indonesia version of the inquiry text
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.freeText.payment
      </td>

      <td>
        Object
      </td>

      <td>
        O
      </td>

      <td>
        Will be used by the bank to show to the consumer after the payment process
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.freeText.payment.english
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        English description of the payment text
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.freeText.payment.indonesia
      </td>

      <td>
        String
      </td>

      <td>
        O
      </td>

      <td>
        Bahasa Indonesia version of the payment text
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.mandiri
      </td>

      <td>
        Array of Objects
      </td>

      <td>
        C
      </td>

      <td>
        Array of Mandiri bill description.<br />(this will become **mandatory** , if Mandiri is chosen as the VA method - **additionalInfo.bank = "mandiri"**)
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.mandiri.billInfo1
      </td>

      <td>
        String (10)
      </td>

      <td>
        C
      </td>

      <td>
        Label 1. Mandiri allows only 10 characters. Exceeding characters will be **truncated**.<br />(this will become mandatory , if Mandiri is chosen as the VA method - **additionalInfo.bank = "mandiri"**)
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.mandiri.billInfo2
      </td>

      <td>
        String (30)
      </td>

      <td>
        C
      </td>

      <td>
        Value for Label 1. Mandiri allows only 30 characters. Exceeding characters will be **truncated**.<br />(this will become **mandatory**, if Mandiri is chosen as the VA method - **additionalInfo.bank = "mandiri"**)
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.mandiri.billInfo3
      </td>

      <td>
        String (10)
      </td>

      <td>
        O
      </td>

      <td>
        Label 2. Mandiri allows only 10 characters. Exceeding characters will be **truncated**.
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.mandiri.billInfo4
      </td>

      <td>
        String (30)
      </td>

      <td>
        O
      </td>

      <td>
        Value for Label 2. Mandiri allows only 30 characters. Exceeding characters will be **truncated**.
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.mandiri.billInfo5
      </td>

      <td>
        String (10)
      </td>

      <td>
        O
      </td>

      <td>
        Label 3. Mandiri allows only 10 characters. Exceeding characters will be **truncated**.
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.mandiri.billInfo6
      </td>

      <td>
        String (30)
      </td>

      <td>
        O
      </td>

      <td>
        Value for Label 3. Mandiri allows only 30 characters. Exceeding characters will be **truncated**.
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.mandiri.billInfo7
      </td>

      <td>
        String (10)
      </td>

      <td>
        O
      </td>

      <td>
        Label 4. Mandiri allows only 10 characters. Exceeding characters will be **truncated**.
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.mandiri.billInfo8
      </td>

      <td>
        String (30)
      </td>

      <td>
        O
      </td>

      <td>
        Value for Label 4. Mandiri allows only 30 characters. Exceeding characters will be **truncated**.
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customField
      </td>

      <td>
        Object
      </td>

      <td>
        O
      </td>

      <td>
        A collection of up to three fields that can be customized by the merchant. These fields will be sent by Midtrans on the HTTP notification. It will also be displayed on the Dashboard under “order detail”
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customField.1
      </td>

      <td>
        String(255)
      </td>

      <td>
        O
      </td>

      <td>
        First field that contains the custom data set by the merchant
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customField.2
      </td>

      <td>
        String(255)
      </td>

      <td>
        O
      </td>

      <td>
        Second field that contains the custom data set by the merchant
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customField.3
      </td>

      <td>
        String(255)
      </td>

      <td>
        O
      </td>

      <td>
        Third field that contains the custom data set by the merchant
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails
      </td>

      <td>
        Object
      </td>

      <td>
        O
      </td>

      <td>
        Customer Detail Information
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails.phone
      </td>

      <td>
        String(15)
      </td>

      <td>
        O
      </td>

      <td>
        Customer Phone number
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails.email
      </td>

      <td>
        String(255)
      </td>

      <td>
        O
      </td>

      <td>
        Customer email
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails.firstName
      </td>

      <td>
        String(255)
      </td>

      <td>
        O
      </td>

      <td>
        Customer First Name<br />Will be shown to user during inquiry
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails.lastName
      </td>

      <td>
        String(255)
      </td>

      <td>
        O
      </td>

      <td>
        Customer Last Name<br />Will be shown to user during inquiry
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails.billingAddress
      </td>

      <td>
        Object
      </td>

      <td>
        O
      </td>

      <td>
        Customer billing address
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails.billingAddress.firstName
      </td>

      <td>
        String(255)
      </td>

      <td>
        O
      </td>

      <td>
        Billing address first name
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails.billingAddress.lastName
      </td>

      <td>
        String(255)
      </td>

      <td>
        O
      </td>

      <td>
        Billing address last name
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails.billingAddress.phone
      </td>

      <td>
        String(15)
      </td>

      <td>
        O
      </td>

      <td>
        Billing address phone
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails.billingAddress.address
      </td>

      <td>
        String(255)
      </td>

      <td>
        O
      </td>

      <td>
        Billing address detail
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails.billingAddress.city
      </td>

      <td>
        String(255)
      </td>

      <td>
        O
      </td>

      <td>
        Billing address city
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails.billingAddress.postalCode
      </td>

      <td>
        String(255)
      </td>

      <td>
        O
      </td>

      <td>
        Billing address postal code
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails.billingAddress.countryCode
      </td>

      <td>
        String(15)
      </td>

      <td>
        O
      </td>

      <td>
        Billing address country code
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails.shippingAddress
      </td>

      <td>
        Object
      </td>

      <td>
        O
      </td>

      <td>
        Customer shipping address
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails.shippingAddress.firstName
      </td>

      <td>
        String(255)
      </td>

      <td>
        O
      </td>

      <td>
        Shipping address first name
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails.shippingAddress.lastName
      </td>

      <td>
        String(255)
      </td>

      <td>
        O
      </td>

      <td>
        Shipping address last name
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails.shippingAddress.phone
      </td>

      <td>
        String(15)
      </td>

      <td>
        O
      </td>

      <td>
        Shipping address phone
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails.shippingAddress.address
      </td>

      <td>
        String(255)
      </td>

      <td>
        O
      </td>

      <td>
        Shipping address detail
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails.shippingAddress.city
      </td>

      <td>
        String(255)
      </td>

      <td>
        O
      </td>

      <td>
        Shipping address city
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails.shippingAddress.postalCode
      </td>

      <td>
        String(255)
      </td>

      <td>
        O
      </td>

      <td>
        Shipping address postal code
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.customerDetails.shippingAddress.countryCode
      </td>

      <td>
        String(15)
      </td>

      <td>
        O
      </td>

      <td>
        Shipping address country code<br />Note: Currently only IDN is supported.
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.items
      </td>

      <td>
        Array of Objects
      </td>

      <td>
        C
      </td>

      <td>
        Item Details<br />Mandatory for Mandiri B2B VA only
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.items\[x].id
      </td>

      <td>
        String(32)
      </td>

      <td>
        O
      </td>

      <td>
        Item ID
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.items\[x].price
      </td>

      <td>
        Object
      </td>

      <td>
        M
      </td>

      <td>
        Price of the item in IDR.
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.items\[x].price.value
      </td>

      <td>
        String (16,2)
      </td>

      <td>
        M
      </td>

      <td>
        The numeric string of the amount up to two decimal places
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.items\[x].price.currency
      </td>

      <td>
        String(3)
      </td>

      <td>
        M
      </td>

      <td>
        Item Price currency. Should be IDR.
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.items\[x].quantity
      </td>

      <td>
        Number
      </td>

      <td>
        M
      </td>

      <td>
        Quantity of the item purchased by the customer.
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.items\[x].name
      </td>

      <td>
        String(64)
      </td>

      <td>
        M
      </td>

      <td>
        Name of the item.
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.items\[x].merchantName
      </td>

      <td>
        String(64)
      </td>

      <td>
        O
      </td>

      <td>
        Name of the merchant selling the item.
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.items\[x].brand
      </td>

      <td>
        String(64)
      </td>

      <td>
        O
      </td>

      <td>
        Brand name of the item.
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.items\[x].category
      </td>

      <td>
        String(64)
      </td>

      <td>
        O
      </td>

      <td>
        Category of the item.
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.items\[x].url
      </td>

      <td>
        String(64)
      </td>

      <td>
        O
      </td>

      <td>
        HTTP URL of the item in the merchant site
      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.flags
      </td>

      <td>
        Object
      </td>

      <td>
        O
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        additionalInfo.flags.shouldRandomizeVaNumber
      </td>

      <td>
        Boolean
      </td>

      <td>
        O
      </td>

      <td>
        When this field is set to **true**, then the VA number suffix (**customerNo**) will be randomized.

        We also suggest to fill **customerNo** with "0000000000" and **virtualAccountNo** with **partnerServiceId** + "0000000000".

        If this value is not sent, Midtrans will acknowledge that merchant do not want to randomize the VA number.
      </td>
    </tr>
  </tbody>
</Table>

<br />

<br />

> 🚧
>
> Note: this is an exhaustive list, please read the API specification above on how to use it.

<br />

> 📘 Specific bank requirements
>
> For BCA VA, limit the customer names (**first\_name** and **last\_name**), to only 30 characters.
>
> For BNI VA, phone number format should start with +62 or 0 +\[area code] with max char = 30. If passed incorrectly, trx will be rejected.

<br />

<br />

> 📘 Custom VA Number
>
> As per mentioned above, this field will be the combination of **partnerServiceId** + **customerNo** , there's some rules that needs to be followed if we want to define our own VA number for our customer :
>
> **General Rules**
>
> * Only digits are allowed.
> * Different banks have different specs on their custom VA numbers. (Please refer to the "**Additional Rules**" below this section)
> * If the number provided is already utilized for another order, then a different unique number will be used instead.
> * If the number provided is longer than the maximum character (***MaxChar***), then the unnecessary digits in the end will be trimmed.
> * If the number provided is shorter than the minimum character (***MinChar***), then **customerNo** will be prefixed with zeros.
>
> **Additional Rules**
>
> These additional rules need to be implemented because each bank have their own accepted format and some of them have unique logic that we need to follow, so the VA number that we create could be accepted by the respective banks.
>
> * CIMB : MaxChar = 16 ; MinChar = 16
> * BCA : MaxChar = 23 ; MinChar = **partnerServiceId** + 6
> * BRI : MaxChar = 18 ; MinChar = 18
> * Mandiri : MaxChar = **partnerServiceId** + 12 ; MinChar = **partnerServiceId** + 6
> * Permata : MaxChar = 16 ; MinChar = 16 ; **partnerServiceId** will always be suffixed with 2 random char sequence number.
> * Danamon : MaxChar = **partnerServiceId** + 12 ; MinChar = **partnerServiceId** + 12
> * BSI: MaxChar = **partnerServiceId** + 12 ; MinChar = **partnerServiceId** + 12
> * SeaBank: MaxChar = **partnerServiceId** + 19 ; MinChar = **partnerServiceId** + 10
> * Saqu: MaxChar = **partnerServiceId** + 12 ; MinChar = **partnerServiceId** + 12
>
> **BNI VA Unique rules**
>
> For BNI, **partnerServiceId** will be altered first, and then MinChar & MaxChar logic will be adjusted using the result of altered **partnerServiceId**
>
> If **partnerServiceId** == 3 char, **partnerServiceId** will prefixed by **"8"**, other than that, it'll be prefixed with **"988"**
>
> For
>
> Prefix = **"8"** , then MaxChar = **partnerServiceId** + 12 ; MinChar = **partnerServiceId** + 12
>
> Prefix = **"988"** , then MaxChar = **parterServiceId** + 8 ; MinChar = **partnerServiceId** + 8
>
> \**When you see MaxChar having an equals value with MinChar, that means any exceeding number will be trimmed, and any deficient number will be left padded with 0.*

```
{
    "partnerServiceId": "   70012",
    "customerNo": "6280123456",
    "virtualAccountNo": "   700126280123456",
    "virtualAccountName": "Jokul Doe",
    "virtualAccountEmail": "jokul@email.com",
    "virtualAccountPhone": "6281828384858",
    "trxId": "midtrans-testing-001",
    "totalAmount": {
        "value": "10000.00",
        "currency": "IDR"
    },
    "additionalInfo": {
        "merchantId": "G059876677",
        "bank": "mandiri",
        "flags": {
                "shouldRandomizeVaNumber": false
            },
        "mandiri": {
            "billInfo1": "bank_name",
            "billInfo2": "mandiri",
            "billInfo3": "Name:",
            "billInfo4": "Budi Utomo",
            "billInfo5": "Class:",
            "billInfo6": "Computer Science",
            "billInfo7": "ID:",
            "billInfo8": "VT-12345"
        },
        "customerDetails": {
            "firstName": "Jokul",
            "lastName": "Doe",
            "email": "jokul@email.com",
            "phone": "+6281828384858",
            "billingAddress": {
                "firstName": "Jukul",
                "lastName": "Doe",
                "address": "Kalibata",
                "city": "Jakarta",
                "postalCode": "12190",
                "phone": "+6281828384858",
                "countryCode": "IDN"
            },
            "shippingAddress": {
                "firstName": "Jukul",
                "lastName": "Doe",
                "address": "Kalibata",
                "city": "Jakarta",
                "postalCode": "12190",
                "phone": "+6281828384858",
                "countryCode": "IDN"
            }
        },
        "customField": {
            "1": "custom-field-1",
            "2": "custom-field-2",
            "3": "custom-field-3"
        },
        "items": [
            {
                "id": "a1",
                "price": {
                    "value": "1000.00",
                    "currency": "IDR"
                },
                "quantity": 3,
                "name": "Apel",
                "brand": "Fuji Apple",
                "category": "Fruit",
                "merchantName": "Fruit-store"

            },
            {
                "id": "a2",
                "price": {
                    "value": "1000.00",
                    "currency": "IDR"
                },
                "quantity": 7,
                "name": "Apel Malang",
                "brand": "Fuji Apple",
                "category": "Fruit",
                "merchantName": "Fruit-store"
            }
        ]
    }
}

```

## Response Header

| Field Name   | Field Type | Mandatory | Field Description                                |
| :----------- | :--------- | :-------- | :----------------------------------------------- |
| Content-Type | String     | M         | Media type of the resource, i.e application/json |
| X-TIMESTAMP  | String     | M         | Client's current local time in ISO-8601          |

```
Content-type:application/json
X-TIMESTAMP:2020-01-01T00:00:00+07:00
```

## Response Body

<table>
  <tr>
    <td><strong>Field Name</strong></td>
    <td><strong>Field Type</strong></td>
    <td><strong>Mandatory</strong></td>
    <td colspan="2"><strong>Field Description</strong></td>
  </tr>

  <tr>
    <td>responseCode</td>
    <td>String(7)</td>
    <td>M</td>
    <td colspan="2">Status code of transaction charge result.</td>
  </tr>

  <tr>
    <td>responseMessage</td>
    <td>String(150)</td>
    <td>M</td>
    <td colspan="2">Description of transaction charge result.</td>
  </tr>

  <tr>
    <td>virtualAccountData</td>
    <td>M</td>
    <td>Object</td>

    <td colspan="2"></td>
  </tr>

  <tr>
    <td>virtualAccountData.partnerServiceId</td>
    <td>M</td>
    <td>String(8)</td>
    <td colspan="2">Company code - will be shared by Midtrans during the onboarding process. Will be left-padded up to 8 characters long</td>
  </tr>

  <tr>
    <td>virtualAccountData.customerNo</td>
    <td>M</td>
    <td>String(20)</td>
    <td colspan="2">Suffix of the VA number. The value will either be randomized or contains the customerNo sent in the request as a substring. Maximum length depends on the bank.</td>
  </tr>

  <tr>
    <td>virtualAccountData.virtualAccountNo</td>
    <td>M</td>
    <td>String(28)</td>
    <td colspan="2">Number generated using the partnerServiceId and the given customerNo in the request.<br /><strong>Note: </strong>The VA number generated will not always be the <em>request.partnerServiceid + request.customerNo</em>. Please use this field as the source of truth for VA number.</td>
  </tr>

  <tr>
    <td>virtualAccountData.virtualAccountName</td>
    <td>M</td>
    <td>String (255)</td>
    <td colspan="2">The customer name</td>
  </tr>

  <tr>
    <td>virtualAccountData.virtualAccountEmail</td>
    <td>String(255)</td>
    <td>O</td>
    <td colspan="2">The customer’s email</td>
  </tr>

  <tr>
    <td>virtualAccountData.virtualAccountPhone</td>
    <td>String(30)</td>
    <td>O</td>
    <td colspan="2">The customer's phone number</td>
  </tr>

  <tr>
    <td>virtualAccountData.trxId</td>
    <td>String(36)</td>
    <td>M</td>
    <td colspan="2">The identifier for the merchant to use for <em>inquiryRequestId </em>in Inquiry Status API.<br />This value will be the same as the request's <strong><em>trxId</em></strong> and <strong><em>X-EXTERNAL-ID </em></strong></td>
  </tr>

  <tr>
    <td>virtualAccountData.totalAmount</td>
    <td>O</td>
    <td>Object</td>

    <td colspan="2"></td>
  </tr>

  <tr>
    <td>virtualAccountData.totalAmount.value</td>
    <td>M</td>
    <td>String (16,2)</td>
    <td colspan="2">Total Amount up to 2 decimal places based with ISO 4217 format</td>
  </tr>

  <tr>
    <td>virtualAccountData.totalAmount.currency</td>
    <td>M</td>
    <td>String(3)</td>
    <td colspan="2">Currency of amount based on ISO 4217</td>
  </tr>

  <tr>
    <td>virtualAccountData.expiredDate</td>
    <td>O</td>
    <td>String(25)</td>
    <td colspan="2">ISO 8601 Datetime when the VA will be expired if not paid<br />Notes: Multi Use VA will not have this field</td>
  </tr>

  <tr>
    <td>additionalInfo</td>
    <td>Object</td>
    <td>M</td>

    <td colspan="2"></td>
  </tr>

  <tr>
    <td>additionalInfo.bank</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Indicates the bank chosen to create the VA at. The banks that can be used will differ based on the banks chosen by the merchant during the onboarding process. Possible values are: Permata, BCA, Mandiri, CIMB, BNI, BRI, Danamon</td>
  </tr>

  <tr>
    <td>additionalInfo.merchantId</td>
    <td>String(10)</td>
    <td>M</td>
    <td colspan="2">This will be the <em>merchantId<strong> </strong></em>shared during the onboarding process</td>
  </tr>

  <tr>
    <td>additionalInfo.subCompanyCode</td>
    <td>String</td>
    <td>O</td>
    <td colspan="2">This field can be used if the VA being created is BCA. It can filled with BCA's sub company code value</td>
  </tr>

  <tr>
    <td>additionalInfo.freeText</td>
    <td>Array of Objects</td>
    <td>O</td>
    <td colspan="2">Will be used by the bank to show to the consumer in the bank app</td>
  </tr>

  <tr>
    <td>additionalInfo.freeText\[x].inquiry</td>
    <td>Object</td>
    <td>O</td>
    <td colspan="2">Will be used by the bank to show to the consumer after the inquiry process</td>
  </tr>

  <tr>
    <td>additionalInfo.freeText\[x].inquiry.english</td>
    <td>String</td>
    <td>O</td>
    <td colspan="2">English description of the inquiry text</td>
  </tr>

  <tr>
    <td>additionalInfo.freeText\[x].inquiry.indonesia</td>
    <td>String</td>
    <td>O</td>
    <td colspan="2">Bahasa Indonesia version of the inquiry text</td>
  </tr>

  <tr>
    <td>additionalInfo.freeText\[x].payment</td>
    <td>Object</td>
    <td>O</td>
    <td colspan="2">Will be used by the bank to show to the consumer after the payment process</td>
  </tr>

  <tr>
    <td>additionalInfo.freeText\[x].payment.english</td>
    <td>String</td>
    <td>O</td>
    <td colspan="2">English description of the payment text</td>
  </tr>

  <tr>
    <td>additionalInfo.freeText\[x].payment.indonesia</td>
    <td>String</td>
    <td>O</td>
    <td colspan="2">Bahasa Indonesia version of the payment text</td>
  </tr>

  <tr>
    <td>additionalInfo.mandiri</td>
    <td>Object</td>
    <td>O</td>
    <td colspan="2">Array of Mandiri bill description</td>
  </tr>

  <tr>
    <td>additionalInfo.mandiri.billInfo1</td>
    <td>String</td>
    <td>O</td>
    <td colspan="2">Label 1. Mandiri allows only 10 characters. Exceeding characters will be <strong>truncated</strong>.</td>
  </tr>

  <tr>
    <td>additionalInfo.mandiri.billInfo2</td>
    <td>String</td>
    <td>O</td>
    <td colspan="2">Value for Label 1. Mandiri allows only 30 characters. Exceeding characters will be <strong>truncated</strong>.</td>
  </tr>

  <tr>
    <td>additionalInfo.mandiri.billInfo3</td>
    <td>String</td>
    <td>O</td>
    <td colspan="2">Label 2. Mandiri allows only 10 characters. Exceeding characters will be <strong>truncated</strong>.</td>
  </tr>

  <tr>
    <td>additionalInfo.mandiri.billInfo4</td>
    <td>String</td>
    <td>O</td>
    <td colspan="2">Value for Label 2. Mandiri allows only 30 characters. Exceeding characters will be <strong>truncated</strong>.</td>
  </tr>

  <tr>
    <td>additionalInfo.mandiri.billInfo5</td>
    <td>String</td>
    <td>O</td>
    <td colspan="2">Label 3. Mandiri allows only 10 characters. Exceeding characters will be <strong>truncated</strong>.</td>
  </tr>

  <tr>
    <td>additionalInfo.mandiri.billInfo6</td>
    <td>String</td>
    <td>O</td>
    <td colspan="2">Value for Label 3. Mandiri allows only 30 characters. Exceeding characters will be <strong>truncated</strong>.</td>
  </tr>

  <tr>
    <td>additionalInfo.mandiri.billInfo7</td>
    <td>String</td>
    <td>O</td>
    <td colspan="2">Label 4. Mandiri allows only 10 characters. Exceeding characters will be <strong>truncated</strong>.</td>
  </tr>

  <tr>
    <td>additionalInfo.mandiri.billInfo8</td>
    <td>String</td>
    <td>O</td>
    <td colspan="2">Value for Label 4. Mandiri allows only 30 characters. Exceeding characters will be <strong>truncated</strong>.</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails</td>
    <td>Object</td>
    <td>O</td>
    <td colspan="2">Customer Detail Information</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails.phone</td>
    <td>String(15)</td>
    <td>O</td>
    <td colspan="2">Customer Phone number</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails.email</td>
    <td>String(255)</td>
    <td>O</td>
    <td colspan="2">Customer email</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails.firstName</td>
    <td>String(255)</td>
    <td>O</td>
    <td colspan="2">Customer First Name</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails.lastName</td>
    <td>String(255)</td>
    <td>O</td>
    <td colspan="2">Customer Last Name</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails.billingAddress</td>
    <td>Object</td>
    <td>O</td>
    <td colspan="2">Customer billing address</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails.billingAddress.firstName</td>
    <td>String(255)</td>
    <td>O</td>
    <td colspan="2">Billing address first name</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails.billingAddress.lastName</td>
    <td>String(255)</td>
    <td>O</td>
    <td colspan="2">Billing address last name</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails.billingAddress.phone</td>
    <td>String(15)</td>
    <td>O</td>
    <td colspan="2">Billing address phone</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails.billingAddress.address</td>
    <td>String(255)</td>
    <td>O</td>
    <td colspan="2">Billing address detail</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails.billingAddress.city</td>
    <td>String(255)</td>
    <td>O</td>
    <td colspan="2">Billing address city</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails.billingAddress.postalCode</td>
    <td>String(255)</td>
    <td>O</td>
    <td colspan="2">Billing address postal code</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails.billingAddress.countryCode</td>
    <td>String(15)</td>
    <td>O</td>
    <td colspan="2">Billing address country code</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails.shippingAddress</td>
    <td>Object</td>
    <td>O</td>
    <td colspan="2">Customer shipping address</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails.shippingAddress.firstName</td>
    <td>String(255)</td>
    <td>O</td>
    <td colspan="2">Shipping address first name</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails.shippingAddress.lastName</td>
    <td>String(255)</td>
    <td>O</td>
    <td colspan="2">Shipping address last name</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails.shippingAddress.phone</td>
    <td>String(15)</td>
    <td>O</td>
    <td colspan="2">Shipping address phone</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails.shippingAddress.address</td>
    <td>String(255)</td>
    <td>O</td>
    <td colspan="2">Shipping address detail</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails.shippingAddress.city</td>
    <td>String(255)</td>
    <td>O</td>
    <td colspan="2">Shipping address city</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails.shippingAddress.postalCode</td>
    <td>String(255)</td>
    <td>O</td>
    <td colspan="2">Shipping address postal code</td>
  </tr>

  <tr>
    <td>additionalInfo.customerDetails.shippingAddress.countryCode</td>
    <td>String(15)</td>
    <td>O</td>
    <td colspan="2">Shipping address country code</td>
  </tr>

  <tr>
    <td>additionalInfo.items</td>
    <td>Array Of Object</td>
    <td>O</td>
    <td colspan="2">Item Details</td>
  </tr>

  <tr>
    <td>additionalInfo.items\[x].id</td>
    <td>String(32)</td>
    <td>O</td>
    <td colspan="2">Item ID</td>
  </tr>

  <tr>
    <td>additionalInfo.items\[x].price</td>
    <td>Object</td>
    <td>M</td>
    <td colspan="2">Price of the item in IDR.</td>
  </tr>

  <tr>
    <td>additionalInfo.items\[x].price.value</td>
    <td>String (ISO4217)</td>
    <td>M</td>
    <td colspan="2">Item Price value</td>
  </tr>

  <tr>
    <td>additionalInfo.items\[x].price.currency</td>
    <td>String(3)</td>
    <td>M</td>
    <td colspan="2">Item Price currency</td>
  </tr>

  <tr>
    <td>additionalInfo.items\[x].quantity</td>
    <td>String(16)</td>
    <td>M</td>
    <td colspan="2">Quantity of the item purchased by the customer.</td>
  </tr>

  <tr>
    <td>additionalInfo.items\[x].name</td>
    <td>String(64)</td>
    <td>O</td>
    <td colspan="2">Name of the item.</td>
  </tr>

  <tr>
    <td>additionalInfo.items\[x].merchantName</td>
    <td>String(64)</td>
    <td>O</td>
    <td colspan="2">Name of the merchant selling the item.</td>
  </tr>

  <tr>
    <td>additionalInfo.items\[x].brand</td>
    <td>String(64)</td>
    <td>O</td>
    <td colspan="2">Brand name of the item.</td>
  </tr>

  <tr>
    <td>additionalInfo.items\[x].category</td>
    <td>String(64)</td>
    <td>O</td>
    <td colspan="2">Category of the item.</td>
  </tr>

  <tr>
    <td>additionalInfo.items\[x].url</td>
    <td>String(64)</td>
    <td>O</td>
    <td colspan="2">HTTP URL of the item in the merchant site</td>
  </tr>
</table>

```
{
    "responseMessage": "Successful",
    "virtualAccountData": {
        "partnerServiceId": "   70012",
        "customerNo": "6280123456",
        "virtualAccountNo": "   700126280123456",
        "expiredDate": "2024-01-27T14:04:54+07:00",
        "virtualAccountEmail": "jokul@email.com",
        "totalAmount": {
            "value": "10000.00",
            "currency": "IDR"
        },
        "virtualAccountPhone": "6281828384858",
        "additionalInfo": {
            "merchantId": "G059876677",
            "bank": "mandiri",
            "mandiri": {
                "billInfo1": "bank_name",
                "billInfo2": "mandiri",
                "billInfo3": "Name:",
                "billInfo4": "Budi Utomo",
                "billInfo5": "Class:",
                "billInfo6": "Computer Science",
                "billInfo7": "ID:",
                "billInfo8": "VT-12345"
            },
            "customerDetails": {
                "firstName": "Jokul",
                "lastName": "Doe",
                "email": "jokul@email.com",
                "phone": "+6281828384858",
                "billingAddress": {
                    "firstName": "Jukul",
                    "lastName": "Doe",
                    "address": "Kalibata",
                    "city": "Jakarta",
                    "postalCode": "12190",
                    "phone": "+6281828384858",
                    "countryCode": "IDN"
                },
                "shippingAddress": {
                    "firstName": "Jukul",
                    "lastName": "Doe",
                    "address": "Kalibata",
                    "city": "Jakarta",
                    "postalCode": "12190",
                    "phone": "+6281828384858",
                    "countryCode": "IDN"
                }
            },
            "customField": {
                "1": "custom-field-1",
                "2": "custom-field-2",
                "3": "custom-field-3"
            },
            "items": [
                {
                    "id": "a1",
                    "price": {
                        "value": "1000.00",
                        "currency": "IDR"
                    },
                    "quantity": 3,
                    "name": "Apel",
                    "brand": "Fuji Apple",
                    "category": "Fruit",
                    "merchantName": "Fruit-store",
                    "url": "https://www.google.com/search?q=apel"
                },
                {
                    "id": "a2",
                    "price": {
                        "value": "1000.00",
                        "currency": "IDR"
                    },
                    "quantity": 7,
                    "name": "Apel Malang",
                    "brand": "Fuji Apple",
                    "category": "Fruit",
                    "merchantName": "Fruit-store",
                    "url": "https://www.google.com/search?q=apel-malang"
                }
            ]
        },
        "virtualAccountName": "Jokul Doe",
        "trxId": "midtrans-testing-001"
    },
    "responseCode": "2002700"
}
```

## List Response Code

<table>
  <tr>
    <td><strong>Response Code</strong></td>
    <td><strong>HTTP Status Code</strong></td>
    <td><strong>Response Message</strong></td>
  </tr>

  <tr>
    <td>2002700</td>
    <td>200</td>
    <td>Success</td>
  </tr>

  <tr>
    <td>4012700</td>
    <td>401</td>
    <td>Unauthorized. Signature</td>
  </tr>

  <tr>
    <td>5002700</td>
    <td>500</td>
    <td>Internal Server Error</td>
  </tr>

  <tr>
    <td>4002700</td>
    <td>400</td>
    <td>Bad Request</td>
  </tr>

  <tr>
    <td>4002702</td>
    <td>400</td>
    <td>Invalid Mandatory Field.</td>
  </tr>

  <tr>
    <td>4042713</td>
    <td>404</td>
    <td>Transaction Not Found</td>
  </tr>

  <tr>
    <td>4002601</td>
    <td>400</td>
    <td>Invalid Field Format X-TIMESTAMP</td>
  </tr>

  <tr>
    <td>4092700</td>
    <td>409</td>
    <td>Conflict</td>
  </tr>

  <tr>
    <td>4032703</td>
    <td>403</td>
    <td>Suspected Fraud</td>
  </tr>
</table>

***

***

# Inquiry Status - Single Use VA

| Path              | /{version}/transfer-va/status |
| :---------------- | :---------------------------- |
| HTTP Method       | POST                          |
| Version           | v1.0                          |
| SNAP version code | 26                            |

## Request Header

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field Name
      </th>

      <th>
        Field Type
      </th>

      <th>
        Mandatory
      </th>

      <th>
        Field Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Content-Type
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Media type of the resource, i.e. application/json
      </td>
    </tr>

    <tr>
      <td>
        X-TIMESTAMP
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Client’s current local time in ISO-8601 format
      </td>
    </tr>

    <tr>
      <td>
        Authorization
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Represents access\_token of a request; string starts with keyword “Bearer ” followed by access\_token. Can get this from Access Token B2B API response.
      </td>
    </tr>

    <tr>
      <td>
        X-SIGNATURE
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Created using symmetric signature HMAC\_SHA512 algorithm
      </td>
    </tr>

    <tr>
      <td>
        X-PARTNER-ID
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Unique identifier for caller (merchant\_id)
      </td>
    </tr>

    <tr>
      <td>
        CHANNEL-ID
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Mandatory field from Bank Indonesia that can take any value with correct format 5 digits numeric string
      </td>
    </tr>

    <tr>
      <td>
        X-EXTERNAL-ID
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Alphanumeric string. Preferably UUID.  Reference number that should be unique across 3 months. The value should also be the same as _request\_body.trxId_

        - _It’s recommended that the merchant appends the said value with their client\_id_\* (client\_key)
      </td>
    </tr>
  </tbody>
</Table>

```
Content-type:application/json
X-TIMESTAMP:2020-01-01T00:00:00+07:00
X-SIGNATURE:da1fa417c72d6b91c257e01e54fac824
Authorization:Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
X-PARTNER-ID:G12345678
X-EXTERNAL-ID:midtrans-testing-001
CHANNEL-ID:12345
```

## Request Body

<table>
  <tr>
    <td><strong>Field Name</strong></td>
    <td><strong>Field Type</strong></td>
    <td><strong>Mandatory</strong></td>
    <td colspan="2"><strong>Field Description</strong></td>
  </tr>

  <tr>
    <td>partnerServiceId</td>
    <td>M</td>
    <td>String(8)</td>
    <td colspan="2">partnerServiceId from Create VA Response</td>
  </tr>

  <tr>
    <td>customerNo</td>
    <td>M</td>
    <td>String(20)</td>
    <td colspan="2">customerNo from Create VA Response</td>
  </tr>

  <tr>
    <td>virtualAccountNo</td>
    <td>M</td>
    <td>String(28)</td>
    <td colspan="2">virtualAccountNo from Create VA Response</td>
  </tr>

  <tr>
    <td>inquiryRequestId</td>
    <td>M</td>
    <td>String(128)</td>
    <td colspan="2">The <em>trxId<strong> </strong></em>from createVA response.</td>
  </tr>

  <tr>
    <td>additionalInfo</td>
    <td>Object</td>

    <td></td>

    <td colspan="2"></td>
  </tr>

  <tr>
    <td>additionalInfo.merchantId</td>
    <td>String(10)</td>
    <td>M</td>
    <td colspan="2">This is the <em>merchantId </em>shared by Midtrans during the onboarding process</td>
  </tr>
</table>

```
{
   "inquiryRequestId": "midtrans-testing-001",
   "partnerServiceId": "   70012",
   "customerNo": "6280123456",
   "virtualAccountNo": "   700126280123456",
   "additionalInfo": {
       "merchantId": "G059876677"
   }
}

```

## Response Header

| Field Name   | Field Type | Mandatory | Field Description                                |
| :----------- | :--------- | :-------- | :----------------------------------------------- |
| Content-Type | String     | M         | Media type of the resource, i.e application/json |
| X-TIMESTAMP  | String     | M         | Client's current local time in ISO-8601          |

```
Content-type:application/json
X-TIMESTAMP:2020-01-01T00:00:00+07:00
```

## Response Body

<table>
  <tr>
    <td><strong>Field Name</strong></td>
    <td><strong>Field Type</strong></td>
    <td><strong>Mandatory</strong></td>
    <td colspan="2"><strong>Field Description</strong></td>
  </tr>

  <tr>
    <td>responseCode</td>
    <td>String(7)</td>
    <td>M</td>
    <td colspan="2">Status code of transaction charge result.</td>
  </tr>

  <tr>
    <td>responseMessage</td>
    <td>String(150)</td>
    <td>M</td>
    <td colspan="2">Description of transaction charge result.</td>
  </tr>

  <tr>
    <td>virtualAccountData</td>
    <td>M</td>
    <td>Object</td>

    <td colspan="2"></td>
  </tr>

  <tr>
    <td>virtualAccountData.paymentFlagReason</td>
    <td>O</td>
    <td>Object</td>

    <td colspan="2"></td>
  </tr>

  <tr>
    <td>virtualAccountData.paymentFlagReason.english</td>
    <td>O</td>
    <td>String(200)</td>
    <td colspan="2">Reason for Payment Status in English</td>
  </tr>

  <tr>
    <td>virtualAccountData.partnerServiceId</td>
    <td>M</td>
    <td>String(8)</td>
    <td colspan="2">customerNo from Create VA Response</td>
  </tr>

  <tr>
    <td>virtualAccountData.customerNo</td>
    <td>M</td>
    <td>String(20)</td>
    <td colspan="2">virtualAccountNo from Create VA Response</td>
  </tr>

  <tr>
    <td>virtualAccountData.virtualAccountNo</td>
    <td>M</td>
    <td>String(28)</td>
    <td colspan="2">The trxId from createVA response</td>
  </tr>

  <tr>
    <td>virtualAccountData.inquiryRequestId</td>
    <td>M</td>
    <td>String(128)</td>
    <td colspan="2">Identifier to be used for performing inquiry<br />This will be the same value as the <em>request.inquiryRequestId</em></td>
  </tr>

  <tr>
    <td>virtualAccountData.paymentRequestId</td>
    <td>C</td>
    <td>String(128)</td>
    <td colspan="2">Unique identifier for this Payment from Midtrans.<br />This value will exist if the payment has been completed</td>
  </tr>

  <tr>
    <td>virtualAccountData.totalAmount</td>
    <td>O</td>
    <td>Object</td>

    <td colspan="2"></td>
  </tr>

  <tr>
    <td>virtualAccountData.totalAmount.value</td>
    <td>M</td>
    <td>String (16,2)</td>
    <td colspan="2">Total Amount up to 2 decimal places based with ISO 4217 format</td>
  </tr>

  <tr>
    <td>virtualAccountData.totalAmount.currency</td>
    <td>M</td>
    <td>String(3)</td>
    <td colspan="2">Currency of amount based on ISO 4217</td>
  </tr>

  <tr>
    <td>virtualAccountData.trxDateTime</td>
    <td>O</td>
    <td>Date(25)</td>
    <td colspan="2">ISO-8601 datetime in GMT+7 when the VA is created</td>
  </tr>

  <tr>
    <td>virtualAccountData.transactionDate</td>
    <td>O</td>
    <td>Date(25)</td>
    <td colspan="2">ISO-8601 datetime in GMT+7 when the VA was paid<br />This field will exist if the VA has been paid</td>
  </tr>

  <tr>
    <td>virtualAccountData.paymentFlagStatus</td>
    <td>O</td>
    <td>String(2)</td>
    <td colspan="2">Status for Payment Flag<br />00 - Success<br />03 - Pending<br />05 - Canceled<br />08 - Expired</td>
  </tr>

  <tr>
    <td>virtualAccountData.paymentFlagReason</td>
    <td>O</td>
    <td>Object</td>
    <td colspan="2">Contains explanation for the payment flag status in different languages</td>
  </tr>

  <tr>
    <td>virtualAccountData.paymentFlagReason.english</td>
    <td>O</td>
    <td>String</td>
    <td colspan="2">Explanation for payment flag status in English</td>
  </tr>

  <tr>
    <td>additionalInfo</td>
    <td>O</td>
    <td>Object</td>

    <td colspan="2"></td>
  </tr>

  <tr>
    <td>additionalInfo.merchantId</td>
    <td>M</td>
    <td>String (10)</td>
    <td colspan="2">This is the <em>merchantId </em>shared by Midtrans during the onboarding process</td>
  </tr>
</table>

```
{
    "additionalInfo": {
        "merchantId": "G059876677"
    },
    "responseMessage": "Successful",
    "virtualAccountData": {
        "partnerServiceId": "   70012",
        "customerNo": "6280123456",
        "virtualAccountNo": "   700126280123456",
        "totalAmount": {
            "currency": "IDR",
            "value": "10000.00"
        },
        "paymentFlagReason": {
            "english": "settlement"
        },
        "paymentFlagStatus": "00",
        "trxDateTime": "2024-04-19T15:18:13+07:00",
        "transactionDate": "2024-04-19T15:19:09+07:00",
        "inquiryRequestId": "midtrans-testing-001",
        "paymentRequestId": "A120240419081813bceyKQUK3iID"
    },
    "responseCode": "2002600"
}
```

## List Response Code

<table>
  <tr>
    <td><strong>Response Code</strong></td>
    <td><strong>HTTP Status Code</strong></td>
    <td><strong>Response Message</strong></td>
  </tr>

  <tr>
    <td>2002600</td>
    <td>200</td>
    <td>Success</td>
  </tr>

  <tr>
    <td>4012600</td>
    <td>401</td>
    <td>Unauthorized. Signature</td>
  </tr>

  <tr>
    <td>4012600</td>
    <td>401</td>
    <td>Unauthorized. Merchant does not have access</td>
  </tr>

  <tr>
    <td>4042601</td>
    <td>404</td>
    <td>Transaction Not Found</td>
  </tr>

  <tr>
    <td>4002602</td>
    <td>400</td>
    <td>Invalid Mandatory Field</td>
  </tr>

  <tr>
    <td>5002600</td>
    <td>500</td>
    <td>Internal Server Error</td>
  </tr>
</table>

***

***

# Inquiry Status - Multi Use VA

| Path              | /{version}/transfer-va/status |
| :---------------- | :---------------------------- |
| HTTP Method       | POST                          |
| Version           | v1.0                          |
| SNAP version code | 26                            |

## Request Header

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field Name
      </th>

      <th>
        Field Type
      </th>

      <th>
        Mandatory
      </th>

      <th>
        Field Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Content-Type
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Media type of the resource, i.e. application/json
      </td>
    </tr>

    <tr>
      <td>
        X-TIMESTAMP
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Client’s current local time in ISO-8601 format
      </td>
    </tr>

    <tr>
      <td>
        Authorization
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Represents access\_token of a request; string starts with keyword “Bearer ” followed by access\_token. Can get this from Access Token B2B API response.
      </td>
    </tr>

    <tr>
      <td>
        X-SIGNATURE
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Created using symmetric signature HMAC\_SHA512 algorithm
      </td>
    </tr>

    <tr>
      <td>
        X-PARTNER-ID
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Unique identifier for caller (merchant\_id)
      </td>
    </tr>

    <tr>
      <td>
        CHANNEL-ID
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Mandatory field from Bank Indonesia that can take any value with correct format 5 digits numeric string
      </td>
    </tr>

    <tr>
      <td>
        X-EXTERNAL-ID
      </td>

      <td>
        String
      </td>

      <td>
        M
      </td>

      <td>
        Alphanumeric string. Preferably UUID.  Reference number that should be unique across 3 months. The value should also be the same as _request\_body.trxId_

        - _It’s recommended that the merchant appends the said value with their client\_id_\* (client\_key)
      </td>
    </tr>
  </tbody>
</Table>

```
Content-type:application/json
X-TIMESTAMP:2020-01-01T00:00:00+07:00
X-SIGNATURE:da1fa417c72d6b91c257e01e54fac824
Authorization:Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
X-PARTNER-ID:G12345678
X-EXTERNAL-ID:midtrans-testing-001
CHANNEL-ID:12345
```

## Request Body

<table>
  <tr>
    <td>partnerServiceId</td>
    <td>String(8)</td>
    <td>M</td>
    <td colspan="2">partnerServiceId from Create VA Response</td>
  </tr>

  <tr>
    <td>customerNo</td>
    <td>String(20)</td>
    <td>M</td>
    <td colspan="2">customerNo from Create VA Response</td>
  </tr>

  <tr>
    <td>virtualAccountNo</td>
    <td>String(28)</td>
    <td>M</td>
    <td colspan="2">virtualAccountNo from Create VA Response</td>
  </tr>

  <tr>
    <td>inquiryRequestId</td>
    <td>String(128)</td>
    <td>M</td>
    <td colspan="2">The <em>trxId<strong> </strong></em>from createVA response.</td>
  </tr>

  <tr>
    <td>additionalInfo</td>
    <td>Object</td>

    <td></td>

    <td colspan="2"></td>
  </tr>

  <tr>
    <td>additionalInfo.merchantId</td>
    <td>String(10)</td>
    <td>M</td>
    <td colspan="2">This is the <em>merchantId </em>shared by Midtrans during the onboarding process</td>
  </tr>

  <tr>
    <td>additionalInfo.page</td>
    <td>String</td>
    <td>O</td>
    <td colspan="2">Index of the search. Default is 0. Min page is 0.</td>
  </tr>

  <tr>
    <td>additionalInfo.pageSize</td>
    <td>String</td>
    <td>O</td>
    <td colspan="2">Number of transactions displayed per page. Default is 10. Max page\_size is 15. Min page\_size is 1.<br />Example : Merchant has five transactions created under a certain order\_id. The transactions are A, B, C, D, E, F (ordered to the latest).<br />Below are the examples on how merchants can use page and pageSize parameters.<br />pageSize is not set, page is not set: Merchant gets F, E, D, C, B, A<br />pageSize is set 2, page is not set: Merchant gets F, E<br />pageSize is set 2, page is set 1: Merchant gets D, C<br />pageSize is set 3, page is set 1: Merchant gets C, B, A</td>
  </tr>
</table>

```
{
   "inquiryRequestId": "midtrans-testing-001",
   "partnerServiceId": "   70012",
   "customerNo": "6280123456",
   "virtualAccountNo": "   700126280123456",
   "additionalInfo": {
       "merchantId": "G059876677",
       "page": "0",
       "pageSize": "2"
   }
}
```

## Response Body

<table>
  <tr>
    <td><strong>Field Name</strong></td>
    <td><strong>Field Type</strong></td>
    <td><strong>Mandatory</strong></td>
    <td colspan="2"><strong>Field Description</strong></td>
  </tr>

  <tr>
    <td>responseCode</td>
    <td>String(7)</td>
    <td>M</td>
    <td colspan="2">Status code of transaction charge result.</td>
  </tr>

  <tr>
    <td>responseMessage</td>
    <td>String(150)</td>
    <td>M</td>
    <td colspan="2">Description of transaction charge result.</td>
  </tr>

  <tr>
    <td>virtualAccountData</td>
    <td>Object</td>
    <td>M</td>

    <td colspan="2"></td>
  </tr>

  <tr>
    <td>virtualAccountData.partnerServiceId</td>
    <td>String(8)</td>
    <td>M</td>
    <td colspan="2">Derivative of X- PARTNER- ID, similar to company code, 8 digit left padding space.</td>
  </tr>

  <tr>
    <td>virtualAccountData.customerNo</td>
    <td>String(20)</td>
    <td>M</td>
    <td colspan="2">Unique number (up to 20 digits).</td>
  </tr>

  <tr>
    <td>virtualAccountData.virtualAccountNo</td>
    <td>String(28)</td>
    <td>M</td>
    <td colspan="2">partnerServiceId (8 digit left padding 0) + customerNo (up to 20 digits).</td>
  </tr>

  <tr>
    <td>virtualAccountData.inquiryRequestId</td>
    <td>String(128)</td>
    <td>M</td>
    <td colspan="2">trxId sent in Create VA</td>
  </tr>

  <tr>
    <td>additionalInfo</td>

    <td></td>

    <td></td>

    <td colspan="2"></td>
  </tr>

  <tr>
    <td>additionalInfo.merchantId</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">This is the merchantId shared by Midtrans during the onboarding process</td>
  </tr>

  <tr>
    <td>additionalInfo.recurringPaymentDetail</td>
    <td>Object</td>
    <td>O</td>

    <td colspan="2"></td>
  </tr>

  <tr>
    <td>additionalInfo.recurringPaymentDetail.recurringOrders</td>
    <td>Array of Objects</td>
    <td>M</td>
    <td colspan="2">All payments related to the parent order trxId</td>
  </tr>

  <tr>
    <td>additionalInfo.recurringPaymentDetail.recurringOrders\[0].totalAmount</td>
    <td>Object</td>
    <td>M</td>

    <td colspan="2"></td>
  </tr>

  <tr>
    <td>additionalInfo.recurringPaymentDetail.recurringOrders\[0].totalAmount.value</td>
    <td>String(ISO 4217) (16,2)</td>
    <td>M</td>
    <td colspan="2">Total Amount with 2 decimal</td>
  </tr>

  <tr>
    <td>additionalInfo.recurringPaymentDetail.recurringOrders\[0].totalAmount.currency</td>
    <td>String(3)</td>
    <td>M</td>
    <td colspan="2">Currency of amount based on ISO 4217</td>
  </tr>

  <tr>
    <td>additionalInfo.recurringPaymentDetail.recurringOrders\[0].paymentFlagReason</td>
    <td>Object</td>
    <td>M</td>

    <td colspan="2"></td>
  </tr>

  <tr>
    <td>additionalInfo.recurringPaymentDetail.recurringOrders\[0].paymentFlagReason.english</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Reason for Payment Status in English</td>
  </tr>

  <tr>
    <td>additionalInfo.recurringPaymentDetail.recurringOrders\[0].paymentRequestId</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Midtrans order id</td>
  </tr>

  <tr>
    <td>additionalInfo.recurringPaymentDetail.recurringOrders\[0].paymentFlagStatus</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Status for Payment Flag<br />00 - Success<br />03 - Pending<br />05 - Canceled<br />08 - Expired</td>
  </tr>

  <tr>
    <td>additionalInfo.recurringPaymentDetail.recurringOrders\[0].trxDateTime</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Datetime when the order created in GMT+7. ISO-8601</td>
  </tr>

  <tr>
    <td>additionalInfo.recurringPaymentDetail.recurringOrders\[0].transactionDate</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Datetime when the payment happened in GMT+7. ISO-8601</td>
  </tr>

  <tr>
    <td>additionalInfo.recurringPaymentDetail.recurringOrders\[0].trxId</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">trxId, appended with randomly generated identifier for second payment and so on<br />Sample first payment: merchant\_order\_id<br />Sample: merchant\_order\_id-030424072903549oVvY</td>
  </tr>

  <tr>
    <td>additionalInfo.recurringPaymentDetail.paginationMetadata</td>
    <td>Object</td>
    <td>M</td>
    <td colspan="2">Pagination of the orders</td>
  </tr>

  <tr>
    <td>additionalInfo.recurringPaymentDetail.paginationMetadata.total</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Total orders related to the trxId</td>
  </tr>

  <tr>
    <td>additionalInfo.recurringPaymentDetail.paginationMetadata.pageSize</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Number of transactions displayed per page.</td>
  </tr>

  <tr>
    <td>additionalInfo.recurringPaymentDetail.paginationMetadata.page</td>
    <td>String</td>
    <td>M</td>
    <td colspan="2">Index of the search.</td>
  </tr>
</table>

```
{
    "responseCode": "2002600",
    "responseMessage": "Successful"
    "virtualAccountData": {
        "partnerServiceId": "   70012",
        "customerNo": "6280123456",
        "virtualAccountNo": "   700126280123456"
    },
    "additionalInfo": {
        "merchantId": "G12345463",
        "recurringPaymentDetail": {
            "recurringOrders": [
                {
                    "totalAmount": {
                        "currency": "IDR",
                        "value": "150000.00"
                    },
                    "paymentFlagReason": {
                        "english": "settlement"
                    },
                    "paymentRequestId": "A120240403072903E6HgHZoE3bID",
                    "paymentFlagStatus": "00",
                    "trxDateTime": "2024-04-03T14:29:03+07:00",
                    "transactionDate": "2024-04-03T14:29:03+07:00",
                    "trxId": "midtrans-testing-001-030424072903549oVvY"
                },
                {
                    "totalAmount": {
                        "currency": "IDR",
                        "value": "5000.00"
                    },
                    "paymentFlagReason": {
                        "english": "settlement"
                    },
                    "paymentRequestId": "A120240403072821jJ3pwMIFEyID",
                    "paymentFlagStatus": "00",
                    "trxDateTime": "2024-04-03T14:28:21+07:00",
                    "transactionDate": "2024-04-03T14:28:49+07:00",
                    "trxId": "midtrans-testing-001"
                }
            ],
            "paginationMetadata": {
                "total": "4",
                "pageSize": "2",
                "page": "1"
            }
        }
    }

```

***

***

# Delete VA

| Path              | /{version}/transfer-va/delete-va |
| :---------------- | :------------------------------- |
| HTTP Method       | POST                             |
| Version           | v1.0                             |
| SNAP version code | 31                               |

## Request Header

| Field Name    | Field Type | Mandatory | Field Description                                                                                                                                       |
| :------------ | :--------- | :-------- | :------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Content-Type  | String     | M         | Media type of the resource, i.e. application/json                                                                                                       |
| X-TIMESTAMP   | String     | M         | Client’s current local time in ISO-8601 format                                                                                                          |
| Authorization | String     | M         | Represents access\_token of a request; string starts with keyword “Bearer ” followed by access\_token. Can get this from Access Token B2B API response. |
| X-SIGNATURE   | String     | M         | Created using symmetric signature HMAC\_SHA512 algorithm                                                                                                |
| X-PARTNER-ID  | String     | M         | Unique identifier for caller (merchant\_id)                                                                                                             |
| CHANNEL-ID    | String     | M         | Mandatory field from Bank Indonesia that can take any value with correct format 5 digits numeric string                                                 |
| X-EXTERNAL-ID | String     | M         | Alphanumeric string. Preferably UUID.  Reference number that should be unique across 3 months                                                           |

```
Content-type:application/json
X-TIMESTAMP:2020-01-01T00:00:00+07:00
X-SIGNATURE:da1fa417c72d6b91c257e01e54fac824
Authorization:Bearer gp9HjjEj813Y9JGoqwOeOPWbnt4CupvIJbU1Mmu4a11MNDZ7Sg5u9a
X-PARTNER-ID:G12345678
X-EXTERNAL-ID:12345678901234567890
CHANNEL-ID:12345
```

## Request Body

<table>
  <tr>
    <td><strong>Field Name</strong></td>
    <td><strong>Field Type</strong></td>
    <td><strong>Mandatory</strong></td>
    <td colspan="2"><strong>Field Description</strong></td>
  </tr>

  <tr>
    <td>partnerServiceId</td>
    <td>String(8)</td>
    <td>M</td>
    <td colspan="2">partnerServiceId from Create VA Response</td>
  </tr>

  <tr>
    <td>customerNo</td>
    <td>String(20)</td>
    <td>M</td>
    <td colspan="2">customerNo from Create VA Response</td>
  </tr>

  <tr>
    <td>virtualAccountNo</td>
    <td>String(28)</td>
    <td>M</td>
    <td colspan="2">virtualAccountNo from Create VA Response</td>
  </tr>

  <tr>
    <td>trxId</td>
    <td>String(64)</td>
    <td>M</td>
    <td colspan="2">This value will be the <em>trxId </em>used in the create VA request.</td>
  </tr>

  <tr>
    <td>additionalInfo</td>
    <td>Object</td>
    <td>O</td>

    <td colspan="2"></td>
  </tr>

  <tr>
    <td>additionalInfo.merchantId</td>
    <td>String(10)</td>
    <td>M</td>
    <td colspan="2">This is the <em>merchantId </em>shared by Midtrans during the onboarding process</td>
  </tr>
</table>

```
{
    "partnerServiceId": "   70012",
    "customerNo": "6280123456",
    "virtualAccountNo": "   700126280123456",
    "trxId": "midtrans-testing-001",
    "additionalInfo": {
        "merchantId": "G059876677"
    }
}
```

## Response Header

| Field Name   | Field Type | Mandatory | Field Description                                |
| :----------- | :--------- | :-------- | :----------------------------------------------- |
| Content-Type | String     | M         | Media type of the resource, i.e application/json |
| X-TIMESTAMP  | String     | M         | Client's current local time in ISO-8601          |

```
Content-type:application/json
X-TIMESTAMP:2020-01-01T00:00:00+07:00
```

## Response Body

<table>
  <tr>
    <td><strong>Field Name</strong></td>
    <td><strong>Field Type</strong></td>
    <td><strong>Mandatory</strong></td>
    <td colspan="2"><strong>Field Description</strong></td>
  </tr>

  <tr>
    <td>responseCode</td>
    <td>String(7)</td>
    <td>M</td>
    <td colspan="2">Response code</td>
  </tr>

  <tr>
    <td>responseMessage</td>
    <td>String(150)</td>
    <td>M</td>
    <td colspan="2">Response description</td>
  </tr>

  <tr>
    <td>virtualAccountData</td>
    <td>Object</td>
    <td>M</td>

    <td colspan="2"></td>
  </tr>

  <tr>
    <td>virtualAccountData.partnerServiceId</td>
    <td>String(8)</td>
    <td>M</td>
    <td colspan="2">partnerServiceId from Create VA Response</td>
  </tr>

  <tr>
    <td>virtualAccountData.customerNo</td>
    <td>String(29)</td>
    <td>M</td>
    <td colspan="2">customerNo from Create VA Response</td>
  </tr>

  <tr>
    <td>virtualAccountData.virtualAccountNo</td>
    <td>String (28)</td>
    <td>M</td>
    <td colspan="2">virtualAccountNo from Create VA Response</td>
  </tr>

  <tr>
    <td>virtualAccountData.trxId</td>
    <td>String(64)</td>
    <td>M</td>
    <td colspan="2">The identifier used by the merchant during create VA. This will be the same as the <em>trxId<strong> </strong></em>in the create VA process</td>
  </tr>

  <tr>
    <td>additionalInfo.merchantId</td>
    <td>String(10)</td>
    <td>M</td>
    <td colspan="2">This is the <em>merchantId </em>shared by Midtrans during the onboarding process</td>
  </tr>
</table>

```
{
    "responseMessage": "Successful",
    "virtualAccountData": {
        "partnerServiceId": "   70012",
        "customerNo": "6280123456",
        "virtualAccountNo": "   700126280123456",
        "additionalInfo": {
            "merchantId": "G059876677"
        },
        "trxId": "midtrans-testing-001"
    },
    "responseCode": "2003100"
}
```

## List Response Code

<table>
  <tr>
    <td><strong>Response Code</strong></td>
    <td><strong>HTTP Status Code</strong></td>
    <td><strong>Response Message</strong></td>
  </tr>

  <tr>
    <td>2003100</td>
    <td>200</td>
    <td>Success</td>
  </tr>

  <tr>
    <td>4003102</td>
    <td>400</td>
    <td>Invalid Mandatory Field</td>
  </tr>

  <tr>
    <td>4013101</td>
    <td>401</td>
    <td>Unauthorized</td>
  </tr>

  <tr>
    <td>5003101</td>
    <td>500</td>
    <td>Internal Server Error</td>
  </tr>

  <tr>
    <td>5042700</td>
    <td>504</td>
    <td>Timeout</td>
  </tr>
</table>

# Additional APIs

1. [Get transaction status API](https://docs.midtrans.com/reference/get-transaction-status-api#fetching-transaction-status-for-bank-transfer-virtual-account-transaction)
2. [Cancel API](https://docs.midtrans.com/reference/cancel-api)

<br />