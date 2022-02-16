# Vpn interface

For vpn session configuration use class `SessionConfig`

Available `Builder` methods

* `withTransport` - set transport name to start session with. Can be used in case multiple transports available
* `withPolicy` - define app policy to use.
  * `AppPolicy.forAll` - vpn will be available for all apps
  * `AppPolicy.Builder.policy` with `AppPolicy.POLICY_FOR_LIST` - apps list allowed to use vpn
  * `AppPolicy.Builder.policy` with `AppPolicy.POLICY_EXCEPT_LIST` - apps list not allowed to use vpn
* `withReason` - define reason for starting session `unified.vpn.sdk.TrackingConstants.GprReasons`. Will be used in analytics
* `withLocation` - define virtual location for session
* `withCountry` - define virtual country for session
* `withPrivateGroup` - define private server for session
* `withVpnParams` - define vpn tunnel params. Like dns servers, additional routes.
* `addDnsRule` - add dns rule for session. More on [Traffic rules](../traffic-rules.md) page. _For Hydra transport only._&#x20;
* `addProxyRule` - add proxy rule for session. More on [Traffic rules](../traffic-rules.md) page. _For Hydra transport only._
* `withFireshieldConfig` - define categorisation service rules (more on [Fireshield](../fireshield-hydra-transport.md) resource page). _For Hydra transport only_
* `withTransportFallback` - define the order of transports to fallback when some error happen.&#x20;
* `keepVpnOnReconnect` - enables the kill switch - no traffic will be allowed while sdk is in connection process or handling the connection error.

Examples:

#### Start VPN with an optimal server

```
final SessionConfig session = new SessionConfig.Builder()
                .withLocation(UnifiedSDK.COUNTRY_OPTIMAL)
                .withReason(TrackingConstants.GprReasons.M_UI)
                .build();
```

#### Start VPN for chrome only

```
final List<String> apps = new ArrayList<String();
apps.add("com.google.chrome");
final SessionConfig session = new SessionConfig.Builder()
                .withLocation(UnifiedSDK.COUNTRY_OPTIMAL)
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

```
final SessionConfig session = //create session config
sdk.getVpn().start(session, new CompletableCallback() {
    @Override
    public void complete() {
        
    }

    @Override
    public void error(@NonNull VpnException e) {

    }
});
```

### Stop vpn

```
sdk.getVpn().stop(TrackingConstants.GprReasons.M_UI, new CompletableCallback() {
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

```
final SessionConfig session = //create session config
sdk.getVpn().restart(session, new CompletableCallback() {
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

```
final SessionConfig session = //create session config
sdk.getVpn().updateConfig(session, new CompletableCallback() {
    @Override
    public void complete() {
        
    }

    @Override
    public void error(@NonNull VpnException e) {

    }
});
```

### Listen for vpn status and traffic updates

```
UnifiedSDK.addVpnStateListener(new VpnStateListener() {
    @Override
    public void vpnStateChanged(@NonNull VpnState vpnState) {
        
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

### Get Current vpn state

```
UnifiedSDK.getVpnState(new Callback<VpnState>() {
    @Override
    public void success(@NonNull VpnState vpnState) {
        
    }

    @Override
    public void failure(@NonNull VpnException e) {

    }
});
```

### Call VPN permission dialog without connecting to vpn

```
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
