---
description: >-
  Your application can include paid functions. Usually free users can have only
  a 100MB bandwidth limit per day but paid user - without any bandwidth
  limitation.
---

# User Payments methods

## Purchase overall flow

### First purchase

* When user is authorized and logged in your application, the default user state is “free” with bandwidth limit.
* A user to add purchase \(in-app subscription\) e.g., In-app purchase on the Android Play or Apple Store.
* The application call POST [`/user/purchase`](https://backend.northghost.com/doc/user/index.html#!/user-controller/sendPurchase) \(same method in SDK\) and send purchase receipt to Platform.
* The Platform verify the purchase against in Purchase service \(for example in Android Play or Apple Store\).
* If the purchase is valid, Platform to remove the bandwidth limit for this user.

### During use

* The Platform will call the Purchase service once a day per user to verify each purchase. 
* If invalid, the user will be converted to a limited user again.

Above process will be done based on Platform _user\_id_, user unique identifier.

## Payment methods in your project

{% hint style="info" %}
Each method should be registered in the project.
{% endhint %}

{% hint style="info" %}
Your project can use more than one Payment methods.
{% endhint %}

The Platform support next Payment methods:

### ![](../../../.gitbook/assets/apple_icon.png) apple

_apple_ - this method support Apple In-App Purchases subscription. It is standard method for iOS and macOS applications.

#### Necessary steps:

1. Make a Shared Secret key from iTunes Connect for In-App Purchase. See the instruction how you can do it:

{% page-ref page="../../../resources/how-to/untitled.md" %}

1. add the "_apple_" method to your project with settings. Example of Payment method Settings:

```text
{
  "url": "https://buy.itunes.apple.com/verifyReceipt",
  "bundle": "com.youapps.vpnapp",
  "password": "3e646cc01cd56ce1b051888bacc0ffa4"
}
```

"_url_" - URL for purchase receipt verification. Standard URL - "[_https://buy.itunes.apple.com/verifyReceipt_](https://buy.itunes.apple.com/verifyReceipt)".

"_bundle_" - the bundle of your iOS or macOS application. You can found it in your [appstoreconnect.apple.com](https://appstoreconnect.apple.com).

"_password_" - Shared Secret key from iTunes Connect for In-App Purchase \(see step 1\)

### ![](../../../.gitbook/assets/google_icon.svg) google

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

"_credentials_" - this JSON block you should replace to your JSON private key \(see step 2\).

### ![](../../../.gitbook/assets/huawei_icon.jpeg) huawei

_huawei_ - this method support Huawei In-App subscription. It is standard method for Android applications published in the Huawei Store.

#### Necessary steps:

1. Set up Huawei IAP. Follow official guideline: 

{% page-ref page="./" %}

   2. Open `agconnect-services.json` file. You need to find `client_id` and `client_secret` for the next step.

   3. Add the "_huawei_" method to your project with settings. Example of Payment method Settings:

```text
{
  "url": "https://subscr-dre.iap.hicloud.com",
  "client_id": "101123456",
  "client_secret": "8970db64cd9f11234567890c98eb80977393aadf553517aff812345678908bff"
}
```

"_url_" - URL for purchase receipt verification. Standard URL of Huawei Store is "[_https://subscr-dre.iap.hicloud.com_](https://subscr-dre.iap.hicloud.com%20)".

"_client\_id_" - client id, can be found in `agconnect-services.json`

"client\_secret" - client secret, can be found in `agconnect-services.json`

   4. Send purchase request

   4.1. Do purchase as it described in the doc: 

{% page-ref page="./" %}

  4.2. Parse result and send purchase to the server 

```text
val purchaseResultInfo: PurchaseResultInfo = Iap.getIapClient(activity).parsePurchaseResultInfoFromIntent(data)
backendApi.purchase(purchaseResultInfo.inAppPurchaseData, "huawei", callback)
```

### ![](../../../.gitbook/assets/plugin_icon.webp) custom methods

If you use another Payments service, we can make a plugin and support your service too. The new service can be one of the popular public services or custom service in your side.

Requirements for the Plugin of a custom service in your side you can see:

{% page-ref page="custom-payments-plugin-requirements.md" %}

Please contact us for any questions about Plugin.

## Actions

### Add new method

If you are going to add new user payment method to the project you need to do next steps:

1. Click button "![](../../../.gitbook/assets/plus_icon.jpeg)**Add**". You will see the new form like this:  

![](../../../.gitbook/assets/new_payment_method.png)

Fill the name and settings of your payment method.

   2. Click button "**New payments method**". Like result you can see this method in the table, for example:  

![](../../../.gitbook/assets/payment_methods.png)

### Edit method parameters

If you going to change settings of an existed payment method, you need to do next steps:

1. Select payment method and click the button "![](../../../.gitbook/assets/edit_icon.png)". You will see the new form like this:  

![](../../../.gitbook/assets/edit_payment_settings.png)

  2. Edit setting JSON and click the button "**Edit payments method**". 

### Delete method

If you going to delete an existed payment method, you need to do next steps:

1. Select payment method for delete and click the button "![](../../../.gitbook/assets/delete_icon.png)". You will see the new form like this:  

![](../../../.gitbook/assets/delete_payment_method.png)

   2. Click the button "**Delete payments method**". 



.

