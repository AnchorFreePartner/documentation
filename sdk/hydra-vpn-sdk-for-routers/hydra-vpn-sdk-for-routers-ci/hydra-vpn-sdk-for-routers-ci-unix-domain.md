# Unix Domain Sockets CI

Dynamic Configuration Interface based on Unix Domain sockets.

* Easy to implement, no external dependencies needed
* Supports both synchronous requests and asynchronous events
* Local machine only

## Configuration

### Minimal working configuration

```text
{
    ...SDK config params...
    "ci_unix_domain" : {}
}
```

### All configuration parameters

```text
"sock"
```

Path to unix domain socket file created by CI. Socket acts like a bi-directional channel, which means one file is used for receiving requests from and sending responses to your app. `SOCK_SEQPACKET` socket type is used. 

_Default:_ `"/var/run/afwrt-ci.sock"`

```text
"su_only"
```

Allow access to file to superuser only. 

_Default:_ `1`

```text
"async_sock"
```

Path to unix domain socket file created by your app. Socket for all kinds of async events from SDK, such as `"route_connected"`, `"bandwidth_info"`, etc. `SOCK_DGRAM` socket type is used. 

It's safe to create `"async_sock"` sometime later. CI can store up to `10` last events in memory before file will be actually created.

_Default:_ `""`\(empty, disabled\)

```text
"disabled"
```

Handy flag to fast disable dynamic interface not removing `"ci_unix_domain"` configuration section 

_Default:_ `0`

## Requests examples

### Ping 

`{ "request" : "ping" }`

### Protect IP address 

`{ "request" : "protect_ip", "ip_addr" : "192.168.50.149", "country_code" : "ca" }`

### Unprotect IP address

`{ "request" : "unprotect_ip", "ip_addr" : "192.168.50.149" }`

### Protect MAC address

`{ "request" : "protect_mac", "mac_addr" : "08:00:27:aa:d7:17", "country_code" : "ca" }`

### Unprotect MAC address

`{ "request" : "unprotect_mac", "mac_addr" : "08:00:27:aa:d7:17" }`

### Protect interface

`{ "request" : "protect_iface", "iface" : "eth2", "country_code" : "ca" }`

### Unprotect interface

`{ "request" : "unprotect_iface", "iface" : "eth2" }`

### Dump config file

`{ "request" : "dump_config", "config_path" : "/etc/afwrt/afwrt-ci.conf" }`

### Get available countries

`{ "request" : "get_countries" }`

