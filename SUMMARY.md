# Table of contents

* [What is Aura Developer Platform](README.md)

## Getting started

* [Sign up to Management Console](getting-started/sign-up-to-dev-console.md)
* [Create a new project](getting-started/add-a-new-project.md)
* [Switch projects](getting-started/switch-projects.md)
* [Change console settings](getting-started/change-console-settings.md)
* [Edit your profile](getting-started/edit-your-profile.md)
* [Keep exploring](getting-started/keep-exploring.md)

## Console details

* [Dashboard](console-details/project-dashboard/README.md)
  * [General](console-details/project-dashboard/general.md)
  * [Location loading](console-details/project-dashboard/location-loading.md)
* [Users](console-details/users/README.md)
  * [User page](console-details/users/user-page.md)
* [Active sessions](console-details/active-sessions.md)
* [Network](console-details/network-locations/README.md)
  * [Locations](console-details/network-locations/locations/README.md)
    * [Location details](console-details/network-locations/locations/location-details.md)
  * [Pools](console-details/network-locations/pools/README.md)
    * [Groups of pool](console-details/network-locations/pools/groups-of-pool.md)
* [Settings](console-details/project-settings/README.md)
  * [General](console-details/project-settings/general/README.md)
    * [Project config description \(JSON format\)](console-details/project-settings/general/project-config-description-json-format.md)
  * [Authentication methods](console-details/project-settings/user-authentification-methods/README.md)
    * [Auth Plugin requirements](console-details/project-settings/user-authentification-methods/auth-plugin-requirements.md)
  * [Payment methods](console-details/project-settings/user-payment-methods/README.md)
    * [Payments Plugin requirements](console-details/project-settings/user-payment-methods/custom-payments-plugin-requirements.md)
  * [VPN](console-details/project-settings/vpn/README.md)
    * [General](console-details/project-settings/vpn/general.md)
    * [VPN Bypass list](console-details/project-settings/vpn/vpn-bypass-list.md)
    * [Client Networks](console-details/project-settings/vpn/client-networks.md)
  * [Fireshield](console-details/project-settings/fireshield.md)
  * [Member](console-details/project-settings/members.md)
* [Export Data](console-details/export-data.md)
* [Log](console-details/logs.md)
* [Billing](console-details/billing.md)

## SDK

* [Unified VPN SDK for Android](sdk/vpn-sdk-for-android/README.md)
  * [Configuration](sdk/vpn-sdk-for-android/configuration.md)
  * [Usage](sdk/vpn-sdk-for-android/usage.md)
  * [CNL List](sdk/vpn-sdk-for-android/cnl-list.md)
  * [Fireshield\(Hydra transport\)](sdk/vpn-sdk-for-android/fireshield-hydra-transport.md)
  * [Traffic rules](sdk/vpn-sdk-for-android/traffic-rules.md)
  * [OpenVPN transport](sdk/vpn-sdk-for-android/openvpn-transport.md)
  * [Reconnection strategy](sdk/vpn-sdk-for-android/reconnection-strategy.md)
  * [Exceptions](sdk/vpn-sdk-for-android/exceptions.md)
  * [Version migration](sdk/vpn-sdk-for-android/version-migration.md)
  * [Changelog](sdk/vpn-sdk-for-android/changelog.md)
* [Hydra VPN SDK for iOS/macOS](sdk/hydra-vpn-sdk-for-ios/README.md)
  * [Changelog](sdk/hydra-vpn-sdk-for-ios/changelog.md)
* [IPSEC VPN SDK for iOS/macOS](sdk/ipsec-vpn-sdk-for-ios-macos.md)
* [Hydra SDK for Windows](sdk/hydra-sdk-for-windows.md)
* [Hydra VPN SDK for Routers](sdk/hydra-vpn-sdk-for-routers/README.md)
  * [SDK. Shared library.](sdk/hydra-vpn-sdk-for-routers/hydra-vpn-sdk-for-routers-sdk.md)
  * [Configuration Interface \(CI\)](sdk/hydra-vpn-sdk-for-routers/hydra-vpn-sdk-for-routers-ci/README.md)
    * [Unix Domain Sockets CI](sdk/hydra-vpn-sdk-for-routers/hydra-vpn-sdk-for-routers-ci/hydra-vpn-sdk-for-routers-ci-unix-domain.md)
    * [REST API CI](sdk/hydra-vpn-sdk-for-routers/hydra-vpn-sdk-for-routers-ci/hydra-vpn-sdk-for-routers-ci-rest-api.md)

## REST API

* [Partner API](https://backend.northghost.com/doc/partner/index.html)
* [User API](https://anchorfreepartner.github.io/apidocs/user.html)

## Sample applications <a id="demo-applications"></a>

* [Hydra VPN SDK demo for iOS](demo-applications/demo-unifysdk-ios.md)
* [IPSEC VPN SDK demo for iOS](demo-applications/ipsec-vpn-sdk-demo-for-ios.md)
* [Hydra VPN SDK demo for Android](demo-applications/anchorfree-hydra-vpn-sdk-demo-for-android.md)
* [Hydra VPN SDK demo for Windows](demo-applications/hydra-vpn-sdk-demo-for-windows.md)
* [OpenVPN SDK for Windows](demo-applications/openvpn-sdk-for-windows.md)

## Resources

* [Use cases](resources/use-cases/README.md)
  * [Public VPN](resources/use-cases/public-vpn.md)
  * [Business VPN](resources/use-cases/business-vpn/README.md)
    * [Creating a Business VPN Project](resources/use-cases/business-vpn/creating-business-vpn.md)
    * [Wi-Fi Security for Business](resources/use-cases/business-vpn/wifi-security-for-business.md)
  * [Fireshield](resources/use-cases/fireshield.md)
  * [Application anti-blocking](resources/use-cases/application-anti-blocking.md)
* [How-to](resources/how-to/README.md)
  * [Create a Firebase project for User Authentication](resources/how-to/create-the-firebase-project-for-user-authentication.md)
  * [AWS CloudFront Distribution of the Platform URL](resources/how-to/aws-cloudfront-distribution.md)
  * [How can I get Shared Secret key from iTunes Connect for In-App Purchase](resources/how-to/untitled.md)
* [FAQ](resources/faq/README.md)
  * [VPN Platform Flow](resources/faq/vpn-platform-flow.md)
  * [What data is collected by the Platform?](resources/faq/what-data-collect-the-platform.md)
  * [What analytic data is collected by your SDK?](resources/faq/what-analytic-data-collect-your-sdk.md)
  * [How the Platform restricts access to our data?](resources/faq/how-the-platform-restrict-access-to-our-data.md)
  * [Why DNS Leak tests often indicate that there is DNS Leak?](resources/faq/why-dns-leak-tests-often-indicate-that-there-is-dns-leak.md)

