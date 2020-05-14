# What analytic data collect your SDK?

The main purpose of the reporting is to improve the connection quality of the SDK. SDK collects anonymous data about device and about connection start and stop attempts.

SDK performs Network Availability Test for better understanding what's  
happening on connection error. It includes diagnostics of the current network connection such a check a Captive Portal, ping a popular public web resource and etc.

## Common properties

### Common Android device related properties:

| **Property Name** | **Type** | **Description** |
| :--- | :--- | :--- |
| af\_platform | String | android |
| uid | String | Application uuid. The kernel user-ID that has been assigned to this application; currently this is not a unique ID \(multiple applications can have the same _uid_\). |
| app\_name | String | Application package name |
| app\_build | String | Id based on app signature. Helpful to figure out if app is cracked. |
| app\_version | String | Application version name |
| app\_release | String | Application version code |
| carrier | String | Telephony carrier |
| has\_telephone | Boolean | If device is a phone |
| memory\_remains | String | Remaining RAM |
| memory\_total | String | Total RAM |
| model | String | android.os.Build.MODEL |
| device\_manufacturer | String | android.os.Build.MANUFACTURER |
| locale | String | Current device locale |
| device\_language | String | Current device language |
| hydra\_base\_url | String | Base api url |
| android\_sdk\_int | String | Build.VERSION.SDK\_INT |
| android\_version\_name | String | Build.VERSION.RELEASE |
| connection\_type | String | Type name of current active network |
| time\_zone | String | Device time zone in format like "-0800" |
| af\_hash | String | Device id generated on first app install |
| sdk\_version | String | SDK version name |
| sdk\_version\_code | Integer | SDK version code |

### Common iOS and macOS device related properties

| **Property Name** | **Type** | **Description** |
| :--- | :--- | :--- |
| af\_platform | String | “ios” |
| app\_name | String | Application package name |
| app\_release | String | Application version code |
| distinct\_id | String | Unique id generated on first app install |
| epoch | Integer | Time of generated event in unix format |
| carrier | String | Telephony carrier name |
| model | String | iPhone model, eg. iPhone8,2 |
| manufacturer | String | “Apple” |
| af\_hash | String | Device id generated on first app install |
| sdk\_version | String | SDK version name |
| lib\_version | String | Analytics SDK version |
| os | String | Device OS \(iOS\) |
| os\_version | String | OS version, eg. 13.1.2 |
| screen\_height | Integer | Device screen height |
| screen\_width | Integer | Device screen width |
| server\_protocol | String | SDK server protocol eg. hydra |
| sim\_country | String | Country of carrier |
| wifi | Bool | Indicates if device is on Wi-Fi network |
| time | Integer | The current time on device in unix format |

### Common connection properties for all platforms

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Property Name</b>
      </th>
      <th style="text-align:left"><b>Type</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">catime</td>
      <td style="text-align:left">Integer</td>
      <td style="text-align:left">Unix millisecond timestamp (milliseconds since Epoch) on the client when
        connection attempt was initiated</td>
    </tr>
    <tr>
      <td style="text-align:left">caid</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Connection Attempt ID assigned by the client when an attempt to establish
        a connection starts (regardless of the result)</td>
    </tr>
    <tr>
      <td style="text-align:left">reason</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Describes why the session was initiated or terminated (user click, reconnect,
        etc).</td>
    </tr>
    <tr>
      <td style="text-align:left">error_code</td>
      <td style="text-align:left">Integer</td>
      <td style="text-align:left">numerical code referring to an error category (0 = success). See section
        &#x201C;error_code&#x201D; Property below.</td>
    </tr>
    <tr>
      <td style="text-align:left">error</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">error description. See &#x201C;error&#x201D; property section below.</td>
    </tr>
    <tr>
      <td style="text-align:left">protocol</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">the protocol used for the connection attempt</td>
    </tr>
    <tr>
      <td style="text-align:left">server_ip (*)</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">the server IP address used to establish a VPN connection (absent in the
        case of unsuccessful result)</td>
    </tr>
    <tr>
      <td style="text-align:left">session_id (*)</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">session ID assigned by the server or VPN in case of successful connection
        attempt, should match server side session_id (could be absent for some
        protocols)</td>
    </tr>
    <tr>
      <td style="text-align:left">hydra_version (*)</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">version of Hydra used to establish a connection</td>
    </tr>
    <tr>
      <td style="text-align:left">notes</td>
      <td style="text-align:left">JSON</td>
      <td style="text-align:left">
        <p>Additional information. For now it holds:</p>
        <ul>
          <li>detailed info about <em>network_availabilty</em> test if one was conducted</li>
          <li>sd_tag - json passed by hydra. Example:</li>
        </ul>
        <p><code>{</code>
        </p>
        <p> <code>&quot;sd_tag&quot;: {</code>
        </p>
        <p> <code>&quot;region_id&quot;: 38,</code>
        </p>
        <p> <code>&quot;isp_name&quot;: &quot;Zayo Bandwidth&quot;,</code>
        </p>
        <p> <code>&quot;coursera_on&quot;: 0,</code>
        </p>
        <p> <code>&quot;isp_org&quot;: &quot;Zayo Bandwidth&quot;</code>
        </p>
        <p> <code>}</code>
        </p>
        <p><code>}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">parent_caid</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>If previous attempt failed and technical reconnect happened (e.g. in case
          of network change or 3 attempts during button click)</p>
        <p>We log here parent caid.</p>
        <p><em>Parent_caid</em> - caid of original connection attempt initiated by
          user.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">is_ipv6_only</td>
      <td style="text-align:left">Integer (0 or 1)</td>
      <td style="text-align:left">Flag that shows if the ISP supports only IPv6 protocol (1 if yes, 0 if
        no). Should be defined by the client.</td>
    </tr>
  </tbody>
