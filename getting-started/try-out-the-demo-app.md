---
description: Get your hands on the real experience with the demo application
---

# Try out the demo app

## General

To get a better idea of the system, we suggest setting up and building a test iOS application, and then see the results of its work in the Management Console. 

You can get the latest demo Xcode project from the repository:

{% embed url="https://github.com/AnchorFreePartner/caketubesdk-demo-ios" %}

{% hint style="info" %}
Instructions from the README file can be omitted, since they have already been implemented in the latest version of the project
{% endhint %}

After you open the project in the Xcode, locate the _AppDelegate.swift_ file and fill the "**carrierId**" variable with the value of **ProjectID** for your project:

```text
CakeTube.instance().configure(CTConfig.create { (c) in
            c.baseUrl = "https://backend.northghost.com"
            c.carrierId = ""
            c.vpnProtocol = .ikEv2
            c.vpnProfileName = "CakeTubeSDK App"
        })
```

You can find the **ProjectID** value in the upper right corner of the Management Console, below the project name

![](../.gitbook/assets/screenshot-2021-06-08-at-19.28.14.png)

{% hint style="warning" %}
ProjectID is set on the project creation form and cannot be changed after that
{% endhint %}

Build the project and run it in the simulator. The running application should look like this:

![](../.gitbook/assets/screenshot-2021-06-08-at-17.26.43.png)

{% hint style="warning" %}
Be aware that simulation of iOS device does not support opening of the VPN sessions and is limited to log in function
{% endhint %}

Try to log in by clicking the respective button and take a look on the **Users** page of the Management Console:

![](../.gitbook/assets/screenshot-2021-06-08-at-17.09.35.png)

You can get a detailed information on the test user by clicking on the row:

![](../.gitbook/assets/screenshot-2021-06-08-at-17.09.45.png)

As you can see, the demo app successfully established connection with the oAuth server and acquired an access token:

![](../.gitbook/assets/screenshot-2021-06-08-at-17.10.01.png)

## Possible issues

* Due to the fact that Xcode and iOS versions are constantly updated, an error may occur:

> Building for iOS Simulator, but the linked and embedded framework was build for iOS + iOS Simulator

This problem can be fixed by setting the following value for the parameter "**Validate Workspace**" in the "**Build settings**" section of the _target_:

![](../.gitbook/assets/screenshot-2021-06-08-at-14.26.51.png)

* If you are building the project on the M1 Apple Silicon, you can also get another error:

> Building for iOS Simulator, but linking in dylib built for iOS

In order to fix it, you will need to add "**arm64"** into the "**Excluded Architecture**" of target's **Build settings**

{% hint style="info" %}
It would probably be missing in the list, you need to type it in
{% endhint %}

![](../.gitbook/assets/screenshot-2021-06-08-at-14.27.21.png)

