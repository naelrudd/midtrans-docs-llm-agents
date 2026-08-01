---
updatedAt: 2026-04-22T15:45:56.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Credential Exchange

This section will explain how merchants prepare to do credential exchange with Midtrans

> 📘 BI-SNAP Compliance
>
> This page describes the credential exchange process between merchants and Midtrans for BI-SNAP Core API integration, including the secure exchange of public keys. This fulfills BI-SNAP requirements for secure key delivery and management (ASPI audit items on public key exchange and delivery method).

<br />

Midtrans will provide the following during the credential exchange process:

* ClientID
* ClientSecret
* PartnerID
* ChannelID

The Partner must provide the following:

* PublicKey (must be in PKCS8 format and PEM encoded)

<br />

> 📘 Onboarding to BI SNAP
>
> If you don't see any BI SNAP menu in your dashboard, we might need to activate it for you first. Reach out to your Midtrans Sales PIC or Support (<support@midtrans.com>) to activate the feature for you.

<br />

## Generate Public and Private Key

<br />

<Image alt="Access Key Page" align="center" src="https://files.readme.io/bdd0befe923f9e49c398c5f060317e6e40b48aa91d6dd2ee7172d548936b4ce1-Image_from_Readme.io.png">
  Access Key Page
</Image>

<br />

Generating access keys can be done via Settings > Access Keys page, within the Payment BI SNAP section.

<br />

> 🚧
>
> Always generate the key pair starting from the Sandbox environment first before generating in Production.  Otherwise, the supported scopes will be empty. If you mistakenly generated the key pair in Production environment, contact Midtrans Support for further assistance.

<br />

### Generating Public and Private Key

<br />

Generate the Private Key first using the first command (line 2), then generate the Public Key using the second command (line 3).

<br />

```text
--generate private-public key pair in PKCS8 format and PEM encoded
openssl genpkey -algorithm rsa -out private-key.pem -outform PEM -pkeyopt rsa_keygen_bits:\<minimum 2048>  
openssl rsa -in private-key.pem -outform PEM -pubout -out public-key.pem

--alternatively if partner system can only consume PKCS1 private key, then partner can convert the public key from PKCS1 to PKCS8
openssl rsa -RSAPublicKey_in -in publicKeyPKCS1.pem -pubout -out publicKeyPKCS8.pem
```

<br />

### Registering the Public Key

Below is an example of how a correct Public Key looks like. Once generated, copy the entire file from the header until footer and then paste it the Dashboard > Settings > Access Keys > Payment BI SNAP then click the `Start generate credential` button. After pasting, click Register.

<br />

```text
-----BEGIN PUBLIC KEY-----  
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAomV+Vm1xlRXanmh108Kusls7SSKec0oCejtc9QG  
Obpd4RnQ+7gihm2k6etnSNP7b+XrpY+fBkiQNaBInii9M10kW9Bhf/M9GH/edL3IqnzDNSi7tcoQgnO7h8x  
mzLNWHTjtR6bkrsdBS5dry6htotaF5KXomuoYgztCdGDOa0W20aeLzYSXIoW7s/Ay5yIXt0xaXTll3/bmez  
leguFPnwQZq5EqZFWlUZvutDi+f2l9rTRY0Fb64y+VAf+mnIbEovGqsPEeF/p97YWxcY7CWm8NsT0lwBVOt  
kmEl967Brz5yvEObF5bJgVodi6mNVsN1ki0MCitIhYO8shcE7eUilQIDAQAB  
-----END PUBLIC KEY-----
```

<br />

<Image alt="Registering the public key" align="center" src="https://files.readme.io/bab7374a3b4af5c7dfaa7979d1ea3c662c4fabec7270fe720b08c2750d25eef6-Copy_public_key.png">
  Registering the public key
</Image>

<br />

### Secured Exchange Method

In order to make sure the credentials are exchanged securely over public networks, the credentials must be encrypted during transit.

<br />

#### Zip encrypted

Midtrans will provide the credentials in a Password Protected Zip file. The Password Protected Zip File and Password to the Zip File will be sent to separate emails.

Merchant must provide the public key in a Password Protected Zip file. The Password Protected Zip File and Password to the Zip File must be sent to separate emails.

<br />

***

<br />

## Public Key Exchange and Delivery Method

<br />

The following describes how public keys are exchanged between merchants and Midtrans, fulfilling BI-SNAP requirements for secure exchange of public keys used for SHA256withRSA signatures.

### Merchant → Midtrans (Merchant's Public Key)

| Step                              | Description                                                                                                                                                                                                                                        |
| :-------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1. Key generation**             | Merchant generates an RSA keypair (minimum 2048-bit) in PKCS#8 format, PEM-encoded, using the OpenSSL commands documented above                                                                                                                    |
| **2. Registration via Dashboard** | Merchant registers their public key via the Midtrans Dashboard ([Settings > Access Keys > Payment BI SNAP](https://dashboard.midtrans.com/settings/access_keys)). The Dashboard is protected by HTTPS (TLS 1.2+) and requires authenticated login. |
| **3. Alternative: Secured email** | For environments where Dashboard access is not available, the public key may be shared via password-protected ZIP file, with the ZIP file and password sent in separate emails                                                                     |
| **4. Verification**               | Upon registration, Midtrans validates the key format (PKCS#8, PEM, minimum 2048-bit RSA) and associates it with the merchant's Client ID                                                                                                           |

<br />

### Midtrans → Merchant (Midtrans' Public Key)

| Step                              | Description                                                                                                                                                                                    |
| :-------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1. Provision**                  | Midtrans generates its RSA keypair within its secure key management infrastructure                                                                                                             |
| **2. Delivery via Dashboard**     | Midtrans' public key is accessible to the merchant via the Dashboard ([Settings > Access Keys](https://dashboard.midtrans.com/settings/access_keys)), protected by authenticated HTTPS session |
| **3. Alternative: Secured email** | Midtrans may deliver its public key via password-protected ZIP file (password sent separately) when Dashboard delivery is not feasible                                                         |
| **4. Verification**               | Merchants should verify the key fingerprint upon receipt. Midtrans support can confirm key fingerprints through a separate authenticated channel if needed                                     |

<br />

### Client Secret Delivery

| Step                      | Description                                                                                                                                                              |
| :------------------------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1. Generation**         | Midtrans generates the client secret during credential provisioning                                                                                                      |
| **2. Delivery**           | Client secret is delivered via the Dashboard or via password-protected ZIP file (password sent separately)                                                               |
| **3. Storage obligation** | Merchants must store the client secret securely (see [Key Management Lifecycle](/reference/security-specification#key-management-lifecycle) for storage recommendations) |

<br />

> 📘 Compliance Note
>
> This process fulfills BI-SNAP requirements for secure exchange of public keys used for SHA256withRSA signatures. All exchanges occur over encrypted channels (HTTPS/TLS 1.2+), and credentials are never transmitted in plaintext over public networks. For key lifecycle management details (rotation, revocation, storage), refer to the [Security Specification](/reference/security-specification#key-management-lifecycle) page.