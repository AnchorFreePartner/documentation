# Configuration Interface \(CI\)

SDK Configuration Interface \(CI\) is a VPN client which use VPN SDK shared library. 

It supports static file configuration and dynamic configuration using [REST API](hydra-vpn-sdk-for-routers-ci-rest-api.md) or [Unix Domain Sockets](hydra-vpn-sdk-for-routers-ci-unix-domain.md).

## Running

```text
afwrt-ci <config_path>
```

`"config_path"` - path to static file configuration which format was described [here](../hydra-vpn-sdk-for-routers-sdk.md#configuration). Can be empty.

_Default:_ `"/etc/afwrt/afwrt-ci.conf"`

## Requests

Request is a json string with `"request"` field and request-specific fields. `"request"` is one of the following values.

### Ping

Just check configuration interface is alive, don't change anything. 

_Value:_ `"ping"` 

_Params:_ None

### Protect IP

Add route for the following IP. 

_Value:_ `"protect_ip"` 

_Params:_ 

* `"ip_addr"` - IP address to protect 
* `"country_code"` - desired VPN country traffic from `"ip_addr"` go to

### Unprotect IP 

Remove route for the following IP. 

_Value:_ `"unprotect_ip"` 

_Params:_

* `"ip_addr"` - IP address to unprotect

### Protect MAC

Add route for the following MAC. 

_Value:_ `"protect_mac"` 

_Params:_ 

* "`mac_addr"` - MAC address to protect
* `"country_code"` - desired VPN country traffic from "mac\_addr" go to

### Unprotect MAC

Remove route for the following MAC. 

_Value:_ `"unprotect_mac"` 

_Params:_ 

* `"mac_addr"` - MAC address to unprotect

### Protect interface

Add route for the following interface. 

_Value:_ `"protect_iface"` 

_Params:_ 

* `"iface"` - interface to protect
* `"country_code"` - desired VPN country traffic from "iface" go to

### Unprotect interface

Remove route for the following interface. 

_Value:_ `"unprotect_iface"` 

_Params:_ 

* `"iface"` - interface to unprotect

### Dump config file 

Dump config to filesystem. 

_Value:_ `"dump_config"` 

_Params:_ 

* `"config_path"` - path to file where config should be dumped. If empty or not specified, dump to a file which used to run afwrt-ci.

### Get available countries 

Get list of available VPN countries. 

_Value:_ `"get_countries"` 

_Params:_ None

## Responses

Response is a json string with `"status"` field and set of optional fileds, such as `"message"` and response-specific fields.

`"status"` is one of the following codes: 

* `-1` - internal error. Allocation errors, internal exceptions. 
* `0` - success. 
* `1` - configuration error. Error changing internal configuration structures. 
* `2` - bad request. Request is not recognized. 
* `3` - bad format. Required request parameters are missing. 
* `4` - VPN error. Error sending request to VPN core.

`"message"` filed contains specific information about error if any.

### Get available countries

_Response fields:_ 

* `"countries"` - json array of country codes available. 

_Response example:_ `{ "status" : 0, "countries" : ["de","no","us"] }`

## Async events

If chosen dynamic interface supports sending of async events, you will get them as is from SDK library. All async events listed [here](../hydra-vpn-sdk-for-routers-sdk.md#callback-events).

## Dynamic interfaces configuration

Please, follow the configuration section of [Unix Domain Sockets](hydra-vpn-sdk-for-routers-ci-unix-domain.md#configuration) or [REST API](hydra-vpn-sdk-for-routers-ci-rest-api.md#configuration). Only one dynamic interface can run in one time or both can be disabled. Unix Domain Sockets interface has higher priority.

