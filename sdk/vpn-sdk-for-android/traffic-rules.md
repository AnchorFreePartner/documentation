# Traffic rules

## Traffic proxy Rules \(Hydra transport\)

Its possible to configure how Hydra will operate with dns and other traffic. To configure it use `addDnsRule` and `addProxyRule` of `SessionConfig.Builder` when starting vpn session.

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

