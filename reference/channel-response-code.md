---
updatedAt: 2026-02-02T04:22:58.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Card Channel Response Code

**Common Response Codes For All Payment Networks (VISA, MASTERCARD, JCB, AMEX):**

<Table>
  <thead>
    <tr>
      <th>
        <b>
          Code
        </b>
      </th>

      <th>
        <b>
          Description
        </b>
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        00
      </td>

      <td>
        Transaction was successful.
      </td>
    </tr>

    <tr>
      <td>
        01
      </td>

      <td>
        The customer’s bank (Card Issuer) has indicated a problem with the payment card number. The customer should contact their bank and should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        02
      </td>

      <td>
        The customer’s bank (Card Issuer) has indicated a problem with the payment card number. The customer should contact their bank and should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        03
      </td>

      <td>
        The Merchant ID is invalid. You should contact your Bank and ensure that you have provided the correct Merchant Account Number.
      </td>
    </tr>

    <tr>
      <td>
        04
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction and requests to retain the customer's payment card. This happens when the card is reported to be lost or stolen. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        05
      </td>

      <td>
        The customer’s bank has declined the transaction as the payment card number has failed a security check, or the funds have been frozen or depleted. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        06
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction as there is a problem with the payment card number. The customer should contact their bank. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        07
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction and requested that your customer’s payment card be retained (card reported lost or stolen). The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        09
      </td>

      <td>
        The customer’s bank (Card Issuer) has indicated a problem with the payment card number. The customer should contact their bank and should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        12
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction because of an invalid format or field. Check the transaction information and try processing the transaction again.
      </td>
    </tr>

    <tr>
      <td>
        13
      </td>

      <td>
        An invalid character such as a symbol or space, is passed to the Midtrans. Check your code implementation. Note: This error happens only in the Sandbox environment. For the Production environment, the amount is verified by Midtrans.
      </td>
    </tr>

    <tr>
      <td>
        14
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction as the payment card number does not exist. Check the payment card information and try processing the transaction again.
      </td>
    </tr>

    <tr>
      <td>
        15
      </td>

      <td>
        The customer’s bank (Card Issuer) does not exist. Check the payment card information and try processing the transaction again.
      </td>
    </tr>

    <tr>
      <td>
        19
      </td>

      <td>
        The transaction has not been processed and the customer should attempt to process the transaction again.
      </td>
    </tr>

    <tr>
      <td>
        21
      </td>

      <td>
        The customer’s bank (Card Issuer) has indicated a problem with the payment card number. The customer should contact their bank and use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        22
      </td>

      <td>
        The customer’s bank (Card Issuer) cannot be contacted during the transaction. The customer should check the payment card information and try processing the transaction again.
      </td>
    </tr>

    <tr>
      <td>
        23
      </td>

      <td>
        An unspecified error has occurred.
      </td>
    </tr>

    <tr>
      <td>
        25
      </td>

      <td>
        The customer’s bank (Card Issuer) does not recognize the payment card details. The customer should check the payment card information and try processing the transaction again.
      </td>
    </tr>

    <tr>
      <td>
        30
      </td>

      <td>
        The customer’s bank (Card Issuer) does not recognize the transaction details. The customer should check the transaction information and try processing the transaction again.
      </td>
    </tr>

    <tr>
      <td>
        31
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction as it does not allow transactions originating through mail, telephone, fax, email, or Internet orders. This error occurs with customers attempting to use a Discover Card. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        33
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction as the payment card has expired or the date is incorrect. Check the expiry date in the transaction and try processing the transaction again.
      </td>
    </tr>

    <tr>
      <td>
        34
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction as there is a suspected fraud on this payment card number.
      </td>
    </tr>

    <tr>
      <td>
        35
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction and requested that the customer’s payment card be retained (card reported lost or stolen). The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        36
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction and requested to retain the customer’s payment card (card reported lost or stolen). The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        37
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction and requested to retain the customer’s payment card (card reported lost or stolen). The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        38
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction as the customer has entered the incorrect PIN three times. The customer’s bank (Card Issuer) has requested you to retain the payment card. The customer should contact the bank and use an alternative card.
      </td>
    </tr>

    <tr>
      <td>
        39
      </td>

      <td>
        The customer’s bank has declined the transaction as the payment card number used is not a credit account. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        40
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction as it does not allow this type of transaction. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        41
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction as the card has been reported lost. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        42
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction as the account type selected is not valid for this payment card number. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        43
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction as the card has been reported stolen. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        44
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction as the account type selected is not valid for this payment card number. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        46
      </td>

      <td>
        Closed account
      </td>
    </tr>

    <tr>
      <td>
        51
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction as the payment card does not have sufficient funds. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        52
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction as the payment card number is associated with a cheque account that does not exist. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        53
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction as the payment card number is associated with a savings account that does not exist. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        54
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction as the payment card appears to have expired. The customer should check the expiry date entered and try again, or use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        55
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction as the customer has entered an incorrect PIN. The customer should re-enter their PIN or use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        56
      </td>

      <td>
        The customer’s bank has declined the transaction as the payment card number does not exist. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        57
      </td>

      <td>
        The customer’s bank has declined the transaction as this payment card cannot be used for this type of transaction. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        58
      </td>

      <td>
        The customer’s bank has declined the transaction as this payment card cannot be used for this type of transaction. This may be associated with a test payment card number. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        59
      </td>

      <td>
        The customer’s bank has declined this transaction as the payment card appears to be fraudulent.
      </td>
    </tr>

    <tr>
      <td>
        60
      </td>

      <td>
        The customer’s bank (Card Issuer) has declined the transaction. The customer should contact their bank and retry the transaction.
      </td>
    </tr>

    <tr>
      <td>
        61
      </td>

      <td>
        The customer’s bank has declined the transaction as it will exceed the customer’s card limit. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        62
      </td>

      <td>
        The customer’s bank has declined the transaction as the payment card has some restrictions. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        63
      </td>

      <td>
        The customer’s bank has declined the transaction. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        64
      </td>

      <td>
        The customer’s bank has declined the transaction due to the amount attempting to be processed. The customer should check the transaction amount and try again.
      </td>
    </tr>

    <tr>
      <td>
        65
      </td>

      <td>
        Exceeds withdrawal frequency limit
      </td>
    </tr>

    <tr>
      <td>
        66
      </td>

      <td>
        The customer’s bank has declined the transaction and request you to contact the bank. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        67
      </td>

      <td>
        The customer’s bank has declined the transaction as the card is suspected to be counterfeit. The customer’s bank (Card Issuer) has requested that your customer’s payment card be retained. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        75
      </td>

      <td>
        The customer’s bank has declined the transaction as the customer has entered the incorrect PIN more than three times. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        82
      </td>

      <td>
        The customer’s bank has declined the transaction as the CVV is incorrect. The customer should check the CVV details and try again. If not successful, the customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        83
      </td>

      <td>
        Ensure card information is correct. Authentication may improve the likelihood of an approval. Retry using correct card information or authentication (such as EMV 3DS).
      </td>
    </tr>

    <tr>
      <td>
        90
      </td>

      <td>
        The customer’s bank is temporarily not able to process this customer’s payment card. The customer should attempt to process this transaction again.
      </td>
    </tr>

    <tr>
      <td>
        91
      </td>

      <td>
        The customer’s bank is unable to be contacted to authorize the transaction. The customer should attempt to process this transaction again.
      </td>
    </tr>

    <tr>
      <td>
        92
      </td>

      <td>
        The customer’s bank cannot be found for routing. This response code is often returned when the customer is using a test payment card number. The customer should attempt to process this transaction again.
      </td>
    </tr>

    <tr>
      <td>
        93
      </td>

      <td>
        The customer’s bank has declined the transaction and requested the customer to contact their bank. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        94
      </td>

      <td>
        The customer’s bank has declined the transaction as this transaction appears to be a duplicate transmission. No action required.
      </td>
    </tr>

    <tr>
      <td>
        96
      </td>

      <td>
        The customer’s bank was not able to process the transaction. The customer should attempt to process this transaction again.
      </td>
    </tr>

    <tr>
      <td>
        Z2
      </td>

      <td>
        Transaction has been reversed, hence cannot be reversed anymore.
      </td>
    </tr>

    <tr>
      <td>
        Z3
      </td>

      <td>
        The customer's bank has declined the capture transaction since the amount is greater than the authorized amount. The customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        BA
      </td>

      <td>
        Transaction failed. Customers should try using another card. The customer should contact their bank and should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        6P
      </td>

      <td>
        Account number did not pass a verification check
      </td>
    </tr>

    <tr>
      <td>
        AG
      </td>

      <td>
        Original Transaction Not Found (Only for Mandiri Issuing Card)
      </td>
    </tr>

    <tr>
      <td>
        AJ
      </td>

      <td>
        Posting is Already Completed (Only for Mandiri Issuing Card)
      </td>
    </tr>
  </tbody>
