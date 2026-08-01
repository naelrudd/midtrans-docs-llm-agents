---
updatedAt: 2026-07-28T09:35:24.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Seamless Payment (Snap-Checkout)

This guide explains how merchants with an existing Snap Checkout integration can enable payments within MiniApp.

<br />

| **Integration Needed** | **Details**                                    |
| :--------------------- | :--------------------------------------------- |
| Mini App Frontend      | Display Snap payment page on frontend          |
| Mini App Backend       | Acquire Snap transaction token on your backend |

# Sequence Diagram:

**Mini app payments Flow diagram**

<Image src="https://files.readme.io/99dd584-snap_sequence_regular.png" alt="671" align="center" />

<br />

**1. User Initiate Order**

* The user decides to place an order in the mini app front end process for order.

**2. \[SNAP-CHECKOUT API] Acquiring Transaction Token on Backend**

* Merchant mini app frontend to call their own backend to retrieve [transaction token](https://docs.midtrans.com/reference/miniapp-x-snap-checkout-payment/#1-acquiring-transaction-token-on-backend)

**3: \[SNAP-CHECKOUT API] Displaying Snap Payment Page on Frontend**

* Merchant mini app to display [snap payment page](https://docs.midtrans.com/reference/miniapp-x-snap-checkout-payment/#2-displaying-snap-payment-page-on-frontend)

**4: \[SNAP-CHECKOUT API] Notify**

* Once the payment is complete. Super App backend will notify the Mini App Backend by **v1.0/debit/notify**
* The contract for the api can be found [here](https://docs.midtrans.com/reference/miniapp-x-snap-checkout-payment/#3-notify).

# New GoPay Merchants:

If you have not integrated with GoPay or have integrated without following the **SNAP-CHECKOUT API** convention, the following points apply :

* You must first onboard **SNAP-CHECKOUT API** convention following below integration steps

# Existing GoPay Merchants:

If you have already integrated with GoPay and follow the **SNAP-CHECKOUT API** convention, the following points apply :

* There is no change in the already integrated SNAP-CHECKOUT API
* For Obtain Transaction Token request, the new object in the existing contract needs to be added under **gopay.pop\_id**. The value for this is shared by the GoPay Team in the MiniApp Workbook sent via email.

<br />

***

# 1. Acquiring Transaction Token on Backend

API request should be done from merchant backend to acquire Snap transaction `token` by providing payment information and *Server Key*. There are at least three components that are required to obtain the Snap token which are explained in the table given below.

<Table>
  <thead>
    <tr>
      <th>
        Element
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `Server Key`
      </td>

      <td>
        API server key. For more details, refer to [Retrieving API Access Keys](/docs/midtrans-account#retrieving-api-access-keys)
      </td>
    </tr>

    <tr>
      <td>
        `order_id`
      </td>

      <td>
        Unique transaction order ID, defined from your side. One ID could be used only once for the order of the material. Allowed character are Alphanumeric, dash(-), underscore(\_), tilde (\~), and dot (.) String, max 50.
      </td>
    </tr>

    <tr>
      <td>
        `gross_amount`
      </td>

      <td>
        Total amount of transaction, defined from your side. Integer.

        When creating 1st transaction, the gross_amount is still required.<br />Although, then the actual accepted payment amount is allowed to be different that the initial gross_amount, so customer can flexibly pay with any acceptable amount.
      </td>
    </tr>
  </tbody>
</Table>

## Charge API Sample Request

<br />

### Endpoints

| Environment | Method | URL                                                     |
| ----------- | ------ | ------------------------------------------------------- |
| Sandbox     | POST   | `https://app.sandbox.midtrans.com/snap/v1/transactions` |
| Production  | POST   | `https://app.midtrans.com/snap/v1/transactions`         |

### HTTP Headers

|               |                     |
| :------------ | :------------------ |
| Accept        | `application/json`  |
| Content-Type  | `application/json`  |
| Authorization | `Basic AUTH_STRING` |

**AUTH\_STRING**: Base64Encode(`"YourServerKey"+":"`)

<br />

<Callout icon="📘" theme="info">
  Midtrans API validates HTTP request by using Basic Authentication method. The username is your **Server Key** while the password is empty. The authorization header value is represented by AUTH_STRING. AUTH_STRING is base-64 encoded string of your username and password separated by colon symbol (**:**). For more details, refer to [ API Authorization and Headers](/docs/api-authorization-headers).
</Callout>

## GoPay Object

```json
"gopay": {
  "pop_id": "990407c8-7c2b-4998-8ef8-0bc67c0c6c55"
}
```

| Parameter | Description                                                                                 |
| --------- | ------------------------------------------------------------------------------------------- |
| pop\_id   | For MiniApp payments, this parameter is mandatory to determine the Point of Purchase (POP). |

### Sample Request

```curl
curl --location --request POST 'https://app.midtrans.com/snap/v1/transactions' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic auth' \
--data '{
    "transaction_details": {
        "order_id": "test-123",
        "gross_amount": 100000
    },
    "gopay": {
        "pop_id": "<pop_id>"
    },
    "callbacks": {
        "finish": "https://www.google.com",
        "error": "https://www.facebook.com"
    }
}'
```
```php
/*Install Midtrans PHP Library (https://github.com/Midtrans/midtrans-php)
composer require midtrans/midtrans-php
                              
Alternatively, if you are not using **Composer**, you can download midtrans-php library 
(https://github.com/Midtrans/midtrans-php/archive/master.zip), and then require 
the file manually.   

require_once dirname(__FILE__) . '/pathofproject/Midtrans.php'; */

//SAMPLE REQUEST START HERE

// Set your Merchant Server Key
\Midtrans\Config::$serverKey = 'YOUR_SERVER_KEY';
// Set to Development/Sandbox Environment (default). Set to true for Production Environment (accept real transaction).
\Midtrans\Config::$isProduction = false;
// Set sanitization on (default)
\Midtrans\Config::$isSanitized = true;
// Set 3DS transaction for credit card to true
\Midtrans\Config::$is3ds = true;

$params = array(
    'transaction_details' => array(
        'order_id' => rand(),
        'gross_amount' => 10000,
    ),
    'customer_details' => array(
        'first_name' => 'budi',
        'last_name' => 'pratama',
        'email' => 'budi.pra@example.com',
        'phone' => '08111222333',
    ),
);

$snapToken = \Midtrans\Snap::getSnapToken($params);
```
```javascript NodeJS
/*Install midtrans-client (https://github.com/Midtrans/midtrans-nodejs-client) NPM package.
npm install --save midtrans-client*/

//SAMPLE REQUEST START HERE

const midtransClient = require('midtrans-client');
// Create Snap API instance
let snap = new midtransClient.Snap({
        // Set to true if you want Production Environment (accept real transaction).
        isProduction : false,
        serverKey : 'YOUR_SERVER_KEY'
    });

let parameter = {
    "transaction_details": {
        "order_id": "YOUR-ORDERID-123456",
        "gross_amount": 10000
    },
    "credit_card":{
        "secure" : true
    },
    "customer_details": {
        "first_name": "budi",
        "last_name": "pratama",
        "email": "budi.pra@example.com",
        "phone": "08111222333"
    }
};

snap.createTransaction(parameter)
    .then((transaction)=>{
        // transaction token
        let transactionToken = transaction.token;
        console.log('transactionToken:',transactionToken);
    })
```
```java
/*Install midtrans-java (https://github.com/Midtrans/midtrans-java) library.
If you are using Maven as the build automation tool for your project,
please add the following dependency to your project's build definition (pom.xml).
<dependencies>
    <dependency>
      <groupId>com.midtrans</groupId>
      <artifactId>java-library</artifactId>
      <version>3.0.0</version>
    </dependency>
</dependencies>
  
If you are using Gradle as the build tool for your project, 
please add the following dependency to your project's build definition (build.gradle).

dependencies {
    implementation 'com.midtrans:java-library:3.0.0'
}

You can also check the functional test 
(https://github.com/Midtrans/midtrans-java/blob/master/library/src/test/java/com/midtrans/java/CoreApiTest.java) for more examples.
*/

//SAMPLE REQUEST START HERE

import com.midtrans.Midtrans;
import com.midtrans.httpclient.SnapApi;
import com.midtrans.httpclient.error.MidtransError;

import java.util.HashMap;
import java.util.Map;
import java.util.UUID;
import org.json.JSONObject;

public class MidtransExample {

    public static void main(String[] args) throws MidtransError {
      // Set serverKey to Midtrans global config
      Midtrans.serverKey = "YOUR_SERVER_KEY";

      // Set value to true if you want Production Environment (accept real transaction).
      Midtrans.isProduction = false;

      // Create params JSON Raw Object request
      public Map<String, Object> requestBody() {
          UUID idRand = UUID.randomUUID();
          Map<String, Object> params = new HashMap<>();

          Map<String, String> transactionDetails = new HashMap<>();
          transactionDetails.put("order_id", idRand);
          transactionDetails.put("gross_amount", "265000");

          Map<String, String> creditCard = new HashMap<>();
          creditCard.put("secure", "true");

          params.put("transaction_details", transactionDetails);
          params.put("credit_card", creditCard);

          return params;
      }

      // Create Token and then you can send token variable to FrontEnd,
      // to initialize Snap JS when customer click pay button
      String transactionToken = SnapApi.createTransactionToken(requestBody())
    }
}

```
```python
#Install midtransclient(https://github.com/Midtrans/midtrans-python-client) PIP package
#pip install midtransclient

#SAMPLE REQUEST START HERE

import midtransclient
# Create Snap API instance
snap = midtransclient.Snap(
    # Set to true if you want Production Environment (accept real transaction).
    is_production=False,
    server_key='YOUR_SERVER_KEY'
)
# Build API parameter
param = {
    "transaction_details": {
        "order_id": "test-transaction-123",
        "gross_amount": 200000
    }, "credit_card":{
        "secure" : True
    }, "customer_details":{
        "first_name": "budi",
        "last_name": "pratama",
        "email": "budi.pra@example.com",
        "phone": "08111222333"
    }
}

transaction = snap.create_transaction(param)

transaction_token = transaction['token']
```
```go
/*Import Midtrans Go module package to your project. Via terminal:
go get -u github.com/midtrans/midtrans-go

and/or on your project code:
import (
    "github.com/midtrans/midtrans-go"
    "github.com/midtrans/midtrans-go/coreapi"
    "github.com/midtrans/midtrans-go/snap"
    "github.com/midtrans/midtrans-go/iris"
)*/

//SAMPLE REQUEST START HERE

// 1. Initiate Snap client
var s = snap.Client
s.New("YOUR-SERVER-KEY", midtrans.Sandbox)
// Use to midtrans.Production if you want Production Environment (accept real transaction).

// 2. Initiate Snap request param
req := & snap.RequestParam{
    TransactionDetails: midtrans.TransactionDetails{
      OrderID:  "YOUR-ORDER-ID-12345",
      GrossAmt: 100000,
    }, 
    CreditCard: &snap.CreditCardDetails{
      Secure: true,
    },
    CustomerDetail: &midtrans.CustomerDetails{
      FName: "John",
      LName: "Doe",
      Email: "john@doe.com",
      Phone: "081234567890",
    },
  }

// 3. Execute request create Snap transaction to Midtrans Snap API
snapResp, _ := s.CreateTransaction(req)
```

For MiniApp payments, **pop\_id** is mandatory. Transactions without pop\_id may not be routed correctly within the MiniApp flow.

The pop\_id (Point of Purchase ID) will be shared via email in the MiniApp Workbook document after requesting a new MiniApp creation.

### Sample Response

```json
{
  "token":"66e4fa55-fdac-4ef9-91b5-733b97d1b862",
  "redirect_url":"https://app.sandbox.midtrans.com/snap/v2/vtweb/66e4fa55-fdac-4ef9-91b5-733b97d1b862"
}
```

### List of Response Code

| Status Code | Description                                                                                                             | Example                                                                       |
| ----------- | ----------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| 201         | Successful creation of Snap token.                                                                                      | "token":"66e4fa55-fdac-4ef9-91b5-733b97d1b862"                                |
| 401         | Failed to create a token, as wrong authorization is sent.                                                               | "Access denied, please check client or server key"                            |
| 4xx         | Failed to create a token, as wrong parameter is sent. Follow the error\_message and check your parameter.               | "transaction\_details.gross\_amount is not equal to the sum of item\_details" |
| 5xx         | Failed to create a token, because of  Midtrans internal error. Most of the time this is temporary, you can retry later. | "Sorry, we encountered internal server error. We will fix this soon."         |

<br />

***

# 2. Displaying Snap Payment Page on Frontend

## <br />Javascript Method

<Callout icon="📘" theme="info">
  ### Tips

  - If you are using frontend framework such as ReactJS and struggling to include the script tag, please [refer to this recommendation](/docs/technical-faq#my-developer-uses-react-js-frontend-framework-and-is-unable-to-use-midtransminjssnapjs-what-should-i-do).
  - To ensure that Snap modal is displayed correctly on a mobile device, please include the viewport meta tag inside your `<head>` tag. The most common implementation is as follows :<br />`<meta name="viewport" content="width=device-width, initial-scale=1">`
  - Optionally, you can also use [JavaScript callbacks](/docs/snap-advanced-feature#javascript-callback) to handle payment events triggered from customer finishing interaction with Snap payment page on frontend.
</Callout>

Include `snap.js` library into your payment page HTML. The table given below describes the components which are required to display Snap payment page.

| Element             | Description                                                                                                                 |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Client Key          | The *Client Key*. For more details refer to [Retrieving API Access Keys](/docs/midtrans-account#retrieving-api-access-keys) |
| `snap.js` url       | `https://app.sandbox.midtrans.com/snap/snap.js`                                                                             |
| transaction `token` | Retrieved from backend in [previous step](#_1-acquiring-transaction-token-on-backend)                                       |

Enter your *Client Key* as the value of `data-client-key` attribute in snap.js script tag.

### Pop Up Mode

Display the Snap Checkout modal by overlaying it over your page (pop up). Start the payment process by calling `window.snap.pay` with transaction `token`.

<br />

```html Basic
<html>
  <head>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- @TODO: replace SET_YOUR_CLIENT_KEY_HERE with your client key -->
    <script type="text/javascript"
      src="https://app.sandbox.midtrans.com/snap/snap.js"
      data-client-key="SET_YOUR_CLIENT_KEY_HERE"></script>
    <!-- Note: replace with src="https://app.midtrans.com/snap/snap.js" for Production environment -->
  </head>

  <body>
    <button id="pay-button">Pay!</button>

    <script type="text/javascript">
      // For example trigger on button clicked, or any time you need
      var payButton = document.getElementById('pay-button');
      payButton.addEventListener('click', function () {
        // Trigger snap popup. @TODO: Replace TRANSACTION_TOKEN_HERE with your transaction token
        window.snap.pay('TRANSACTION_TOKEN_HERE');
        // customer will be redirected after completing payment pop-up
      });
    </script>
  </body>
</html>
```
```html With JS Callback
<html>
  <head>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- @TODO: replace SET_YOUR_CLIENT_KEY_HERE with your client key -->
    <script type="text/javascript"
      src="https://app.sandbox.midtrans.com/snap/snap.js"
      data-client-key="SET_YOUR_CLIENT_KEY_HERE"></script>
    <!-- Note: replace with src="https://app.midtrans.com/snap/snap.js" for Production environment -->
  </head>

  <body>
    <button id="pay-button">Pay!</button>

    <script type="text/javascript">
      // For example trigger on button clicked, or any time you need
      var payButton = document.getElementById('pay-button');
      payButton.addEventListener('click', function () {
        // Trigger snap popup. @TODO: Replace TRANSACTION_TOKEN_HERE with your transaction token
        window.snap.pay('TRANSACTION_TOKEN_HERE', {
          onSuccess: function(result){
            /* You may add your own implementation here */
            alert("payment success!"); console.log(result);
          },
          onPending: function(result){
            /* You may add your own implementation here */
            alert("wating your payment!"); console.log(result);
          },
          onError: function(result){
            /* You may add your own implementation here */
            alert("payment failed!"); console.log(result);
          },
          onClose: function(){
            /* You may add your own implementation here */
            alert('you closed the popup without finishing the payment');
          }
        })
      });
    </script>
  </body>
</html>
```

Learn more about [Snap's Javascript Callback here](/docs/snap-advanced-feature) and Snap's Javascript optional parameters [here.](/docs/snap-advanced-feature#snapjs-main-functions).

After following the steps given above, the sample Snap page is displayed as shown below.

![](https://files.readme.io/b8fc165-snap-popup-preview.gif "snap-popup-preview.gif")

Or try the demo [here](https://demo.midtrans.com).

After the payment is completed, customer is redirected back to `Finish URL`. It is specified on [Midtrans Dashboard](/docs/snap-advanced-feature#configuring-redirect-url), under menu **Settings > Snap Preference > System Settings >**`Finish URL` .

***

# 3. Notify

Note: This is the Backend API required to retrieve the payment response.

In the SNAP-based Core API flow, Midtrans will call Payment Notification API on the merchant side to send payment notifications. Merchant should implement this Payment Notification API as stated in the contract below.

<Callout icon="📘" theme="info">
  Midtrans will generate a pair of **private and public key** for signature generation and share the public key to merchant. Merchant will then need to give Midtrans a **partner id** that will be used in request header as **X-PARTNER-ID**.
</Callout>

<Callout icon="🚧" theme="warn">
  Please make sure to whitelist this set of IPs to be able to accept notification from Midtrans.

  ```
  <Table align={["left","left"]}>
    <thead>
      <tr>
        <th style={{ textAlign: "left" }}>
          Environment
        </th>
  ```

  ```
      <th style={{ textAlign: "left" }}>
        IPs
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        Staging
      </td>

      <td style={{ textAlign: "left" }}>
        3.1.141.98/32

        52.76.190.190/32

        13.251.192.204/32

        8.215.39.156/32

        8.215.77.79/32

        147.139.213.119/32

        8.215.56.11/32

        8.215.39.87/32

        8.215.42.0/32

        8.215.59.158/32

        149.129.222.246/32

        8.215.26.108/32

        8.215.13.84/32
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Sandbox
      </td>

      <td style={{ textAlign: "left" }}>
        34.142.147.133/32

        34.142.169.131/32

        34.142.231.22/32

        35.240.161.215/32

        34.142.227.232/32

        34.124.184.175/32

        35.197.130.2/32

        34.142.233.114/32

        8.215.26.211/32

        8.215.22.135/32

        8.215.93.92/32

        8.215.93.214/32

        8.215.93.76/32

        8.215.33.37/32

        8.215.26.148/32

        8.215.194.225/32

        8.215.12.199/32

        149.129.255.111/32
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Production
      </td>

      <td style={{ textAlign: "left" }}>
        13.228.166.126/32

        52.220.80.5/32

        3.1.123.95/32

        8.215.30.222/32

        147.139.209.49/32

        8.215.32.142/32

        147.139.163.77/32

        8.215.25.24/32

        8.215.3.193/32

        147.139.210.20/32

        149.129.238.95/32

        8.215.9.206/32

        147.139.134.22/32
      </td>
    </tr>
  </tbody>
  ```

  ```
  </Table>
  ```
</Callout>

<Callout icon="⚠️" theme="warn">
  ### **Notes on Future Compatibility and Best Practices**

  To ensure your integration remains robust and scalable, please be aware that Midtrans **may introduce additional parameters** to the payment notification payload in the future, most likely under the additionalInfo section, but not limited to it. These enhancements are designed to provide greater flexibility and support for evolving business needs.

  To prevent any issues caused by these future changes, we strongly recommend that merchants always perform **signature verification on the entire payload**, rather than validating fields individually. This practice ensures a seamless, secure, and simple implementation that can adapt to future updates without requiring significant changes on your side.
</Callout>

## Receiving payment notifications for GoPay and GoPay Tokenization (non Pre-Auth) transaction

This section will describe how merchant should implement payment notification API for GoPay and GoPay Tokenization (non-Pre Auth) transactions for Midtrans to call.

| Path              | /`{version}`/debit/notify |
| :---------------- | :------------------------ |
| HTTP Method       | POST                      |
| Version           | v1.0                      |
| SNAP Service Code | 56                        |

### Request Header

<table>
  <tr>
    <td><strong>Field Name</strong></td>
    <td><strong>Field Type</strong></td>
    <td><strong>Mandatory</strong></td>
    <td colspan="2"><strong>Field Description</strong></td>
  </tr>

  <tr>
    <td>
      Content-type
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Media type of the resource, i.e. application/json
    </td>
  </tr>

  <tr>
    <td>
      X-TIMESTAMP
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Client’s current local time in ISO-8601 format
    </td>
  </tr>

  <tr>
    <td>
      X-SIGNATURE
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Created using asymmetric signature

      <p>
        Asymmetric-Signature format:
      </p>

      <p>
        SHA256withRSA (privateKey, stringToSign) with
      </p>

      <p>
        stringToSign = HTTPMethod +”:“+ EndpointUrl +":“+ Lowercase(HexEncode(SHA-256(minify(RequestBody)))) + ":“ + TimeStamp
      </p>
    </td>
  </tr>

  <tr>
    <td>
      X-PARTNER-ID
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Unique identifier for partner
    </td>
  </tr>

  <tr>
    <td>
      X-EXTERNAL-ID
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Numeric string. Reference number that should be unique in the same day or 1 day idempotency key
    </td>
  </tr>
</table>

```
Content-type:application/json
X-TIMESTAMP:2024-03-19T14:30:00+07:00
X-SIGNATURE: da1fa417c72d6b91c257e01e54fac824
X-PARTNER-ID: 
X-EXTERNAL-ID:12345678901234567890
CHANNEL-ID:12345
```

### Request Body

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td>
      <strong>Field Description</strong>
    </td>
  </tr>

  <tr>
    <td>
      createdTime
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td>
      Transaction created timestamp
    </td>
  </tr>

  <tr>
    <td>
      latestTransactionStatus
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Latest transaction status

      <p>
        <strong>Possible Values: </strong>
      </p>

      <ul>
        <li>00 - Success</li>

        <li>03 - Pending</li>

        <li>04 - Refunded</li>

        <li>05 - Canceled</li>

        <li>06 - Failure</li>

        <li> 08 - Expiry </li>

        <li> 09 - Rejected</li>
      </ul>
    </td>
  </tr>

  <tr>
    <td>
      originalReferenceNo
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Transaction identifier on service provider system. For e.g: GopayOrderId<strong> </strong>
    </td>
  </tr>

  <tr>
    <td>
      finishedTime
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td>
      Transaction completed timestamp (for latestTranscationStatus = 00)
    </td>
  </tr>

  <tr>
    <td>
      originalPartnerReferenceNo
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td>
      Original transaction identifier on service consumer system. (Merchant’s orderId)
    </td>
  </tr>

  <tr>
    <td>
      originalExternalId
    </td>

    <td>
      String(36)
    </td>

    <td>
      O
    </td>

    <td>
      Original External-ID on header message when doing charge (/payment-host-to-host)
    </td>
  </tr>

  <tr>
    <td>
      merchantId
    </td>

    <td>
      String
    </td>

    <td>
      O
    </td>

    <td>
      Merchant ID
    </td>
  </tr>

  <tr>
    <td>
      amount
    </td>

    <td>
      Object
    </td>

    <td>
      O
    </td>

    <td>
      Transaction amount
    </td>
  </tr>

  <tr>
    <td>
      amount.value
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Transaction amount
    </td>
  </tr>

  <tr>
    <td>
      amount.currency
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Transaction currency
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo
    </td>

    <td>
      Object
    </td>

    <td>
      M
    </td>

    <td>
      Additional info
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory
    </td>

    <td>
      Array of Object
    </td>

    <td>
      C
    </td>

    <td>
      Array of refund transactions. Only available if transaction status is <code>refund</code>
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundNo
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Unique identifier of refund transaction generated by provider.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundStatus
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Refund status. Possible values:<br />

      * 00 --> Refund success<br />
      * 06 --> Refund failed
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.partnerRefundNo
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Unique identifier of refund transaction generated by client.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundAmount
    </td>

    <td>
      Object
    </td>

    <td>
      M
    </td>

    <td>
      Refund amount
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundAmount.value
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Net amount of the refund. If it's IDR then the value includes 2 decimal digits.

      <p>
        e.g. IDR 10.000,- will be placed with 10000.00
      </p>
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundAmount.currency
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Currency
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.reason
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Refund reason
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.refundHistory.refundTime
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Refund time
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.totalRefundAmount
    </td>

    <td>
      Object
    </td>

    <td>
      C
    </td>

    <td>
      Total refund amount. Only available if transaction status is <code>refund</code> or <code>partial refund</code>.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.totalRefundAmount.value
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Total refund amount. If it's IDR then the value includes 2 decimal digits.

      <p>
        e.g. IDR 10.000,- will be placed with 10000.00
      </p>
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.totalRefundAmount.currency
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Currency
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.userPaymentDetails
    </td>

    <td>
      Array of object
    </td>

    <td>
      M
    </td>

    <td>
      Payment option used by user. This will be not available for deeplink redirection payment flow with <b>pending</b> status.
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.userPaymentDetails.payMethod
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Payment method used by user. E.g: gopay
    </td>
  </tr>

  <tr>
    <td>
      additionalInfo.userPaymentDetails.payOption
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td>
      Payment option used by user. <br /> Possible value: <br /> - GoPay = `GOPAY_WALLET` <br /> - GoPay Later = `PAY_LATER` <br /> - GoPay Tabungan by Jago = `GOPAY_SAVINGS`
    </td>
  </tr>
</table>

```
{
    "createdTime": "2020-01-01T00:00:00+07:00",
    "latestTransactionStatus": "00",
    "originalReferenceNo": "gopayOrderId",
    "finishedTime": "2020-01-02T00:00:00+07:00",
    "originalPartnerReferenceNo": "merchant-order-id",
    "transactionStatusDesc": "desc",
   "originalExternalId":"merchant-order-id",
    "additionalInfo": { 
        "userPaymentDetails": [
         {
           "payMethod": "gopay",
           "payOption": "GOPAY_WALLET"
         }
        ],
         "refundHistory":[
  	{
     	     	"refundNo":"96194816941239812",
      			"refundStatus":"00",
     	     	"partnerReferenceNo":"239850918204981205970",
          		"refundAmount":{
          	   	     	"value":"12345678.00",
         	    	     	"currency":"IDR"
     	     	},
     	     	"refundDate":"2020-12-23T07:44:16+07:00",
          		"reason":"Customer Complain"
  	}
   ]
    }
}
```

### Response Header

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td colspan="2">
      <strong>Field Description</strong>
    </td>
  </tr>

  <tr>
    <td>
      Content-type
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Media type of the resource, i.e. application/json
    </td>
  </tr>

  <tr>
    <td>
      X-TIMESTAMP
    </td>

    <td>
      String
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Client’s current local time in ISO-8601 format
    </td>
  </tr>
</table>

```
Content-type: application/json
X-TIMESTAMP: 2024-03-19T14:30:00+07:00
```

### Response Body

<table>
  <tr>
    <td>
      <strong>Field Name</strong>
    </td>

    <td>
      <strong>Field Type</strong>
    </td>

    <td>
      <strong>Mandatory</strong>
    </td>

    <td colspan="2">
      <strong>Field Description</strong>
    </td>
  </tr>

  <tr>
    <td>
      responseCode
    </td>

    <td>
      String (7)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Error code to specify the error returned.
    </td>
  </tr>

  <tr>
    <td>
      responseMessage
    </td>

    <td>
      String (150)
    </td>

    <td>
      M
    </td>

    <td colspan="2">
      Debug message to provide more information.
    </td>
  </tr>
</table>

```
{
   "responseCode":"2005600",
   "responseMessage":"Request has been processed successfully"
}
```

# Additional APIs

1. [Refund API](https://docs.midtrans.com/reference/refund-api)
2. [Cancel API](https://docs.midtrans.com/reference/cancel-api)
3. [Get Transaction Status API](https://docs.midtrans.com/reference/get-transaction-status-api)
4. [Payment Notification API](https://docs.midtrans.com/reference/payment-notification-api)

<br />