---
updatedAt: 2026-03-16T07:31:12.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# MiniApp Security Guidelines

This guide explains security best practices for building GoPay MiniApps and highlights common mistakes developers should avoid to protect credentials, APIs, and user data. 🔒

When you develop miniapps, you are advised to follow standard security guidelines to reduce the likelihood that you introduce security vulnerabilities into your miniapps. Since miniapps are essentially web applications that run inside the GoPay app, you should follow security guidelines for web applications. Several guidelines from OWASP that you could follow are:

1. [OWASP Developer Guide](https://owasp.org/www-project-developer-guide/)
2. [OWASP Application Security Verification Standard](https://owasp.org/www-project-application-security-verification-standard/)
3. [OWASP Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
4. [OWASP Top Ten Web Application Security Risks](https://owasp.org/www-project-top-ten/)
5. [OWASP Top Ten API Security Risks](https://owasp.org/API-Security/)

In addition to the above, you should specifically adhere to the following important guidelines:

1. Managing GoPay-issued credentials
   1. GoPay-issued credentials include GoPay client token (i.e., the token used to call the /v1/mini-apps/authorizations/token API) and GoPay user token (i.e., the token used to call the /v1/mini-apps/rewards API).
   2. GoPay client token must not be hardcoded in miniapp front-end. Knowledgable users can extract this token from miniapp front-end, and misuse it for malicious purposes.
   3. GoPay client token must not be hardcoded in source code repository. Employees who have access to source code repository can retrieve this token, and misuse it for malicious purposes.
   4. GoPay client token and GoPay user token must not be returned to miniapp front-end. Knowledgable users can extract these tokens from traffic between miniapp front-end and back-end, and misuse them for malicious purposes.
   5. GoPay client token and GoPay user token must not be logged in plain text form. Redact GoPay client token and GoPay user token in logged messages, such as HTTP requests, HTTP responses, and program exceptions.
   6. GoPay client token and GoPay user token must be stored securely in encrypted form within access-controlled storage.
2. Miniapp back-end API authentication
   1. Use your own credentials for miniapp back-end API authentication.
   2. Do not use GoPay user tokens to authenticate miniapp front-end access to miniapp back-end. Knowledgable users can extract GoPay user tokens from traffic between miniapp front-end and back-end, and misuse them for malicious purposes.
   3. Do not use GoPay account IDs to authenticate miniapp front-end access to miniapp back-end. GoPay account IDs are public information known to every miniapp.
3. Cheating detection
   1. For games, use anti-cheat technology to prevent users from manipulating the games. Knowledgable users can falsify scores, fraudulently claim winnings, and obtain undeserved rewards.
4. User permission
   1. Use the JSAPI SDK to request users for permissions (e.g., location, camera).
   2. Do not ask users for unnecessary permissions. The issued GoPay user tokens will be given access according to the granted permissions.
5. User privacy
   1. Do not ask users to enter GoPay credentials (e.g, PIN, OTP).
   2. Do not ask users to enter personal information (e.g., home address, credit card number) without any legitimate business needs.
   3. Do not show GoPay account IDs to users, since they are internal information.
   4. Follow applicable data privacy regulations if you collect, process, and store personal information. If you collect personal information, provide the terms and conditions, and ask for user consent.

If you experience security incidents, especially due to leakage of GoPay client token and GoPay user token, please inform us immediately via email at <gopay-mini-app-integrations@gojek.com>.