</Table>

<br />

**Additional Response Codes For VISA:**

<Table>
  <thead>
    <tr>
      <th>
        <b>
          Code
        </b>
      </th>

      <th>
        <b>
          Description
        </b>
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        8
      </td>

      <td>
        Transaction approved with ID
      </td>
    </tr>

    <tr>
      <td>
        68
      </td>

      <td>
        Time out
      </td>
    </tr>

    <tr>
      <td>
        71
      </td>

      <td>
        PIN Not Changed
      </td>
    </tr>

    <tr>
      <td>
        76
      </td>

      <td>
        Unable to locate previous message (no match on retrieval reference number)
      </td>
    </tr>

    <tr>
      <td>
        77
      </td>

      <td>
        Previous message located for a repeat or reversal, but repeat or reversal data inconsistent with original message
      </td>
    </tr>

    <tr>
      <td>
        78
      </td>

      <td>
        Blocked, first used — Transaction from new cardholder, and card not properly unblocked
      </td>
    </tr>

    <tr>
      <td>
        79
      </td>

      <td>
        Transaction reversed
      </td>
    </tr>

    <tr>
      <td>
        80
      </td>

      <td>
        Visa transactions: credit issuer unavailable. Private label: invalid date
      </td>
    </tr>

    <tr>
      <td>
        81
      </td>

      <td>
        PIN cryptographic error found (error found by VIC security module during PIN decryption)
      </td>
    </tr>

    <tr>
      <td>
        82
      </td>

      <td>
        Negative Online CAM, dCVV, iCVV, or CVV results Or Offline PIN authentication interrupted
      </td>
    </tr>

    <tr>
      <td>
        83
      </td>

      <td>
        STIP cannot approve
      </td>
    </tr>

    <tr>
      <td>
        84
      </td>

      <td>
        Pre-auth time too great
      </td>
    </tr>

    <tr>
      <td>
        85
      </td>

      <td>
        No reason to decline request for account number verification, address verification, CVV2 verification, or credit voucher or merchandise return
      </td>
    </tr>

    <tr>
      <td>
        86
      </td>

      <td>
        Cannot verify PIN
      </td>
    </tr>

    <tr>
      <td>
        87
      </td>

      <td>
        Purchase Amount Only, No Cash Back Allowed
      </td>
    </tr>

    <tr>
      <td>
        88
      </td>

      <td>
        Unable to authorize
      </td>
    </tr>

    <tr>
      <td>
        89
      </td>

      <td>
        Ineligible to receive
      </td>
    </tr>

    <tr>
      <td>
        91
      </td>

      <td>
        Issuer unavailable or switch inoperative (STIP not applicable or available for this transaction) Issuers can respond with this code, which V.I.P. passes to the acquirer without invoking stand-in processing (STIP). Issuer processors use the code to indicate they cannot perform authorization on issuers’ behalf. Code causes decline at POS.
      </td>
    </tr>

    <tr>
      <td>
        1A
      </td>

      <td>
        Additional customer authentication required
      </td>
    </tr>

    <tr>
      <td>
        B1
      </td>

      <td>
        B116 Surcharge amount not permitted on Visa cards
      </td>
    </tr>

    <tr>
      <td>
        B2
      </td>

      <td>
        Surcharge not supported
      </td>
    </tr>

    <tr>
      <td>
        N0
      </td>

      <td>
        Unable to authorize. Transaction failed. Customers should try using another card.
      </td>
    </tr>

    <tr>
      <td>
        N3
      </td>

      <td>
        Cash service not available
      </td>
    </tr>

    <tr>
      <td>
        N4
      </td>

      <td>
        Cashback request exceeds issuer limit
      </td>
    </tr>

    <tr>
      <td>
        N5
      </td>

      <td>
        Resubmitted transaction over max days limit
      </td>
    </tr>

    <tr>
      <td>
        N7
      </td>

      <td>
        Decline for CVV2 failure <br /> The customer’s bank has declined the transaction as the CVV is incorrect. The customer should check the CVV details and try again. If not successful, the customer should use an alternate payment card.
      </td>
    </tr>

    <tr>
      <td>
        N8
      </td>

      <td>
        Transaction amount exceeds pre-authorized approval amount
      </td>
    </tr>

    <tr>
      <td>
        P2
      </td>

      <td>
        P2 Invalid biller information
      </td>
    </tr>

    <tr>
      <td>
        P5
      </td>

      <td>
        PIN change/unblock request declined
      </td>
    </tr>

    <tr>
      <td>
        P6
      </td>

      <td>
        Unsafe PIN
      </td>
    </tr>

    <tr>
      <td>
        R0
      </td>

      <td>
        Stop payment order
      </td>
    </tr>

    <tr>
      <td>
        R1
      </td>

      <td>
        Revocation of authorization order
      </td>
    </tr>

    <tr>
      <td>
        R3
      </td>

      <td>
        Revocation of all authorizations order
      </td>
    </tr>

    <tr>
      <td>
        Z3
      </td>

      <td>
        Unable to go online; declined
      </td>
    </tr>

    <tr>
      <td>
        XA
      </td>

      <td>
        Forward to issuer
      </td>
    </tr>

    <tr>
      <td>
        XD
      </td>

      <td>
        Forward to issuer
      </td>
    </tr>

    <tr>
      <td>
        Q1
      </td>

      <td>
        Card authentication failed Or Offline PIN authentication interrupted
      </td>
    </tr>

    <tr>
      <td>
        Q5
      </td>

      <td>
        Transaction has been settled, hence cannot be settled anymore.
      </td>
    </tr>

    <tr>
      <td>
        T0
      </td>

      <td>
        Approval, keep first check
      </td>
    </tr>

    <tr>
      <td>
        T1
      </td>

      <td>
        Check OK, no conversion
      </td>
    </tr>

    <tr>
      <td>
        T2
      </td>

      <td>
        Invalid RTTN
      </td>
    </tr>

    <tr>
      <td>
        T3
      </td>

      <td>
        Amount greater than limit
      </td>
    </tr>

    <tr>
      <td>
        T4
      </td>

      <td>
        Unpaid items, failed NEG
      </td>
    </tr>

    <tr>
      <td>
        T5
      </td>

      <td>
        Duplicate check number
      </td>
    </tr>

    <tr>
      <td>
        T6
      </td>

      <td>
        MICR error
      </td>
    </tr>

    <tr>
      <td>
        T7
      </td>

      <td>
        Too many checks
      </td>
    </tr>

    <tr>
      <td>
        W1
      </td>

      <td>
        Declined - multiple exemptions selected
      </td>
    </tr>

    <tr>
      <td>
        W2
      </td>

      <td>
        Declined – selected exemption is invalid for the card brand of the transaction
      </td>
    </tr>

    <tr>
      <td>
        5C
      </td>

      <td>
        Transaction not supported/blocked by issuer
      </td>
    </tr>

    <tr>
      <td>
        9G
      </td>

      <td>
        Blocked by cardholder/contact cardholder
      </td>
    </tr>
  </tbody>
