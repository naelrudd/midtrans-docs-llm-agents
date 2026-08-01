---
updatedAt: 2026-01-28T07:49:51.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Webview

Snap can also be embedded within your mobile app using WebView.

<br />

1. [Demo](https://sample-demo-dot-midtrans-support-tools.et.r.appspot.com/snap-webview) for native applications (Android and iOS)
2. [Demo](https://github.com/veritrans/Midtrans-Sample-SnapWebView/tree/master) for cross-platform applications (Flutter and React Native)

<br />

> 📘 Note
>
> Snap uses JavaScript in order to run properly. If you having issues accessing the Snap page in order to check out you may need to enable JavaScript

```javascript
webView.settings.javaScriptEnabled = true
webView.settings.javaScriptCanOpenWindowsAutomatically = true
webView.settings.domStorageEnabled = true
webView.settings.setAppCacheEnabled(true)
webView.settings.databaseEnabled = true
webView.settings.allowFileAccessFromFileURLs = true
webView.settings.allowFileAccess = true
webView.settings.allowContentAccess = true
webView.settings.cacheMode = WebSettings.LOAD_NO_CACHE

// react-native
<WebView
  ...
  ...
  javaScriptEnabled={true}
  javaScriptCanOpenWindowsAutomatically={true}
  domStorageEnabled={true}
  cacheEnabled={true}
  allowFileAccessFromFileURLs={true}
  allowFileAccess={true}
  cacheMode="LOAD_NO_CACHE"
>

// flutter
WebView(
...
...
    javascriptMode: JavascriptMode.unrestricted,
)
```

> 🚧 Custom JS Injection
>
> We strongly discourage merchant from injecting any custom JS into the Webview during payment flow.  It is expected that Merchant will honor customer’s privacy by not tracking any input that customer made within the Webview especially on sensitive data, as legal consequences could follow

<br />

### Download File inside Webview

> 📘 Note
>
> Snap offers downloadable files within the app. By default, these files will automatically download when accessed through a web browser. However, if you are using a webview within the app, additional configuration is required for the download to work properly.

```Text Dart/Flutter
import 'dart:convert';
import 'dart:io';

import 'package:flutter/material.dart';
import 'package:webview_flutter/webview_flutter.dart'; // webview_flutter ^4.x
import 'package:path_provider/path_provider.dart'; // ^2.x


class SnapWebViewScreen extends StatefulWidget {
  @override
  State<SnapWebViewScreen> createState() => _SnapWebViewState();
}

class _SnapWebViewState extends State<SnapWebViewScreen> {
  late final WebViewController _controller;

  @override
  void initState() {
    super.initState();

    _controller = WebViewController()
      ..setJavaScriptMode(JavaScriptMode.unrestricted)
      ..addJavaScriptChannel(
        'Downloader',
        onMessageReceived: (message) async {
          final payload = jsonDecode(message.message);
          final bytes = base64Decode(payload['data']);

          final directory = await getTemporaryDirectory();
          final file = File('${directory.path}/qr.png');

          await file.writeAsBytes(bytes);
        },
      )
      ..setNavigationDelegate(
        NavigationDelegate(
          onPageFinished: (url) {
            _controller.runJavaScript(_blobInterceptorScript);
          },
        ),
      )
      ..loadRequest(Uri.parse('your-url'));
  }

  static const String _blobInterceptorScript = '''
    (function () {
      if (window.__blobHookInstalled) return;
      window.__blobHookInstalled = true;

      function sendBlobToFlutter(blob) {
        const reader = new FileReader();
        reader.onloadend = function () {
          Downloader.postMessage(JSON.stringify({
            filename: 'qr.png',
            data: reader.result.split(',')[1]
          }));
        };
        reader.readAsDataURL(blob);
      }

      // Intercept fetch (modern implementations)
      const originalFetch = window.fetch;
      window.fetch = function (input, init) {
        return originalFetch(input, init).then(function (response) {
          const url = typeof input === 'string' ? input : input.url;
          if (url && url.includes('/qr-code')) {
            response.clone().blob().then(sendBlobToFlutter);
          }
          return response;
        });
      };

      // Intercept XMLHttpRequest (legacy / axios)
      const origOpen = XMLHttpRequest.prototype.open;
      const origSend = XMLHttpRequest.prototype.send;

      XMLHttpRequest.prototype.open = function (method, url) {
        this._url = url;
        return origOpen.apply(this, arguments);
      };

      XMLHttpRequest.prototype.send = function () {
        this.addEventListener('load', function () {
          if (this._url && this._url.includes('/qr-code') && this.response instanceof Blob) {
            sendBlobToFlutter(this.response);
          }
        });
        return origSend.apply(this, arguments);
      };
    })();
  ''';

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: WebViewWidget(controller: _controller),
    );
  }
}


```

> 🚧 Important Notes
>
> Blob data must be captured directly from the network response (fetch or XMLHttpRequest).
> The JavaScript snippet must be injected into the WebView context using runJavaScript

```Text JS/React-Native
import React, { useState } from 'react';
import { View, Alert, StyleSheet, ActivityIndicator } from 'react-native';
import { WebView } from 'react-native-webview';
import RNFS from 'react-native-fs';
import RNFetchBlob from 'rn-fetch-blob';

const WebviewComponent = ({ uri }) => {
  const [isLoading, setLoading] = useState(true);

  // Handle file download for 'blob:' URLs
  const handleDownload = async (url) => {
    const downloadDest = `${RNFS.DocumentDirectoryPath}/${new Date().getTime()}.png`;  // Save path

    RNFetchBlob.config({
      fileCache: true,
      path: downloadDest,  // Download destination path
    })
      .fetch('GET', url)   // Fetch the file from the URL
      .then((res) => {
        Alert.alert('Download Complete', `File downloaded to: ${res.path()}`);
      })
      .catch((error) => {
        Alert.alert('Download Error', error.message);
      });
  };

  return (
    <View style={styles.wrapper}>
      <WebView
        source={{ uri: uri || DEFAULT_URI }}
        onLoad={() => setLoading(false)}
        javaScriptEnabled={true}
        domStorageEnabled={true}
        onShouldStartLoadWithRequest={(request) => {
          // Intercept and handle 'blob:' URLs for download
          if (request.url.startsWith('blob:')) {
            handleDownload(request.url);  // Call download handler
            return false;  // Prevent default navigation
          }
          return true;  // Allow other URLs to load
        }}
      />
      {isLoading && (
        <View style={styles.loader}>
          <ActivityIndicator size='large' color='blue' />
        </View>
      )}
    </View>
  );
};

const styles = StyleSheet.create({
  wrapper: { flex: 1 },
  loader: {
    position: 'absolute',
    top: '50%',
    right: 0,
    left: 0,
  },
});

export default WebviewComponent;

```

> 🚧 Invalid Routing blob
>
> We recommend merchants implement this workaround, especially when using QRIS, Alfamart, or Indomaret payment channels, as these channels involve downloading files such as QR codes, barcode images, and PDF documents.