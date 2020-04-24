---
description: The list of User Authentication methods of the project.
---

# User Authentication methods

Client applications can use these methods for User authentication. See parameter "_auth\_method_" in SDK or REST API [_/user/login_](https://backend.northghost.com/doc/user/index.html#!/user-controller/loginDevice). Each project user should be registered in the project. 

The project can use more than one user authentication methods.

The Platform support next Authentication methods:

### anonymous

_anonymous_ - anonymous authentication method. A user device will be registered as an anonymous user without any additional details. 

{% hint style="info" %}
The anonymous user can be free or paid but not exist as a way to add additional devices to this user account.
{% endhint %}

Auth Settings:

```text
{}
```

### firebase

_firebase_ - this user authentication method sup\[port the Google Firebase Authentication Service:

{% page-ref page="./" %}

This service support different of user sign-in methods - ![](../../../.gitbook/assets/email_icon.png) _Email/password_, ![](../../../.gitbook/assets/phone_icon.svg) _Phone,_ ![](../../../.gitbook/assets/google_icon.svg) _Google_, ![](../../../.gitbook/assets/facebook_icon.svg) _Facebook_, ![](../../../.gitbook/assets/mslive_icon.svg) _Microsoft_, ![](../../../.gitbook/assets/apple_icon.png) _Apple_ and more. 

{% hint style="info" %}
If a user sign-in 2 or more devices with the same sign-in account, all devices will be assigned to one user account. The authorized user can be free or paid \(applies to all of his devices\).
{% endhint %}

Auth Settings:

```text
{
   "firebase_api_key": "AIzaSyBAw-hTjkyR78yqQccPVQHdNAdbJas_Lb0"
}
```

where "_firebase\_api\_key_" is the key of the Firebase project.  How to create a Firebase project: 

{% page-ref page="../../../resources/how-to/create-the-firebase-project-for-user-authentication.md" %}

### custom methods

If you have a User authentication service, we can make a plugin and support your service for your projects. Requirements for the Plugin you can see:

{% page-ref page="auth-plugin-requirements.md" %}

Please contact us for any questions about Plugin.

