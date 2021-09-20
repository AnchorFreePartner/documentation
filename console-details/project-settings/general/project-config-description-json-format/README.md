---
description: JSON config includes the full list of the project parameters.
---

# Project config description \(JSON format\)

An example of JSON config is:

```text
{
  "allow_login_for_blocked_users": true,
  "application": {
     "android": {
        "support": [
           "alexey@anchorfree.com",
           "n.slushkin@anchorfree.com"
        ],
        "a_param1": 1,
        "a_param2": 2
      },
      "ios": {
         "i_param1": 1,
         "i_param2": 2
      },
      "windows-desctop": {
         "w_param1": 1,
         "w_param2": 2
      }
   },
   "sd": {
      "android": { 
          ....
      }, ....
   },
   "files": {
      "bpl": "1a420b6f34466fc14bd88a814e9b31f153856d11",
      "cnl": "5880169e4aef949b0ae93924d9526ec679bd5a54"
   },
   "server_pool": "pub-default", 
   "server_group": "touchvpn",
   "disable_optimal_location": false,
   "labels_for_unlimited": ["netflix"]
}
```

**allow\_login\_for\_blocked\_users** **\(**_true_ ****or ****_false_**\)** - allow \(_true_\) login for blocked users. The blocked user can't open a VPN session or use other Platform services.

**application** - the remote config by platform \(“_android_”, “_ios_”, “_windows-desktop_”, …\). You can set any additional parameters for your application.

**support** - support emails for the project. You can set email addresses in case users want to contact support in the application. Please set this parameter in the Member tab:

{% page-ref page="../../members.md" %}

**sd** - special parameters for Hydra VPN protocol and Firebase service. Please contact us for any changes to this parameter.

**files** - section with specific files for this project. For example, the file with a list of bypass URLs \(_BPL_\).

**bpl** - bypass list ID. If you put URLs on the bypass list, the BPL file will be automatically created and added to this JSON config. To learn how to add URLs to BPL, see the "VPN Bypass list" tab:

{% page-ref page="../../vpn/vpn-bypass-list.md" %}

The SDK will download the BPL file regularly and use it for the Bypass feature. A URL for downloading the file looks like this: _https://internal.northghost.com/storage/project/**project\_name**/files/bpl/**1a420b6f34466fc14bd88a814e9b31f153856d11**_

where _project\_name_ is your project ID, _1a420b6f34466fc14bd88a814e9b31f153856d11_ - is the BPL file ID

**cnl** - the list of client network IDs. If you set networks to the CNL, the CNL file will be automatically created and added to this JSON config. To learn how to add networks to CNL, see the "Client Networks" tab:

{% page-ref page="../../vpn/client-networks.md" %}

The SDK will download the CNL file regularly and use it for the CNL feature. 

**“server\_pool”** - a pull of VPN nodes for this project. “_pub-default_” - the default pull name.

**“private\_pools”** - a pull of private servers, available only for this project. _\[“pvt-1”, “pvt-2”\]_ - the list of private pull names. Please contact us for additional details.

“**disable\_optimal\_location”** \(_true_ or _false_\) - enable or disable optimal location function for the project. The default - _false_. This Parameter will be added automatically if you enable the "**Optimal location**" parameter in General.

**“labels\_for\_limited”** - list of profile labels without traffic limits. For example, the “netflix” label should enable the Netflix traffic offloading to special VPN nodes configured to support Netflix.

