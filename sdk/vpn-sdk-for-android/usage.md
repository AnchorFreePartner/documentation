# Usage

## Usage

### Set Up

To set up sdk, you should call **getInstance** method with your specific details

```text
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

### Defer VPN service initialisation

Add boolean resource to disable vpn service

```text
<bool name="vpn_process_enabled">false</bool>
```

To enable service later:

```text
PackageManager pm = context.getPackageManager();
pm.setComponentEnabledSetting(new ComponentName(context, AFVpnService.class), PackageManager.COMPONENT_ENABLED_STATE_ENABLED, PackageManager.DONT_KILL_APP);
```

### Authentication

Aura Partner VPN Backend supports OAuth authentication with a partner's OAuth server, this is a primary authentication method.

Steps to implement OAuth:

* Deploy and configure OAuth service. Service should be publicly available on the Internet.
* Configure Partner Backend to use OAuth service.
* Implement client OAuth for your application
* Retrieve access token in client app, this token will be used to initialize and sign in to Android Partner

There are some auth method types:

```text
AuthMethod.anonymous();
AuthMethod.firebase(token); // should be configured when creating an app
AuthMethod.customOauth(token); // specific OAuth type, should be configured when creating an app
```

Login implementation example:

```text
AuthMethod authMethod = AuthMethod.firebase(token);
sdk.getBackend().login(authMethod, new Callback<User>() {
   @Override
   public void success(User response) {
       
   }
   @Override
   public void failure(VpnException error) {
       
   }
});
```

### List available countries

```text
sdk.getBackend().countries(new Callback<AvailableCountries>() {
    @Override
    public void success(AvailableCountries response) {
        
    }

    @Override
    public void failure(HydraException error) {
        
    }
});
```

### Configure VPN session

For vpn session configuration use class `SessionConfig`

Available `Builder` methods

* `withTransport` - set transport name to start session with. Can be used in case multiple transports available
* `withPolicy` - define app policy to use.
  * `AppPolicy.forAll` - vpn will be available for all apps
  * `AppPolicy.Builder.policy` with `AppPolicy.POLICY_FOR_LIST` - apps list allowed to use vpn
  * `AppPolicy.Builder.policy` with `AppPolicy.POLICY_EXCEPT_LIST` - apps list not allowed to use vpn
* `withReason` - define reason for starting session `com.anchorfree.reporting.TrackingConstants.GprReasons`. Will be used in analytics
* `withVirtualLocation` - define virtual location for session \(country\)
* `withPrivateGroup` - define private server for session
* `withVpnParams` - define vpn tunnel params. Like dns servers, additional routes.
* `addDnsRule` - add dns rule for session. More on [Traffic rules](traffic-rules.md) page. _For Hydra transport only._ 
* `addProxyRule` - add proxy rule for session. More on [Traffic rules](traffic-rules.md) page. _For Hydra transport only._
* `withFireshieldConfig` - define categorisation service rules \(more on [Fireshield](fireshield-hydra-transport.md) resource page\). _For Hydra transport only_
* `withTransportFallback` - define the order of transports to fallback when some error happen. 
* `keepVpnOnReconnect` - enables the kill switch - no traffic will be allowed while sdk is in connection process or handling the connection error.

Examples:

#### Start VPN with an optimal server

```text
final SessionConfig session = new SessionConfig.Builder()
                .withVirtualLocation(UnifiedSDK.COUNTRY_OPTIMAL)
                .withReason(TrackingConstants.GprReasons.M_UI)
                .build();
```

#### Start VPN for chrome only

```text
final List<String> apps = new ArrayList<String();
apps.add("com.google.chrome");
final SessionConfig session = new SessionConfig.Builder()
                .withVirtualLocation(UnifiedSDK.COUNTRY_OPTIMAL)
                .withReason(TrackingConstants.GprReasons.M_UI)
                .appPolicy(AppPolicy.newBuilder().policy(AppPolity.POLICY_FOR_LIST).appList(apps).build())
                .build(); 
```

#### Analytics reasons

* `M_UI` - manually from ui
* `M_SYSTEM` - manually from system
* `M_OTHER` - manually from another place
* `A_APP_RUN` - auto on app run
* `A_RECONNECT` - auto on reconnect
* `A_ERROR` - auto after error
* `A_SLEEP` - auto after sleep
* `A_NETWORK` - auto on network event
* `A_OTHER` - auto on other reason

### Start VPN session

```text
final SessionConfig session = //create session config
sdk.getVPN().start(session, new CompletableCallback() {
    @Override
    public void complete() {
        
    }

    @Override
    public void error(@NonNull VpnException e) {

    }
});
```

### Stop vpn

```text
sdk.getVPN().stop(TrackingConstants.GprReasons.M_UI, new CompletableCallback() {
    @Override
    public void complete() {
        //VPN was stopped
    }

    @Override
    public void error(@NonNull VpnException e) {
        //Failed to stop vpn
    }
});
```

### Restart vpn

Will restart vpn session with new config without IDLE state

```text
final SessionConfig session = //create session config
sdk.getVPN().restart(session, new CompletableCallback() {
    @Override
    public void complete() {
        
    }

    @Override
    public void error(@NonNull VpnException e) {

    }
});
```

### Update session config

Can update some vpn session configs without restarting vpn session. Can be used to update Fireshield rules

```text
final SessionConfig session = //create session config
sdk.getVPN().updateConfig(session, new CompletableCallback() {
    @Override
    public void complete() {
        
    }

    @Override
    public void error(@NonNull VpnException e) {

    }
});
```

### Listen for vpn status and traffic updates

```text
UnifiedSDK.addVpnStateListener(new VpnStateListener() {
    @Override
    public void vpnStateChanged(@NonNull VPNState vpnState) {
        
    }

    @Override
    public void vpnError(@NonNull VpnException e) {

    }
});

UnifiedSDK.addTrafficListener(new TrafficListener() {
    @Override
    public void onTrafficUpdate(long rx, long tx) {
        
    }
});

//stop listening for update
UnifiedSDK.removeTrafficListener(...);
UnifiedSDK.removeVpnStateListener(...);
```

### Purchases functionality

```text
sdk.getBackend().purchase("json from google", new CompletableCallback() {
   @Override
   public void complete() {
       //purchase request success
   }

   @Override
   public void error(VpnException e) {
        //failed to process purchase
   }
});
sdk.getBackend().deletePurchase(purchaseID, new CompletableCallback() {
   @Override
   public void complete() {
       //request success
   }

   @Override
   public void error(VpnException e) {
        //failed to process request
   }
});
```

### Get data about user

```text
//get information about remaining traffic for user
sdk.getBackend().remainingTraffic(new Callback<RemainingTraffic>() {
    @Override
    public void success(@NonNull RemainingTraffic remainingTraffic) {
        
    }

    @Override
    public void failure(@NonNull VpnException e) {

    }
});
//get information about current logged in user
sdk.getBackend().currentUser(new Callback<User>() {
    @Override
    public void success(@NonNull User user) {
        
    }

    @Override
    public void failure(@NonNull VpnException e) {

    }
});
```

### Get Current vpn state

```text
UnifiedSDK.getVpnState(new Callback<VPNState>() {
    @Override
    public void success(@NonNull VPNState vpnState) {
        
    }

    @Override
    public void failure(@NonNull VpnException e) {

    }
});
```

### Call VPN permission dialog without connecting to vpn

```text
VpnPermissions.request(new CompletableCallback() {
    @Override
    public void complete() {
        //permission was granted
    }

    @Override
    public void error(@NonNull VpnException e) {

    }
});
```

## 

