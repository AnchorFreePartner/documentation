# Defer VPN service initialisation

Add boolean resource to disable vpn service

```
<bool name="vpn_process_enabled">false</bool>
```

To enable service later:

```
PackageManager pm = context.getPackageManager();
pm.setComponentEnabledSetting(new ComponentName(context, AFVpnService.class), PackageManager.COMPONENT_ENABLED_STATE_ENABLED, PackageManager.DONT_KILL_APP);
```

