# Fireshield\(Hydra transport\)

## Categorization service \(aka Fireshield\) \(Hydra transport only\)

Unified SDK provides ability to categorize domains goes through VPN and perform specified action on them. To configure you need to create instance of **FireshieldConfig** and pass it to **SessionConfig.Builder** when starting vpn session

```text
final SessionInfo session = new SessionConfig.Builder()
                .withVirtualLocation(UnifiedSDK.COUNTRY_OPTIMAL)
                .withReason(TrackingConstants.GprReasons.M_UI)
                .withFireshieldConfig(createFireshieldConfig())
                .build();
sdk.getVPN().start(session, new CompletableCallback() {
    @Override
    public void complete() {

    }

    @Override
    public void error(@NonNull VpnException e) {

    }
});
```

### Create fireshield config

Categorization configuration based on specification of categories and rules for categories

To create categories you can use one of factory methods

* **FireshieldCategory.Builder.vpn** - will create category, with action VPN \( traffic \(encrypted\) goes through the tunnel as IP packets \)
* **FireshieldCategory.Builder.proxy** - will create category, with action proxy\(traffic \(encrypted\) goes through the tunnel just as payload \(for TCP only\)\)
* **FireshieldCategory.Builder.bypass** - will create category, with action bypass\(traffic goes directly to its destination, without vpn tunnel\)
* **FireshieldCategory.Builder.block** - will create category, with action block\(traffic gets blocked\)
* **FireshieldCategory.Builder.blockAlertPage** - will create category, with action block\(traffic gets blocked\) and redirection to Alert Page specified\(works for http only\)

To create category rules\(which domains gets to specified category\) you can use one of factory methods

* **FireshieldCategoryRule.Builder.fromAssets** - create category rules from file stored in **assets** folder
* **FireshieldCategoryRule.Builder.fromDomains** - create category rules from list of domains
* **FireshieldCategoryRule.Builder.fromFile** - create category rules from file on sdcard/internal storage

To addition to category file configuration its possible to use online categorization services

Possible values defined as constants in **FireshieldConfig.Services**

Alert page configuration

**AlertPage** static method create accepts two parameters: domain and path, on categorization action user will be redirected to \[https://domain/page?url=&lt;blocked\_url&gt;\]

```text

FireshieldConfig createFireshieldConfig(){
        FireshieldConfig.Builder builder = new FireshieldConfig.Builder();
        builder.enabled(true);
        builder.alertPage(AlertPage.create("connect.bitdefender.net", "safe_zone"))
        builder.addService(FireshieldConfig.Services.IP);
        builder.addService(FireshieldConfig.Services.SOPHOS);
        builder.addCategory(FireshieldCategory.Builder.vpn(FireshieldConfig.Categories.SAFE));//need to add safe category to allow safe traffic
        builder.addCategory(FireshieldCategory.Builder.block(FireshieldConfig.Categories.MALWARE));
        builder.addCategoryRule(FireshieldCategoryRule.Builder.fromAssets(FireshieldConfig.Categories.MALWARE,"malware-domains.txt"));
        return builder.build();
}


## Receive information about categorized domains

SDK will fire callback when transport detect access to configure rule.

```java
UnifiedSDK.addVpnCallListener(new VpnCallback() {
    @Override
    public void onVpnCall(@NonNull Parcelable parcelable) {
        if (parcelable instanceof HydraResource){
            // handle categorization information
        }
    }
});
```

SDK provides access to some categorization stats

```text
final FireshieldStats stats = new FireshieldStatus();
//get total scanned connections count
stats.getScannedConnectionsCount(new Callback<Integer>() {
    @Override
    public void success(@NonNull Integer integer) {

    }

    @Override
    public void failure(@NonNull VpnException e) {

    }
});
//get current session scanned connections count
stats.getSessionScannedConnectionsCount();

//reset total scanned connections count
stats.resetScannedConnectionsCount();
```

## 

