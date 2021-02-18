# OpenVPN transport

## OpenVPN transport support

If your project TargetSDK is 29 and you use Google App Bundle for application distribution, add

```text
android.bundle.enableUncompressedNativeLibs=false
```

to your **gradle.properties** to make OpenVPN transport work on Android Q. If you are not using Google App Bundle, this step is not required.

To add OpenVPN transport support:

1. Add OpenVPN depencency to `build.gradle`:

```text
com.github.AnchorFreePartner.hydra-sdk-android:openvpn:{VERSION_NAME}
```

    2. Register both or one transport with SDK config:

```text
List<TransportConfig> transports = new ArrayList<>();
transports.add(HydraTransportConfig.create());
transports.add(OpenVpnTransportConfig.tcp());
UnifiedSDK.update(transportConfigs, callback);
```

    3. Specify transport on VPN start:

```text
final SessionInfo session = new SessionConfig.Builder()
                .withVirtualLocation(UnifiedSDK.COUNTRY_OPTIMAL)
                .withReason(TrackingConstants.GprReasons.M_UI)
                .withTransport(CaketubeTransport.TRANSPORT_ID_TCP)
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

## 

