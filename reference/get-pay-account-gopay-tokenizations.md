---
updatedAt: 2026-09-28T12:00:08.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Get Pay Account (GoPay Tokenizations)

Get Pay Account is triggered to get GoPay's account linked status. This method is only applicable for GoPay Tokenizations.

Endpoints: `/api/v1/core/pay/account/{{account_id}}`

HTTP Method: `GET`

## Response Body

```json 200 - Enabled
{
  "status_code": "200",
  "payment_type": "gopay",
  "account_id": "00000269-7836-49e5-bc65-e592afafec14",
  "account_status": "ENABLED",
  "metadata": {
    "payment_options": [
      {
        "name": "GOPAY_WALLET",
        "active": true,
        "balance": {
          "value": "1000000.00",
          "currency": "IDR"
        },
        "metadata": {},
        "token": "eyJ0eXBlIjogIkdPUEFZX1dBTExFVCIsICJpZCI6ICIifQ=="
      },
      {
        "name": "PAY_LATER",
        "active": true,
        "balance": {
          "value": "350000.00",
          "currency": "IDR"
        },
        "metadata": {},
        "token": "eyJ0eXBlIjogIlBBWV9MQVRFUiIsICJpZCI6ICIifQ=="
      }
    ]
  }
}
```
```json 200 - Pending
{
  "status_code": "201",
  "payment_type": "gopay",
  "account_id": "00000269-7836-49e5-bc65-e592afafec14",
  "account_status": "PENDING"
}
```
```json 200 - Expired
{
  "status_code": "204",
  "payment_type": "gopay",
  "account_id": "00000269-7836-49e5-bc65-e592afafec14",
  "account_status": "EXPIRED"
}
```
```json 200 - Disabled
{
  "status_code": "204",
  "payment_type": "gopay",
  "account_id": "00000269-7836-49e5-bc65-e592afafec14",
  "account_status": "DISABLED"
}
```

| Field           | Type   | Description                                                                                 |
| --------------- | ------ | ------------------------------------------------------------------------------------------- |
| status\_code    | String | Status code of the API result.                                                              |
| payment\_type   | String | Payment channel associated with the account.                                                |
| account\_id     | String | Customer account ID to be used for payment.                                                 |
| account\_status | String | Status of the account. Possible values are `PENDING`, `EXPIRED`, `ENABLED`, and `DISABLED`. |
| metadata        | Object | Additional data from the specific payment provider, that is, *GoPay*.                       |

More information about GoPay Tokenizations can be seen [here](https://docs.midtrans.com/reference/gopay-tokenization-1)