---
updatedAt: 2025-11-11T00:28:24.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Create Subscription Retry Schedule Object

```json Create Subscription Scheduler Object
"retry_schedule": {
  "interval": 1,
  "interval_unit": "day",
  "max_interval": 3,
}
```

| JSON Attribute | Description                                                                                                                                                                         | Type    | Required |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- |
| interval       | Subscription's retry interval given by merchant.                                                                                                                                    | Integer | Optional |
| interval\_unit | Retry interval temporal unit. <br />**Note**: Supports `minute`, `hour`, and `day`.                                                                                                 | String  | Optional |
| max\_interval  | Maximum retry interval of subscription (up to 3 times). Subscription will end after maximum interval is reached. If specified as 0, failed subscription charge will not be retried. | Integer | Optional |