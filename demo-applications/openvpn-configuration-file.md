---
description: Learn how to compose an .ovpn file from the UserAPI responses
---

# OpenVPN configuration file

{% hint style="warning" %}
This article is valid for OpenVPN 2.4
{% endhint %}

To compose a valid .ovpn file, you should make a call to the UserAPI and use several field values from the response. Specifically: [**GET /user/provide**](https://anchorfreepartner.github.io/apidocs/user.html#get-/user/provide)****

{% hint style="info" %}
Please make sure to use a proper "protocol" parameter value (the one you actually are going to use for the VPN connection)
{% endhint %}

#### Minimal requirements

```
client
dev tun
proto tcp-client
remote 0.0.0.0 443
auth-user-pass passfile.txt
<ca>
</ca>
```

| Option         | Values                                                                       | Description                                                                                                                                                                                                                                                                                                                                                     |
| -------------- | ---------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| client         | <ul><li><strong>client</strong></li><li>server</li></ul>                     | Defines that we want to configure an OpenVPN client, not a server                                                                                                                                                                                                                                                                                               |
| dev            | <ul><li><strong>tun</strong></li><li>tap</li></ul>                           | Defines virtual device we are going to use (**tun** devices encapsulate IPv4 or IPv6 (OSI Layer 3) while **tap** devices encapsulate Ethernet 802.3 (OSI Layer 2)                                                                                                                                                                                               |
| proto          | <ul><li><strong>tcp-client</strong></li><li>tcp-server</li><li>udp</li></ul> | Defines a network protocol to use                                                                                                                                                                                                                                                                                                                               |
| remote         | <ul><li>IP</li><li>server-name</li></ul>                                     | Defines a server address and a port to connect. The value for this option should be taken from the **servers.address** and **server.port** fields of the API response.                                                                                                                                                                                          |
| auth-user-pass | -                                                                            | <p>Should have a file name as a value. The file itself should contain the username and the password in that <strong>exact</strong> order, on <strong>separate</strong> lines. The actual values should be taken from the respective API response fields. </p><p></p><p>If the file is omitted, username/password are going to be prompted from the console.</p> |
| \<ca>\</ca>    | -                                                                            | Should include a security certificate from the API response field **openvpn-tcp **/ **openvpn-udp**                                                                                                                                                                                                                                                             |

{% hint style="warning" %}
According to the [OpenVPN man page](https://community.openvpn.net/openvpn/wiki/Openvpn24ManPage?\_\_cf\_chl\_jschl\_tk\_\_=pmd\_DpFO2k2lNzrI96Ei.BPoyQDjjQR.r5fmJIOiwVAMChU-1631540713-0-gqNtZGzNAfujcnBszQm9), it is impossible to inline username and password directly in the configuration file
{% endhint %}

Additional options can be used for fine-tuning:

* tun-mtu,&#x20;
* tun-mtu-extra,&#x20;
* ping,&#x20;
* cipher,&#x20;
* auth&#x20;

More information on those and other options can be found in the official OpenVPN documentation.
