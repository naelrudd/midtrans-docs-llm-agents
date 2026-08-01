---
updatedAt: 2025-11-10T22:41:14.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Security Information

Security is the top priority at Midtrans. Midtrans monitors both internal and external factors to ensure that your payments are secure.

***

## Midtrans Security

* **PCI DSS**<br />\
  PCI-DSS (Payment Card Industry Data Security Standard) is a certificate or license issued by the PCI Security Standards Council to maintain the security of all transaction activities through Midtrans payment systems. Midtrans has implemented all security standards, set by the PCI Standard Council, on network and payment systems to minimize any security risk that could interfere with transaction processes in our system.\
  Midtrans has been audited by the QSA (Qualified Security Assessor) certified by PCI Council. Midtrans is PCI compliant with [PCI Service Provider Level 1](http://www.visa.com/splisting/searchGrsp.do?companyNameCriteria=midtrans) certification, which is the most stringent level of certification currently available in the payments industry.

* **ISO 27001**<br />\
  ISO27001 (or commonly known as ISO / IEC 27001) is a certificate or license issued by the Internal Standards Organization (ISO) which regulates security management information system.\
  We have implemented the ISO27001 standard on our system and network to maintain the security of our information.

* **AES 256**<br />\
  AES (Advanced Encryption Standard) is an encryption standard that was issued by the National Institute of Standards and Technology (NIST). It is generally used to maintain the confidentiality of data.\
  At Midtrans, we use AES-256 as a standard of encryption of all transaction data that goes in and out of our system.

* **Fraud Detection System**<br />At Midtrans, we analyze, process, and manage each transaction in detail with our machine learning tool. After these steps, the behavior patterns are analyzed using details such as payment location, email detail, time, and so on.

  Source: <https://midtrans.com/security>

## HTTPS for Secure Connections

We enforce [TLS/SSL encryption](https://www.cloudflare.com/learning/ssl/what-is-ssl/) to all of our public endpoints [via HTTPS](https://www.cloudflare.com/learning/ssl/what-is-https/), including our public website and Merchant Administration Portal. To ensure that communication coming from merchants & their customers are securely encrypted over the network.

`midtrans.min.js` and `snap.js` are also securely hosted over HTTPS. We suggest merchants not to host these files on their servers, and should use Midtrans provided url.

Please make sure your system are able to communicate with Midtrans securely by referring to [this article about SSL/TLS](https://midtrans.com/id/blog/time-to-upgrade-to-tls-version-1-2).

To connect securely, your system must support our TLS configurations. We recommend upgrading to TLS 1.3 for optimal security and performance—faster handshakes reduce latency in mobile e-wallet flows.

**Requirements**

* Use HTTPS only—no plain HTTP.
* Support Server Name Indication (SNI) for hostname verification.

### Supported TLS Versions and Cipher Suites

We support only modern protocols to protect against vulnerabilities. Older versions (TLS 1.0/1.1) are disabled.

| TLS Version | Status                | Preferred Cipher                                    | Supported Cipher                                                                                               |
| :---------- | :-------------------- | :-------------------------------------------------- | :------------------------------------------------------------------------------------------------------------- |
| TLS 1.3     | Enabled (recommended) | TLS\_AES\_128\_GCM\_SHA256 (128 bits, Curve 25519)  | - TLS\_AES\_256\_GCM\_SHA384 (256 bits, Curve 25519) - TLS\_CHACHA20\_POLY1305\_SHA256 (256 bits, Curve 25519) |
| TLS 1.2     | Enabled               | ECDHE-RSA-CHACHA20-POLY1305 (256 bits, Curve 25519) | - ECDHE-RSA-AES128-GCM-SHA256 (128 bits, Curve 25519) - ECDHE-RSA-AES256-GCM-SHA384 (256 bits, Curve 25519)    |

### Supported Key Exchange Groups

| TLS Version | Group                                                  |
| :---------- | :----------------------------------------------------- |
| TLS 1.3     | - secp256r1 (NIST P-256, 128 bits) - x25519 (128 bits) |
| TLS 1.2     | - secp256r1 (NIST P-256, 128 bits) - x25519 (128 bits) |

Prefer x25519 for performance.

### Supported HTTP Versions

Over HTTPS:

* HTTP/1.1: For basic compatibility.
* HTTP/2: Recommended for multiplexing—speeds up batch requests.

We are not officially supporting HTTP version older than 1.1  due to performance and security reasons.

## Card Data Secure Transmission

By following above points, all the data transmission coming from customer device to Midtrans is encrypted over the network layer via SSL/HTTPS. That means data transmission is end-to-end encrypted (customer-to-Midtrans), and secure from any third-party. Only Customer and Midtrans side can see the real value of data being transmitted, unless a third-party has direct control over the user’s device (which means already compromised anyway) or is able to decrypt SSL/HTTPS.

In order to ensure the customer-to-Midtrans encryption are properly implemented, merchants are required to use official Midtrans provided JavaScript library (midtrans.min.js, snap.js, or Mobile SDK) for card transactions. Merchants are strictly prohibited to record card credentials to their own system, unless PCI DSS certified.

Note: Some auditors may run into false-positive reports about being able to see credentials transmitted in plain text. This is possible when the audit is done on the customer device itself, in which case, the data is expected to be visible (not yet encrypted) from the customer device. The better approach is auditors should try to check from non-customer devices such as the network layer or lower layer (as third-party between Midtrans and customer). In that case they will expect to see that the data is securely encrypted from any unauthorized party.

Please also note that HTTPs GET method automatically encrypts any GET query / request credentials (via TLS/HTTPS). Although it sometimes can reveal the destination web domain (which is a safe public information), it **will not** expose any confidential parameter.

## Sensitive Data Encryption

Security is a priority at Midtrans and all transactions processed by our system are always securely encrypted. Midtrans never store any sensitive information in the system and all transactions are transmitted and processed via secured networks.

All encryption and security procedures follow the PCI-DSS standards to ensure highest security protection.

## Vulnerability Disclosure

Midtrans is always open to inputs or suggestions related our security processes. If you believe you have found a bug or security issue in Midtrans, please contact `security@midtrans.com` or [Contact Us Page](https://midtrans.com/contact-us) and we will respond as soon as possible. We encourage your cooperation to disclose it responsibly with us.

## Keep Your Server Key Secured

The *Server Key* you obtained from your Midtrans account is strictly informed only to you as a Merchant. The *Server Key* should be kept secret. To learn more about how to secure your *Server Key*, please refer to [this article](https://midtrans.com/id/blog/bagaimana-cara-menyimpan-server-key-dengan-aman).

## Keep Sensitive Parameters Secured

Payment parameters (JSON payload) like `gross_amount`, `order_id`, `credit_card.secure`, and so on are also sensitives, those shouldn't be directly editable from customer side. Otherwise, you are risking your customer being able to modify the payment amount (you may receive wrong/less amount of payment), order id, and/or 3D Secure configuration (you will be more prone to fraud).

This is your implementation responsibility, it can be securely managed from your backend, e.g: via validation and implementation logic.

## Securely Verify Payment Status

Learn more on how to [securely verify payment status](/docs/https-notification-webhooks#verifying-notification-authenticity), to avoid system security/financial liability on merchant side.

## Others

With the various Security protections provided above,

Implementing SSL certificate pinning on your end is not recommended. If you want to implement SSL certificate pinning, please make sure to [understand the considerations explained in this article.](/docs/technical-faq#what-should-be-considered-when-merchant-want-to-do-ssl-certificate-pinning)

In most cases Mutual (2-way) TLS Authentication (mTLS) should not be needed, and is not recommended due to maintenance complexity. In case you really need to proceed with implementing it, please consult with your Midtrans Business PIC first.