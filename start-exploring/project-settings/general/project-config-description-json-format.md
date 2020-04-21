---
description: JSON config includes the full list parameters of a project.
---

# Project config description \(JSON format\)

The example of JSON config is

```text
{
  "default_licene_id": 1,
  "default_traffic_limit": 200000000,
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
      "bpl": "1a420b6f34466fc14bd88a814e9b31f153856d11"
   },
   "server_pool": "pub-default", 
   "server_group": "touchvpn",
   "disable_optimal_location": false,
   "labels_for_unlimited": ["netflix"]
}
```

**default\_licene\_id** - optional, long;

**default\_traffic\_limit** - optional, long

**application** - the remote config by platforms \(“android”, “ios”, “windows-desctop”, …\)

**support** - support emails for the “mystique” project

**allow\_login\_for\_blocked\_users** - allow login for blocked users

**bpl** - bypass list. Example: [internal.northghost.com/storage/project/project\_name/files/bpl/1a420b6f34466fc14bd88a814e9b31f153856d11](http://internal.northghost.com/storage/project/project_name/files/bpl/1a420b6f34466fc14bd88a814e9b31f153856d11)

**project\_name** - the actual carrier\_id 1a420b6f34466fc14bd88a814e9b31f153856d11 - the actual hash from remote config

**“server\_pool”:“pub-default”** - new geomapping, “pub-default” - pull name

**“private\_pools”:\[“pvt-1”, “pvt-2”\] - new geomapping, “pvt-1”** - private pull name

**“server\_group”: “touchvpn”** - the group of servers for grafana reports

“**disable\_optimal\_location”: false/true** diableenable selectiong optimal location, default false

**“labels\_for\_limited”:** list of profile labels for all users, for users without traffic limit, for users with traffic limit. For example, label “netflix” should enable netflix traffic offloading on VPN servers configured to support it.

