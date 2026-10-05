---
updatedAt: 2026-09-28T12:00:08.000Z
agentTools:
  projectIndex: https://docs.midtrans.com/llms.txt
---

# Advanced Features

Core API has various optional parameters that can be utilized to integrate with more advanced use cases. This section will explain advance features specific for Partner Solutions, other general features can be seen on this docss [docs](https://docs.midtrans.com/docs/coreapi-advanced-features)

<br />

***

<br />

## Transaction Split

With this feature, as a partner, you can split the gross amount and MDR fee of a transaction to your merchants.

<br />

> 📘 Glossary
>
> In this context, gross amount is the amount that will be added on your withdrawable balance.
>
> MDR fee is transaction fee that is deducted for each transaction.

<br />

You can add `transaction_split_settings` parameter to define how will you split the transaction.

<br />

```json JSON Parameters
{
  ...
  "transaction_split_settings": {
    "gross_amount_split": {
      "type": "percentage",
      "split_rules": [
        {
          "merchant_id": "G000002",
          "value": "85"
        },
        {
          "merchant_id": "G000003",
          "value": "15"
        }
      ]
    },
    "fee_split": {
      "type": "percentage",
      "split_rules": [
        {
          "merchant_id": "G000002",
          "value": "50"
        },
        {
          "merchant_id": "G000003",
          "value": "50"
        }
      ]
    }
  },
  ...
}
```

<br />

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Parameter
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
        `gross_amount_split`
      </td>

      <td>
        Define the rules for splitting the transaction amount
      </td>

      <td>
        Object
      </td>

      <td>
        Optional\*\
        `required` when `fee_split` is not defined
      </td>
    </tr>

    <tr>
      <td>
        `gross_amount_split.type`
      </td>

      <td>
        Type of the split, possible values are `percentage`
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
        `gross_amount_split.split_rules`
      </td>

      <td>
        Define the detail of the split
      </td>

      <td>
        Array of Object
      </td>

      <td>
        Required
      </td>
    </tr>

    <tr>
      <td>
        `gross_amount_split.split_rules.*.merchant_id`
      </td>

      <td>
        Merchant ID which will receive amount of the transaction
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
        `gross_amount.split_rules.*.value`
      </td>

      <td>
        Value of the split based on type.  

        * Percentage: percentage of the amount that will merchant receive
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
        `fee_split`
      </td>

      <td>
        Define the rules for splitting the transaction fee
      </td>

      <td>
        Object
      </td>

      <td>
        Optional\*\
        `required` when `gross_amount_split` is not defined
      </td>
    </tr>

    <tr>
      <td>
        `fee_split.type`
      </td>

      <td>
        Type of the split, possible values are `percentage`
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
        `fee_split.split_rules`
      </td>

      <td>
        Define the detail of the split
      </td>

      <td>
        Array of Object
      </td>

      <td>
        Required
      </td>
    </tr>

    <tr>
      <td>
        `fee_split.split_rules.*.merchant_id`
      </td>

      <td>
        Merchant ID which will bear the transaction fee
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
        `fee_split.split_rules.*.value`
      </td>

      <td>
        Value of the split based on type.  

        * Percentage: percentage of the fee that will be borne by merchant
      </td>

      <td>
        String
      </td>

      <td>
        Required
      </td>
    </tr>
  </tbody>
</Table>

<br />

### Things to Note

* You can split only the gross amount, only the fee, or both.
* When the `type` is `percentage`, the total value must be equals to 100%.
* Specified `merchant_id` must be registered under your Partner setup.

<br />

### Sample Calculation

With transaction amount Rp 100.000, transaction fee Rp 4.440, and this split configuration:

```json Split Configuration
{
  ...
  "transaction_split_settings": {
    "gross_amount_split": {
      "type": "percentage",
      "split_rules": [
        {
          "merchant_id": "G000002",
          "value": "85"
        },
        {
          "merchant_id": "G000003",
          "value": "15"
        }
      ]
    },
    "fee_split": {
      "type": "percentage",
      "split_rules": [
        {
          "merchant_id": "G000002",
          "value": "50"
        },
        {
          "merchant_id": "G000003",
          "value": "50"
        }
      ]
    }
  },
  ...
}
```

<br />

The split result will be:

* Merchant `G000002`:
  * Receive Rp 82.780 (85% \* 100.000 - 2.220)
  * Bear Rp 2.220 of the fee (50% \* 4.440)
* Merchant `G000003`:
  * Receive Rp 12.780 (15% \* 100.000 - 2.220)
  * Bear Rp 2.220 of the fee (50% \* 4.440)