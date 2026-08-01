---
updatedAt: 2025-11-11T00:28:15.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Bank Transfer (Virtual Account) Object

For more details on customizing VA number, go [here](/docs/coreapi-advanced-features#specifying-custom-va-number-and-va-description).

```json BCA VA Object
"bank_transfer":{
  "bank": "bca",
  "va_number": "111111",
  "free_text": {
       "inquiry": [
             {
                 "id": "Free Text ID Free Text ID Free Text ID",
                 "en": "Free Text EN Free Text EN Free Text EN"
             }
       ],
       "payment": [
             {
                 "id": "Free Text ID Free Text ID Free Text ID",
                 "en": "Free Text EN Free Text EN Free Text EN"
             }
       ]
  },
  "bca": {
    "sub_company_code": "00000"
  }
}
```
```json Permata VA Object
"bank_transfer":{
  "bank": "permata",
  "va_number": "111111",
  "permata": {
    "recipient_name": "SUDARSONO"
  }
}
```
```json BNI VA Object
"bank_transfer":{
     "bank": "bni",
     "va_number": "111111"
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
        bank
      </td>

      <td>
        Bank name which processes bank transfer transaction. Possible values are `permata`, `bni`, `bri`, and `bca`.
      </td>

      <td>
        String(255)
      </td>

      <td>
        Required
      </td>
    </tr>

    <tr>
      <td>
        va\_number
      </td>

      <td>
        Custom VA number assigned by you. If shorter than minimum then Midtrans will add trailing 0s as most significant bits. If longer than maximum then Midtrans will trim the remaining least significant bits. <ul><li>**BCA VA**: Accepts 6-18 digits</li><li>**Permata VA**: Accepts 12 digits.</li><li>**BNI VA**: Accepts 8 (For 5 digits Client ID) or 12 digits (For 3 digits Client ID).</li><li>**BRI VA**: Accepts 18 digits.</li><li>**CIMB VA**: Accepts 12 digits.</li></ul>
      </td>

      <td>
        String(255)
      </td>

      <td>
        Optional
      </td>
    </tr>

    <tr>
      <td>
        free\_text
      </td>

      <td>
        List of free texts. <br />**Note**: Right now only used for BCA VA.
      </td>

      <td>
        [JSON Object](#free-text-object) Array
      </td>

      <td>
        Optional
      </td>
    </tr>

    <tr>
      <td>
        bca
      </td>

      <td>
        Specific parameters for BCA VA.
      </td>

      <td>
        [JSON Object](#bca-va-object)
      </td>

      <td>
        Optional
      </td>
    </tr>

    <tr>
      <td>
        permata
      </td>

      <td>
        Specific parameters for Permata VA.
      </td>

      <td>
        [JSON Object](#permata-va-object)
      </td>

      <td>
        Optional
      </td>
    </tr>
  </tbody>
</Table>

<br />

***

<br />

## Free Text Object

| JSON Attribute | Description                      | Type                                            | Required |
| -------------- | -------------------------------- | ----------------------------------------------- | -------- |
| inquiry        | Free texts shown during inquiry. | [JSON Object](#inquirypayment-object) Array(10) | Optional |
| payment        | Free texts shown during payment. | [JSON Object](#inquirypayment-object) Array(10) | Optional |

<br />

***

<br />

## Inquiry/Payment Object

| JSON Attribute | Description                            | Type       | Required |
| -------------- | -------------------------------------- | ---------- | -------- |
| id             | Free text message in Bahasa Indonesia. | String(50) | Required |
| en             | Free text message in English.          | String(50) | Required |

<br />

***

<br />

## BCA VA Object

| JSON Attribute     | Description                                                                              | Type   | Required |
| ------------------ | ---------------------------------------------------------------------------------------- | ------ | -------- |
| sub\_company\_code | BCA sub company code directed for this transactions. <br />**Note**: Default is `00000`. | String | Optional |

<br />

***

<br />

## Permata VA Object

| JSON Attribute  | Description                                                                                                                           | Type   | Required |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- |
| recipient\_name | Recipient name shown on the payment details. It is shown as 20 characters uppercase string. <br />**Note**: Default is merchant name. | String | Optional |

<br />

***

<br />

## BNI VA Object

| JSON Attribute | Description                                                                              | Type        | Required |
| -------------- | ---------------------------------------------------------------------------------------- | ----------- | -------- |
| bank           | The name of the bank which processes the transaction using Bank Transfer payment method. | String(255) | Required |
| va\_number     | Custom VA number assigned by merchant. Min length 1, max length 8                        | String(255) | Optional |