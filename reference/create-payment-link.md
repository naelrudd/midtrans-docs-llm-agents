---
updatedAt: 2026-05-11T08:11:23.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Create Payment Link

Merchant sends HTTP API request with the desired transaction details to this endpoint, and will get API response mainly with the Payment Link URL. The URL then should be shared to & opened by Customer, to initiates payment.

<br />

***

<br />

## Request

<br />

**Endpoints:** `/v1/payment-links`\
**HTTP Method:** `POST`\
**Headers:**

<br />

```text
Accept: application/json
Content-Type: application/json
Authorization: Basic AUTH_STRING
```

<br />

`AUTH_STRING` value is result of Base64Encode(`"YourServerKey"+":"`)

<br />

Midtrans API validates HTTP request by using Basic Authentication method. The username is your **Server Key** while the password is empty. The authorization header value is represented by AUTH\_STRING. AUTH\_STRING is base-64 encoded string of your username and password separated by colon symbol (**:**). For more details, refer to [ API Authorization and Headers](/docs/api-authorization-headers).

<br />

### Request Body

<br />

```json
{
  "transaction_details": {
    "order_id": "001",
    "gross_amount": 190000,
    "payment_link_id": "for-payment-123"
  },
  "customer_required": true,
  "credit_card": {
    "secure": true,
    "bank": "bca",
    "installment": {
      "required": false,
      "disabled": false,
      "terms": {
        "bni": [
          3,
          6,
          12
        ],
        "mandiri": [
          3,
          6,
          12
        ],
        "cimb": [
          3
        ],
        "bca": [
          3,
          6,
          12
        ],
        "offline": [
          6,
          12
        ]
      }
    }
  },
  "usage_limit": 1,
  "expiry": {
    "start_time": "2022-04-01 18:00 +0700",
    "duration": 20,
    "unit": "days"
  },
  "enabled_payments": [
    "credit_card",
    "bca_va",
    "indomaret"
  ],
  "item_details": [
    {
      "id": "pil-001",
      "name": "Pillow",
      "price": 95000,
      "quantity": 2,
      "brand": "Midtrans",
      "category": "Furniture",
      "merchant_name": "PT. Midtrans"
    }
  ],
  "customer_details": {
    "first_name": "John",
    "last_name": "Doe",
    "email": "john.doe@midtrans.com",
    "phone": "+62181000000000",
    "notes": "Thank you for your purchase. Please follow the instructions to pay.",
    "customer_details_required_fields": [
      "first_name",
      "phone",
      "email"
    ]
  },
  "title": "test title",
  "payment_link_type": "DYNAMIC_AMOUNT",
  "dynamic_amount": {
    "min_amount": 5000,
    "max_amount": 5000,
    "preset_amount": 5000
  },
  "custom_field1": "custom field 1 content",
  "custom_field2": "custom field 2 content",
  "custom_field3": "custom field 3 content",
  "callbacks": {
    "finish": "https://www.google.com?merchant_order_id=test-122"
  }
}
```

<br />

### Request JSON Body Details

