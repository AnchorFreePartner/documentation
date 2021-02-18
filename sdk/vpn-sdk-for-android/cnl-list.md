# CNL List

## Client network list \(aka CNL\)

Unified SDK provides ability to automatically start/stop vpn sessions when a user changes networks. List of network conditions is configured in the dashboard. Open `https://developer.anchorfree.com/`, under your project, select **Settings**-&gt;**Client Networks**. Configure list of network conditions \(ssid, bssid, authorization, type\) and actions \(start/stop\).

After the first start of vpn connection sdk will download configuration from server. When user is not running an active vpn session, sdk will show a notification configured by CNL state of `NotificationConfigBuilder`

```text
NotificationConfig.Builder builder = NotificationConfig.newBuilder();
builder.inCnl("Title","Message");
```

If no notification title/message configured, it will use a default one:

* `title` - CNL
* `message` - Waiting

Rules' matching:

When a device changes network connection, SDK will look through configured networks in CNL list and match current configuration with server

If network type is set to WiFi:

* If ssid and bsid are empty - it will match any Wifi network
* If authentication is `Does not matter` - it will match open and protected networks
* If you want to match network by SSID and/or BSSID on android 8.1+ \(API 27\), you need to set up and request runtime permission for the location.
* If you want to match network by SSID and/or BSSID on android 10+ \(API 29\), you need to set up and request runtime permission for the location.

In case of missing permission, SDK will not be able to get network SSID and BSSID.

When a user changes network while a vpn session is up and running, and a new network was matched with CNL rules with **Disabled** action, SDK will not reconnect to this network and throw `CnlBlockedException` in `VpnStateListener#vpnError` callback.

