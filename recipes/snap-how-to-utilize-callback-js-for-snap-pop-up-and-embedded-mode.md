---
updatedAt: 2025-11-11T00:24:06.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# [SNAP] How to utilize callback js for Snap Pop Up and Embedded mode

```javascript JavaScript
window.snap.pay('TRANSACTION_TOKEN_HERE', {
  onSuccess: function(result){
    /* You may add your own implementation here */
    alert("payment success!"); console.log(result);
  },
  onPending: function(result){
    /* You may add your own implementation here */
    alert("wating your payment!"); console.log(result);
  },
  onError: function(result){
    /* You may add your own implementation here */
    alert("payment failed!"); console.log(result);
  },
  onClose: function(){
    /* You may add your own implementation here */
    alert('you closed the popup without finishing the payment');
  }
})
```

# Open payment page

<!-- javascript@1 -->

This recipe will use a sample implementation of Snap Pop Up mode - see recipe [here](/recipes/snap-how-to-open-snap-through-pop-up). 

For Snap Embedded, refer to how to embed Snap UI modal within your app/page via this recipe [here](/recipes/snap-how-to-embed-snap-ui), then implement the steps below to implement callback functions within `window.snap.embedded` instead.

---

`window.snap.pay('SNAP_TRANSACTION_TOKEN', options)` will open the payment page for that specific Snap Token you retrieved [here](/docs/snap-snap-integration-guide#successful-sample-response), which is tied to specific Order ID.

# Callback support

<!-- javascript@2-17 -->

Snap.js supports callbacks. It can be used to trigger your custom JavaScript implementation on each event.

# Success callback

<!-- javascript@2-5 -->

`onSuccess` is a function that will be triggered when payment is successful.

For success callback's result JSON properties, refer to [this docs](/reference/snap-js)

# Pending callback

<!-- javascript@6-9 -->

`onPending` is a function that will be triggered when payment's status in Midtrans is pending, which is applicable for payment that requires further customer action, such as bank transfer or over the counter payments.

For pending callback's result JSON properties, refer to [this docs](/reference/snap-js)

# Error callback

<!-- javascript@10-13 -->

`onError` is a function that will be triggered when there is a payment failure after several attempts.

For error callback's result JSON properties, refer to [this docs](/reference/snap-js)

# Close callback

<!-- javascript@14-17 -->

`onClose` is a function that will be triggered when customer has closed the Snap popup.