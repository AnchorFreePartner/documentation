# Exceptions

## Exceptions

All exceptions SDK can throw extends **unified.vpn.sdk.VpnException**

There are couple of main derivatives of this exception:&#x20;

**PartnerApiException** - Thrown in case of server API errors

**getCode** - HTTP error code

**getContent** - response content

Possible values for **getContent**:

* `CODE_NOT_AUTHORIZED` - user is not authorized. Need to call HydraSdk.login
* `CODE_SESSIONS_EXCEED` - session limit is reached in accordance with the ToS
* `CODE_DEVICES_EXCEED` - device limit is reached in accordance with the ToS
* `CODE_OAUTH_ERROR` - returns in all cases when an authentication error occurred on OAuth server
* `CODE_TRAFFIC_EXCEED` - reached active traffic limitation in accordance with the ToS
* `CODE_SERVER_UNAVAILABLE` - server temporarily unavailable or server not found
* `CODE_INTERNAL_SERVER_ERROR` - internal server error
* `USER_SUSPENDED` - user suspended
* `CODE_PARSE_EXCEPTION` - failed to parse server response

#### **VpnTransportException**

Thrown when error happens in VPN transport

**getCode** - code of error

* `HydraVpnTransportException` - is thrown by **Hydra** transport
* `OpenVpnTransportException` - is thrown by **OpenVPN** transport

Possible values for **getCode** on **Hydra** transport

* `HydraVpnTransportException.HYDRA_ERROR_BROKEN` - VPN connection broken
* `HydraVpnTransportException.HYDRA_ERROR_CONNECT` - Hydra fails to connect to server
* `HydraVpnTransportException.HYDRA_DCN_BLOCKED_BW` - Hydra server reported traffic exceedance, connection interrupted
* `HydraVpnTransportException.HYDRA_DCN_BLOCKED_AUTH` - Hydra server reported auth failure

Possible values for **getCode** on **OpenVPN** transport

* `OpenVpnTransportException.CONNECTION_BROKEN_ERROR` - server interrupted connection
* `OpenVpnTransportException.CONNECTION_FAILED_ERROR` - failed to connect to server
* `OpenVpnTransportException.CONNECTION_AUTH_FAILURE` - server reported auth failure

#### **NetworkRelatedException**

Thrown in case of server connection problems

#### **WrongStateException**

Thrown when calling `start` or `stop` in wrong SDK state

#### **InternalException**

Thrown for any other unexpected cases. In **getCause** you can get original source exception

#### **CnlBlockedException**

Thrown when connecting to network that has **Disabled** state in CNL config.
