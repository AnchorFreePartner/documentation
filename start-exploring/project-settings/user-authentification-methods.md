---
description: The list of User Authentication methods of the project.
---

# User Authentication methods

Client applications can use these methods for User authentication. See parameter "_auth\_method_" in SDK or REST API [_/user/login_](https://backend.northghost.com/doc/user/index.html#!/user-controller/loginDevice). Each project user should be registered in the project. 

The Platform support next Authentication methods:

### anonymous

_anonymous_ - anonymous authentication method. A user device will be registered as an anonymous user without any additional details. The anonymous user can be free or paid but not exist as a way to add additional devices to this user account.

Auth Settings:

```text
{}
```

### firebase

_firebase_ - this user authentication method sup\[port the Google Firebase Authentication Service:

{% page-ref page="user-authentification-methods.md" %}

This service support different of user sign-in methods - ![](../../.gitbook/assets/image%20%2828%29.png)_Email/password_, ![](../../.gitbook/assets/image.png)_Phone,_ ![](../../.gitbook/assets/image%20%281%29.png)_Google_, ![](../../.gitbook/assets/image%20%286%29.png)_Facebook_, ![](../../.gitbook/assets/image%20%284%29.png)_Microsoft_, ![](../../.gitbook/assets/image%20%288%29.png)_Apple_ and more.

Auth Settings:

```text
{
   "firebase_api_key": "AIzaSyBAw-hTjkyR78yqQccPVQHdNAdbJas_Lb0"
}
```

where "_firebase\_api\_key_" is the key of the Firebase project.  How to create a Firebase project: 

{% hint style="info" %}
test
{% endhint %}

{% page-ref page="../../resources/how-to/create-the-firebase-project-for-user-authentication.md" %}

### custom authentication methods

...

