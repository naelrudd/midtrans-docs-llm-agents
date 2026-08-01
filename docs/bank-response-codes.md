---
updatedAt: 2025-11-11T00:13:34.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Bank Response Codes

### Denied by Bank - Response Codes

When a charge request for Credit Card is received, there are layers of security that it has to go through. The last one would be the Bank’s automated authorization system. The bank’s authorization system take various factors into account, such as spending habits, account balance, card information, etc.

In cases where your customers’ transactions are declined by the banks, Midtrans shares as much information as what we receive from the bank, **through HTTP notification and within the[dashboard ↗](https://account.midtrans.com/login) (Merchant Administration Portal)**. Information through API is in the form of codes, while information on dashboard is in the form of words (more user friendly).

While in some cases the banks may provide helpful explanation such as “insufficient funds”, “invalid card number”, “expired cards”, unfortunately some other explanation such as “do not honour” are rather generic where it is less likely to know the exact reason for decline of payment. Please see the meaning of "do not honour" [here ↗](https://support.midtrans.com/hc/en-us/articles/360000158033-What-does-Do-Not-Honour-05-mean-).

After logging into the dashboard, go to “transactions” menu and click on the denied transaction that you would like to find out more about and you will be redirected to the page below. Click on the "i" icon to see the “Invalid Card Number (14)” information.

![](https://files.readme.io/9fd2497-image.png)

Here is the an example of how the charge response API sent by Midtrans. Please refer to the “**status\_message**” field below.

```
{  
 "transaction_time": "2019-09-09 05:07:19",  
 "transaction_status": "deny",  
 "transaction_id": "bf9k2ba0-7hb9-88ah-o778-b1124376b3bd",  
 "status_message": "midtrans payment notification",  
 "status_code": "202",  
 "signature_key": "uu819dnk8jk880qerwlkai909018371jjhdo0129ddj89hj119fhk09134hj777jk36hy7ji89017fh77nvb123h3ef81uh73e40i8u3vhs8h1327hhhdfer89nccs9o",  
 "promo_details": {  
 "original_amount": "500007.00",  
 "code": "TEST_PROMO_UNLIMITED"  
 },  
 "payment_type": "credit_card",  
 "order_id": "ABC-889",  
 "metadata": {  
 "merchant_phone_number": "08129228011",  
 "merchant_partner_name": "ID_144",  
 "merchant_emails": [  
 "outdoor@mail.com",  
 "other@mail.com"  
 ],  
 "merchant_address": "Jl Jend Sudirman Kav 10-11 Jakarta Pusat 10220, DKI Jakarta, indonesia"  
 },  
 "masked_card": "459920-2414",  
 "gross_amount": "17000.00",  
 "fraud_status": "accept",  
 "eci": "01",  
 "custom_field3": "custom field 3 content",  
 "custom_field2": "custom field 2 content",  
 "custom_field1": "custom field 1 content",  
 "currency": "IDR",  
 "channel_response_message": "Do not honour",  
 "channel_response_code": "05",  
 "card_type": "credit",  
 "bank": "mandiri",  
 "approval_code": " "  
}
```

In this example, we can see that the denied by bank code is 05.\
You may refer to the list of [codes here ↗](https://api-docs.midtrans.com/#channel-response-code.) for more explanation for meaning of each codes.