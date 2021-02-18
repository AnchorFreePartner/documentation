# Reconnection strategy

## SDK reconnection logic on network switch

By default, SDK will automatically handle network reconnection when user switches between networks.

If VPN is ON and user disables network connection, SDK transfers to the **PAUSED** state. After network connection is enabled, SDK automatically connects to the last successful config.

The same behaviour happens in case of a transport error during connection. The exceptions are as follows:

* `CODE_NOT_AUTHORIZED` - user is not authorized. Need to call HydraSdk.login
* `CODE_SESSIONS_EXCEED` - session limit is reached in accordance with the ToS
* `CODE_DEVICES_EXCEED` - devices limit is reached in accordance with the ToS
* `CODE_OAUTH_ERROR` - returns in all cases when an authentication error occurred on OAuth-server
* `CODE_TRAFFIC_EXCEED` - exceeded the traffic limit in accordance with the ToS
* `USER_SUSPENDED` - user suspended

To control this behaviour, use:

```text
 UnifiedSDK.setReconnectionEnabled(false);
```

## 

