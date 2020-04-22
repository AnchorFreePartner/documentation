# Client Networks

To access Client Networks, open up the portal and select Settings.  Client Networks will be one of the tabs.

By setting up a network with this feature, the VPN will be automatically turned on or off depending on what rule is set for the network.

**Adding a Network**

Select ![](../../.gitbook/assets/image%20%2822%29.png) Add

A dialog will appear: 

![](../../.gitbook/assets/image%20%2823%29.png)

Select Type of Network.  The options are WIFI, WWAN \(Mobile Phone Network\) or LAN \(Ethernet\).

If WIFI is chosen, another dialog will appear:

![](../../.gitbook/assets/image%20%2818%29.png)

Enter the SSID \(Name of the WiFi network\)  or the BSSID \(MAC address of the Wi-Fi network\).

Authorized \(If the network has a password or not\) options are Yes, No or "Does not matter".

Finally, pick the Action option.   Either select enable or disable, to automatically turn on the VPN \(enable\) or turn off the VPN when this network is used.

**Download**

Selecting this option will cause the list of networks to be downloaded as a JSON file onto your device.

**Editing an Existing Network**

Just select the ![](../../.gitbook/assets/image%20%2825%29.png) pencil to the right of the name of the network that you want to modify. Make sure to click on save after any changes.

**Deleting a Network**

Click on the ![](../../.gitbook/assets/image%20%2820%29.png) trash can  that is right of the network that needs to be deleted.

**Priority of Rules**

In the picture below, the BobsNetwork is on the first line as well as the second.  The way the system works, the higher on this list the higher the priority the rules of the network are given.  In this situation, BobsNetwork will have the VPN enabled and will ignore the second line where it disables the VPN.

![](../../.gitbook/assets/image%20%2827%29.png)

**Changing order of the Network**

The order of these networks can be easily changed.  Just select the number of the network on the far left and drag it to the new location.

