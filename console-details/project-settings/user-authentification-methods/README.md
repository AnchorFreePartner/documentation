---
description: Find out how to manage authentication methods of your project
---

# Authentication methods

## Overview

{% hint style="warning" %}
The "Auth method" tab is visible for the project owner role only
{% endhint %}

![](../../../.gitbook/assets/screenshot-2021-10-04-at-7.34.50-pm.png)

{% hint style="info" %}
**Auth settings** column values are masked by default. You can reveal the real value by clicking on the ![](../../../.gitbook/assets/closed-eye.svg) button and hide it back by clicking on the ![](../../../.gitbook/assets/opened-eye.svg) button
{% endhint %}

## Methods

Client applications can use these methods for User authentication. See parameter "_auth\_method_" in SDK or REST API [_/user/login_](https://backend.northghost.com/doc/user/index.html#!/user-controller/loginDevice). Each project user should be registered in the project.&#x20;

The project can use more than one user authentication method. The Platform supports the following authentication methods:

### Anonymous

_anonymous_ - anonymous authentication method. A user device will be registered as an anonymous user without any additional details.&#x20;

{% hint style="info" %}
An anonymous user can be free or paid but additional devices cannot be added to this user account.
{% endhint %}

Auth Settings:

```
{}
```

### Firebase

_firebase_ - this user authentication method supports the Google Firebase Authentication Service.

This service supports different user sign-in methods - ![](../../../.gitbook/assets/email\_icon.png) _Email/password_, ![](../../../.gitbook/assets/phone\_icon.svg) _Phone,_ ![](../../../.gitbook/assets/google\_icon.svg) _Google_, ![](../../../.gitbook/assets/facebook\_icon.svg) _Facebook_, ![](../../../.gitbook/assets/mslive\_icon.svg) _Microsoft_, ![](../../../.gitbook/assets/apple\_icon.png) _Apple_ and more.&#x20;

{% hint style="info" %}
If a user signs in on 2 or more devices using the same account, all devices will be assigned to that user account. An authorized user can be free or paid (applies to all of his devices).
{% endhint %}

Auth Settings:

```
{
   "firebase_api_key": "AIzaSyBAw-hTjkyR78yqQccPVQHdNAdbJas_Lb0"
}
```

where "_firebase\_api\_key_" is the key of the Firebase project.  To learn how to create a Firebase project, refer to this:&#x20;

{% content-ref url="../../../resources/how-to/create-the-firebase-project-for-user-authentication.md" %}
[create-the-firebase-project-for-user-authentication.md](../../../resources/how-to/create-the-firebase-project-for-user-authentication.md)
{% endcontent-ref %}

### Custom methods

If you have a User authentication service, we can make a plugin and support your service for your projects. Requirements for the Plugin are listed here:

{% content-ref url="auth-plugin-requirements.md" %}
[auth-plugin-requirements.md](auth-plugin-requirements.md)
{% endcontent-ref %}

Please contact us if you have any questions about the Plugin.

## Actions

### Adding a new method

If you are going to add new user authentication method to the project you need to do the following:

1. Click the "![](../../../.gitbook/assets/plus\_icon.jpeg)**Add**" button. You will see a form that looks like this:

![Create authentication method dialog](../../../.gitbook/assets/add\_new\_auth.png)

Fill in the name of your authentication method. For anonymous method - "_anonymous_", for Firebase - "firebase", for custom -  _the name of your plugin_.

Then, you have to input the settings of the authentication method.

&#x20;  2\. Click "**New auth method**". As a result, this new authentication method should show up in the table, for example:

![Authentication methods settings overview](../../../.gitbook/assets/auth\_methods.png)

### Editing method parameters

If you are going to change settings of an existing authentication method, you need to do the following:

1. Select an authentication method and click the "![](../../../.gitbook/assets/edit\_icon.png)" button. You will see a form that looks like this:

![Edit authentication method dialog](../../../.gitbook/assets/edit\_auth\_settings.png)

&#x20; 2\. Edit the JSON and click "**Edit auth method**".&#x20;

### Delete method

If you are going to delete an existing authentication method, you need to do the following:

1. Select an authentication method you want to delete and click the "![](../../../.gitbook/assets/delete\_icon.png)" button. You will see a form that looks like this:

![Delete authentication method dialog](../../../.gitbook/assets/delete\_auth\_method.png)

&#x20;  2\. Click "**Delete auth method**".&#x20;

