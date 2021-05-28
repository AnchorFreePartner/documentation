# Client Networks

By setting up a network with this feature, the VPN will be automatically turned on or off depending on what rule is set for the network. 

You can create and manage a list of rules for all users in this tab.

## **Actions**

### **Adding a rule**

If you are going to add a new network rule to the project, you need to do the following steps:

1. Click "![](../../../.gitbook/assets/plus_icon.jpeg)**Add**". You will see a new form:

![](../../../.gitbook/assets/add_new_networkrule.png)

  2. Select Type of Network.  The options are _WIFI_, _WWAN_ \(Mobile Phone Network\) or _LAN_ \(Ethernet\). If _WIFI_ is chosen, another dialog will appear:  

![](../../../.gitbook/assets/add_wifirule_networkrule.png)

* Enter a SSID \(Name of the WiFi network\) or a BSSID \(MAC address of the Wi-Fi network\). Optional field.
* Authorized options are _Yes_, _No_ or _Does not matter_ \(if the network has a password\).
* Finally, pick the Action option. Either select _enable_ or _disable_, to automatically turn on the VPN \(enable\) or turn off the VPN when this network is used.

  3. Click **Save** to add new rule. As a result, you will see the new rule in the list of rules:

![](../../../.gitbook/assets/list_networkrules.png)

### **Download a list of rules**

Selecting this action \(![](../../../.gitbook/assets/download_icon.webp)Download\) will cause the list of networks to be downloaded as a JSON file onto your device.

### **Editing a rule**

Just click the ![](../../../.gitbook/assets/edit_icon.png) button to the right of the name of a network that you want to modify. Make sure to click **Save** after changing a rule.

### **Deleting a rule**

Click on the ![](../../../.gitbook/assets/delete_icon.png) button that is on the right of the network that needs to be deleted.

### **Rule priority**

In the picture below, BobsNetwork is in the first line as well as the second. The higher on this list, the higher the priority of a rule of the network is. In this situation, BobsNetwork will have the VPN enabled and will ignore the second line where the VPN is disabled.

![](../../../.gitbook/assets/image%20%287%29.png)

### **Changing order of the Networks**

The order of these networks can be easily changed. Just click the number to the left of the network and drag it where you want it to be.

