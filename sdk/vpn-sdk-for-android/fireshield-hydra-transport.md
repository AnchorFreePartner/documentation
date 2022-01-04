# Fireshield(Hydra transport)

## Categorization service (aka Fireshield) (Hydra transport only)

Unified SDK provides ability to categorize domains, goes through VPN and performs specified actions on them. To configureit, you need to create an instance of **FireshieldConfig** and pass it to **SessionConfig.Builder** when starting a VPN session:

```
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

### Creating a fireshield config

Categorization configuration based on specification of categories and rules for categories.

To create categories, you can use one of factory methods:

* **FireshieldCategory.Builder.vpn** - create a category with **VPN** action (traffic (encrypted) goes through the tunnel as IP packets )
* **FireshieldCategory.Builder.proxy** - create a category with **Proxy** action (traffic (encrypted) goes through the tunnel as a payload (for TCP only))
* **FireshieldCategory.Builder.bypass** - create a category with **Bypass** action (traffic goes directly to its destination, without a vpn tunnel)
* **FireshieldCategory.Builder.block** - create a category with **Block** action (traffic gets blocked)
* **FireshieldCategory.Builder.blockAlertPage** - create a category with **Block** action (traffic gets blocked) and a redirection to a specified Alert Page (works for HTTP only)

To create category rules (which domains get to specified category) you can use one of the factory methods:

* **FireshieldCategoryRule.Builder.fromAssets** - create category rules from file stored in **Assets** folder
* **FireshieldCategoryRule.Builder.fromDomains** - create category rules from the list of domains
* **FireshieldCategoryRule.Builder.fromFile** - create category rules from file on SD card/internal storage

To add to a category file configuration it's possible to use online categorization services.

Possible values are defined as constants in **FireshieldConfig.Services.**

### Alert page configuration

**AlertPage** static method accepts two parameters: domain and path, on categorization action user will be redirected to \[https://domain/page?url=\<blocked\_url>]

````

FireshieldConfig createFireshieldConfig(){
        FireshieldConfig.Builder builder = new FireshieldConfig.Builder();
        builder.enabled(true);
        builder.alertPage(AlertPage.create("connect.bitdefender.net", "safe_zone"))
        builder.addService(FireshieldConfig.Services.IP);
        builder.addService(FireshieldConfig.Services.BITDEFENDER);
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
````

SDK provides access to some categorisation stats

```
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
