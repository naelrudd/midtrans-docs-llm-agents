---
updatedAt: 2025-11-11T00:29:22.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Fetch Promotion (GoPay Tokenization)

Fetch promotion is triggered to fetch available GoPay promotions based on user account and transaction amount. Merchants can then show the available promotion on the merchant's page and have customers pre-select the promo and apply it when charging.

This feature is only available for GoPay Tokenization.

<br />

> 📘
>
> Fetch Promotion currently is only available in Production.
>
> To enable Fetch Promotion, please contact your Midtrans Sales PIC or Midtrans Support.

> 📘 Fetch Promotion API can also be used alongside with BI-SNAP account linking flow
>
> Merchant can also calls the Fetch Promotion API using BI-SNAP account linking flow with the adjustment as follows:
>
> 1. Merchant don't need to pass Midtrans account ID in the query paramater. Merchant will only need to call this endpoint with these query parameters: `BASE_URL/v2/gopay/promo/?gross_amount={gross_amount}&currency={currency}`
> 2. Merchant to pass Authorization-Customer token acquired from BI-SNAP account linking in the request header: `Authorization-Customer: Bearer <BI-SNAP authorization-customer token>`

## Fetch Promotion Request

| HTTP Method | Endpoint                                                                               | Definition                 |
| ----------- | -------------------------------------------------------------------------------------- | -------------------------- |
| GET         | `BASE_URL/v2/gopay/promo/{account_id}?gross_amount={gross_amount}&currency={currency}` | Fetch available promotions |

<br />

| JSON Attribute | Description                                | Type   | Required |
| -------------- | ------------------------------------------ | ------ | :------- |
| account\_id    | Customer account id to be used for payment | String | Required |
| gross\_amount  | Transaction gross amount                   | String | Required |
| currency       | Transaction currency. Default: `IDR`       | String | Optional |

<br />

***

<br />

## Fetch Promotion Response

```json Sample Response - Success
{
    "account_id": "00000269-7836-49e5-bc65-e592afafec14",
    "status_code": "200",
    "recommended_promotion_id": "CASHBACK|acbec7d4-b30b-44ac-9c42-f5d767419a72|8bb3c041-c71e-40f3-892b-688fda2ec979||2021-02-22|2021-02-23",
    "promotions": [
        {
            "id": "CASHBACK|acbec7d4-b30b-44ac-9c42-f5d767419a72|8bb3c041-c71e-40f3-892b-688fda2ec979||2021-02-22|2021-02-23",
            "code": "100PCCASHBACK",
            "type": "CASHBACK",
            "actual_payable_amount": "100.00",
            "promotion_amount": "100.00",
            "minimum_applicable_amount": "100.00",
            "currency": "IDR/SGD/VND/THB",
            "description": "100 percent cashback",
            "short_description": "short-desc",
            "title": "100PCCASHBACK",
            "valid_from": "2021-02-22 17:00:00",
            "valid_till": "2021-02-23 17:00:00",
            "tnc_url": "",
            "limit_per_user": 15,
            "source": "GOPAY_PROMO",
            "promotion_value": {
                "money": {
                    "type": "PERCENTAGE",
                    "value": "100"
                }
            }
        }
    ]
}

```
```asp Sample Response - No Available Promotion
{
   "account_id": "00000269-7836-49e5-bc65-e592afafec14",
   "status_code":"200",
   "promotions":[]
}
```
```asp Sample Response - Account ID Doesn't Exist Error
{
  "id": "00000269-7836-49e5-bc65-e592afafec14",
  "status_code": "400",
  "status_message": "Account doesn’t exist"
}
```
```asp Sample Response - Gross Amount is Missing Error
{
  "id": "00000269-7836-49e5-bc65-e592afafec1",
  "status_code": "400",
  "status_message": "One or more parameters in the payload is invalid.",
  "validation_messages": [“gross_amount is required”]
}
```

<HTMLBlock>{`
<div></div>

<style></style><table>
<tr><th colspan="2">JSON Attribute</th><th>Description</th><th>Type</th></tr>
<tr><td colspan="2">account_id</td><td>Customer account id to be used for payment</td><td>String</td></tr>
<tr><td colspan="2">status_code</td><td>Status code of the API result</td><td>String</td></tr>
<tr><td colspan="2">recommended_promotion_id</td><td>Recommended promotion id based on order details</td><td>String</td></tr>
<tr><td colspan="2">promotions</td><td>List of applicable GoPay promotion information</td><td>Array</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;id</td><td>Promotion id. Will be used in Charge API to apply promotion.</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;code</td><td>Promotion code</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;type</td><td>Promotion type</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;actual_payable_amount</td><td>Transaction gross amount</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;promotion_amount</td><td>Promotion/cashback amount</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;minimum_applicable_amount</td><td>Minimum transaction amount for promotion</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;currency</td><td>Currency</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;description</td><td>Promotion description</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;title</td><td>Promotion title</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;valid_from</td><td>Start of promotion period</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;valid_till</td><td>End of promotion period</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;tnc_url</td><td>Terms & condition url</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;limit_per_user</td><td>Maximum usage per user within promotion period</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;source</td><td>Promotion source</td><td>String</td></tr>
<tr><td></td><td>&nbsp;&nbsp;&nbsp;promotion_value</td><td>Promotion value</td><td>Object</td></tr>
<tr></tr>
  
</table>
`}</HTMLBlock>