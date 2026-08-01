---
updatedAt: 2026-07-23T05:48:45.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Frontend SDKs V2

This guide explains the technical specifications of JSAPIs that is available to be called from your application's frontend.

# Integrate SDK

1. **Include the gpContainer SDK in Your Codebase**<br />To use the SDK, add the following
   ```html
   <script src="https://gwk.gopayapi.com/sdk/stable/gp-container.min.js"></script>
   ```

2. **Invoking SDK Methods**<br />To call any JSAPI from the SDK, use the following format:
   ```javascript
   (window.gpContainer?.call){
     window.gpContainer.call(className, methodName, params, successCallback, failureCallback, timeout);
   }
   ```

***

# Supported JSAPIs

GPLocation (need to change all openlinks)

| API                                                                                     | Function                                             | Requires Consent |
| :-------------------------------------------------------------------------------------- | :--------------------------------------------------- | :--------------- |
| GPLocation.[getLocation](https://docs.midtrans.com/reference/frontend-v2/#get-location) | Obtain user's device longitude and latitude location | Yes              |

GPMiniAppAuth

| API                                                                                         | Function                                                   | Requires Consent |
| :------------------------------------------------------------------------------------------ | :--------------------------------------------------------- | :--------------- |
| GPMiniAppAuth.[getAuthCode](https://docs.midtrans.com/reference/frontend-v2/#get-auth-code) | Get an auth code used to identify the current user session | No               |

GPNavigator

| API                                                                                            | Function                                                   | Requires Consent |
| :--------------------------------------------------------------------------------------------- | :--------------------------------------------------------- | :--------------- |
| GPNavigator.[launchDeeplink](https://docs.midtrans.com/reference/frontend-v2/#launch-deeplink) | Open a third-party app or page using a custom deeplink     | No               |
| GPNavigator.[launchUri](https://docs.midtrans.com/reference/frontend-v2/#launch-uri)           | Open a browser or in-app page using a universal or web URI | No               |

GP

| API                                                                                               | Function                                                                                                  | Requires Consent |
| :------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------------------------------- | :--------------- |
| GP.[launchPayment](https://docs.midtrans.com/reference/frontend-v2/#launch-payment)               | Automatically redirect users to the GoPay app to complete the payment, then return them to your Mini App. | No               |
| GP.[getBankAccountToken](https://docs.midtrans.com/reference/frontend-v2/#get-bank-account-token) | Request and tokenize the user’s linked bank account information                                           | Yes              |

GPSystem

| API                                                                                                     | Function                                                                  | Requires Consent |
| :------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------ | :--------------- |
| GPSystem.[getSystemInfo](https://docs.midtrans.com/reference/frontend-v2/#get-system-info)              | Get device's system info such as OS, model, and app version               | Yes              |
| GPSystem.[getRootedDeviceInfo](https://docs.midtrans.com/reference/frontend-v2/#get-rooted-device-info) | Get device's rooted info                                                  | Yes              |
| GPSystem.[getWifiInfo](https://docs.midtrans.com/reference/frontend-v2/#get-wifi-info)                  | Get the device’s connected Wi-Fi details, such as SSID or signal strength | Yes              |

GPConsent

| API                                                                                           | Function                                                                                                                                                                | Requires Consent |
| :-------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------- |
| GPConsent.[getUserConsent](https://docs.midtrans.com/reference/frontend-v2/#get-user-consent) | Show a postlaunch popup consent page and ask for user consent for accessing certain features such sensitive including PII, location, systeminfo, device permission data | Yes              |

GPMotion

| API                                                                                                 | Function                                                          | Requires Consent |
| :-------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------- | :--------------- |
| GPMotion.[startAccelerometer](https://docs.midtrans.com/reference/frontend-v2/#start-accelerometer) | Start monitoring acceleration of the device in 3D space           | No               |
| GPMotion.[stopAccelerometer](https://docs.midtrans.com/reference/frontend-v2/#stop-accelerometer)   | Stop monitoring acceleration                                      | No               |
| GPMotion.[startCompass](https://docs.midtrans.com/reference/frontend-v2/#start-compass)             | Start receiving compass direction data (magnetic heading)         | No               |
| GPMotion.[stopCompass](https://docs.midtrans.com/reference/frontend-v2/#stop-compass)               | Stop receiving compass data                                       | No               |
| GPMotion.[listenGyro](https://docs.midtrans.com/reference/frontend-v2/#listen-gyro)                 | Start receiving gyroscope data (rotation rate around device axes) | No               |
| GPMotion.[listeningShake](https://docs.midtrans.com/reference/frontend-v2/#listening-shake)         | Listen for shake gesture events                                   | No               |
| GPMotion.[vibrate](https://docs.midtrans.com/reference/frontend-v2/#vibrate)                        | Trigger vibration on the device                                   | No               |

GPFile

| API                                                                  | Function                                                    | Requires Consent |
| :------------------------------------------------------------------- | :---------------------------------------------------------- | :--------------- |
| GPFile.[save](https://docs.midtrans.com/reference/frontend-v2/#save) | To save image and PDF in iOS (Android is not supported yet) | No               |

GPShare

| API                                                                     | Function                                 | Requires Consent |
| :---------------------------------------------------------------------- | :--------------------------------------- | :--------------- |
| GPShare.[share](https://docs.midtrans.com/reference/frontend-v2/#share) | To share text format to the social media | No               |

GPBase

| API                                                                                        | Function                                   | Requires Consent |
| :----------------------------------------------------------------------------------------- | :----------------------------------------- | :--------------- |
| GPBase.[getLocale](https://docs.midtrans.com/reference/frontend-v2/#getlocale)             | To get the app locale, supported ID and EN | No               |
| GPBase.[copyToClipboard](https://docs.midtrans.com/reference/frontend-v2/#copytoclipboard) | To copy content to clipboard               | No               |

GPCamera

| API                                                                              | Function                                                                              | Requires Consent |
| :------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------ | :--------------- |
| GPCamera.[takePhoto](https://docs.midtrans.com/reference/frontend-v2/#takephoto) | Allow users to capture photos with the device camera or upload them from the gallery. | Yes              |

GPAnalytics

| API                                                                                   | Function                                                                                                | Requires Consent |
| :------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------ | :--------------- |
| GPAnalytics.[trackEvent](https://docs.midtrans.com/reference/frontend-v2/#trackevent) | To send structured events back to GoPay, enabling visibility on how users interact within the mini app. | No               |

***

# [Version History](https://docs.midtrans.com/update/reference/version-history)

***

# JSAPIs Specification (v1.0.0)

<Callout icon="📝" theme="default">
  ### Note

  - Data will be null in case of success = false, and vice versa.
  - Error will be null in case of success = true, and vice versa.
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

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

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
    "error_code": "",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "",
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

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

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
    "error_code": "",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "",
    "ret": "GP_EXCEPTION"   
}
```

## Launch Deeplink

Sample Request:

```Text Javascript
var params = {
  deeplink: "string"
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

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

```Text JSON
{
		success: true,
		"ret": "GP_SUCCESS" 
}
```

```Text JSON
{
    "success": false,
    "error_code": "300",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "Permission denied",
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

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

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
    "error_code": "300",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "Permission denied",
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

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

```Text JSON
{
    "success": true,
		"ret": "GP_SUCCESS"
}
```

```Text JSON
{
    "success": false,
    "error_code": "",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "",
    "ret": "GP_EXCEPTION"   
}
```

## Get System Info

Sample Request:

```Text Javascript
window.gpContainer.call(  
  "GPSystem",  
  "getSystemInfo",  
  {},  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

```Text JSON
{
    success: boolean,
    data?: {
      platform: string,
      is_emulator: boolean,
      brand: string,
      model: string,
      product: string,
      uuid: string,
      idfa: string,
      idfv: string
    },
		"ret": "GP_SUCCESS"
}
```

```Text JSON
{
    "success": false,
    "error_code": "",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "",
    "ret": "GP_EXCEPTION"   
}
```

## Get Rooted Device Info

Sample Request:

```Text Javascript
window.gpContainer.call(  
  "GPSystem",  
  "getRootedDeviceInfo",  
  {},  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

```Text JSON
{
    success: boolean,
    data?: {
      is_rooted: string
    },
		"ret": "GP_SUCCESS"
}
```

```Text JSON
{
    "success": false,
    "error_code": "",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "",
    "ret": "GP_EXCEPTION"   
}
```

## Get Wifi Info

Sample Request:

```Text Javascript
window.gpContainer.call(  
  "GPSystem",  
  "getWifiInfo",  
  {},  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

```Text JSON
{
    success: boolean,
    data?: {
      wifi_bssid: string,
      wifi_ssid: string,
    },
		"ret": "GP_SUCCESS"
}
```

```Text JSON
{
    "success": false,
    "error_code": "",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "",
    "ret": "GP_EXCEPTION"   
}
```

## Get User Consent

Note: Certain Features requires consent as a prerequisite. If you configured the consent as postlaunch, you need to trigger this SDK to show the consent popup and get user consent.

You won't need to call this SDK if it's configured as prelaunch mandatory.

Sample Request:

```Text Javascript
var params = {
  scope: 'location'
/**
scope is consent_name provided below, you must have the right permissions and consent configured to show this
*/
};

window.gpContainer.call(  
  "GP",  
  "authorize",  
  params,  
  function(response) {  
		if (response.successScope['location']) {
              	alert('success authorize location');
              	//call the jsapi you need to use
            }
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

| JSAPI                 | consent\_name                                            |
| :-------------------- | :------------------------------------------------------- |
| getLocation(GoPay)    | location                                                 |
| getCamera(Javascript) | camera                                                   |
| getProfile(GoPay)     | You can get this from the error response from getProfile |

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

```Text JSON
{
    data: {
        successScope: {"location": true}
    },
    success: boolean,
		"ret": "GP_SUCCESS"
}
```

```Text JSON
{
    "success": false,
    "error_code": "",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "",
    "ret": "GP_EXCEPTION"   
}
```

Possible Error Codes:

| Error Code | Description                |
| :--------- | :------------------------- |
| 100        | Method not supported error |
| 105        | User not found             |
| 200        | Incomplete parameter error |
| 201        | Invalid type error         |
| 202        | Parameter data error       |
| 203        | Miniapp not registered     |
| 300        | No permission error        |
| 303        | Malformed Authorization    |
| 400        | Device not supported       |
| 401        | Network error              |
| 500        | Superapp error             |
| 900        | Unable to process          |

## Get Bank Account Token

Sample Request:

```Text Javascript
window.gpContainer.call(
  "GP",
  "getBankAccountToken",
  {},
  function(response) {
    console.log('success:', response);
  },
  function(error) {
    console.log('error:', error);
  }
);
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

```Text JSON
{
    success: boolean,
    data?: {
      token: string
    },
		"ret": "GP_SUCCESS"
}
```

```Text JSON
{
    "success": false,
    "error_code": "",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "",
    "ret": "GP_EXCEPTION"   
}
```

## Start Accelerometer

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
  "startAccelerometer",  
  params,  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);

// Listen to Compass result
document.addEventListener('GPMotion.Event.accelerometer', (e: GPMotionAccelerometerData) => {
  console.log('Received gpAsyncCallback event:', JSON.stringify(e));
});
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

```Text JSON
{
    "success": true,
    "ret": "GP_SUCCESS",
		"msg": "ACCELEROMETER_STARTED"
}
```

```Text JSON
{
    x: double,
    y: double,
    z: double
}
```

```Text JSON
{
    "success": false,
    "error_code": "",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "",
    "ret": "GP_EXCEPTION"   
}
```

## Stop Accelerometer

Sample Request:

```Text Javascript
window.gpContainer.call(  
  "GPMotion",  
  "stopAccelerometer",  
  {},  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
  );
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

```Text JSON
{
    "success": true,
		"ret": "GP_SUCCESS",
		"msg": "ACCELEROMETER_STOPPED"
}
```

```Text JSON
{
    "success": false,
    "error_code": "",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "",
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
document.addEventListener('GPMotion.Event.compass', (e: GPMotionCompassData) => {
  console.log('Received gpAsyncCallback event:', JSON.stringify(e));
});
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

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
    "error_code": "",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "",
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

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

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
    "error_code": "",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "",
    "ret": "GP_EXCEPTION"   
}
```

## Listen Gyro

Sample Request:

```Text Javascript
var params = {
/**
on - Enable or disable monitoring of the gyroscope. (response would be GYROSCOPE_STARTED or GYROSCOPE_STOPPED)
frequency - The interval between gyroscope events.
*/
        on: true,
        frequency: 100
};

window.gpContainer.call(  
  "GPMotion",  
  "listenGyro",  
  {},  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);

// Listen to gyroscope
document.addEventListener('motion.gyro', (e: GPMotionGyroscopeData) => {
  console.log('Received gpAsyncCallback event:', JSON.stringify(e));
});
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

```Text JSON
{
    "success": true,
    "ret": "GP_SUCCESS",
		"msg": "GYROSCPOPE_STARTED"
}
```

```Text JSON
{
    x: double,
    y: double,
    z: double
}
```

```Text JSON
{
    "success": false,
    "error_code": "",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "",
    "ret": "GP_EXCEPTION"   
}
```

## Listening Shake

Sample Request:

```Text Javascript
var params = {
// on: specifies whether to enable monitoring of the shake gesture. (response would be SHAKE_STARTED or SHAKE_STOPPED)
//frequency: optional. The minimum interval between shake events. 
//shakeThreshold: optional. The acceleration threshold used to identify shake gestures. 
//shakeNum: optional. The number of shake gestures used to generate a shake event. 
        bool on = 1;
    	  number frequency = 2; 
      	number shakeThreshold = 3;
     	 	number shakeNum = 4
};

window.gpContainer.call(  
  "GPMotion",  
  "listeningShake",  
  params,  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);

// Listen to Shake
document.addEventListener('motion.shake', (e: GPMotionShakeData) => {
  console.log('Received gpAsyncCallback event:', JSON.stringify(e));
});
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

```Text JSON
{
    "success": true,
    "ret": "GP_SUCCESS",
		"msg": "SHAKE_STARTED"
}
```

```Text JSON
{
    x: double,
    y: double,
    z: double
}
```

```Text JSON
{
    "success": false,
    "error_code": "",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "",
    "ret": "GP_EXCEPTION"   
}
```

## Vibrate

Sample Request:

```Text Javascript
var params = {
        // The vibration duration.
        duration: 7000
        };

window.gpContainer.call(  
  "GPMotion",  
  "vibrate",  
  params,  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

```Text JSON
{
    "success": true,
		"ret": "GP_SUCCESS"
}
```

```Text JSON
{
    "success": false,
    "error_code": "",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "",
    "ret": "GP_EXCEPTION"   
}
```

## Save

Sample Request:

```Text Javascript
var params = {
/**
url: the download URL of the file
name: the name of the file after the file is downloaded.The default name is 
timestamp_gpwebkit. This param is optional
destination: destination can either be 
"DOWNLOADS", (IOS & Android)
"DOCUMENTS", (Android)
"PICTURES", (IOS & Android)
"DCIM" (Android)
Based on that file will be saved either to local storage or gallery
*/
        string url = "imageUrl";
		    string name = "Images";
    		string destination = "PICTURES";
        };

window.gpContainer.call(  
  "GPFile",  
  "save",  
  params,  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);

// Listen to Save success
document.addEventListener('GPFile.Event.saveSuccess', (e) => {
          console.log('Received gpAsyncCallback event:', e.detail);
          showResult("downloadAsyncResult", e.detail);
        });

// Listen to Save failed
  document.addEventListener('GPFile.Event.saveFailed', (e) => {
          console.log('Received gpAsyncCallback event:', e.detail);
          showResult("downloadAsyncResult", e.detail);
        });
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

```Text JSON
{
		"success": true,
		"msg": "SAVE_STARTED",
		"ret": "GP_SUCCESS"
}
```

```Text JSON
{
		"msg": "SAVE_SUCCESS"
}
```

```Text JSON
{
		"msg": "SAVE_FAILED"
}
```

## Share

Sample Request:

```Text Javascript
var params = {
        text: "string",
        };

window.gpContainer.call(  
  "GPShare",  
  "share",  
  params,  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

```Text JSON
{
    "success": true,
		"ret": "GP_SUCCESS"
}
```

```Text JSON
{
    "success": false,
    "error_code": "",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "",
    "ret": "GP_EXCEPTION"   
}
```

## GetLocale

Sample Request:

```Text Javascript
window.gpContainer.call(  
  "GPBase",  
  "getLocale",
	{},
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

```Text JSON
{
    "success": true,
    "ret": "GP_SUCCESS",
		"app_locale": "en_ID" // You will receive the value in en_ID or id_ID , en_ID for English and id_ID for Indonesia
}
```

```Text JSON
{
    "success": false,
    "error_code": "",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "",
    "ret": "GP_EXCEPTION"   
}
```

## CopyToClipboard

Sample Request:

```Text Javascript
var params = {
        text: "string"
        };

window.gpContainer.call(  
  "GPBase",  
  "copyToClipboard",  
  params,  
  function(response) {  
    console.log('success:', response);  
  },  
  function(error) {  
    console.log('error:', error);  
  }  
);
```

Sample Response: ([error codes](https://docs.midtrans.com/reference/frontend-v2/#error-codes))

```Text JSON
{
    "success": true,
		"ret": "GP_SUCCESS"
}
```

```Text JSON
{
    "success": false,
    "error_code": "",
    "error_type": "JS_BRIDGE_ERROR",
    "error_message": "",
    "ret": "GP_EXCEPTION"   
}
```

## takePhoto

Sample Request:

```Text Javascript
var photoLocalPath; // Stores the local file path.var params = {
        mode: 'camera',// possible values camera, photo
        needBase64: true// default value is false
};
window.gpContainer.call('GPCamera', 'takePhoto', params, function(e) {
     var uploadParams = {
              // The path of the photo to be uploadedpath: e.localPath
              //base64 data is passed if : e.base64Data
      };
      // Implement your own logic to send the formData to a backend service for file storage.
      ...
      ...
}, function(e) {
        alert('takePhoto failure: ' + JSON.stringify(e));
});
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

<br />

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

<br />

## Error Codes

Category:

| Category             | Code | Description                                                                                       |
| :------------------- | :--- | :------------------------------------------------------------------------------------------------ |
| Platform Error       | 1xx  | Platform-related errors, such as opening GoPay deeplink while you're testing on the web           |
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

<br />