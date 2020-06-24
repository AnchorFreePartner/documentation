---
description: >-
  Learn about VPN and a way of providing unlimited number of users with secure,
  fast, anonymous and unrestricted access to any website. You can create your
  own application and upload it anywhere.
---

# Public VPN

VPN stands for Virtual Private Network. A VPN connects your device to the Internet through another computer. You’re connecting to the Internet through another computer’s Internet connection, rather than directly through your own. Aside from that, the VPN also encrypts the data you send, so that it’s kept secure.

A simple analogy would be sending a postcard with and without an envelope \(via VPN and without it, respectively\). If you send your postcard without an envelope, somebody \(an Internet Service Provider or even a hacker\) can easily read its contents. On the other hand, if you use an envelope, the postcards contents will remain much harder to read, thus preserving your privacy. It is as simple as that!

VPN protocols determine exactly how data is routed through a connection. These protocols have different specifications based on the benefits and desired circumstances; for example, some VPN protocols prioritize data throughput speed while others focus on masking or [encrypting](https://www.netmotionsoftware.com/blog/security/data-encryption-101/) data packets for privacy and security. We offer SDKs using 3 different VPN protocols: IPSEC, OpenVPN and proprietary Hydra protocol.

* IPSEC/L2TP: Layer 2 Tunnel Protocol is a replacement of the PPTP VPN protocol. This protocol does not provide any encryption or privacy out-of-the-box and is frequently paired with security protocol IPSEC. Once implemented, L2TP/IPSEC is extremely secure and has no known vulnerabilities. Keywords: widely used, good speeds, easily blocked due to reliance of UDP on single port.
* OpenVPN: OpenVPN is an open source protocol that allows developers access to its underlying code. This protocol has grown in popularity due to its use of \(virtually unbreakable\) AES-256 bit key encryption with 2048-bit RSA authentication and a 160-bit SHA1 hash algorithm. Keywords: open source, strongest encryption, slower speeds.
* Hydra: to learn about this protocol, please refer to the [FAQ](https://support.hotspotshield.com/hc/en-us/articles/360000374343-What-s-the-protocol-used-by-Hotspot-Shield-).

Public VPN is the product we developed so you can let anyone use fast, secure and safe VPN. You can either use a sample application or build your own app from scratch using provided SDKs. A user just presses 'Connect' and receives all the benefits of a secure network. Tha application creates a VPN tunnel that connects the user with the Internet.

The main features of Public VPN are:

* Your real IP address is concealed, so it allows you to maintain your online privacy and search the web anonymously;
* Whatever node you choose, thousands of people are using it day and night, thus it is much harder for other people to access your search history;
* All the traffic from your computer to the node is encrypted, even if you are using a public network, so a potential hacker is much less likely to intercept it;
* Access any website in countries that have restricted connection to those sites;
* By connecting to a server in a different country, you can conceal your geographical location \(or change it to acquire offers for certain countries by online shops\).

To create an application for users, we provide SDKs for different platforms and with different VPN protocols: 

* [VPN SDK for Android](https://pango.gitbook.io/pango-platform/sdk/untitled) ![](../../.gitbook/assets/metronome-playstore-logo-png-clipart-thumbnail.jpg) \(supports Hydra and OpenVPN protocols\)
* [Hydra VPN SDK for iOS/macOS](https://pango.gitbook.io/pango-platform/sdk/hydra-vpn-sdk-for-ios) ![](../../.gitbook/assets/appstore-black-n-white.png)![](../../.gitbook/assets/apple-logo-computer-icons-png-favpng-wbktizskbkzbdeyzujybp9ke7.jpg) 
* [IPSEC VPN SDK for iOS/macOS](https://pango.gitbook.io/pango-platform/sdk/ipsec-vpn-sdk-for-ios-macos) ![](../../.gitbook/assets/appstore-black-n-white.png)![](../../.gitbook/assets/apple-logo-computer-icons-png-favpng-wbktizskbkzbdeyzujybp9ke7.jpg) 
* [Hydra SDK for Windows](https://pango.gitbook.io/pango-platform/sdk/hydra-sdk-for-windows) ![](../../.gitbook/assets/ms-store-black-n-white.png) 
* [HydraVPN SDK for Routers](https://pango.gitbook.io/pango-platform/sdk/hydravpn-sdk-for-routers)

If you are looking for a sample application, you do not have to go elsewhere, we got them right here:

* [Hydra VPN SDK demo for iOS](https://pango.gitbook.io/pango-platform/demo-applications/untitled) ![](../../.gitbook/assets/appstore-black-n-white.png) 
* [IPSEC VPN SDK demo for iOS](https://pango.gitbook.io/pango-platform/demo-applications/ipsec-vpn-sdk-demo-for-ios) ![](../../.gitbook/assets/appstore-black-n-white.png) 
* [Hydra VPN SDK demo for Android](https://pango.gitbook.io/pango-platform/demo-applications/anchorfree-hydra-vpn-sdk-demo-for-android) ![](../../.gitbook/assets/metronome-playstore-logo-png-clipart-thumbnail.jpg) 
* [Hydra VPN SDK demo for Windows](https://pango.gitbook.io/pango-platform/demo-applications/hydra-vpn-sdk-demo-for-windows) ![](../../.gitbook/assets/ms-store-black-n-white.png) 
* [OpenVPN SDK for Windows](https://pango.gitbook.io/pango-platform/demo-applications/openvpn-sdk-for-windows) ![](../../.gitbook/assets/ms-store-black-n-white.png) 

When using a sample application, you just have to set a server to connect to and you are good to go.

