---
description: The list of User Payment methods of the project.
---

# User Payments methods

Your application can include paid functions. For example, free users can have only a 100MB bandwidth limit per day but paid user - without any bandwidth limitation. To support this logic the application should provide to the Platform a purchase receipt for verification and registration.

There is the client-side method POST /user/purchase \(included in SDK methods too\) with parameter "type". This parameter decides what the user payment method used for user application. Each method should be registered in the project. 

The project can use more than one User Payment methods.

The Platform support next Payment methods:

### apple

_apple_ - this method support Apple In-App Purchases subscription. It is standard method for iOS and macOS applications. 

#### Necessary steps: 

1. Make a Shared Secret key from iTunes Connect for In-App Purchase. See the instruction how you can do it:

{% page-ref page="../../../resources/how-to/untitled.md" %}

   2. add the "_apple_" method to your project with settings. Example of Payment method Settings:

```text
{
  "url": "https://buy.itunes.apple.com/verifyReceipt",
  "bundle": "com.youapps.vpnapp",
  "password": "3e646cc01cd56ce1b051888bacc0ffa4"
}
```

"_url_" - URL for purchase receipt verification. Standard URL - "[_https://buy.itunes.apple.com/verifyReceipt_](https://buy.itunes.apple.com/verifyReceipt)".

"_bundle_" - the bundle of your iOS or macOS application. You can found it in your [appstoreconnect.apple.com](https://appstoreconnect.apple.com).

"_password_" -  Shared Secret key from iTunes Connect for In-App Purchase \(see step 1\)

### google

_google_ - this method support Google In-App subscription. It is standard method for Android applications published in the Google Play Store.

#### Necessary steps: 

1. Make an API project, from the API Access link in your Google Play console
2. Make a new service account, **save** the JSON private key that gets generated. You'll need to take this file to your server.
3. Press Done in the Play console's service account section to refresh and then grant access to the service account
4. Go get a google api client library for your server platform from [https://developers.google.com/api-client-library](https://developers.google.com/api-client-library)
5. Use your particular platform's client library to build a service interface and directly read the result of your purchase verification. 
6. add the "_google_" method to your project with settings. Example of Payment method Settings:

```text
{
  "credentials": {
    "type": "service_account",
    "project_id": "api-3333333333333333333-333333",
    "private_key_id": "3333333333333333333333333333333333333333",
    "private_key": "-----BEGIN PRIVATE KEY----- MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQC3eWGUsgiwXzEG ...= -----END PRIVATE KEY----- ",
    "client_email": "perchaseverification@api-8590733015157495171-576381.iam.gserviceaccount.com",
    "client_id": "110405678044800470496",
    "auth_uri": "https://accounts.google.com/o/oauth2/auth",
    "token_uri": "https://accounts.google.com/o/oauth2/token",
    "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
    "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/perchaseverification%40api-1111111115157495171-511181.iam.gserviceaccount.com"
  },
  "application": "AnchorFree-Backend/1.0"
}
```

"_application_": "_AnchorFree-Backend/1.0_" - the constant.

"_credentials_" -  this JSON block you should replace to your JSON private key \(see step 2\). 

### huawei

_huawei_ - this method support Huawei In-App subscription. It is standard method for Android applications published in the Huawei Store.

#### Necessary steps:

1. ...
2. .
3. add the "_huawei_" method to your project with settings. Example of Payment method Settings:

   ```text
   {
     "url": "https://subscr-dre.iap.hicloud.com",
     "client_id": "101123456",
     "client_secret": "8970db64cd9f11234567890c98eb80977393aadf553517aff812345678908bff"
   }
   ```

"_url_" - URL for purchase receipt verification. Standard URL of Huawei Store is "[_https://subscr-dre.iap.hicloud.com_](https://subscr-dre.iap.hicloud.com
)".

"_client\_id_" - 

"client\_secret" - 

### custom methods

If you use another Payments service, we can make a plugin and support your service too. The new service can be one of the popular public services or custom service in your side. 

Requirements for the Plugin of a custom service in your side you can see:

{% page-ref page="custom-payments-plugin-requirements.md" %}

Please contact us for any questions about Plugin.

