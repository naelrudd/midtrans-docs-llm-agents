---
updatedAt: 2025-11-11T00:42:51.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Getting Started

To start using the BI-SNAP version of Core API, merchants will first need to do credentials exchange with Midtrans. To do this, merchants need to prepare and submit the following items as part of the onboarding process.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        No.
      </th>

      <th style={{ textAlign: "left" }}>
        Items to prepare
      </th>

      <th style={{ textAlign: "left" }}>
        Definition
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        1
      </td>

      <td style={{ textAlign: "left" }}>
        Merchant's public and private key
      </td>

      <td style={{ textAlign: "left" }}>
        Merchant needs to create their public and private key (generated using PKCS8 standard) for signature generation that will be used when calling Access Token API.  

        Notes:  

        1. Public key is merchant’s key that will be shared with Midtrans for signature decryption purpose <br /> 2. Private key is merchant’s confidential key that will be saved on merchant’s side
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        2
      </td>

      <td style={{ textAlign: "left" }}>
        Merchant's redirect URL <br /><br /> *Required only for GoPay Tokenization flow*
      </td>

      <td style={{ textAlign: "left" }}>
        Merchant needs to share the redirection URL that will be used as redirection URL after user has authorized linking/payment on Gojek/GoPay app
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        3
      </td>

      <td style={{ textAlign: "left" }}>
        Merchant’s outgoing IP
      </td>

      <td style={{ textAlign: "left" }}>
        Merchant’s IP that will be whitelisted on Midtrans side. Only shared IP will be allowed to call Midtrans’ API
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        4
      </td>

      <td style={{ textAlign: "left" }}>
        Merchant's notification URL *Required if merchant consumed notification from Midtrans*
      </td>

      <td style={{ textAlign: "left" }}>
        Midtrans will send payment notification to the merchant's notification URL shared by merchants
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        5
      </td>

      <td style={{ textAlign: "left" }}>
        Merchant ID (MID)
      </td>

      <td style={{ textAlign: "left" }}>
        Merchant needs to complete registration on [midtrans.com](https://midtrans.com/id/passport) to acquire Merchant ID. Merchant can use an existing MID if wishes to. 
      </td>
    </tr>
  </tbody>
</Table>

<br />

Midtrans will then share the following items for merchant to store and use when calling Midtrans' API.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        No.
      </th>

      <th>
        Items provided by Midtrans
      </th>

      <th>
        Definition
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        1
      </td>

      <td>
        Midtrans’ public key <br />\
        *Required if merchant consumed notification from Midtrans*
      </td>

      <td>
        Midtrans will share its public key to merchant. By using Midtrans public key, merchant will be able to decrypt signature that is sent from Midtrans when calling merchant’s notification endpoint
      </td>
    </tr>

    <tr>
      <td>
        2
      </td>

      <td>
        Client ID
      </td>

      <td>
        Merchant’s client ID that will be given by Midtrans, will be used as X-CLIENT-KEY on request’s header in B2B Access Token API
      </td>
    </tr>

    <tr>
      <td>
        3
      </td>

      <td>
        Client Secret
      </td>

      <td>
        Merchant’s secret key that will be given by Midtrans, will be used for symmetric signature generation for Transactional API’s header
      </td>
    </tr>

    <tr>
      <td>
        4
      </td>

      <td>
        Partner ID
      </td>

      <td>
        Merchant’s partner ID that will be given by Midtrans, will be used as X-PARTNER-ID on Transactional API’s header
      </td>
    </tr>

    <tr>
      <td>
        5
      </td>

      <td>
        Midtrans outgoing IP <br /><br /> *Required if merchant consumed notification from Midtrans*
      </td>

      <td>
        Midtrans’ IP that merchant needs to whitelist to receive notification from Midtrans <br />\
        Staging:\
        3.1.141.98/32\
        52.76.190.190/32\
        13.251.192.204/32 <br /><br /> Production:\
        13.228.166.126/32\
        52.220.80.5/32\
        3.1.123.95/32
      </td>
    </tr>
  </tbody>
</Table>