# Application setup

### Create application project

First of all, you need to create an Xcode iOS/macOS application project.

### Install application SDK

Once application is created, you should link application SDK and prepare target. It can be done using CocoaPods or manually. We're providing SDK packed as `xcframework`, which means it can be used both for iOS and macOS apps.

#### [CocoaPods](https://guides.cocoapods.org/using/using-cocoapods.html)

```ruby
# Podfile
use_frameworks!

target 'YOUR_APP_TARGET_NAME' do
    pod 'VPNApplicationSDK'
end
```

Replace `YOUR_APP_TARGET_NAME` and then, in the `Podfile` directory, type:

```bash
$ pod install
```

#### Manual

1. Copy **VPNApplicationSDK.xcframework** file to some place inside your project folder on disk.
2. Go to _Project -> App Target -> General_ and drag copied framework to _Frameworks, Libraries and Embedded Content_ section.
3. Make sure framework is embed (you can check this option near framework name in the same section).
4. Link **NetworkExtension** system framework to your app target.
5. Go to _Project -> App Target -> Build Settings_ and:

* Set _Enable Bitcode_ to **NO**;
* [Add](https://developer.apple.com/library/content/qa/qa1490/\_index.html) `-ObjC` to _Other Linker Flags_.

1. Staying in the same place, perform _Import paths_ setting setup:

#### iOS

* Add `${PROJECT_DIR}/your-path-to-sdk/VPNApplicationExtendedSDK.xcframework/AdditionalModules/ios`
* Add `${PROJECT_DIR}/your-path-to-sdk/VPNApplicationExtendedSDK.xcframework/AdditionalModules/ios-simulator`
* Add `${PROJECT_DIR}/your-path-to-sdk/VPNApplicationExtendedSDK.xcframework/AdditionalModules/objc`
* Replace `your-path-to-sdk` with correct path inside your project on disk
* Select `recursive` for all paths

#### macOS

* Add `${PROJECT_DIR}/your-path-to-sdk/VPNApplicationExtendedSDK.xcframework/AdditionalModules/macos`
* Add `${PROJECT_DIR}/your-path-to-sdk/VPNApplicationExtendedSDK.xcframework/AdditionalModules/objc`
* Replace `your-path-to-sdk` with correct path inside your project on disk
* Select `recursive` for all paths

### Setup App ID

Next you need to perform all needed setup on [Apple developer portal](https://developer.apple.com).

#### Setup on developer portal

Go to _Apple developer portal->Certificates, Identifiers & Profiles->Identifiers_ and add new identifier for your app (or use an existing ID if you already have one). You should enable next capabilities:

* Personal VPN

#### Turn on capabilities in project

Go back to _Project -> App Target -> Signing and Capabilities_ and add the following capabilities:

#### iOS

* Personal VPN

#### macOS

* App Sandbox
  * Incoming Connections (Server)
  * Outgoing Connections (Client)
* Personal VPN

### Integration Checklist & Troubleshooting

Checklist that should help you to verify correct integration:

* **VPNApplicationSDK.framework** is added to the Application target.
* _Enable Bitcode_ is set to "No" and `-ObjC` is present in "Other linker flags" for Application target.
* _Import paths_ is configured inside build settings.
* Personal VPN (General > Capabilities) is enabled for Application target and App ID on developer portal.