</Table>

<br />

**Additional Response Code From MASTERCARD Payment Network:**

<Table>
  <thead>
    <tr>
      <th>
        <b>
          Code
        </b>
      </th>

      <th>
        <b>
          Description
        </b>
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        70
      </td>

      <td>
        Contact Card Issuer
      </td>
    </tr>

    <tr>
      <td>
        71
      </td>

      <td>
        PIN Not Changed
      </td>
    </tr>

    <tr>
      <td>
        72
      </td>

      <td>
        Accounts Not Yet Activated
      </td>
    </tr>

    <tr>
      <td>
        76
      </td>

      <td>
        Invalid/nonexistent To Account specified
      </td>
    </tr>

    <tr>
      <td>
        77
      </td>

      <td>
        Invalid/nonexistent From Account specified
      </td>
    </tr>

    <tr>
      <td>
        78
      </td>

      <td>
        Invalid/nonexistent account specified (general)
      </td>
    </tr>

    <tr>
      <td>
        79
      </td>

      <td>
        Lifecycle Declines
      </td>
    </tr>

    <tr>
      <td>
        80
      </td>

      <td>
        System not available
      </td>
    </tr>

    <tr>
      <td>
        81
      </td>

      <td>
        Domestic Debit Transaction Not Allowed (Regional use only)
      </td>
    </tr>

    <tr>
      <td>
        82
      </td>

      <td>
        Policy Declines
      </td>
    </tr>

    <tr>
      <td>
        83
      </td>

      <td>
        Fraud/Security
      </td>
    </tr>

    <tr>
      <td>
        84
      </td>

      <td>
        Invalid Authorization Life Cycle
      </td>
    </tr>

    <tr>
      <td>
        85
      </td>

      <td>
        Not declined. Valid for all zero amount transactions.
      </td>
    </tr>

    <tr>
      <td>
        86
      </td>

      <td>
        PIN Validation not possible
      </td>
    </tr>

    <tr>
      <td>
        87
      </td>

      <td>
        Purchase Amount Only, No Cash Back Allowed
      </td>
    </tr>

    <tr>
      <td>
        88
      </td>

      <td>
        Cryptographic failure
      </td>
    </tr>

    <tr>
      <td>
        89
      </td>

      <td>
        Unacceptable PIN—Transaction Declined—Retry
      </td>
    </tr>
  </tbody>
