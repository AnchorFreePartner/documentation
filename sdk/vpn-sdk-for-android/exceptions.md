# Exceptions

## Exceptions

All exceptions sdk can throw extends **com.anchorfree.vpnsdk.exceptions.VpnException**

There are couple of main derivatives of this exception

#### **PartnerApiException**

Thrown in case of server api errors.

**getCode** - HTTP error code

**getContent** - response content

Possible values for getContent:

* `CODE_NOT_AUTHORIZED` - user is not authorized. Need to call HydraSdk.login
* `CODE_SESSIONS_EXCEED` - Session limit is achieved in accordance with the ToS
* `CODE_DEVICES_EXCEED` - Devices limit is achieved in accordance with the ToS
* `CODE_OAUTH_ERROR` - Returns in all cases when an authentication error occurred through OAuth-server
* `CODE_TRAFFIC_EXCEED` - Ended limitation traffic activated in accordance with the terms of the license
* `CODE_SERVER_UNAVAILABLE` - Server temporary unavailable or server not found
* `CODE_INTERNAL_SERVER_ERROR` - Internal server error
* `USER_SUSPENDED` - User Suspended
* `CODE_PARSE_EXCEPTION` - Failed to parse server response

#### **VpnTransportException**

Thrown when error happen in vpn transport

**getCode** - code of error

* `HydraVpnTransportException` - is thrown by **Hydra** transport
* `CaketubeTransportException` - is thrown by **OpenVPN** transport

Possible values for getCode on **Hydra** transport

* `HydraVpnTransportException.HYDRA_ERROR_BROKEN` - VPN connection broken
* `HydraVpnTransportException.HYDRA_ERROR_CONNECT` - Hydra fails to connect to server
* `HydraVpnTransportException.HYDRA_DCN_BLOCKED_BW` - Hydra server reported traffic exceed. Connection interrupted
* `HydraVpnTransportException.HYDRA_DCN_BLOCKED_AUTH` - Hydra server reported auth failed

Possible values for getCode on **OpenVPN** transport

* `CaketubeTransportException.CONNECTION_BROKEN_ERROR` - server interrupted connection
* `CaketubeTransportException.CONNECTION_FAILED_ERROR` - failed to connect to server
* `CaketubeTransportException.CONNECTION_AUTH_FAILURE` - server reported auth failed

#### **NetworkRelatedException**

Thrown in case of network problem communicating to server

#### **WrongStateException**

Thrown when calling `start` or `stop` in wrong sdk state

#### **InternalException**

Thrown for any other unexpected cases. In **getCause** you can get original source exception

#### **CnlBlockedException**

Thrown when connecting to network that has **Disabled** state in CNL config.

