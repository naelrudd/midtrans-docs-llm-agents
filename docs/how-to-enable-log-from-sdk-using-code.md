---
updatedAt: 2025-11-11T00:13:10.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# How to enable log from SDK using code ?

There is an initiation method that need to be execute.\
Please follow below code to make it happen.

Here is what look like in code :

```
SdkUIFlowBuilder.init(CONTEXT, BuildConfig.CLIENT_KEY, BuildConfig.BASE_URL, new TransactionFinishedCallback()  
{  
@Override  
public void onTransactionFinished(TransactionResult result) {  
// Handle finished transaction here.  
}  
})  
.enableLog(true)  
.buildSDK();
```

> 🚧 NOTE💡
>
> This can be used only if you integrate with Android.