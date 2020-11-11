# CNL List

## Client network list \(aka CNL\)

Unified SDK provides ability to automatically start/stop vpn session when user changes network. List of network conditions are configured on dashboard. Open `https://developer.anchorfree.com/`, under your project select **Settings**-&gt;**Client Networks** Configure list of network conditions\(ssid, bssid, authorization, type\) and actions\(start/stop\).

After vpn connection first start sdk will download configuration from server. When user is not running active vpn session, sdk will show notification configured by CNL state of `NotificationConfigBuilder`

```text
NotificationConfig.Builder builder = NotificationConfig.newBuilder();
builder.inCnl("Title","Message");
```

If no notification title/message configured it will use defauult one:

* `title` - CNL
* `message` - Waiting

Rules matching:

When device changes network connection SDK will look through configured networks in CNL list and match current configuration with server

If network type is set to WiFi:

* if ssid and bsid are empty - it will match any Wifi network
* if authentication is `Does not matter` - it will match open and protected networks
* If you want to match network by SSID and/or BSSID on android 8.1+ \(API 27\) you need to setup and request runtime permission for use location.
* If you want to match network by SSID and/or BSSID on android 10+ \(API 29\) you need to setup and request runtime permission for use location.

In case of missing permission, SDK will not be able to get network SSID and BSSID.

When user changes network when has vpn session up and running, and new network was matched with CNL rules with action **Disabled**, sdk will not reconnect to this network and throw `CnlBlockedException` in `VpnStateListener#vpnError` callback.

