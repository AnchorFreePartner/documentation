# Authentication

Aura Partner VPN Backend supports OAuth authentication with a partner's OAuth server, this is a primary authentication method.

Steps to implement OAuth:

* Deploy and configure OAuth service. Service should be publicly available on the Internet.
* Configure Partner Backend to use OAuth service.
* Implement client OAuth for your application
* Retrieve access token in client app, this token will be used to initialize and sign in to Android Partner

There are some auth method types:

```
AuthMethod.anonymous();
AuthMethod.firebase(token); // should be configured when creating an app
AuthMethod.customOauth(token); // specific OAuth type, should be configured when creating an app
```

Login implementation example:

```
AuthMethod authMethod = AuthMethod.firebase(token);
sdk.getBackend().login(authMethod, new Callback<User>() {
   @Override
   public void success(User response) {
       
   }
   @Override
   public void failure(VpnException error) {
       
   }
});
```

