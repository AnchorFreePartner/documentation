# Set Up

To set up sdk, you should call **getInstance** method with your specific details

```
public class MyApplication extends Application {
   @Override
   public void onCreate() {
       super.onCreate();
       final ClientInfo info = ClientInfo.newBuilder()
                     .baseUrl("http://yourvpnbackend.com") // set base url for api calls
                     .carrierId("carrier id") // set your carrier id
                     .build();
       final UnifiedSDK sdk = UnifiedSDK.getInstance(info);
   }
}
```

###
