# Which is the best way - using Fireshield or setting up a DNS service and force the SDK to use it?

We recommend using full VPN mode that sends all traffic to the remote server only if there is a need to protect user data from interception \(for instance, on an unsecured WiFi\) or to change the user’s IP address \(for instance, when traveling\).

In other cases, we recommend using Fireshield mode that sends safe traffic in bypass.

If there are a preferred DNS service, Fireshield can enforce its use and, if a request is not blocked, send the traffic directly to the resolved IP address. However, if used alone, this may have some limitations:

* No additional protection from “suspicious” requests that are not blocked due to possibility of the false alarm \(“request score” is not leveraged\).
* Some applications may use built-in IPs, or resolve IPs without issuing recognized DNS requests.

To address these problems, Fireshield is able to:

* Analyze each request after it is issued: see the IP address, whether it was resolved by a recognized DNS or not.
* Send suspicious requests through the VPN server to provide additional protection: hide user IP and / or apply additional server-side rules.

