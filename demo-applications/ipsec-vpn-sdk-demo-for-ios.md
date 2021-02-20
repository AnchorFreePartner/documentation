---
description: >-
  This is a demo application for iOS with basic usage of CakeTube (IPSEC) VPN
  SDK.
---

# IPSEC VPN SDK demo for iOS

[GitHub project link](https://github.com/AnchorFreePartner/caketubesdk-demo-ios)

## Compatibility

* iOS 9 or newer

## SDK Quick Installation Guide

Download latest SDK: [CakeTubeSDK for iOS](https://firebasestorage.googleapis.com/v0/b/web-portal-for-partners.appspot.com/o/products%2FCakeTubeSDK%20iOS.zip?alt=media)

### Install CakeTube SDK

In your project

* Add **CakeTubeSDK.framework** for **Application** target

In your project: _Project &gt; Build Settings_:

* Set _Other Linker Flags_ to `-ObjC`.

Make sure Personal VPN entitlement is enabled for your application.

In your AppDelegate object initialize SDK:

```text
// AppDelegate.swift or any other class to initialize SDK

CakeTube.instance().configure(CTConfig.create { (c) in
    c.baseUrl = "BASE_URL"
    c.carrierId = "CARRIER_ID"
    c.vpnProfileName = "YOUR_APP_NAME" // will be shown in System Settings -> VPN
})
```

Make sure if you are logged in before connecting VPN, if not – sign in with any available method.

```text
CakeTube.instance().login(with: CTAuthMethod.anonymous(), completion: { (user, e) in
	// Do stuff
})
```

After you're logged in, you're good to go start VPN:

```text
CakeTube.instance().startVPN { (location, e) in
	// VPN is being started to server in country that is provided by `location` class
	// Rely on notification center status notifications for exact VPN state
}
```

Handle VPN state notifications:

```text
NotificationCenter.default.addObserver(forName: NSNotification.Name.CTVPNStatusDidChange, object: nil, queue: OperationQueue.main) { [unowned self] (notifictaion) in
    if CakeTube.instance().vpnStatus == .connected {
    	// Do stuff
    }
}
```

If you have to choose VPN server country before connecting, you can call `availableServers` and then `startVpn` with specific country.

```text
// Get a list of countries 
CakeTube.instance().availableServers { [weak self] (locations, e) in
	// Do stuff
	let someLocation = locations[0]
	CakeTube.instance().setServer(someLocation)
	// Next startVPN will use this location to connect 
}
```

For more detailed information refer to [CakeTube SDK documentation](https://pango.gitbook.io/pango-platform/sdk/ipsec-vpn-sdk-for-ios-macos)

