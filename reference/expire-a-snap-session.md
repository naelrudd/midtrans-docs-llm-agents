---
updatedAt: 2025-11-10T22:58:46.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Expire a Snap Session

Set a custom expiry time for a Snap session with the following methods.

## Set a custom expiry for the Snap page only (default is 24 hours)

***

<br />

As long as Snap page is not expired, said page can be reopened again even after customer closes the page by reopening the URL with the specific session's Snap token. Page expiry can be set via Snap Preference or specified during get token via API request.

<br />

> **Note** : Snap does not send any webhook upon page expiry.

<br />

### Set via Snap Preference

<br />

To set, go to [Snap Preference](https://dashboard.midtrans.com/settings/snap_preference) > System Settings, then configure the Page Expiry Settings. Page expiry settings will not affect payment methods with configurable expiry time via Payment Expiry Settings section in Snap Preference.

Note : minimum accepted expiry is 5 mins, max is 7 days.

<br />

### Specify via API Request

<br />

Specify during Snap token creation via API request. Page expiry is **optional**.

<br />

#### Request Body (JSON Parameters)

```json JSON Parameters
...
"page_expiry": {
    "duration": 3,
    "unit": "hours"
}
...
```
```curl Sample Charge API Request
curl -X POST \
  https://app.sandbox.midtrans.com/snap/v1/transactions \
  -H 'Accept: application/json'\
  -H 'Authorization: Basic U0ItTWlkLXNlcnZlci1UT3ExYTJBVnVpeWhoT2p2ZnMzVV7LZU87' \
  -H 'Content-Type: application/json' \
  -d '{
  "transaction_details": {
    "order_id": "CustOrder-102",
    "gross_amount": 13000
  },
  "page_expiry": {
    "duration": 3,
    "unit": "hours"
  }
}'
```

| Parameter  | Description                                                             | Type    | Required |
| ---------- | ----------------------------------------------------------------------- | ------- | -------- |
| `duration` | Page expiry duration in numbers                                         | Integer | Required |
| `unit`     | Expiry unit. Options: `day, hour, minute` (plural terms also accepted). | String  | Required |

<br />

## Set a custom expiry for payment methods

***

<br />

Configure individual payment method's expiry time by going to [Snap Preference](https://dashboard.midtrans.com/settings/snap_preference) > System Settings > Payment Expiry Settings. Check said section for more info on each payment method's default expiry time.

If payment method expiry is longer than page expiry time, customer can still make payment as long as they have the VA number/QRIS image/OTC payment code even though Snap page is expired and no longer accessible.

<br />

> 📘 Expiry Behavior for Card Payment
>
> * Card form's expiry time will follow Snap Page expiry settings (there's no separate payment method expiry settings for it). If Snap page has already expired, customer will not be able to access the card payment form.
> * However, once customer has clicked Pay upon filling the card payment details and reached the OTP/3DS page, expiry time will then follow issuing bank's OTP page expiry time.

<br />

## Specify blanket expiry for Snap page and payment methods via API request

***

<br />

Configure blanket expiry (for both Snap page and payment methods) for a specific transaction.

<br />

### Sample Request

<br />

```json JSON Parameters
...
  "expiry": {
    "start_time": "2020-04-13 18:11:08 +0700",
    "unit": "minutes",
    "duration": 180
  }
...
```
```curl Sample Charge API Request
curl -X POST \
  https://app.sandbox.midtrans.com/snap/v1/transactions \
  -H 'Accept: application/json'\
  -H 'Authorization: Basic U0ItTWlkLXNlcnZlci1UT3ExYTJBVnVpeWhoT2p2ZnMzVV7LZU87' \
  -H 'Content-Type: application/json' \
  -d '{
  "transaction_details": {
    "order_id": "CustOrder-102",
    "gross_amount": 13000
  },
  "expiry": {
    "start_time": "2020-04-13 18:11:08 +0700",
    "unit": "minutes",
    "duration": 180
  }
}'
```

| Parameter    | Description                                                                                                                                                                                      | Type        | Required   |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------- | ---------- |
| `start_time` | Timestamp in `YYYY-MM-DD HH:MM:SS +0700`.<br/>If not specified, transaction time will be used as start time (when customer confirm payment channel). Time Zone is Western Indonesian Time (WIT). | String(255) | Optional\* |
| `duration`   | Expiry duration in numbers                                                                                                                                                                       | Integer     | Required   |
| `unit`       | Expiry unit. Options: `day, hour, minute` (plural term also accepted).                                                                                                                           | String      | Required   |

<br />

## Additional Info

***

<br />

* Minimum accepted expiry is 5 mins, max is 7 days.
* Priority hierarchy for expiry (if transaction is not created yet) from most to least prioritized :\
  &#x9;	a. `page_expiry` object in API\
  &#x9;	b. `expiry` object in API (custom expiry)\
  &#x9;	c. Page expiry settings in Snap Preference
* Once customer chooses a payment method and if `expiry` object is not specified, expiry counter in Snap checkout page will be updated to follow individual payment method's expiry settings as specified in Snap Preference > System Settings.