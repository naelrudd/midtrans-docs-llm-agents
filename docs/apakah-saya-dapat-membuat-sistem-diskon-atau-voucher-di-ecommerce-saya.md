---
updatedAt: 2025-11-11T00:18:43.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Apakah saya dapat membuat sistem diskon atau voucher di eCommerce saya?

Iya. Anda dapat membuat sistem diskon atau voucher dengan menggunakan parameter ‘item’.

Berikut adalah contoh:

*\[Item\_name]/ item = 100,000\
Voucher / item = -50,000\
Gross amount= 50,000*

**Berikut adalah tampilan dalam bentuk code :**

```
...............................

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

$item3_details = array(  
    'id' => 'a3',  
    'price' => -50000,  
    'quantity' => 1,  
    'name' => "Voucher"  
   );

$item_details = array ($item1_details, $item2_details, $item3_details);

................................

```