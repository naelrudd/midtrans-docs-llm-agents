---
updatedAt: 2025-11-11T00:28:27.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Subscription Schedule Object

```json Subscription Schedule Object
"schedule": {
  "interval": 1,
  "interval_unit": "month",
  "max_interval": 12,
  "current_interval": 2,
  "start_time": "2019-05-29 09:11:01",
  "previous_execution_at": "2019-05-29 09:11:01",
  "next_execution_at": "2019-06-29 09:11:01"
}
```

| JSON Attribute          | Description                                                                                                                                                                                                                                      | Type    |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------- |
| interval                | Subscription interval specified by you.                                                                                                                                                                                                          | Integer |
| interval\_unit          | Unit of time interval.<br />**Note**: Supports `month`, `week`, `day`.                                                                                                                                                                           | String  |
| max\_interval           | Maximum interval of subscription. Subscription ends after the maximum interval is reached.                                                                                                                                                       | Integer |
| current\_interval       | Current interval of subscription / count of charge at current time.                                                                                                                                                                              | Integer |
| start\_time             | Timestamp of subscription in `yyyy-MM-dd HH:mm:ss` format. Time Zone: GMT+7 .                                                                                                                                                                    | String  |
| previous\_execution\_at | Timestamp of last succeeded charge in `yyyy-MM-dd HH:mm:ss` format. Time Zone: GMT+7. <br /> **Note**: On create subscription, timestamp value will be the same as `start_time`, but if `start_time` has not passed yet, the value will be null. | String  |
| next\_execution\_at     | Timestamp of next scheduled charge in `yyyy-MM-dd HH:mm:ss` format. Time Zone: GMT+7.                                                                                                                                                            | String  |