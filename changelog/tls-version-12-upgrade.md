Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# TLS Version 1.2 Upgrade

As we're always improving the security control to make our environment and connection secure for better web surfing, please be informed that we will upgrade Midtrans products\*. This upgrade-maintenance is scheduled on 1st February 2024 and it is required to upgrade your TLS version to 1.2 at minimum.\
There is a possibility to cause the connection failure such as breaking HTTPS traffic of transaction process or the API endpoints could not be accessible IF the minimum requirement of TLS version 1.2 was not met.\
Shall you encounter any access problem, please ensure to update all your browsers and OpenSSL to the latest version. Below are the reference links for upgrading your browsers:\
Firefox\
Chrome Safari Edge\
For other browsers, please visit their respective web page. Direct hit or access to the system (without browser), you can refer to this link (upgrade OpenSSL).\
Note:

1. If you're using windows version below Windows 7 or Windows Server 2008 SP2, please try to update the registry configuration based on this article. Otherwise, please upgrade your OS platform.
2. Only Android 5.x and higher are supporting TLS 1.2. Therefore, please upgrade your Android version.\
   PLEASE NOTE that the obsolete OS or platform will no longer be supported. (Please refer to this link for device/platform compatibility)\
   If the issue persists, please contact <support@midtrans.com.> Thank you for your kind attention.

For servers here are the guide for different programming languages:

php: <https://www.php.net/manual/en/migration56.openssl.php>

go: <https://pkg.go.dev/crypto/tls>

java: <https://www.java.com/en/configure_crypto.html>

ruby: <https://docs.ruby-lang.org/en/master/OpenSSL/SSL/SSLContext.html>

javascript: <https://nodejs.org/api/tls.html>

Impacted Midtrans Products:

1.Core Api

2.Snap

3.Payment link

4.Subscriptions

5.Mobile sdk

<br />