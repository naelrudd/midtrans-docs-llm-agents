---
updatedAt: 2025-11-11T00:33:07.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Transaction Status

The table given below describes the `transaction_status` used by Midtrans APIs.

<HTMLBlock>{`
<table>
  <tr>
    <th style="width:150px"><b>Status</b></th>
  <th style="width:150px"><b>Description<b></th>
  <th style="width:120px"><b>Possible change(s)<b></th>
  </tr>
  <tr>
  <td><code>authorize</code></td>
  <td>Midtrans authorizes the payment card used for the transaction. Must be captured to process the balance. </br><b>Note</b>: This is valid for payment card only.</td>
  <td><code>capture</code>,</br> <code>cancel</code></td>
  </tr>
  <tr>
  <td><code>capture</code></td>
 <td>The transaction is successful and the card balance is captured successfully. If no action is taken by you, the transaction will be successfully settled within 24 hours or within the agreed settlement time with your partner bank. The transaction status is <code>settlement</code>. It is safe to assume a successful payment.</td>
  <td><code>settlement</code>,</br> <code>cancel</code></td>
  </tr>
  <tr>
  <td><code>settlement</code></td>
  <td>The transaction is successfully settled. Funds have been credited to your account.</td>
  <td><code>refund</code>,</br> <code>chargeback</code>,</br> <code>partial_refund</code>,</br> <code>partial_chargeback</code></td>
  </tr>
  <tr>
  <td><code>deny</code></td>
  <td>The credentials used for payment are rejected by the payment provider or Midtrans Fraud Detection System (FDS). To know the reason and details for the denied transaction, see the <code>status_message</code> in the response.</td>
  <td>N/A</td>
  </tr>
  <tr>
  <td><code>pending</code></td>
  <td>The transaction is created and is waiting to be paid by the customer at the payment providers like direct debit, Bank Transfer, E-wallet, and so on.</td>
  <td><code>settlement</code>,</br> <code>deny</code>,</br> <code>cancel</code>,</br> <code>expire</code></td>
  </tr>
  <tr>
  <td><code>cancel</code></td>
  <td>The transaction is cancelled. This can be triggered by Midtrans or the partner bank. Note: For card payments, cancel status is triggered by Midtrans in case of Pre-Authorization transaction when an Authorized transaction exceeded the capture time limit</td>
  <td>N/A</td>
  </tr>
  <tr>
  <td><code>refund</code></td>
  <td>The transaction is marked to be refunded. Refund status is triggered by you.</td>
  <td><code>N/A</code></td>
  </tr>
  <tr>
  <td><code>partial_refund</code></td>
  <td>The transaction is marked to be partially refunded.</td>
  <td><code>refund</code></td>
  </tr>
  <tr>
  <td><code>chargeback</code></td>
  <td>The transaction is marked to be charged back. </br><b>Note</b>: Applicable for payment card only.</td>
  <td><code>N/A</code></td>
  </tr>
  <tr>
  <td><code>partial_chargeback</code></td>
  <td>The transaction is marked to be partially charged back.</td>
  <td><code>chargeback</code></td>
  </tr>
  <tr>
  <td><code>expire</code></td>
  <td>The transaction is not available for processing, because the payment was delayed.</td>
  <td>N/A</td>
  </tr>
  <tr>
  <td><code>failure</code></td>
  <td>Unexpected error occurred during transaction processing.</td>
  <td>N/A</td>
  </tr>
  </table>
`}</HTMLBlock>