---
updatedAt: 2025-11-11T00:12:38.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Can we implement discount or voucher?

Yes. We recommend you use the ‘item’ parameter for discounts or vouchers when sending payment requests to us.

Here below is a simple example:

\[Item name] / item = 100.000\
Voucher / Item = -50.000\
Gross Amount = 50.000

**Here is what looks like in the code :**

```
$item1_details = array(  
    'id' => 'a1',  
    'price' => 25000,  
    'quantity' => 2,  
    'name' => "Apple"  
    );

$item2_details = array(  
    'id' => 'a2',  
    'price' => 50000,  
    'quantity' => 1,  
    'name' => "Orange"  
   );

**$item3_details = array(  
    'id' => 'a3',  
    'price' => -50000,  
    'quantity' => 1,  
    'name' => "Voucher"  
   );**

$item_details = array ($item1_details, $item2_details, **$item3_details**);
```