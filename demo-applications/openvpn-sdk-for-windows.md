---
description: >-
  Windows SDK is a part of Aura Platform which contains the client-side
  libraries and server-side applications needed to implement custom VPN
  infrastructure.
---

# OpenVPN SDK for Windows

Download [the last version SDK](https://firebasestorage.googleapis.com/v0/b/web-portal-for-partners.appspot.com/o/products%2FCakeTubeSDK\_Win\_version\_1.3.3.218\_partnerapi\_1.0.2.42%20\_with\_TAP\_signed.zip?alt=media\&token=80766b10-1121-4bb9-9e38-af8159409ab7)

The Windows SDK provides API allowing:

* authenticate clients on VPN Server
* connect clients to VPN Server

## Prerequisites

OS: Windows 7, 8.0, 8.1, 10 Software: .NET Framework 4.5 Nuget dependencies: No third party dependencies are required

## Setup

In order to use the SDK the steps described below must be performed.

1. Install TAP Driver as Administrator via command line: ./tapinstall.exe install "AFTap.inf" "aftap0901"
2. Install VPN Windows Service as Administrator via command line: ./VpnService.exe -install
3. To uninstall service later: ./VpnService.exe -uninstall

## Initialize

### CakeTube Class

Performs initialization of SDK

#### Methods

| Syntax                                                                                                             | Description                                                                                                                                                                                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| static void Initialize(string serviceName, string carrierId, string baseUrl)                                       | Initializes all SDK states and dependencies.                                                                                                                                                                                                                                                       |
| static void Initialize(string serviceName, string carrierId, string baseUrl, bool autoConnect)                     | Initializes all SDK states and dependencies. Set "autoConnect" to true if SDK should reconnect on network switch.                                                                                                                                                                                  |
| static void Initialize(string serviceName, string carrierId, string baseUrl, string openVpnPath)                   | Initializes all SDK states and dependencies. "openVpnPath" is a custom path for OpenVpn binaries. Default path is "%temp%\service\_name", If "openVpnPath" is null or empty binaries will be extracted to default location.                                                                        |
| static void Initialize(string serviceName, string carrierId, string baseUrl, bool autoConnect, string openVpnPath) | Initializes all SDK states and dependencies. Set "autoConnect" to true if SDK should reconnect on a network switch. "openVpnPath" is a custom path for OpenVpn binaries. Default path is "%temp%\service\_name", If "openVpnPath" is null or empty binaries will be extracted to default location. |

#### Properties

| Syntax                   | Description                                                                         |
| ------------------------ | ----------------------------------------------------------------------------------- |
| VpnConnectionService     | The service for connect/disconnect operations.                                      |
| VpnWindowsServiceHandler | The handler that allows to interact with Windows service., check its state and etc. |
| BackendService           | The service that allows to perform backend related requests.                        |

#### Example

```
CakeTube.Initialize("CakeTube Demo Vpn Service", "afdemo", "https://backend.northghost.com");
```

## Authentication

Aura Partner VPN Backend uses OAuth authentication as a primary authentication method.

Steps to implement OAuth:

* Deploy and configure OAuth service. Service should be publicly available in Internet.
* Configure Partner Backend to use OAuth service.
* Implement client OAuth for your application.
* Retrieve access token in client app, this token will be used to initialize and sign in Windows Partner SDK.

### VpnServerService Class

Manages client user: authentication, credentials retrieval, user info. Recommended place to create this service is an Application singleton class.

#### Methods

| Syntax                                                                         | Description                                                                      |
| ------------------------------------------------------------------------------ | -------------------------------------------------------------------------------- |
| Task< LoginResponse > LoginAsync(LoginParams)                                  | Logs in to vpn server.                                                           |
| Task< LogoutResponse > LogoutAsync(LogoutParams)                               | Performs logout on server side.                                                  |
| Task< IsVpnResponse > IsVpnAsync()                                             | Checks if VPN connection is established.                                         |
| Task< VerifyResponse > VerifyAsync(VerifyParams)                               | Cheks if received credentials are still valid.                                   |
| Task< ConfigResponse > ConfigAsync()                                           | Gets configuration data from server.                                             |
| Task< CredentialsResponse > CredentialsAsync(CredentialsParams)                | Gets credentials for establishing vpn connection.                                |
| Task< NodesResponse > NodesAsync(NodesParams)                                  | Gets available vpn countries. Requires access token as parameter.                |
| Task< VpnCountersResponse > CountersAsync(GetCountersRequestParams)            | Gets incoming and outcoming vpn traffic from the server.                         |
| Task< RemainingTrafficResponse > RemainingTrafficAsync(RemainingTrafficParams) | Gets remaining traffic for the current user.                                     |
| Task< PurchaseResponse > PurchaseAsync(PurchaseParams)                         | Performs a purchase on the backend.                                              |
| Task< CurrentResponse > CurrentAsync(CurrentParams)                            | Gets current user info.                                                          |
| Task< RemoteConfigResponse > RemoteConfigAsync(RemoteConfigParams)             | Gets remote config for an app. Hydra only                                        |
| Task< ProvideResponse > ProvideAsync(ProvideParams)                            | Gets credentials for establishing vpn connection for several servers. Hydra only |
| Task< BypassDomainsResponse > BypassDomainsAsync(BypassDomainsParams)          | Gets a list of domains that will be bypassed. Hydra ONLY                         |
| Task< NetworkRulesResponse > NetworkRulesAsync(NetworkRulesParams)             | Gets . Hydra ONLY                                                                |

## Connection

### VpnConnectionService Class

Manages device's VPN connection. To establish VPN connection user should manually install TAP driver and Vpn Windows Service as described in the Setup section.

Recommended place to create this service is an Application singleton class. This service is used to communicate with VPN Windows service and manages connection.

#### Methods

| Syntax                                         | Description            |
| ---------------------------------------------- | ---------------------- |
| Task< bool > ConnectAsync(CredentialsResponse) | Opens Vpn connection.  |
| void Disconnect()                              | Closes VPN connection. |

#### Properties

| Syntax                                | Description                        |
| ------------------------------------- | ---------------------------------- |
| VpnConnectionState VpnConnectionState | Provides current connection state. |

#### Events

| Syntax                                                | Description                                                          |
| ----------------------------------------------------- | -------------------------------------------------------------------- |
| VpnConnectionStateChangedEventHandler VpnStateChanged | Notifies subscribers about Vpn Connection state changes.             |
| VpnTrafficChangedEventHandler VpnTrafficChanged       | Notifies subscribers about changes of consumed network traffic value |
| VpnTrafficLimitReached VpnTrafficLimitReached         | Notifies subscribers when traffic limit reached                      |

## Logging

The SDK provides two types of logging: console logging and file logging. Both can be used the same time.

### CakeTubeLogger Class

#### Methods

| Syntax                                     | Description                        |
| ------------------------------------------ | ---------------------------------- |
| static void AddHandler(BaseLoggerListener) | Adds a handler of a specific type. |

### FileLoggerListener Class inherited from BaseLoggerListener

#### Constructor

| Syntax                          | Description                                                                |
| ------------------------------- | -------------------------------------------------------------------------- |
| FileLoggerListener(string path) | Initializes a new instance of FileLoggerListener. Path is a full filename. |

### ConsoleLoggerListener Class inherited from BaseLoggerListener

#### Constructor

| Syntax                  | Description                                                                                   |
| ----------------------- | --------------------------------------------------------------------------------------------- |
| ConsoleLoggerListener() | Initializes a new instance of ConsoleLoggerListener. A log will be written to console output. |
