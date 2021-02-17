---
description: Supports Hydra and OpenVPN protocols
---

# Unified VPN SDK for Android

Current version:[![](https://camo.githubusercontent.com/96e035b772594b98ab503a86e2fb294d9a78044f/68747470733a2f2f6a69747061636b2e696f2f762f416e63686f7246726565506172746e65722f68796472612d73646b2d616e64726f69642e737667)](https://jitpack.io/#AnchorFreePartner/hydra-sdk-android)

## General

Android SDK is a part of Aura Partner SDK which contains client-side libraries and server-side applications needed to implement custom VPN infrastructure.

### Versioning convention

Android SDK versioning is in format MAJOR.MINOR.PATCH and should be associated with version in Jira. [See conventioning rules](https://semver.org/)

The Android SDK provides API containing:

* Classes and methods to authorize client users
* Ability to connect to backend VPN service

### Compatibility

Android min sdk version 15

### **Changelog**

SDK versions list is [**here**](changelog.md)\*\*\*\*

### Version Migration

For migration between versions, check [**this**](version-migration.md)\*\*\*\*

### Prerequisites

In order to be able to use the SDK, the following steps have to be done:

1. Register an account at [developer.aura.com](https://developer.aura.com/)
2. Create a project and use a name for your project as a Public key. Private key is optional.
3. Use SDK where `carrierId` equals given _Public Key_ and `baseUrl` equals _URL_ from the project details.

## Installing

To use this library, you should add **jitpack** repository.

Add this to root `build.gradle`

```text
allprojects {
    repositories {
        ...
        maven {
            url "https://jitpack.io"
        }
    }
}
```

And then  add dependencies in `build.gradle` of your app module. Version name is available at the top of this document.

```text
dependencies {

    implementation 'com.github.AnchorFreePartner.hydra-sdk-android:sdk:{VERSION_NAME}'

}
```

## Other Resources:

* [Configuration](configuration.md)
* [Usage](usage.md)
* [Client network list](cnl-list.md)
* [Fireshield](fireshield-hydra-transport.md)
* [Traffic rules](traffic-rules.md)
* [OpenVPN transport](openvpn-transport.md)
* [Reconnection](reconnection-strategy.md)
* [Exceptions](exceptions.md)

## Sample App

You can find source code of sample app with integrated sdk on [GitHub](https://github.com/AnchorFreePartner/hydrasdk-demo-android)

## Contact US

If you have problems integrating the sdk or found an issue, feel free to submit a bug to [GitHub](https://github.com/AnchorFreePartner/hydrasdk-demo-android/issues/new).