</table>## Properties for _app\_start_ event \(iOS\) ???

| **Property Name** | **Type** | **Description** |
| :--- | :--- | :--- |
| first | Bool | Indicates the first launch of the app. |

## Connection events

There are 4 connection events:

* **connection\_start,** 
* **connections\_start\_detailed,** 
* **connection\_end,** 
* **connection\_end\_detailed**. 

We are using **\*\_detailed** events mostly for diagnostic if a connection really works and what the possible reason if a connection could not be established.

### Event: _connection\_start_

Event reports every connection attempt.

Properties specific for event _connection\_start_:

| **Property Name** | **Type** | **Notes** |
| :--- | :--- | :--- |
| duration | Integer | how long it took to establish a connection or stop trying to connect, in **milliseconds** |
| notes | JSON | Provides the additional information if any related to the connection process. |

### Event: _connection\_start\_detailed_

Event reports additional details regarding all finished connection attempts to particular IPs \(main, offload\), including successful.

If the connection attempt was unsuccessful, network availability check should be performed and reported in network\_availability and notes properties.

Properties specific for event _connection\_start\_detailed_:

| **Property Name** | **Type** | **Notes** |
| :--- | :--- | :--- |
| network\_availability | Float | Share of passed Network Availability tests rounded to 2 digits after decimal point. |
| notes | JSON | detailed results of the Network Availability Test. |
| details | JSON | an array of JSONs with connection results to all low level attempts to connect. |

### Event: _connection\_end_

The event should be reported when a Connection is terminated. All properties specific for connection-related events should be reported for this event as well.

Properties specific for event _connection\_end_:

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Property Name</b>
      </th>
      <th style="text-align:left"><b>Type</b>
      </th>
      <th style="text-align:left"><b>Notes</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">duration</td>
      <td style="text-align:left">Integer</td>
      <td style="text-align:left">the session&apos;s duration, in <b>milliseconds</b>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">traffic</td>
      <td style="text-align:left">JSON</td>
      <td style="text-align:left">
        <p>JSON with consumed traffic stats (in bytes), e.g.:</p>
        <p>{</p>
        <p>&quot;bytes_in&quot;: 100,</p>
        <p>&quot;bytes_out&quot;: 100</p>
        <p>}</p>
      </td>
    </tr>
  </tbody>
</table>### Event: _connection\_end\_detailed_

When a connection is terminated unexpectedly \(no user intention to terminate the session\), network availability tests should be performed and _connection\_end\_detailed_ event should be reported. If user has canceled, no need to send the event.  
Properties specific for event _connection\_end\_detailed:_

| **Property Name** | **Type** | **Notes** |
| :--- | :--- | :--- |
| network\_availability | Float | Share of passed Network Availability tests rounded to 2 digits after the decimal point. |
| notes | JSON | detailed results of the Network Availability Test. |