<br />

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Parameter
      </th>

      <th>
        Required
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        [transaction_details](#transaction_details-object)
      </td>

      <td>
        **required**
      </td>

      <td>
        Object
      </td>

      <td>
        Specific information regarding the transaction.
      </td>
    </tr>

    <tr>
      <td>
        customer_required
      </td>

      <td>
        optional
      </td>

      <td>
        Boolean
      </td>

      <td>
        If set as True, Payment Link will prompt user to fill in customer details (name, phone and email) before customer can proceed to pay - which field set as mandatory can be specified in `customer_details`. If set as false, Payment Link will still show the customer details input form but it's not mandatory (customer can continue to the next page without filling any)
      </td>
    </tr>

    <tr>
      <td>
        [customer_details](#customer_details-object)
      </td>

      <td>
        optional
      </td>

      <td>
        Object
      </td>

      <td>
        Specific information regarding the customer.<br />**Note:** If Merchant sends customer_detail’s email on the request, Midtrans will send the created Payment Link url to the customer’s email.
      </td>
    </tr>

    <tr>
      <td>
        [item_details](#item_details-object)
      </td>

      <td>
        optional
      </td>

      <td>
        Object
      </td>

      <td>
        Details of the purchased items. Will be shown to customer during payment and shown in Midtrans Dashboard.
      </td>
    </tr>

    <tr>
      <td>
        usage_limit
      </td>

      <td>
        optional
      </td>

      <td>
        integer
      </td>

      <td>
        Maximum number of allowed successful/paid transactions. Max accepted value is `1000000` (1 million usage). <br />**Note:** Each successful/paid payment will consume a "usage" quota. A `pending` payment (payment attempted, but still waiting for Customer to make payment e.g. waiting Bank Transfer, Gopay, QRIS, etc.) will temporarily hold a usage quota, but if it is abandoned/left-unpaid (becomes `expire`) it will release the usage quota back.
      </td>
    </tr>

    <tr>
      <td>
        [expiry](#expiry-object)
      </td>

      <td>
        optional
      </td>

      <td>
        Object
      </td>

      <td>
        Customizable transaction lifetime. Once the duration exceeded, the link will no longer be available.
      </td>
    </tr>

    <tr>
      <td>
        enabled_payments
      </td>

      <td>
        optional
      </td>

      <td>
        Array
      </td>

      <td>
        Customizable list of payment methods that will be shown during payment. If not specified, by default all active payment methods are shown.<br />**Options:**<br />credit_card, echannel, permata_va, bca_va, bni_va, bri_va, cimb_va, danamon_va, bsi_va, gopay, shopeepay, other_qris, alfamart, indomaret, akulaku, kredivo.
      </td>
    </tr>

    <tr>
      <td>
        title
      </td>

      <td>
        optional
      </td>

      <td>
        String(255)
      </td>

      <td>
        Title to show in your payment link page that will be seen by your customer. Max char supported is 40.
      </td>
    </tr>

    <tr>
      <td>
        payment_link_type
      </td>

      <td>
        optional
      </td>

      <td>
        String(255)
      </td>

      <td>
        Pass the value `DYNAMIC_AMOUNT` if you want to use dynamic amount feature. Note that item_details and gross_amount will be ignored if the type passed is `DYNAMIC_AMOUNT`.  
        If payment_link_type is not passed, by default Payment Link will create a `FIXED_AMOUNT` payment link.
      </td>
    </tr>

    <tr>
      <td>
        [dynamic_amount](/reference/create-payment-link#dynamic_amount-object)
      </td>

      <td>
        optional
      </td>

      <td>
        Object
      </td>

      <td>
        Optional object if you're creating a payment link with dynamic amount features. You can set max/min amount and preset amount within this object.
      </td>
    </tr>

    <tr>
      <td>
        custom_field1
      </td>

      <td>
        optional
      </td>

      <td>
        String(255)
      </td>

      <td>
        Retrievable custom text that you can pass to Midtrans on field 1. Wil be shown in Midtrans Dashboard, & sent on HTTP Notification.
      </td>
    </tr>

    <tr>
      <td>
        custom_field2
      </td>

      <td>
        optional
      </td>

      <td>
        String(255)
      </td>

      <td>
        Retrievable custom text that you can pass to Midtrans on field 2. Wil be shown in Midtrans Dashboard, & sent on HTTP Notification.
      </td>
    </tr>

    <tr>
      <td>
        custom_field3
      </td>

      <td>
        optional
      </td>

      <td>
        String(255)
      </td>

      <td>
        Retrievable custom text that you can pass to Midtrans on field 3. Wil be shown in Midtrans Dashboard, & sent on HTTP Notification.
      </td>
    </tr>

    <tr>
      <td>
        callbacks
      </td>

      <td>
        optional
      </td>

      <td>
        Object
      </td>

      <td>
        Callback finish URL where user will be redirected after finishing a transaction. Can append query param if needed.
      </td>
    </tr>

    <tr>
      <td>
        [credit_card](/reference/json-objects#credit-card-object)
      </td>

      <td>
        optional
      </td>

      <td>
        Object
      </td>

      <td>
        Credit card payment options.
      </td>
    </tr>

    <tr>
      <td>
        [bni_va](/reference/json-objects#bni-virtual-account-object)
      </td>

      <td>
        optional
      </td>

      <td>
        Object
      </td>

      <td>
        Customizable Virtual Account number & options for BNI VA.
      </td>
    </tr>

    <tr>
      <td>
        [permata_va](/reference/json-objects#permata-virtual-account-object)
      </td>

      <td>
        optional
      </td>

      <td>
        Object
      </td>

      <td>
        Customizable Virtual Account number & options for Permata VA.
      </td>
    </tr>

    <tr>
      <td>
        [bca_va](/reference/json-objects#bca-virtual-account-object)
      </td>

      <td>
        optional
      </td>

      <td>
        Object
      </td>

      <td>
        Customizable Virtual Account number & options for BCA VA.
      </td>
    </tr>

    <tr>
      <td>
        [bri_va](/reference/json-objects#bri-virtual-account-object)
      </td>

      <td>
        optional
      </td>

      <td>
        Object
      </td>

      <td>
        Customizable Virtual Account number & options for BRI VA.
      </td>
    </tr>

    <tr>
      <td>
        [cimb_va](/reference/json-objects#cimb-virtual-account-object)
      </td>

      <td>
        optional
      </td>

      <td>
        Object
      </td>

      <td>
        Customizable Virtual Account number & options for CIMB VA.
      </td>
    </tr>
  </tbody>
</Table>

<br />

#### transaction\_details object

<br />

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Parameter
      </th>

      <th>
        Required
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        order_id
      </td>

      <td>
        **required**
      </td>

      <td>
        String(50)
      </td>

      <td>
        Unique transaction ID. A single ID could be used only once by a Merchant. Allowed Symbols are dash(-), underscore(_), tilde (~), and dot (.).
      </td>
    </tr>

    <tr>
      <td>
        gross_amount
      </td>

      <td>
        **required**
      </td>

      <td>
        Integer
      </td>

      <td>
        Total payment amount Customer expected to pay. Required for FIXED_AMOUNT, do not use for DYNAMIC_AMOUNT  
        **Note:**  
        The Sum of Subtotal (item price multiplied by quantity) of all the item details needs to be exactly the same as the gross_amount inside transaction_details object.
      </td>
    </tr>

    <tr>
      <td>
        payment_link_id
      </td>

      <td>
        optional
      </td>

      <td>
        String(50)
      </td>

      <td>
        Unique Link ID that will be used as part of the resulting payment URL. A single ID could be used only once. Allowed characters are alphanumeric ​​[a-z, 0-9] and hyphens [-].  
        **Note:**  
        By default auto generated by midtrans.  
        [Tips for generating the payment_link_id](https://docs.midtrans.com/reference/create-payment-link#security-tips-for-customizable-url)
      </td>
    </tr>
  </tbody>
</Table>

<br />

#### credit\_card object

<HTMLBlock>{`
<table>
  <tr>
   <th>Parameter</th>
   <th>Required</th>
   <th>Type</th>
   <th>Description</th>
  </tr>
  <tr>
   <td>secure</td>
   <td>optional</td>
   <td>Boolean</td>
   <td>Specify whether 3D-Secure authentication should be used for Card payment method. <br><strong>Note:</strong> It is recommended to specify <strong>true</strong> for most cases.  Default: false.</td>
  </tr>
  <tr>
   <td>bank</td>
   <td>optional</td>
   <td>String</td>
   <td>Specify which acquiring bank is preferred for Card payment method. <br>If not specified, Midtrans will auto determine accordingly. It is <strong>recommended to not specify it.</strong> <br><strong>Options</strong>: bca, bni, mandiri, cimb, bri, danamon, maybank, mega.</td>
  </tr>
  <tr>
   <td>channel</td>
   <td>optional</td>
   <td>String</td>
   <td>Specify which acquiring channel is preferred for Card payment method's acquiring bank. <br>If not specified, Midtrans will auto determine accordingly. It is <strong>recommended to not specify it.</strong><br><strong>Options</strong>: migs</td>
  </tr>
  <tr>
   <td>type</td>
   <td>optional</td>
   <td>String</td>
   <td>Card payment transaction type. It is <strong>recommended to not specify it.</strong> <br><strong>Options</strong>: authorize, authorize_capture  <br><strong>Default: </strong>authorize_capture</td>
  </tr>
  <tr>
   <td>whitelist_bins</td>
   <td>optional</td>
   <td>Array</td>
   <td> Specify list of card BIN numbers that will be allowed to pay. The BIN value can be either a prefix(up to 8 digits) of card number or the name of a bank, in which case all the cards issued by that bank will be allowed.</td>
  </tr>
  <tr>
   <td><a href="/reference/json-objects">installment.required</a></td>
   <td>optional</td>
   <td>Boolean</td>
   <td>Specify whether Customer is required to pay with installment for card payment method, if installment feature is enabled. It is <strong>recommended to not specify it.</strong><br> <strong>Default</strong>: false</td>
  </tr>
  <tr>
   <td><a href="/reference/json-objects">installment.terms</a></td>
   <td>optional</td>
   <td>Object</td>
   <td>Specify list of allowed installment terms, if installment feature is enabled. It is <strong>recommended to not specify it.</strong> </td>
  </tr>
</table>
`}</HTMLBlock>

<br />

#### expiry object

<HTMLBlock>{`
<table>
  <tr>
   <th>Parameter</th>
   <th>Required</th>
   <th>Type</th>
   <th>Description</th>
  </tr>
  <tr>
   <td>start_time</td>
   <td>optional</td>
   <td>String <br>Timestamp in yyyy-MM-dd HH:mm:ss Z format</td>
   <td>Timestamp of when the expiry period should start. If not specified, transaction time will be used as start time when payment link is created</td>
  </tr>
  <tr>
   <td>duration</td>
   <td><strong>required</strong></td>
   <td>Integer</td>
   <td>Expiry duration value.</td>
  </tr>
  <tr>
   <td>unit</td>
   <td><strong>required</strong></td>
   <td>String</td>
   <td>Expiry duration unit. <br><strong>Options</strong>: day, hour, minute.</td>
  </tr>
</table>
`}</HTMLBlock>

<br />

#### item\_details object

The value of these parameters will be specified by Merchant.

<HTMLBlock>{`
<table>
  <tr>
   <th>Parameter</th>
   <th>Required</th>
   <th>Type</th>
   <th>Description</th>
  </tr>
  <tr>
   <td>item_id</td>
   <td>optional</td>
   <td>String</td>
   <td>Item ID.</td>
  </tr>
  <tr>
   <td>price</td>
   <td><strong>required</strong></td>
   <td>Integer</td>
   <td>Price of the item.  <br><strong>NOTE</strong>: Don’t add decimal.</td>
  </tr>
  <tr>
   <td>quantity</td>
   <td><strong>required</strong></td>
   <td>Integer</td>
   <td>Quantity of the item.  <br><strong>NOTE</strong>: Must be greater than or equal 1.</td>
  </tr>
  <tr>
   <td>name</td>
   <td><strong>required</strong></td>
   <td>String(50)</td>
   <td>Name of the item.</td>
  </tr>
  <tr>
   <td>brand</td>
   <td>optional</td>
   <td>String(50)</td>
   <td>Brand of the item.</td>
  </tr>
  <tr>
   <td>category</td>
   <td>optional</td>
   <td>String(50)</td>
   <td>Category of the item.</td>
  </tr>
  <tr>
   <td>merchant_name</td>
   <td>optional</td>
   <td>String(50)</td>
   <td>Merchant selling the item. Useful if you have multiple sub-merchants within your commerce platform.</td>
  </tr>
</table>
`}</HTMLBlock>

<br />

> 📘 Implementing Discounts
>
> You can actually input negative amount as part of the item details in the case there's a need to show Discounts as part of the checkout item details. Make sure however the final gross amount sent is the correct sum of all item details, otherwise charge will fail.

<br />

#### customer\_details object

The value of these parameters will be specified by Merchant. If Merchant provide customer\_details object in the request, merchant should provide minimum one of three required field as shown below.

<HTMLBlock>{`
<table>
  <tr>
   <th>Parameter</th>
   <th>Required</th>
   <th>Type</th>
   <th>Description</th>
  </tr>
  <tr>
   <td>first_name</td>
   <td><strong>required*</strong></td>
   <td>String(50)</td>
   <td>Customer's first name.</td>
  </tr>
  <tr>
   <td>last_name</td>
   <td>optional</td>
   <td>String(50)</td>
   <td>Customer's last name.</td>
  </tr>
  <tr>
   <td>email</td>
   <td><strong>required*</strong></td>
   <td>String(50)</td>
   <td>Customer's email address.</td>
  </tr>
  <tr>
   <td>phone</td>
   <td><strong>required*</strong></td>
   <td>String(20)</td>
   <td>Customer's phone number.</td>
  </tr>
  <tr>
   <td>notes</td>
   <td>optional</td>
   <td>String(255)</td>
   <td>Customizable email instructions.</td>
  </tr>
  <tr>
   <td>customer_details_required_fields</td>
   <td>optional</td>
   <td>Array of String(255)</td>
   <td>When <code>customer_required</code> is <code>true</code>, merchant could specify which fields are required between <code>"first_name"</code>, <code>"phone"</code> and <code>"email"</code> to be filled by customer</td>
  </tr>
</table>
`}</HTMLBlock>

<br />

> 📘 Specific bank requirements
>
> For BCA VA, limit the customer names (**first\_name** and **last\_name**), to only 30 characters.
>
> For BNI VA, phone number format should start with +62 or 0 +\[area code] with max char = 30. If passed incorrectly, trx will be rejected.

<br />

<br />

#### Virtual Account Object

<HTMLBlock>{`
<table>
  <tr>
   <th>Parameter</th>
   <th>Required</th>
   <th>Type</th>
   <th>Description</th>
  </tr>
  <tr>
   <td><a href="/reference/custom-virtual-account-number">va_number</a></td>
   <td>optional</td>
   <td>String(11)</td>
   <td>Custom Virtual Account Number.</td>
  </tr>
</table>
`}</HTMLBlock>

<br />

#### dynamic\_amount object

| Parameter      | Required | Type    | Description                                                                                                  |
| :------------- | :------- | :------ | :----------------------------------------------------------------------------------------------------------- |
| min\_amount    | optional | Integer | Min amount that customer can input in payment link page.                                                     |
| max\_amount    | optional | Integer | Max amount that customer can input in payment link page.                                                     |
| preset\_amount | optional | Integer | Prefilled amount - customer will see this amount upon opening payment link page, but they can still edit it. |

<br />

### Request Sample

> See sample request on the right -- try it yourself!

<br />

***

<br />

## Response

<br />

For successful response you will receive HTTP status code `2xx` as a response. For failure response you may receive HTTP status code `4xx` or `5xx`.

<br />

### Sample Success Response

<br />

```json HTTP Status Code: &#x60;200&#x60;
{
   "order_id": "concert-ticket-05",
   "payment_url": "https://app.sandbox.midtrans.com/payment-links/amazing-ticket-payment-123"
}
```

<br />

### Sample Failure Response

<br />

```json HTTP Status Code: &#x60;409&#x60;
{
   "error_messages": [
       "The Order ID 'order-123' has been taken"
   ]
}
```

```json HTTP Status Code: &#x60;401&#x60;
{
   "error_messages": "Access denied due to unauthorized request"
}
```

```json HTTP Status Code: &#x60;400&#x60;
{
   "error_messages": [
       "Invalid JSON data provided.",
       "This Payment Link ID 'payment-112' has been taken",
       "payment_link_id must only contain alphanumeric characters [a-z, 0-9] and hyphens [-]"
   ]
}
```

<br />

### Response JSON Body Details

<br />

Response properties are conditional, depending on whether the API response is success or failure. E.g. error\_messages may only exists on failure response.

<br />

### HTTP Status Code

<br />

<HTMLBlock>{`
<table>
  <tr>
   <th>Status Code</th>
   <th>Descriptions</th>
  </tr>
  <tr>
   <td>200</td>
   <td>Request is successful</td>
  </tr>
  <tr>
   <td>409</td>
   <td>Duplicate order ID. Order ID has already been utilized previously</td>
  </tr>
  <tr>
   <td>401</td>
   <td>Access denied due to unauthorized request</td>
  </tr>
  <tr>
   <td>400</td>
   <td>Validation Error / Invalid JSON</td>
  </tr>
  <tr>
   <td>500</td>
   <td>Internal Server Error</td>
  </tr>
</table>
`}</HTMLBlock>

***

### Security Tips for Customizable URL

<Callout icon="🚧" theme="warn">
  It's mandatory to ensure the link is not guessable in order to protect you and your customer.  
  For example, having an enumerated number in the custom url can impose a risk that anyone can guess the next number: <b> /merchant-payment-order-001 </b>

  Each payment link is recommended to have the following properties:

  * Non-guessability: Links should be unpredictable to prevent unauthorized access or brute-force attacks.
  * Usability: Links should be reasonably short and manageable for sharing (e.g., via email, SMS, or QR code).
  * Uniqueness: Each payment link must be unique to prevent collisions.
  * Scalability: The algorithm should handle high volumes of link generation without performance issues.

  In order to do achieve these goals, here are some sample algorithm you can try.

  1. UUID / UUIDv4: This has a negligible chance of collision (2^128 possibilities)
  2. Cryptographically Secure Random Token: Enhance non-guessability by generating a random token using a cryptographically secure random number generator.
  3. Hash order information: Use a cryptographic hash function like SHA-256 to create a fixed-length, non-reversible token. For usability, truncate the hash to a reasonable length (e.g., 16–20 bytes) to keep the link manageable
</Callout>

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "info": {
    "title": "coreapi",
    "version": "1.0"
  },
  "servers": [
    {
      "url": "https://api.sandbox.midtrans.com"
    }
  ],
  "components": {
    "securitySchemes": {
      "sec0": {
        "type": "http",
        "scheme": "basic"
      }
    }
  },
  "security": [
    {
      "sec0": []
    }
  ],
  "paths": {
    "/v1/payment-links": {
      "post": {
        "summary": "Create Payment Link",
        "description": "",
        "operationId": "create-payment-link",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "required": [
                  "transaction_details",
                  "usage_limit"
                ],
                "properties": {
                  "transaction_details": {
                    "type": "object",
                    "required": [
                      "order_id",
                      "gross_amount"
                    ],
                    "properties": {
                      "order_id": {
                        "type": "string",
                        "default": "concert-ticket-01"
                      },
                      "gross_amount": {
                        "type": "integer",
                        "default": 100000,
                        "format": "int32"
                      }
                    }
                  },
                  "usage_limit": {
                    "type": "integer",
                    "default": 2,
                    "format": "int32"
                  },
                  "customer_details": {
                    "type": "object",
                    "properties": {}
                  }
                }
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "200",
            "content": {
              "application/json": {
                "examples": {
                  "Result": {
                    "value": "{\n   \"order_id\": \"concert-ticket-05\",\n   \"payment_url\": \"https://app.sandbox.midtrans.com/payment-links/amazing-ticket-payment-123\"\n}"
                  }
                },
                "schema": {
                  "type": "object",
                  "properties": {
                    "order_id": {
                      "type": "string",
                      "example": "concert-ticket-05"
                    },
                    "payment_url": {
                      "type": "string",
                      "example": "https://app.sandbox.midtrans.com/payment-links/amazing-ticket-payment-123"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "400",
            "content": {
              "application/json": {
                "examples": {
                  "Error": {
                    "value": "{\n   \"error_messages\": [\n       \"Invalid JSON data provided.\",\n       \"This Payment Link ID 'payment-112' has been taken\",\n       \"payment_link_id must only contain alphanumeric characters [a-z, 0-9] and hyphens [-]\"\n   ]\n}"
                  }
                },
                "schema": {
                  "type": "object",
                  "properties": {
                    "error_messages": {
                      "type": "array",
                      "items": {
                        "type": "string",
                        "example": "Invalid JSON data provided."
                      }
                    }
                  }
                }
              }
            }
          }
        },
        "deprecated": false
      }
    }
  },
  "x-readme": {
    "headers": [],
    "explorer-enabled": true,
    "proxy-enabled": true
  },
  "x-readme-fauxas": true
}
```