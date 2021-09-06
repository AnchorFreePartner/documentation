# Changelog

### 3.4.17

* fix for reconnection with kill switch enabled

### 3.4.16

* Fix for cash on &gt; 100 calls to registerNetworkCallback

### 3.4.15

* Fix for encryption Initialization race condition
* Fix stuck on connecting after app update

### 3.4.13

* custom external logger

### 3.4.12

* various bug fixes 
* memory usage improvements

### 3.4.11

* Compatibility with Android S preview

### 3.4.10

* Android 11 timeout fix

### 3.4.9

* various bug fixes 

### 3.4.6 - 3.4.8

* analytics improvements

### 3.4.5

* reconnection loop fix

### 3.4.4

* analytics fix

### 3.4.3

* Remaining traffic fix

### 3.4.1 - 3.4.2

* internal improvements

### 3.4.0

* Hydra transport updated
* Various bug fixes 
* Added
  * TrafficRule\#blockDns
  * TrafficRule\#blockPkt
  * TrafficRule\#udp
  * TrafficRule\#tcp 
* Deprecated
  * TrafficRule\#block 

### 3.3.3

* analytics improvements

### 3.3.2

* captive portal detection improvements
* remote backend urls

### 3.3.1

* Fixes
  * network detection fixes
  * local cnl fixes

### 3.3.0

* Fixes
  * CaptivePortal behaviour when access was given
  * analytics improvements

#### 3.2.0

* Fixes
  * Blast transport initialization
  * rare crashes
  * analytics fix

#### 3.1.2

* Added
  * SessionConfig\#keepVpnOnReconnect
  * UnifiedSDK\#setReconnectionEnabled\(boolean\)
* Fixes
  * Fix relogin on NOT\_AUTHORIZED error
  * rare crashes
  * analytics crashes

#### 3.1.1

* Fixes
  * Documentation on android 10 connect openvpn
* Added
  * UnifiedSDKConfigBuilder\#runCallbacksOn
  * UnifiedSDK\#update\(CallbackMode\)
* Deprecated
  * UnifiedSDKConfigBuilder\#idfaEnabled

#### 3.1.0

* Added
  * SessionConfig.Builder\#withTransportFallback - configure transport fallback on multiple transports configured
* Fixed
  * Always On disconnect issue
  * Captive portal detection
  * Security improvements

#### 3.0.0

* Complete sdk refactoring

#### 2.4.1

* Openvpn android q support
* Internal fixes
* Fireshield runtime whitelist

#### 2.4.0

* Client network list
* Private servers
* Internal fixes

#### 2.3.1

* Fix for internal account migration from older versions

#### 2.3.0

* Added support for OpenVPN transport

#### 2.2.4

* Internal analytics improvements

#### 2.2.0

* Internal improvements

#### 2.2.1

* Removed sticky vpn service on network loss and reconnection

#### 2.0.0

* Internal refactoring
* Removed all deprecated versions
* startVPN/stopVPN errors are forwarded also to vpnError callback of HydraSdk.addVpnListener\(\). Callbacks on startVpn/stopVpn will be called when operation is finished
* Cannot turn off notification for PAUSED state
* new VpnState - PAUSED - sdk moves to this state when connection was lost due to network loss, and will be restored on network connected
* vpnError callback now gets base HydraException

#### 1.2.1

* updated vpn transport lib

#### 1.2.0

* remote domain bypass lists integrated

#### 1.1.0

* Supports VPN Always on feature

#### 1.0.2

* No significant changes

#### 1.0.1

* No significant changes

#### 1.0.0

* Added
  * class SessionConfig to configure starting vpn session
  * To update vpn config without restarting vpn\(limited options update\) void updateConfig\(@NonNull final SessionConfig sessionConfig, @NonNull final CompletableCallback callback\)
  * void startVPN\(@NonNull final SessionConfig sessionConfig, @NonNull final Callback callback\)
* Deprecated
  * void startVPN\(@TrackingConstants.GprReason @NonNull final String reason, @NonNull final Callback callback\)
  * void startVPN\(@NonNull final String countryCode, @TrackingConstants.GprReason @NonNull final String reason, @NonNull final Callback callback\)
  * void startVPNForApps\(@NonNull final String countryCode, @NonNull final List allowedApps, @TrackingConstants.GprReason @NonNull final String reason, @NonNull final Callback callback\)
  * void startVPNExceptApps\(@NonNull final String countryCode, @NonNull final List disallowedApps, @TrackingConstants.GprReason @NonNull final String reason, @NonNull final Callback callback\)
  * addBlacklistDomain
  * addBlacklistDomains
  * addBypassDomains

#### 0.28.7-alpha2

* Changed
  * ServerCredentials now have multiple servers we are trying to connect

#### 0.28.5

* Added
  * method **channelId** to **NotificationConfig** for notifications support on Android O+

#### 0.28.4

* Changed
  * HydraSDKConfig.Builder to HydraSDKConfigBuilder
  * ApiCallback to Callback in all public HydraSdk calls
  * ApiCompletableCallback to CompletableCallback in all public HydraSdk calls
  * VPNException with VPNException.WRONG\_STATE code to WrongStateException
  * NotAuthorizedException to ApiHydraException with HttpsURLConnection.HTTP\_UNAUTHORIZED code
  * NetworkException to NetworkRelatedException
  * SystemPermissionsErrorException to VPNException with VPNException.VPN\_FD\_NULL\_NO\_PERMISSIONS
* Removed
  * HttpException
  * SystemPermissionsErrorException

#### 0.28.3

* Deprecated
  * TrafficStats getTrafficStats\(\)
  * VPNState getVpnState\(\)
  * void current\(@NonNull final Callback callback\)
  * void startVPNForApps\(@NonNull final List allowedApps, @TrackingConstants.GprReason @NonNull final String reason, @NonNull final Callback callback\)
  * void startVPNExceptApps\(@NonNull final List disallowedApps, @TrackingConstants.GprReason @NonNull final String reason, @NonNull final Callback callback\)
  * boolean isLoggingEnabled\(\)
  * void setLoggingEnabled\(\)
  * boolean isVpnStarted\(\)
  * VPNState getVpnState\(\)

