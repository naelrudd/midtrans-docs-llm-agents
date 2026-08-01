---
updatedAt: 2025-11-10T22:58:57.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Customer Details Object

```json Customer Details Object
"customer_details": {
  "first_name": "TEST",
  "last_name": "UTOMO",
  "email": "test@midtrans.com",
  "phone": "+628123456",
  "billing_address": {
    "first_name": "TEST",
    "last_name": "UTOMO",
    "phone": "081 2233 44-55",
    "address": "Sudirman",
    "city": "Jakarta",
    "postal_code": "12190",
    "country_code": "IDN"
  },
  "shipping_address": {
    "first_name": "TEST",
    "last_name": "UTOMO",
    "phone": "0 8128-75 7-9338",
    "address": "Sudirman",
    "city": "Jakarta",
    "postal_code": "12190",
    "country_code": "IDN"
  }
}
```

| JSON Attribute    | Description                  | Type        | Required |
| ----------------- | ---------------------------- | ----------- | -------- |
| first\_name       | Customer's first name.       | String(255) | Optional |
| last\_name        | Customer's last name.        | String(255) | Optional |
| email             | Customer's email address.    | String(255) | Optional |
| phone             | Customer's phone number.     | String(255) | Optional |
| billing\_address  | Customer's billing address.  | JSON Array  | Optional |
| shipping\_address | Customer's shipping address. | JSON Array  | Optional |

<br />

> 📘 Specific bank requirements
>
> For BCA VA, limit the customer names (**first\_name** and **last\_name**), to only 30 characters.
>
> For BNI VA, phone number format should start with +62 or 0 +\[area code] with max char = 30. If passed incorrectly, trx will be rejected.

<br />

***

## Billing Address Object

| JSON Attribute | Description                                                                                                                                                                 | Type        | Required |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | -------- |
| first\_name    | Customer's first name.                                                                                                                                                      | String(255) | Optional |
| last\_name     | Customer's last name.                                                                                                                                                       | String(255) | Optional |
| phone          | Customer's phone number.                                                                                                                                                    | String(255) | Optional |
| address        | Customer's billing address.                                                                                                                                                 | String(255) | Optional |
| city           | City of the billing address.                                                                                                                                                | String(255) | Optional |
| postal\_code   | Postal code of the billing address. <br /> **Note**: Allowed characters are alphabets, numbers, dash (`-`), and space (` `).                                                | String(255) | Optional |
| country\_code  | Country ID of the billing address. Value: IDN. [ISO 3166-1 alpha-3](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3). <br /> **Note**: Currently only `IDN` is supported.  | String(3)   | Optional |

<br />

***

## Shipping Address Object

| JSON Attribute | Description                                                                                                                                                                | Type        | Required |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | -------- |
| first\_name    | Customer's shipping first name.                                                                                                                                            | String(255) | Optional |
| last\_name     | Customer's shipping last name.                                                                                                                                             | String(255) | Optional |
| phone          | Customer's shipping phone number.                                                                                                                                          | String(255) | Optional |
| address        | Customer's shipping address.                                                                                                                                               | String(255) | Optional |
| city           | City of the shipping address.                                                                                                                                              | String(255) | Optional |
| postal\_code   | Postal code of the shipping address. <br /> **Note**: Allowed characters are alphabets, numbers, dash (`-`), and space (` `).                                              | String(255) | Optional |
| country\_code  | Country ID of the shipping address. Value: IDN. [ISO 3166-1 alpha-3](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3) <br /> **Note**: Currently only `IDN` is supported. | String(3)   | Optional |