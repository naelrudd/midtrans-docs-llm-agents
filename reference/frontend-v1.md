---
updatedAt: 2026-03-16T07:33:54.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Frontend SDKs V1

This guide explains the technical specifications of JSAPIs that is available to be called from your application's frontend.

# Integrate SDK

1. **Include the gpContainer SDK in Your Codebase**\
   To use the SDK, add the following `<script>` tag to your HTML or application entry point
   ```
   <script src="https://gwk.gopayapi.com/sdk/stable/gp-container.min.js"></script>
   ```

2. **Invoking SDK Methods**\
   To call any JSAPI from the SDK, use the following format:
   ```
   window.gpContainer.call(className, methodName, params, successCallback, failureCallback, timeout);
   ```
   <br />

***

# Supported JSAPIs

GPLocation (need to change all openlinks)

| API                                                                                    | Function                      | Requires Consent |
| :------------------------------------------------------------------------------------- | :---------------------------- | :--------------- |
| GPLocation.[getLocation](https://docs.midtrans.com/reference/frontend-v1#get-location) | Obtain user's device location | yes              |

GPMiniAppAuth

| API                                                                                         | Function                                                   | Requires Consent |
| :------------------------------------------------------------------------------------------ | :--------------------------------------------------------- | :--------------- |
| GPMiniAppAuth.[getAuthCode](https://docs.midtrans.com/reference/frontend-v1/#get-auth-code) | Get an auth code used to identify the current user session | No               |

GPNavigator

| API                                                                                            | Function                                                   | Requires Consent |
| :--------------------------------------------------------------------------------------------- | :--------------------------------------------------------- | :--------------- |
| GPNavigator.[launchDeeplink](https://docs.midtrans.com/reference/frontend-v1/#launch-deeplink) | Open a third-party app or page using a custom deeplink     | No               |
| GPNavigator.[launchUri](https://docs.midtrans.com/reference/frontend-v1/#launch-uri)           | Open a browser or in-app page using a universal or web URI | No               |

GP

| API                                                                                 | Function                                                                                                  | Requires Consent |
| :---------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------- | :--------------- |
| GP.[launchPayment](https://docs.midtrans.com/reference/frontend-v1/#launch-payment) | Automatically redirect users to the GoPay app to complete the payment, then return them to your Mini App. | No               |

GPMotion

| API                                                                                     | Function                                                  | Requires Consent |
| :-------------------------------------------------------------------------------------- | :-------------------------------------------------------- | :--------------- |
| GPMotion.[startCompass](https://docs.midtrans.com/reference/frontend-v1/#start-compass) | Start receiving compass direction data (magnetic heading) | No               |
| GPMotion.[stopCompass](https://docs.midtrans.com/reference/frontend-v1/#stop-compass)   | Stop receiving compass data                               | No               |

Prompt

| API                                                                       | Function                                      | Android | IOS     |
| :------------------------------------------------------------------------ | :-------------------------------------------- | :------ | :------ |
| GPUIToast.[toast](https://docs.midtrans.com/reference/frontend-v1/#toast) | Displays a toast in the center of the screen. | Support | Support |

GPNavigationBar

| API                                                                                      | Function                                                 | Android | IOS     |
| :--------------------------------------------------------------------------------------- | :------------------------------------------------------- | :------ | :------ |
| GPNavigationBar.[update](https://docs.midtrans.com/reference/frontend-v1/#update-navbar) | Configures the navigation bar of the current page.       | Support | Support |
| GPNavigationBar.[getHeight](https://docs.midtrans.com/reference/frontend-v1/#getheight)  | Obtains the height of the navigation bar in the miniapp. | Support | Support |

GPAnalytics

| API                                                                                   | Function                                                                                                | Requires Consent |
| :------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------ | :--------------- |
| GPAnalytics.[trackEvent](https://docs.midtrans.com/reference/frontend-v1/#trackevent) | To send structured events back to GoPay, enabling visibility on how users interact within the mini app. | No               |

***

# [Version History](https://docs.midtrans.com/update/reference/version-history)

***

# JSAPIs Specification (v1.0.0)

<Callout icon="📝" theme="default">
  ### Note

  * Data will be null in case of success = false, and vice versa.
  * Error will be null in case of success = true, and vice versa.
</Callout>

## Get Location

Sample Request:

```Text Javascript
var params = {
	// Specify whether to obtain a high-precision location.
	enable_high_accuracy: true
};

window.gpContainer.call(  
  "GPLocation",  
  "getLocation",  
  params,  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v1/#error-codes))

```Text JSON
{
    "success": true,
    "data": {
      "coords": {
        "longitude": 77.5946,
        "latitude": 12.9716,
        "time": 12
      }
    },
    "ret": "GP_SUCCESS" 
}
```

```Text JSON
{
    "success": false,
    "errorCode": "",
    "errorType": "JS_BRIDGE_ERROR",
    "errorMessage": "",
    "ret": "GP_EXCEPTION"   
}
```

## Get Auth Code

Sample Request:

```Text Javascript
window.gpContainer.call(  
  "GPMiniAppAuth",  
  "getAuthCode",  
  {},  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v1/#error-codes))

```Text JSON
{
    "success": true,
    "data": {
        authCode: "GBNURP5WyBIqXiGxKv2cO8Qj4CyS0qZrRK5O4e8ehdnHpowG6k5pkj2SsF7BqGIF"
    },
		"ret": "GP_SUCCESS" 
}
```

```Text JSON
{
    "success": false,
    "errorCode": "",
    "errorType": "JS_BRIDGE_ERROR",
    "errorMessage": "",
    "ret": "GP_EXCEPTION"   
}
```

## Launch Deeplink

Sample Request:

```Text Javascript
var params = {
  deeplink: "gopay://..."
};

window.gpContainer.call(  
  "GPNavigator",  
  "launchDeeplink",  
  params,  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

Sample Response:  ([error codes](https://docs.midtrans.com/reference/frontend-v1/#error-codes))

```Text JSON
{
		success: true,
		"ret": "GP_SUCCESS" 
}
```

```Text JSON
{
    "success": false,
    "errorCode": "300",
    "errorType": "JS_BRIDGE_ERROR",
    "errorMessage": "Permission denied",
    "ret": "GP_EXCEPTION"   
}
```

## Launch Payment

Sample Request:

```Text Javascript
const webUrl = response.webRedirectUrl;

function convertToGoPayDeepLink(url) {
    const urlObj = new URL(url);
    const params = urlObj.search;
    return `gopay://merchanttransfer${params}`;
}
const deepLink = convertToGoPayDeepLink(webUrl);

// Assign to params object
var params = {
  deeplink: deepLink
};

window.gpContainer.call(  
  "GP",  
  "launchPayment",  
  params,  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v1/#error-codes))

```Text JSON
{
    success: true,
    data: {
        status: "success"
    },
		"ret": "GP_SUCCESS"
}
```

```Text JSON
{
    "success": false,
    "errorCode": "300",
    "errorType": "JS_BRIDGE_ERROR",
    "errorMessage": "Permission denied",
    "ret": "GP_EXCEPTION"   
}
```

| Status    | Description                                                                |
| :-------- | :------------------------------------------------------------------------- |
| success   | User have successfully paid the transaction                                |
| failed    | User cancelled the transaction                                             |
| pending   | There's an error processing the transaction                                |
| cancelled | User goes back to the miniapp without completing or cancelling the payment |

## Launch Uri

Sample Request:

```Text Javascript
var params = {
  uri: "string"
};

window.gpContainer.call(  
  "GPNavigator",  
  "launchUri",  
  params,  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v1/#error-codes))

```Text JSON
{
    "success": true,
		"ret": "GP_SUCCESS"
}
```

```Text JSON
{
    "success": false,
    "errorCode": "300",
    "errorType": "JS_BRIDGE_ERROR",
    "errorMessage": "Permission denied",
    "ret": "GP_EXCEPTION"   
}
```

## Start Compass

Sample Request:

```Text Javascript
var params = {
/**
interval is either "game", "ui", or "normal". "normal" is default
"game" : 20ms
"ui": 60ms
"normal": 200ms
*/
  interval: 'normal'
};

window.gpContainer.call(  
  "GPMotion",  
  "startCompass",  
  params,  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);

// Listen to Compass result
document.addEventListener('GPMotion.Event.compass', function (e) {
        alert('event compass: ' + JSON.stringify(e.param));
});
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v1/#error-codes))

```Text JSON
{
    "success": true,
    "ret": "GP_SUCCESS",
		"msg": "COMPASS_STARTED"
}
```

```Text JSON
{
    direction: double, // The value due north between [0,360)
    timestamp: int64
}
```

```Text JSON
{
    "success": false,
    "errorCode": "",
    "errorType": "JS_BRIDGE_ERROR",
    "errorMessage": "",
    "ret": "GP_EXCEPTION"   
}
```

## Stop Compass

Sample Request:

```Text Javascript
window.gpContainer.call(  
  "GPMotion",  
  "stopCompass",  
  {},  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v1/#error-codes))

```Text JSON
{
    "success": true,
		"ret": "GP_SUCCESS",
		"msg": "COMPASS_STOPPED"
}
```

```Text JSON
{
    "success": false,
    "errorCode": "",
    "errorType": "JS_BRIDGE_ERROR",
    "errorMessage": "",
    "ret": "GP_EXCEPTION"   
}
```

## update

Sample Request:

```Text Javascript
{
  title: '',
  titleColor: '#FF00FF',
  barStyle: 'float',
  backgroundColor: '#00FFFF00',
  hideBackButton: 'false'
}

window.gpContainer.call(  
  "GPNavigationBar",  
  "update",  
  params,  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v1/#error-codes))

```Text JSON
{
    "success": true,
		"ret": "GP_SUCCESS"
}
```

```Text JSON
{
    "success": false,
    "errorCode": "",
    "errorType": "JS_BRIDGE_ERROR",
    "errorMessage": "",
    "ret": "GP_EXCEPTION"   
}
```

## getHeight

Sample Request:

```Text Javascript
window.gpContainer.call(  
  "GPNavigationBar",  
  "getHeight",  
  {},  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v1/#error-codes))

```Text JSON
{
    "success": true,
		"ret": "GP_SUCCESS"
}
```

```Text JSON
{
    "success": false,
    "errorCode": "",
    "errorType": "JS_BRIDGE_ERROR",
    "errorMessage": "",
    "ret": "GP_EXCEPTION"   
}
```

## update NavBar

Sample Request:

```Text Javascript
var params = {
  title: '',
  titleColor: '#FFFFFF00', //the last two digits for opacity, remove it to not make transparent
  barStyle: 'float',
  backgroundColor: '#FFFFFF00',
  hideBackButton: 'false'
        };

window.gpContainer.call(  
  "GPNavigationBar",  
  "update",  
  params,  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

```Text Javascript
var params = {
  title: '',
  titleColor: '#FFFFFF00', //the last two digits for opacity, remove it to not make transparent
  barStyle: 'float',
  backgroundColor: '#FFFFFF00',
  hideBackButton: 'false'
        };

window.gpContainer.call(  
  "GPNavigationBar",  
  "update",  
  params,  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v1/#error-codes))

```Text JSON
{
    "success": true,
		"ret": "GP_SUCCESS"
}
```

```Text JSON
{
    "success": false,
    "errorCode": "",
    "errorType": "JS_BRIDGE_ERROR",
    "errorMessage": "",
    "ret": "GP_EXCEPTION"   
}
```

## getHeight

Sample Request:

```Text Javascript
window.gpContainer.call(  
  "GPNavigationBar",  
  "getHeight",  
  {},  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v1/#error-codes))

```Text JSON
{
    "success": true,
		"ret": "GP_SUCCESS"
}
```

```Text JSON
{
    "success": false,
    "errorCode": "",
    "errorType": "JS_BRIDGE_ERROR",
    "errorMessage": "",
    "ret": "GP_EXCEPTION"   
}
```

## toast

Sample Request:

```Text Javascript
var params = {
        // The toast message that you want to display.
        message: 'Toast information',
        // The duration for which the toast message is displayed.
        duration: 5
        };

window.gpContainer.call(  
  "GPUIToast",  
  "toast",  
  params,  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v1/#error-codes))

```Text JSON
{
    "success": true,
		"ret": "GP_SUCCESS"
}
```

```Text JSON
{
    "success": false,
    "errorCode": "",
    "errorType": "JS_BRIDGE_ERROR",
    "errorMessage": "",
    "ret": "GP_EXCEPTION"   
}
```

<br />

## trackEvent

Sample Request:

```Text Javascript
var params = {
        "eventName": "Your event name",
        "metaData": {
                "mini_app_version": "Version ABC",
                "mini_app_id": "ID-123",
                "page_id":"page-3","error_code":"qwe","error_description":""    
        }
};

window.gpContainer.call(  
  "GPAnalytics",  
  "trackEvent",  
  params,  
  function(response) {},  
  function(error) {}  
);

```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

```Text JSON
{
  "callbackId": "alphanumeric string",
  "success": true,
  "ret": "GP_SUCCESS"
}
```

```Text JSON
{
  "callbackId":"alphanumeric string",
  "errorCode":"GP_PARAM_ERR",
  "errorMessage":"metaData can not be empty",
  "ret":"GP_PARAM_ERR"
}
```

| Field                                          | Description                                                                                                       | Format | Mandatory / Optional | Sample                                                      |
| :--------------------------------------------- | :---------------------------------------------------------------------------------------------------------------- | :----- | :------------------- | :---------------------------------------------------------- |
| eventName                                      | This is the event name that will describe what the event or user specific activity is inside the mini app.        | String | Mandatory            | GP Mini App User Completed Level 4                          |
| metaData                                       | Extra properties that merchants can send with the specific event.                                                 | Map    | Mandatory            | Sample below                                                |
| mini\_app\_id                                  | The mini app identifier (can provide and distinguish for each version as well)                                    | String | Optional             | "mini\_app\_id":"abcd1234"                                  |
| mini\_app\_version                             | The mini app version (if any)                                                                                     | String | Optional             | 1.0                                                         |
| user\_action                                   | To define the user action if it's viewed or clickedada                                                            | String | Optional             | viewed, clicked                                             |
| completed\_action                              | To define what the completed action by the user                                                                   | String | Optional             | payment, rewards, task completion, item id, item name, etc. |
| page\_id                                       | To define if the user is on the specific page inside the mini app                                                 | String | Optional             | page\_xyz                                                   |
| page\_name                                     | To define if the user is on the specific page inside the mini app                                                 | String | Optional             | mini\_app\_pet\_homepage                                    |
| component\_id                                  | To define if the user is having the interaction (clicked) with the specific component inside the mini app         | String | Optional             | cta\_123                                                    |
| url                                            | To define if there is a redirection component inside the cta when the user is having the interaction with         | String | Optional             | gopay://                                                    |
| error\_code(use only if there is any error)    | To indicate the error code when there is a technical glitch inside the mini app                                   | String | Optional             | 500                                                         |
| error\_description(use only if there is error) | To indicate the error message that is displayed to the users when there is a technical glitch inside the mini app | String | Optional             | User id not found                                           |

<br />

## Error Codes

Category:

| Category             | Code | Description                                                                                       |
| :------------------- | :--- | :------------------------------------------------------------------------------------------------ |
| Platform Error       | 1xx  | Platform-related errors, such as opening gopay deeplink while you're testing on the web           |
| Miniapp Error        | 2xx  | Such as method invocation error calling openDeeplink with a wrong deeplink format                 |
| Permission Error     | 3xx  | Permission-related error, such as getting user location but the user does not give the permission |
| Device related Error | 4xx  | Returned on device-related error such as network error                                            |
| Superapp Error       | 5xx  | Error from the superapp side (imagine this as server error)                                       |

Error Code List:

| Codes | Description                | Happens When                                                                                              |
| :---- | :------------------------- | :-------------------------------------------------------------------------------------------------------- |
| 100   | Method not supported error | The miniapp is calling a method that's not supported on the platform.                                     |
| 200   | Incomplete parameter error | The method call have incomplete parameters                                                                |
| 201   | Invalid type error         | The method call have invalid parameters. E.g. providing int while the required type is string             |
| 202   | Parameter data error       | The parameters being called is not supported by gopay. E.g. calling open deeplink with non-gopay deeplink |
| 203   | Miniapp not registered     | The miniapp you're developing is not registered inside gopay system                                       |
| 300   | No permission error        | Miniapp does not have access to the method being called                                                   |
| 400   | Device not supported       | The resource being requested is not supported by the device                                               |
| 401   | Network Error              | Internet related problem such as slow or disconnected internet                                            |
| 500   | Superapp error             | Superapp related error. Happens if there's an internal error in gopay while a resource is requested       |