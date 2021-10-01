# Hydra VPN SDK demo for OpenWRT

{% hint style="info" %}
Please pay attention that this limited version does not support dynamic configuration via websockets or any kind of statistics/reporting and can send a lot of debug information to stdout.
{% endhint %}

[GitHub project link](https://github.com/AnchorFreePartner/hydra-sdk-wrt/tree/ng)

## Compatibility

* OpenWRT v19.07.3 or later

## Installation and running

* for x86\_64 target

`opkg install afwrt-ws_0.3_x86_64.ipk`  


* for mvebu/cortexa9 target

`opkg install afwrt-ws_0.3_arm_cortex-a9_vfpv3-d16.ipk`  


If package installation was succeeded, the next files should appear on your WRT system:

* /usr/lib/libafwrt.so        - VPN SDK library
* /usr/bin/afwrt-ws          - VPN SDK demo client
* /etc/afwrt/whoami.in   - VPN SDK library configuration template
* /etc/afwrt-ws.conf        - VPN SDK client configuration

Please take a look at the section below and check /etc/afwrt-ws.conf was configured properly for your setup and execute afwrt-ws binary with root privileges.

You can download [pre-compiled library and binary files for x86\_64](https://firebasestorage.googleapis.com/v0/b/web-portal-for-partners.appspot.com/o/products%2FHydraSDK_OpenWRT_version_latest.zip?alt=media&token=8ec44727-dc79-4299-b17c-b926840473e3) architecture  


### Configuration

Most of the options could be left unchanged for this demo. But the next options should be updated properly in afwrt-ws.conf:

* "wan\_ifname": name of your "Wide Area Network" interface, which your device connected to the internet through
* "protected\_ip\_addrs": array of protected IP addresses on the internal network you want to test, with Country \(Virtual Location\) code for each

Option "token" is hard coded until the second release. It will be retrieved internally using the “[/user/login](https://anchorfreepartner.github.io/apidocs/user.html#post-/user/login)” method. 

{% hint style="info" %}
The advantage of x86\_64 format is that this build can be deployed and tested on any developer machine w/o real hardware. We recommend using VirtualBox.

VBox-based environment could be set up according to the instruction:

[https://openwrt.org/docs/guide-user/virtualization/virtualbox-vm](https://openwrt.org/docs/guide-user/virtualization/virtualbox-vm)
{% endhint %}

### Available country codes

In the current release, a list of available country codes is hardcoded by the following ones:

* ar
* au
* br
* ca
* ch
* cz
* de
* dk
* es
* fr
* gb
* hk
* id
* ie
* in
* it
* jp
* mx
* nl
* no
* ro
* ru
* se
* sg
* tr
* ua
* us

From the next release, this list will be retrieved dynamically from the backend server using the “[/user/countries](https://anchorfreepartner.github.io/apidocs/user.html#get-/user/countries)” method.

## Possible issues

`$ wget example.net`

`Resolving example.net... failed: Name or service not known.`

Please check your router DNS settings. Dnsmasq may not be configured properly or DHCP-client configured on WAN interface can’t get DNS-server address from your DHCP server.  


