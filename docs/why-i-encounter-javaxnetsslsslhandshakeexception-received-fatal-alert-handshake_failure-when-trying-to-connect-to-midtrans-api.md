---
updatedAt: 2025-11-11T00:16:24.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Why I encounter `javax.net.ssl.SSLHandshakeException: Received fatal alert: handshake_failure` when trying to connect to Midtrans API ?

This usually caused by outdated Java client.\
Please check the **Java version, web framework version**, and **OS version** used to connect. Please make sure you are not using outdated version, and stay updated.

For example if your versions are Java version 7, web framework version Spring 3.1, and OS version windows 7.\
Please update the Java version, because version 7 is no longer officially supported by Oracle (<https://java.com/en/download/faq/java_7.xml>). Other than that, Spring and OS version is also outdated. Using outdated platforms make your system vulnerable to security threats, which is not suitable environment for handling payments.