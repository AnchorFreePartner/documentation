---
description: Learn how to compose an .ovpn file from the UserAPI responses
---

# OpenVPN configuration file

{% hint style="warning" %}
This article is valid for OpenVPN 2.4
{% endhint %}

To compose a valid .ovpn file, you should make a call to the UserAPI and use several field values from the response. Specifically: [**GET /user/provide**](https://anchorfreepartner.github.io/apidocs/user.html#get-/user/provide)\*\*\*\*

{% hint style="info" %}
Please make sure to use a proper "protocol" parameter value \(the one you actually are going to use for the VPN connection\)
{% endhint %}

#### Minimal requirements

```text
client
dev tun
proto tcp-client
remote 0.0.0.0 443
auth-user-pass passfile.txt
<ca>
</ca>
```

<table>
  <thead>
    <tr>
      <th style="text-align:left">Option</th>
      <th style="text-align:left">Values</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">client</td>
      <td style="text-align:left">
        <ul>
          <li><b>client</b>
          </li>
          <li>server</li>
        </ul>
      </td>
      <td style="text-align:left">Defines that we want to configure an OpenVPN client, not a server</td>
    </tr>
    <tr>
      <td style="text-align:left">dev</td>
      <td style="text-align:left">
        <ul>
          <li><b>tun</b>
          </li>
          <li>tap</li>
        </ul>
      </td>
      <td style="text-align:left">Defines virtual device we are going to use (<b>tun</b> devices encapsulate
        IPv4 or IPv6 (OSI Layer 3) while <b>tap</b> devices encapsulate Ethernet
        802.3 (OSI Layer 2)</td>
    </tr>
    <tr>
      <td style="text-align:left">proto</td>
      <td style="text-align:left">
        <ul>
          <li><b>tcp-client</b>
          </li>
          <li>tcp-server</li>
          <li>udp</li>
        </ul>
      </td>
      <td style="text-align:left">Defines a network protocol to use</td>
    </tr>
    <tr>
      <td style="text-align:left">remote</td>
      <td style="text-align:left">
        <ul>
          <li>IP</li>
          <li>server-name</li>
        </ul>
      </td>
      <td style="text-align:left">Defines a server address and a port to connect. The value for this option
        should be taken from the <b>servers.address</b> and <b>server.port</b> fields
        of the API response.</td>
    </tr>
    <tr>
      <td style="text-align:left">auth-user-pass</td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">
        <p>Should have a file name as a value. The file itself should contain the
          username and the password in that <b>exact</b> order, on <b>separate</b> lines.
          The actual values should be taken from the respective API response fields.</p>
        <p></p>
        <p>If the file is omitted, username/password are going to be prompted from
          the console.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&lt;ca&gt;&lt;/ca&gt;</td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">Should include a security certificate from the API response field <b>openvpn-tcp </b>/ <b>openvpn-udp</b>
      </td>
    </tr>
  </tbody>
</table>

{% hint style="warning" %}
According to the [OpenVPN man page](https://community.openvpn.net/openvpn/wiki/Openvpn24ManPage?__cf_chl_jschl_tk__=pmd_DpFO2k2lNzrI96Ei.BPoyQDjjQR.r5fmJIOiwVAMChU-1631540713-0-gqNtZGzNAfujcnBszQm9), it is impossible to inline username and password directly in the configuration file
{% endhint %}

Additional options can be used for fine-tuning:

* tun-mtu, 
* tun-mtu-extra, 
* ping, 
* cipher, 
* auth 

More information on those and other options can be found in the official OpenVPN documentation.

