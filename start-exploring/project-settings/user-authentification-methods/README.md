---
description: The list of User Authentication methods of the project.
---

# User Authentication methods

Client applications can use these methods for User authentication. See parameter "_auth\_method_" in SDK or REST API [_/user/login_](https://backend.northghost.com/doc/user/index.html#!/user-controller/loginDevice). Each project user should be registered in the project. 

The project can use more than one user authentication methods.

The Platform support next Authentication methods.

## Methods

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

## Actions

### Add new method

If you are going to add new user authentication method to the project you need to do next steps:

1. Click button "![](../../../.gitbook/assets/plus_icon.jpeg)**Add**". You will see the new form like this:

![](../../../.gitbook/assets/add_new_auth.png)

Fill the name of your authentication method. For anonymous method - "_anonymous_", for Firebase - "firebase", for custom - _name of your plugin_.

Fill the settings of the authentication method.

   2. Click button "**New auth method**". Like result you can see this authentication method in the table, for example:

![](../../../.gitbook/assets/auth_methods.png)

### Edit method parameters

If you going to change settings of an existed authentication method, you need to do next steps:

1. Select authentication method and click the button "![](../../../.gitbook/assets/edit_icon.png)". You will see the new form like this:

![](../../../.gitbook/assets/edit_auth_settings.png)

  2. Edit setting JSON and click the button "**Edit auth method**". 

### Delete method

If you going to delete an existed authentication method, you need to do next steps:

1. Select authentication method for delete and click the button "![](../../../.gitbook/assets/delete_icon.png)". You will see the new form like this:

![](../../../.gitbook/assets/delete_auth_method.png)

   2. Click the button "**Delete auth method**". 



