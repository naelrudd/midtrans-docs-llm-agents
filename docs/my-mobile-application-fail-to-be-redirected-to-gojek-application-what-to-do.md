---
updatedAt: 2025-11-11T00:16:25.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# My mobile application fail to be redirected to GOJEK application, what to do?

If you are using **android application web view**, there's configuration needed to allow open **deeplink** to other application.

Please make sure that the web view allow opening **gojek://** deeplink protocol.\
Please refer to **[this link ↗](https://stackoverflow.com/questions/25672330/how-to-enable-deep-linking-in-webview-on-android-app/32714613#32714613)** for more detail. You need to modify your web view **shouldOverrideUrlLoading** functions as follows :

```
 @Override  
 public boolean shouldOverrideUrlLoading(WebView view, String url) {  
        LogUtils.info(TAG, "shouldOverrideUrlLoading: " + url);  
        Intent intent;
   
				if (url.contains("gojek://")) {
        	intent = new Intent(Intent.ACTION_VIEW);
        	intent.setData(Uri.parse(url));
        	startActivity(intent);

       	 return true;
    } 
 }
```

On **iOS application web view**, you need to add **LSApplicationQueriesSchemes** key to your app’s **Info.plist,** please find the detail on below code :

```
<key>LSApplicationQueriesSchemes</key>  
<array>  
<string>gojek</string>  
</array>
```