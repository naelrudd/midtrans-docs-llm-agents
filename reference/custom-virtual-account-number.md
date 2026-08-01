---
updatedAt: 2025-11-10T22:58:44.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Bank Transfer - Custom VA Number

A virtual account number contains two parts. for example, in `{91012}{12435678}` , the first part is the company code and the second part is a unique code. The second part can be customized for [BCA VA](/reference/bca-virtual-account), [Permata VA](/reference/permata-virtual-account), [BNI VA](/reference/bni-virtual-account),  [BRI VA](/reference/bri-virtual-account), [CIMB VA](https://docs.midtrans.com/reference/cimb-virtual-account-1), and [Danamon VA](https://docs.midtrans.com/reference/danamon-virtual-account) payment types.

<br />

* Only digits are allowed.

* Different banks have different specs on their custom VA numbers. Please see the documentation on the respective banks.

* If the number provided is already utilized for another order, then a different unique number will be used instead.

* If the number provided is longer than required, then the unnecessary digits in the end will be trimmed.

* If the number provided is shorter than required, then the number will be prefixed with zeros.

<br />

```json BCA VA
{
  "bca_va": {
    "va_number": "55555555555"
  }
}
```
```json Permata VA
{
  "permata_va": {
    "va_number": "1234567890"
  }
}
```
```json BNI VA
{
  "bni_va": {
    "va_number": "12345678"
  }
}
```
```json BRI VA
{
  "bri_va": {
    "va_number": "1234567863214"
  }
}
```
```Text CIMB VA
{
  "cimb_va": {
    "va_number": "1234567890123"
  }
}
```
```Text Danamon VA
{
  "danamon_va": {
    "va_number": "123456789012345"
  }
}
```