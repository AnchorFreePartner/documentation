# Traffic rules

## Traffic proxy Rules \(Hydra transport\)

Its possible to configure how Hydra will operate with dns and other traffic. To configure it use `addDnsRule` and `addProxyRule` of `SessionConfig.Builder` when starting vpn session.

### DNS

Whenever dns resolution takes place it's intercepted by hydra vpn and domain-based rules might be applied.

Domain-based rules affect how dns resolution will proceed as well as how further connections to particular domain will be routed.

Domains might be classified according to types below:



| type | dns resolution |
| :--- | :--- |
| bypass | dns request will proceed in bypass to hydra vpn. |
| proxy | no dns resolution will take place on client-side. Non-routable IP \(NRIP\) is returned to application. |
| vpn | no dns resolution will take place on client-side. Non-routable IP \(NRIP\) is returned to application. |
| blockDns | no dns resolution takes place. |

These rules can be created and added to `SessionConfig.Builder#addDnsRule`with the following methods.

* TrafficRule.Builder.bypass
* TrafficRule.Builder.proxy
* TrafficRule.Builder.blockDns
* TrafficRule.Builder.vpn

The data sources can be:

* fromAssets
* fromFile
* fromDomains
* fromResource

### Other

Whenever traffic other than DNS reaches hydra vpn, domain-based rules are the first ones to be considered in order to route content through the correct data path.

These rules can be created and added to `SessionConfig.Builder#addProxyRule`with the following methods.

* TrafficRule.Builder.bypass
* TrafficRule.Builder.proxy
* TrafficRule.Builder.blockPkt
* TrafficRule.Builder.vpn

The data sources can be:

* fromAssets
* fromFile
* fromDomains
* fromResource
* fromIp
* udp
* tcp

### Examples

To bypass local network traffic and let local network resource accessible you can configure ip mask rule

```text
final SessionConfig builder = new SessionConfig.Builder();
builder.addProxyRule(TrafficRule.Builder.bypass().fromIp("192.168.1.0", 24)); //all traffic to net 192.168.1.0 will go outside vpn tunnel
```

To block all dns requests to domains in project assets file

```text
final SessionConfig builder = new SessionConfig.Builder();
builder.addDnsRule(TrafficRule.Builder.block().fromAssets("blocklist.txt"));
```

