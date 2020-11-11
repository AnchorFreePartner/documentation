# Reconnection strategy

## SDK reconnection logic on network switch

By default sdk will automatically handle network reconnection when user switches between network.

If VPN is ON and user disable network connection SDK gets to **PAUSED** state. After network connection is enabled, sdk automatically connects with last successful config.

The same behaviour happen in case of transport error during the connection. Except of unrecoverable exceptions:

* `CODE_NOT_AUTHORIZED` - user is not authorized. Need to call HydraSdk.login
* `CODE_SESSIONS_EXCEED` - Session limit is achieved in accordance with the ToS
* `CODE_DEVICES_EXCEED` - Devices limit is achieved in accordance with the ToS
* `CODE_OAUTH_ERROR` - Returns in all cases when an authentication error occurred through OAuth-server
* `CODE_TRAFFIC_EXCEED` - Ended limitation traffic activated in accordance with the terms of the license
* `USER_SUSPENDED` - User Suspended

To control this behaviour use

```text
 UnifiedSDK.setReconnectionEnabled(false);
```

## 