### Property for “_error\_code_”

#### _connection\_start_

| **error\_code** | **Description** |
| :--- | :--- |
| 0 \(success\) | No error \(connection has established successfully\) |
| 1 \(internal error\) | Internal problems during initialization or establishing communication \(e.g. Failed to open TUN, VPN permissions are not given, Hydra "Bad Configuration" error, etc.\) or any other unclassified errors |
| 2 \(connection error\) | Failed to establish a connection due to networking issues \(e.g. host is unreachable, can't send data, timeout on receiving data, etc.\) |
| 4 \("no network" error\) | Network has been lost during the connection \(e.g. WiFi lost or changed\) or network is up, but unavailable \(e.g. due to walled garden or as mobile data is disabled\) |
| 6 \(canceled\) | The connection establishment has been terminated in the middle of the process. No connection has been established. |
| 7 \(app level error\) | Application denied to start establishing the VPN connection \(i.e. user tried to use some elite features from the free app, PC adapter is not ready to connect\) |

#### _connection\_end_

| **error\_code** | **Description** |
| :--- | :--- |
| 0 \(success\) | No error \(connection has ended as expected and successfully\) |
| 1 \(internal error\) | Internal problem that broke established connection \(e.g. OpenVPN or Hydra quit unexpectedly, etc.\) |
| 2 \(connection error\) | Connection has broken due to connection problems \(e.g. Hydra or OpenVPN detected communication problem, etc.\) |
| 3 \(connection stuck\) | Connection is established, but no exchange happening \("KeepAlive problem"\) |

### Property for “_error_”

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>error_code</b>
      </th>
      <th style="text-align:left"><b>error</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0 (success)</td>
      <td style="text-align:left">Empty</td>
      <td style="text-align:left">No error</td>
    </tr>
    <tr>
      <td style="text-align:left">1 (internal error)</td>
      <td style="text-align:left">Platform specific details</td>
      <td style="text-align:left">
        <p>Internal problems during initialization, establishing communication or
          operation (e.g. Failed to open TUN, Hydra &quot;Bad Configuration&quot;
          error, VPN permissions are not given, etc.)</p>
        <p>Also, this class should be used for any unclassified errors. It is expected
          that the details will be clear from the &quot;error&quot; value.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2 (connection error)</td>
      <td style="text-align:left">HTTP error code or a VPN/Hydra error code</td>
      <td style="text-align:left">Connection has not been established or broken due to connection problems
        (e.g. Hydra or OpenVPN detected communication problem, etc.)</td>
    </tr>
    <tr>
      <td style="text-align:left">3 (connection stuck)</td>
      <td style="text-align:left">Platform specific details</td>
      <td style="text-align:left">Connection is established, but no exchange happening (&quot;KeepAlive
        problem&quot;)</td>
    </tr>
    <tr>
      <td style="text-align:left">4 (&quot;no network&quot; error)</td>
      <td style="text-align:left">Platform specific details</td>
      <td style="text-align:left">Network has been lost during the connection (e.g. WiFi lost or changed)
        or network is up, but unavailable (e.g. due to walled garden or as mobile
        data is disabled)</td>
    </tr>
    <tr>
      <td style="text-align:left">5 (failed)</td>
      <td style="text-align:left">Error code returned by backend (e.g. 40301)</td>
      <td style="text-align:left">Request has succeeded, but have had an error result code</td>
    </tr>
  </tbody>
</table>## Reasons

### connection\_start

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Name</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">m_ui</td>
      <td style="text-align:left">Connection is initiated by a user clicking in application UI button, widget,
        notification window, etc.</td>
    </tr>
    <tr>
      <td style="text-align:left">m_system</td>
      <td style="text-align:left">Connection is initiated via user&apos;s click/action from a system menu.</td>
    </tr>
    <tr>
      <td style="text-align:left">m_tray</td>
      <td style="text-align:left">Connection is initiated by a user clicking on ongoing notification or
        tile services</td>
    </tr>
    <tr>
      <td style="text-align:left">m_other</td>
      <td style="text-align:left">Connection is initiated via some other user&apos;s actions.</td>
    </tr>
    <tr>
      <td style="text-align:left">a_app_run</td>
      <td style="text-align:left">Connection is initiated automatically as the result of an app launch that
        is configured to trigger it.</td>
    </tr>
    <tr>
      <td style="text-align:left">a_reconnect</td>
      <td style="text-align:left">
        <p>Connection is initiated after intended (without an error) previous session
          termination. This can be result of:</p>
        <ul>
          <li>Changing Virtual Locations</li>
          <li>Upgrading or Downgrading</li>
          <li>Keeping intended VPN connection (UI/user intention requires VPN to be
            on)</li>
          <li>etc.</li>
        </ul>
        <p><em>Note that this reason should only be used if the connection is initiated right after the previous connection termination and as long as we are trying to initiate connection. That is, if while reconnecting network become unavailable, the reason for the first session initiation after the network become available shall be a_network (not a_reconnect). However, in case the session initiation failed, for the next attempt to initiate the session, the same reason (a_network) shall be used.</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">a_error</td>
      <td style="text-align:left">
        <p>Connection is initiated as a result of retry from the previous session
          termination due to an error.</p>
        <p><em>Note that this reason should only be used if connection is initiated right after the previous connection termination and as long as we are trying to initiate connection. That is, if the error has happened due to the network lost, the reason for the first session initiated after the network become available shall be a_network (not a_error). However, in case the session initiation failed, for the next attempt to initiate the session, the same reason (a_error) shall be used.</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">a_sleep</td>
      <td style="text-align:left">Connection is initiated due to device returned from the sleep mode (resume),
        hibernation mode, etc.</td>
    </tr>
    <tr>
      <td style="text-align:left">a_network</td>
      <td style="text-align:left">
        <p>Connection is initiated due to the status of the network has changed (network
          become available). In this case, we shall reconnect in of the following
          cases:</p>
        <ul>
          <li>We were connected manually, so regardless of the wifi protection settings</li>
          <li>The network requires protection as per user&apos;s setting (automatic
            protection)</li>
        </ul>
        <p><em>Note the reconnect due to network switch is covered by this reason (not a_reconnect).</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">a_other</td>
      <td style="text-align:left">
        <p>Connection is initiated automatically due to any other reason.</p>
        <p><em>Note the share of a_other reason should be few percent. In case it is not so, extra reasons shall be introduced.</em>
        </p>
      </td>
    </tr>
  </tbody>
</table>### connection\_end

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Name</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">m_ui</td>
      <td style="text-align:left">Connection is terminated by a user clicking in application UI button,
        widget, notification window, etc.</td>
    </tr>
    <tr>
      <td style="text-align:left">m_system</td>
      <td style="text-align:left">
        <p>Connection is terminated via user&apos;s click/action from a system menu.</p>
        <p>For iOS, turn off inside device&apos;s setting.</p>
        <p>For Android, turn off from system&apos;s VPN notification (aka <b>revoke</b>).</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">m_tray</td>
      <td style="text-align:left">Connection is terminated by user clicking on ongoing notification or tile
        services</td>
    </tr>
    <tr>
      <td style="text-align:left">m_other</td>
      <td style="text-align:left">
        <p>Connection is terminated via some other user&apos;s actions.</p>
        <p><em>Note the share of m_other reason should be few percent. In case it is not so, extra reasons shall be introduced.</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">a_error</td>
      <td style="text-align:left">
        <p>Connection is terminated due to an error (including unavailability of
          the network).</p>
        <p>Error description shall be provided in error_code and error properties.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">a_sleep</td>
      <td style="text-align:left">Connection is terminated due to device goes to sleep, suspend, shut down,
        etc.</td>
    </tr>
    <tr>
      <td style="text-align:left">a_reconnect</td>
      <td style="text-align:left">
        <p>Connection is terminated intentionally in order to immediately reconnect.
          This can be result of:</p>
        <ul>
          <li>Changing Virtual Locations</li>
          <li>Upgrading or downgrading</li>
          <li>Client version updating</li>
          <li>etc.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">a_network</td>
      <td style="text-align:left">Connection is terminated due to the network has changed</td>
    </tr>
    <tr>
      <td style="text-align:left">a_other</td>
      <td style="text-align:left">
        <p>Connection is terminated automatically due to any other reason.</p>
        <p><em>Note the share of a_other reason should be few percent. In case it is not so, extra reasons shall be introduced.</em>
        </p>
      </td>
    </tr>
  </tbody>
</table>## Network Availability Test

There are several reasons for a connection attempt to fail or an established connection to drop unexpectedly. It can be an infrastructure issue or a client bugs that can and shall be fixed. It can be a blockage that should be addressed by changing of the configuration or in worst case improving the VPN core and re-releasing the client. But it can also be a. problem with the network that can’t be fixed in principle.

In order to distinguish these cases, a **network availability test** will be performed on every unsuccessful connect or unintended disconnect that will report whether the network in available or not.

This test includes: check captive portal, current network type, ping test and certificate test.

### Captive Portal test
This test is to check if there is a Captive portal. It usually means that  
all requests are redirected by network provider to their own login page.

To detect this case SDK sends a request to one of urls from the list and expects response code 204:  
 https://google.com/generate_204,  
 https://gstatic.com/generate_204,  
 https://maps.google.com/generate_204,  
 https://www.google.com/generate_204,  
 https://clients3.google.com/generate_204

### Ping test
TODO

### Network type test

SDK calls system api to check if any type of network interface is
established.
For example on older versions of Android SDK uses api  
https://developer.android.com/reference/android/net/ConnectivityManager#getNetworkInfo(android.net.Network)

### Certificate test
In some particular cases there can be more significant issues with your connection like
issues with web certificates.
To test this case SDK sends a request to one of the following url and checks that certificate
is valid:

https://google.com/,  
https://apple.com,  
https://microsoft.com,  
https://yahoo.com,  
https://baidu.com,  
https://amazon.com,  
https://instagram.com,  
https://linkedin.com,  
https://ebay.com,  
https://bing.com,  
https://goo.gl,  
https://outlook.live.com,  
https://wikipedia.org,  
https://office.com

## Event samples

### _connection\_start_

```text
{
  "event": "connection_start",
  "id": "1",
  "properties": {
    "af_platform": "android",
    "reason": "m_ui",
    "app_version": "3.2.0",
    "is_ipv6_only": "0",
    "locale": "US",
    "error": "Captive Portal",
    "device_manufacturer": "Google",
    "duration": "1107",
    "uid": 10079,
    "protocol": "hydra",
    "hydra_version": "release-hydra-v5.0.4-2-g980098b",
    "catime": "1585089436276",
    "caid": "37EAC37405964FF9A7C41094F66E8C4C",
    "sdk_version": "3.2.0",
    "model": "Android SDK built for x86",
    "memory_total": 1567338496,
    "memory_remains": 760401920,
    "seq_no": 12,
    "app_release": 403219,
    "connection_type": "WiFi",
    "android_version_name": "8.1.0",
    "has_telephone": true,
    "sd_in_tunnel": "0",
    "time_zone": "-0700",
    "app_name": "com.northghost.hydraclient.kotlin",
    "carrier": "Android",
    "sdk_version_code": "403219",
    "app_build": 444722979,
    "android_sdk_int": 27,
    "error_code": "4",
    "time": 1585089437403,
    "device_language": "en"
  }
}
```

### _connection\_start\_detailed_

```text
{
  "event": "connection_start_detailed",
  "id": "2",
  "properties": {
    "af_platform": "android",
    "reason": "m_ui",
    "notes": "{\"network_availability_test\":[{\"type\":\"http certificate\",\"url\":\"https:\\/\\/ebay.com\",\"result\":\"ok\"},{\"type\":\"captive portal\",\"url\":\"https:\\/\\/clients3.google.com\\/generate_204\",\"result\":\"ok\"},{\"type\":\"network interface\",\"result\":\"wifi\"}]}",
    "app_version": "3.2.0",
    "is_ipv6_only": "0",
    "locale": "US",
    "error": "Captive Portal",
    "device_manufacturer": "Google",
    "duration": "1107",
    "uid": 10079,
    "protocol": "hydra",
    "hydra_version": "release-hydra-v5.0.4-2-g980098b",
    "catime": "1585089436276",
    "caid": "37EAC37405964FF9A7C41094F66E8C4C",
    "sdk_version": "3.2.0",
    "model": "Android SDK built for x86",
    "details": "[]",
    "memory_total": 1567338496,
    "memory_remains": 758894592,
    "seq_no": 13,
    "app_release": 403219,
    "connection_type": "WiFi",
    "network_availability": "1.0",
    "android_version_name": "8.1.0",
    "has_telephone": true,
    "sd_in_tunnel": "0",
    "time_zone": "-0700",
    "app_name": "com.northghost.hydraclient.kotlin",
    "carrier": "Android",
    "sdk_version_code": "403219",
    "app_build": 444722979,
    "android_sdk_int": 27,
    "error_code": "4",
    "time": 1585089438040,
    "device_language": "en"
  }
}
```

### _connection\_end_

```text
{
  "event": "connection_end",
  "id": "6",
  "properties": {
    "af_platform": "android",
    "reason": "m_ui",
    "vl_code": "OPT",
    "app_version": "3.2.0",
    "is_ipv6_only": "0",
    "locale": "US",
    "error": "VpnException:VPN stopped by RemoteVpn",
    "device_manufacturer": "Google",
    "duration": "4188",
    "uid": 10079,
    "protocol": "hydra",
    "hydra_version": "release-hydra-v5.0.4-2-g980098b",
    "catime": "1585089615598",
    "caid": "8DDF0415954648DE9EB0C2A28895191A",
    "sdk_version": "3.2.0",
    "server_ip": "92.38.148.65",
    "hydra_base_url": "https://api-prod-partner-us-west-2.northghost.com/",
    "model": "Android SDK built for x86",
    "memory_total": 1567338496,
    "af_hash": "YWZkZW1vXzE2MDg3ODc0********",
    "memory_remains": 757387264,
    "traffic": "{\"bytes_in\":0,\"bytes_out\":269}",
    "hydra_carrier": "afdemo",
    "seq_no": 16,
    "app_release": 403219,
    "connection_type": "WiFi",
    "android_version_name": "8.1.0",
    "has_telephone": true,
    "sd_in_tunnel": "0",
    "session_id": "SA65D3CBED0DF7198653B682836EEE9-00",
    "time_zone": "-0700",
    "app_name": "com.northghost.hydraclient.kotlin",
    "carrier": "Android",
    "sdk_version_code": "403219",
    "partner_carrier": "afdemo",
    "app_build": 444722979,
    "android_sdk_int": 27,
    "error_code": "1",
    "time": 1585089619889,
    "device_language": "en",
    "server_protocol": "hydra"
  }
}
```

### _connection\_end\_detailed_

```text
{
  "event": "connection_end_detailed",
  "id": "8",
  "properties": {
    "af_platform": "android",
    "reason": "m_ui",
    "vl_code": "OPT",
    "notes": "{\"network_availability_test\":[{\"type\":\"http certificate\",\"url\":\"https:\\/\\/google.com\\/\",\"result\":\"ok\"},{\"type\":\"captive portal\",\"url\":\"https:\\/\\/google.com\\/generate_204\",\"result\":\"ok\"},{\"type\":\"network interface\",\"result\":\"wifi\"}]}",
    "app_version": "3.2.0",
    "is_ipv6_only": "0",
    "locale": "US",
    "error": "VpnException:VPN stopped by RemoteVpn",
    "device_manufacturer": "Google",
    "duration": "4188",
    "uid": 10079,
    "protocol": "hydra",
    "hydra_version": "release-hydra-v5.0.4-2-g980098b",
    "catime": "1585089615598",
    "caid": "8DDF0415954648DE9EB0C2A28895191A",
    "sdk_version": "3.2.0",
    "server_ip": "92.38.148.65",
    "hydra_base_url": "https://api-prod-partner-us-west-2.northghost.com/",
    "model": "Android SDK built for x86",
    "memory_total": 1567338496,
    "af_hash": "YWZkZW1vXzE2MDg3OD********",
    "memory_remains": 755924992,
    "traffic": "{\"bytes_in\":0,\"bytes_out\":269}",
    "hydra_carrier": "afdemo",
    "seq_no": 17,
    "app_release": 403219,
    "connection_type": "WiFi",
    "network_availability": "1.0",
    "android_version_name": "8.1.0",
    "has_telephone": true,
    "sd_in_tunnel": "0",
    "session_id": "SA65D3CBED0DF7198653B682836EEE9-00",
    "time_zone": "-0700",
    "app_name": "com.northghost.hydraclient.kotlin",
    "carrier": "Android",
    "sdk_version_code": "403219",
    "partner_carrier": "afdemo",
    "app_build": 444722979,
    "android_sdk_int": 27,
    "error_code": "1",
    "time": 1585089620336,
    "device_language": "en",
    "server_protocol": "hydra"
  }
}
```

