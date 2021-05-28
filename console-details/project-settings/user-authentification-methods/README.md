---
description: The list of User Authentication methods of the project.
---

# Authentication methods

Client applications can use these methods for User authentication. See parameter "_auth\_method_" in SDK or REST API [_/user/login_](https://backend.northghost.com/doc/user/index.html#!/user-controller/loginDevice). Each project user should be registered in the project. 

The project can use more than one user authentication methods.

The Platform supports the following Authentication methods.

## Methods

### Anonymous

_anonymous_ - anonymous authentication method. A user device will be registered as an anonymous user without any additional details. 

{% hint style="info" %}
An anonymous user can be free or paid but additional devices cannot be added to this user account.
{% endhint %}

Auth Settings:

```text
{}
```

### Firebase

_firebase_ - this user authentication method supports the Google Firebase Authentication Service:

{% page-ref page="./" %}

This service supports different user sign-in methods - ![](../../../.gitbook/assets/email_icon.png) _Email/password_, ![](../../../.gitbook/assets/phone_icon.svg) _Phone,_ ![](../../../.gitbook/assets/google_icon.svg) _Google_, ![](../../../.gitbook/assets/facebook_icon.svg) _Facebook_, ![](../../../.gitbook/assets/mslive_icon.svg) _Microsoft_, ![](../../../.gitbook/assets/apple_icon.png) _Apple_ and more. 

{% hint style="info" %}
If a user signs in on 2 or more devices using the same account, all devices will be assigned to that user account. An authorized user can be free or paid \(applies to all of his devices\).
{% endhint %}

Auth Settings:

```text
{
   "firebase_api_key": "AIzaSyBAw-hTjkyR78yqQccPVQHdNAdbJas_Lb0"
}
```

where "_firebase\_api\_key_" is the key of the Firebase project.  To learn how to create a Firebase project, refer to this: 

{% page-ref page="../../../resources/how-to/create-the-firebase-project-for-user-authentication.md" %}

### Custom methods

If you have a User authentication service, we can make a plugin and support your service for your projects. Requirements for the Plugin are listed here:

{% page-ref page="auth-plugin-requirements.md" %}

Please contact us if you have any questions about the Plugin.

## Actions

### Adding a new method

If you are going to add new user authentication method to the project you need to do the following:

1. Click the "![](../../../.gitbook/assets/plus_icon.jpeg)**Add**" button. You will see a form that looks like this:

![](../../../.gitbook/assets/add_new_auth.png)

Fill in the name of your authentication method. For anonymous method - "_anonymous_", for Firebase - "firebase", for custom -  _the name of your plugin_.

Then, you have to input the settings of the authentication method.

   2. Click "**New auth method**". As a result, this new authentication method should show up in the table, for example:

![](../../../.gitbook/assets/auth_methods.png)

### Editing method parameters

If you are going to change settings of an existing authentication method, you need to do the following:

1. Select an authentication method and click the "![](../../../.gitbook/assets/edit_icon.png)" button. You will see a form that looks like this:

![](../../../.gitbook/assets/edit_auth_settings.png)

  2. Edit the JSON and click "**Edit auth method**". 

### Delete method

If you are going to delete an existing authentication method, you need to do the following:

1. Select an authentication method you want to delete and click the "![](../../../.gitbook/assets/delete_icon.png)" button. You will see a form that looks like this:

![](../../../.gitbook/assets/delete_auth_method.png)

   2. Click "**Delete auth method**". 