</Table>

<br />

**Additional Response Code From AMEX (AMERICAN EXPRESS):**

<Table>
  <thead>
    <tr>
      <th>
        <b>
          Code
        </b>
      </th>

      <th>
        <b>
          Description
        </b>
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        000
      </td>

      <td>
        Approved <br /> Please be noted, 00 in Amex also mark as Approved (Refer to common response codes above)
      </td>
    </tr>

    <tr>
      <td>
        001
      </td>

      <td>
        Approved with ID
      </td>
    </tr>

    <tr>
      <td>
        002
      </td>

      <td>
        Partial Approval (Prepaid Cards only)
      </td>
    </tr>

    <tr>
      <td>
        100
      </td>

      <td>
        Deny
      </td>
    </tr>

    <tr>
      <td>
        101
      </td>

      <td>
        Expired Card / Invalid Expiration Date
      </td>
    </tr>

    <tr>
      <td>
        106
      </td>

      <td>
        Exceeded PIN attempts
      </td>
    </tr>

    <tr>
      <td>
        107
      </td>

      <td>
        Please Call Issuer
      </td>
    </tr>

    <tr>
      <td>
        109
      </td>

      <td>
        Invalid merchant
      </td>
    </tr>

    <tr>
      <td>
        110
      </td>

      <td>
        Invalid amount
      </td>
    </tr>

    <tr>
      <td>
        111
      </td>

      <td>
        Invalid account / Invalid MICR (Travelers Cheque)
      </td>
    </tr>

    <tr>
      <td>
        115
      </td>

      <td>
        Requested function not supported
      </td>
    </tr>

    <tr>
      <td>
        117
      </td>

      <td>
        Invalid PIN
      </td>
    </tr>

    <tr>
      <td>
        119
      </td>

      <td>
        Cardmember not enrolled / not permitted
      </td>
    </tr>

    <tr>
      <td>
        122
      </td>

      <td>
        Invalid card security code (a.k.a., CID, 4DBC, 4CSC)
      </td>
    </tr>

    <tr>
      <td>
        125
      </td>

      <td>
        Invalid effective date
      </td>
    </tr>

    <tr>
      <td>
        181
      </td>

      <td>
        Format error
      </td>
    </tr>

    <tr>
      <td>
        183
      </td>

      <td>
        Invalid currency code
      </td>
    </tr>

    <tr>
      <td>
        187
      </td>

      <td>
        Deny - New card issued
      </td>
    </tr>

    <tr>
      <td>
        189
      </td>

      <td>
        Deny - Canceled or Closed Merchant/SE
      </td>
    </tr>

    <tr>
      <td>
        200
      </td>

      <td>
        Deny - Pick up card
      </td>
    </tr>

    <tr>
      <td>
        900
      </td>

      <td>
        Accepted - ATC Synchronization
      </td>
    </tr>

    <tr>
      <td>
        909
      </td>

      <td>
        System Malfunction (Cryptographic error)
      </td>
    </tr>

    <tr>
      <td>
        912
      </td>

      <td>
        Issuer not available
      </td>
    </tr>
  </tbody>
