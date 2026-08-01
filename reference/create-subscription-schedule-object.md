---
updatedAt: 2025-11-10T22:59:19.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Create Subscription Schedule Object

```json Create Subscription Scheduler Object
"schedule": {
  "interval": 1,
  "interval_unit": "month",
  "max_interval": 12,
  "start_time": "2019-05-29 09:11:01 +0700"
}
```

<Table>
  <thead>
    <tr>
      <th>
        JSON Attribute
      </th>

      <th>
        Description
      </th>

      <th>
        Type
      </th>

      <th>
        Required
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        interval
      </td>

      <td>
        Subscription's interval given by merchant.
      </td>

      <td>
        Integer
      </td>

      <td>
        Required
      </td>
    </tr>

    <tr>
      <td>
        interval\_unit
      </td>

      <td>
        Interval temporal unit. <br />**Note**: Supports `day`, `week`, and `month`.
      </td>

      <td>
        String
      </td>

      <td>
        Required
      </td>
    </tr>

    <tr>
      <td>
        max\_interval
      </td>

      <td>
        Maximum interval of subscription. Subscription will end after maximum interval is reached.\
        If `max_interval` is set to `0` will be executed once.\
        If `max_interval` is `null` or omitted from the payload, the subscription will continue indefinitely until manually deactivated.
      </td>

      <td>
        Integer
      </td>

      <td>
        Optional
      </td>
    </tr>

    <tr>
      <td>
        start\_time
      </td>

      <td>
        Timestamp of subscription in `yyyy-MM-dd HH:mm:ss Z`. The value must be after the current time. If specified, first payment will happen on `start_time`. If `start_time` is not specified, the default value for `start_time` will be the date after the first interval after current time.
      </td>

      <td>
        String
      </td>

      <td>
        Optional
      </td>
    </tr>
  </tbody>
</Table>