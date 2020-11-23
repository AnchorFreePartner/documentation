# SDK. Shared library.

Router SDK provides a [shared library](hydra-vpn-sdk-for-routers-sdk.md) \(with C header file\) which can be integrated with Application using C calls.

## SDK C API

```text
int afwrt_init(const char params_json, void (event_callback)(const char *event_str));
```

Initialize library. Must be called once before using the library. 

`params_json` - configuration in json format. See ["Configuration"](hydra-vpn-sdk-for-routers-sdk.md#configuration) section below. Can't be NULL. 

`event_callback` - callback function to receive periodic SDK events. See ["Callback events" ](hydra-vpn-sdk-for-routers-sdk.md#callback-events)section below. Can be NULL.

```text
int afwrt_deinit(void); 
```

Deinitialize library. Must be called once after using the library.

```text
int afwrt_start(void);
```

Start library main loop. Blocking call.

```text
int afwrt_stop(void);
```

Stop library event loop.

```text
char* afwrt_get_available_countries(void);
```

Returns json string with list of available VPN locations, or NULL on error. String must be free\(\)-ed by the caller. 

Return string example: `[ "br", "ca", "de", "fr", "gb", "it", "jp", "mx", "us" ]`

```text
int afwrt_protect_ip_addr(const char *ip_addr, const char *country);
```

Add rule to route traffic from specified IP address via specified VPN country. Returns 0 on success, -1 on error. Safe to call multiple times to change country.

`ip_addr` - IP address to protect

`country` - VPN country to route traffic to

```text
int afwrt_unprotect_ip_addr(const char *ip_addr);
```

Remove rule to route traffic from specified IP address via VPN. Returns 0 on success, -1 on error.

`ip_addr` - IP address to unprotect

```text
int afwrt_protect_mac_addr(const char *mac_addr, const char *country);
```

Add rule to route traffic from specified MAC address via specified VPN country. Returns 0 on success, -1 on error. Safe to call multiple times to change country.

`mac_addr` - MAC address to protect

`country` - VPN country to route traffic to

```text
int afwrt_unprotect_mac_addr(const char *mac_addr);
```

Remove rule to route traffic from specified MAC address via VPN. Returns 0 on success, -1 on error.

`mac_addr` - MAC address to unprotect

```text
int afwrt_protect_iface(const char *iface, const char *country);
```

Add rule to route traffic from specified interface via specified VPN country. Returns 0 on success, -1 on error. Safe to call multiple times to change country.

`iface` - interface to protect

`country` - VPN country to route traffic to

```text
int afwrt_unprotect_iface(const char *iface);
```

Remove rule to route traffic from specified interface via VPN. Returns 0 on success, -1 on error.

`iface` - interface to unprotect

## Callback events

```text
"route_connected"
```

This event is sent when link to one of virtual locations became active. 

_Example:_ `{ "event": "route_connected", "route_name": "us" }`

```text
"route_disconnected"
```

This event is sent when active link to one of virtual locations became inactive due to SDK stop, network condition or for the other external reason. 

_Example:_ `{ "event": "route_disconnected", "route_name": "us" }`

```text
"route_failed"
```

This event is sent when link to one of virtual locations can not be established. 

_Example:_ `{ "event": "route_failed", "route_name": "fr", "reason_details": "connection failed" }`

```text
"bandwidth_info"
```

Event is sent periodically to client application. 

_Example:_ `{ "event": "bandwidth_info", "bandwidth_info": [ { "data_interval_ms": 100, "n_points": 100, "points_downstream": 0, "points_upstream": 0, "route_name": "us" }, { "data_interval_ms": 100, "n_points": 100, "points_downstream": 0, "points_upstream": 0, "route_name": "de" } ] }`

## Configuration

### Minimal working configuration

```text
{
    "tun_ifname" : "wrt0",
    "wan_ifname" : "eth1"
}
```

### All configuration parameters

```text
"tun_ifname"
```

Name of virtual TUN interface created by SDK. 

_Example:_ `"wrt0"`

```text
"wan_ifname"
```

Name of virtual TUN interface created by SDK. 

_Example:_ `"eth1"`

```text
"vl_default"
```

Default virtual location, country code. By default, all traffic routed to SDK TUN interface goes through this location. If not specified or empty, SDK will try to get optimal location which can be configured on backend side. 

_Default:_ `""`\(empty, see above\)

_Example:_ `"us"`

```text
"backend"
```

Backend server address. 

_Default:_ `"`[`https://`](https://backend.northghost.com)`default-backend.net"`

```text
"data_report_interval"
```

Event report interval in milliseconds. Time interval between bandwidth events \(see ["Callback events"](hydra-vpn-sdk-for-routers-sdk.md#callback-events) section above\). 

_Default:_ `30000` \(30 seconds\)

```text
"default_gateway"
```

Redirect all traffic including router's to SDK TUN interface. Do not create any specific iptables rule for protected IP, MAC or interface\(see ["Routing"](hydra-vpn-sdk-for-routers-sdk.md#routing) section below\), but add a global traffic redirection rule. 

_Default:_ `0`

```text
"config_dir"
```

Location of VPN core temporary files. SDK creates or updates a set of temporary files on each start. There should be already created directory for them. 

_Default:_ `"/etc/afwrt"`

```text
"tun_dev_path"
```

Path to OS tun device. 

_Default:_ `"/dev/net/tun"`

```text
"tun_addr"
```

IPv4 address of SDK TUN interface. 

_Default:_ `"100.73.0.73"`

```text
"protected_ip_addrs"
```

Array of protected IP addresses with not empty `"ip_addr"` and `"country_code"` fields. 

_Default:_ `""`\(empty, no IP addresses to protect\). 

_Example:_ `"protected_ip_addrs": [ { "ip_addr": "192.168.50.159", "country_code": "us" }, { "ip_addr": "192.168.50.139", "country_code": "de" } ]`

```text
"protected_mac_addrs"
```

 Array of protected MAC addresses with not empty `"mac_addr"` and `"country_code"` fields. 

_Default:_ `""`\(empty, no MAC addresses to protect\). 

_Example:_ `"protected_mac_addrs": [ { "mac_addr": "08:00:27:AA:D7:17", "country_code": "us" }, { "mac_addr": "09:01:28:AB:D8:18", "country_code": "de" } ]`

```text
"protected_ifaces"
```

Array of interfaces with not empty `"iface"`and `"country_code"` fields. 

_Default:_ `""`\(empty, no interface to protect\). 

_Example:_ `"protected_ifaces": [ { "iface": "eth1", "country_code": "us" }, { "iface": "br0", "country_code": "de" } ]`

## OS level routing

To protect traffic, SDK creates TUN device and routes all packets or packets with specific source IP, MAC or interface to it. To achieve this, SDK creates a set of routing and/or firewall\(iptables\) rules.

### Simple scenario. `"default_gateway"` option enabled.

Redirect just all traffic including router's to TUN device. 

To be smarter, SDK not changing default route of router's "main" table, but adding two big subnets with high metric. "0.0.0.0/1" and "128.0.0.0/1" for IPv4, for example.

```text
# ip route show table main
0.0.0.0/1 dev wrt0 scope link  metric 1000 
128.0.0.0/1 dev wrt0 scope link  metric 1000 
```

### Advanced scenario. `"default_gateway"` option disabled.

Selective routing by IP, MAC, or interface name. 

First, SDK creates routing table 47 with TUN device default gateway.

```text
# ip route show table 47
default dev wrt0 
```

Second, SDK creates a rule to forward all packets with 0x8 mark to table 47.

```text
# ip rule
10:	from all fwmark 0x8 lookup 47
```

Third, SDK creates custom iptables chain which will contain all specific IP, MAC and interface rules.

```text
# iptables -L -t mangle
Chain PREROUTING (policy ACCEPT)
target     prot opt source               destination         
afwrt_chain  all  --  anywhere             anywhere 
```

Such rules can be loaded from config on initialization phase or changed dynamically using protection methods above. Each rule marks specified IP, MAC or interface with 0x8 mark. 

Example of interface, MAC and IP rules:

```text
# iptables -L -t mangle -v
Chain afwrt_chain (1 references)
 pkts bytes target     prot opt in     out     source               destination         
    0     0 MARK       all  --  eth2   any     anywhere             anywhere             MARK set 0x8
    0     0 MARK       all  --  any    any     anywhere             anywhere             MAC 08:00:27:AA:D7:17 MARK set 0x8
    1    76 MARK       all  --  any    any     192.168.50.139       anywhere             MARK set 0x8
```

It doesn't matter in which order rules will appeared. All routing priority logic done by SDK internally \(see [below](hydra-vpn-sdk-for-routers-sdk.md#routing-rules-priority)\).

## VPN Core level routing

Regardless of OS level Routing mechanism, core is always ready to do selective routing based on IP, MAC and interface rules if any. If no rules specified, traffic will go to `"vl_default"` route as described [above](hydra-vpn-sdk-for-routers-sdk.md#all-configuration-parameters).

## Routing rules priority

MAC address rule has higher priority than IP address rule. IP address rule has higher priority than Interface rule.

For example, there are following rules:

* route traffic from device with MAC address `"08:00:27:AA:D7:17"` via `"us"`
* route traffic from device with IP address `"192.168.50.139"` via `"de"`

If both addresses \(MAC and IP\) belongs to the same device, traffic will be routed via `"us"` VPN country.

## MAC and Interface to IP resolution

To be able to distinguish device traffic on L3 network layer SDK needs it's IP address. 

SDK maintains mapping from MAC or Interface to IP addresses internally. 

It subscribes to changes in neighbors table using netlink, asking for ones with the following states: `NUD_REACHABLE`, `NUD_DELAY`, `NUD_PROBE`, `NUD_PERMANENT`, `NUD_STALE`.

## Dependencies

`libc` `kmod-tun` `ca-bundle` `libnetfilter-conntrack`