</Table>

<br />

**Additional Response Codes From Midtrans:**

<Table>
  <thead>
    <tr>
      <th>
        <b>
          Code
        </b>
      </th>

      <th>
        <b>
          Description
        </b>
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        E9
      </td>

      <td>
        Generic Error if network response code is empty from bank or processor
      </td>
    </tr>

    <tr>
      <td>
        1
      </td>

      <td>
        Request-ID not present in request
      </td>
    </tr>

    <tr>
      <td>
        110
      </td>

      <td>
        Unauthorized
      </td>
    </tr>

    <tr>
      <td>
        112
      </td>

      <td>
        Wallet Blocked
      </td>
    </tr>

    <tr>
      <td>
        123
      </td>

      <td>
        KYC not approved
      </td>
    </tr>

    <tr>
      <td>
        132
      </td>

      <td>
        transaction in progress error
      </td>
    </tr>

    <tr>
      <td>
        153
      </td>

      <td>
        Invalid intent-token combination
      </td>
    </tr>

    <tr>
      <td>
        156
      </td>

      <td>
        Payment method currently disabled
      </td>
    </tr>

    <tr>
      <td>
        158
      </td>

      <td>
        invalid transaction type; should be either of REFUND or REVERT
      </td>
    </tr>

    <tr>
      <td>
        159
      </td>

      <td>
        Payment option token passed is invalid
      </td>
    </tr>

    <tr>
      <td>
        161
      </td>

      <td>
        unsupported service country
      </td>
    </tr>

    <tr>
      <td>
        164
      </td>

      <td>
        validate credit not supported (unsupported payment option & service country combination)
      </td>
    </tr>

    <tr>
      <td>
        201
      </td>

      <td>
        Not Enough Balance
      </td>
    </tr>

    <tr>
      <td>
        202
      </td>

      <td>
        Excessive Balance
      </td>
    </tr>

    <tr>
      <td>
        213
      </td>

      <td>
        Monthly wallet balance limit exceeded
      </td>
    </tr>

    <tr>
      <td>
        220
      </td>

      <td>
        Currency mismatch. Example: Attempt to perform a transaction using SGD on ID wallet
      </td>
    </tr>

    <tr>
      <td>
        303
      </td>

      <td>
        Field cannot be blank
      </td>
    </tr>

    <tr>
      <td>
        803
      </td>

      <td>
        Card used as payment method could not be found
      </td>
    </tr>

    <tr>
      <td>
        811
      </td>

      <td>
        Reservation failed due to low balance
      </td>
    </tr>

    <tr>
      <td>
        817
      </td>

      <td>
        Payment rejected by the backend
      </td>
    </tr>

    <tr>
      <td>
        831
      </td>

      <td>
        Card used as payment method has expired
      </td>
    </tr>

    <tr>
      <td>
        900
      </td>

      <td>
        Generic Service Error
      </td>
    </tr>

    <tr>
      <td>
        903
      </td>

      <td>
        Forbidden Operation
      </td>
    </tr>

    <tr>
      <td>
        1804
      </td>

      <td>
        Order already queued or fulfilled
      </td>
    </tr>

    <tr>
      <td>
        1818
      </td>

      <td>
        Order already canceled
      </td>
    </tr>

    <tr>
      <td>
        1823
      </td>

      <td>
        Order expired
      </td>
    </tr>

    <tr>
      <td>
        2101
      </td>

      <td>
        Invalid amount
      </td>
    </tr>

    <tr>
      <td>
        2700
      </td>

      <td>
        Unsupported country
      </td>
    </tr>

    <tr>
      <td>
        2701
      </td>

      <td>
        Country and currency combinations do not match
      </td>
    </tr>

    <tr>
      <td>
        2903
      </td>

      <td>
        Invalid request error
      </td>
    </tr>

    <tr>
      <td>
        3007
      </td>

      <td>
        Order not found
      </td>
    </tr>

    <tr>
      <td>
        3066
      </td>

      <td>
        Order not in CREATED state
      </td>
    </tr>

    <tr>
      <td>
        3067
      </td>

      <td>
        Order not in cancellable state
      </td>
    </tr>

    <tr>
      <td>
        3073
      </td>

      <td>
        Order Already In terminal status
      </td>
    </tr>

    <tr>
      <td>
        3076
      </td>

      <td>
        Max permissible refund instructions exceeded error
      </td>
    </tr>

    <tr>
      <td>
        3077
      </td>

      <td>
        Max permissible payment instructions exceeded
      </td>
    </tr>

    <tr>
      <td>
        4060
      </td>

      <td>
        Order rejected by Fraud Rules Service
      </td>
    </tr>

    <tr>
      <td>
        6302
      </td>

      <td>
        Payer blocked due to OFAC match rule
      </td>
    </tr>

    <tr>
      <td>
        6303
      </td>

      <td>
        Payee blocked due to OFAC match rule
      </td>
    </tr>

    <tr>
      <td>
        11009
      </td>

      <td>
        Payment Provider Challenged Auth
      </td>
    </tr>

    <tr>
      <td>
        11010
      </td>

      <td>
        Payment Provider Challenge Failed
      </td>
    </tr>

    <tr>
      <td>
        11017
      </td>

      <td>
        Merchant blocked from using payment method
      </td>
    </tr>
  </tbody>
</Table>