---
description: >-
  Your application can include paid functions. Usually, free users can only have
  a 50MB per day, while paid users usually have no traffic limit.
---

# Payment methods

## Purchase flow overview

### First purchase

* When a user is authorized and logged in your application, their user state is “free” with a traffic limit.
* A user purchases in-app subscription, e.g., in-app purchase on Android Play or Apple Store.
* The application calls a POST method [`/user/purchase`](https://backend.northghost.com/doc/user/index.html#!/user-controller/sendPurchase) \(the same method in SDK\) and sends a purchase receipt to the Platform.
* The Platform verifies the purchase in the Purchase service \(e.g., in Android Play or Apple Store\).
* If the purchase is valid, the Platform removes the traffic limit for the user.

### After the first purchase

* The Platform will call the Purchase service once a day per user to verify each purchase. 
* If the purchase is invalid, the traffic limit is returned for the user.

The process described above will be based on the Platform's _user\_id_, user's unique identifier.

## Payment methods in your project

{% hint style="info" %}
Each method should be registered in the project.
{% endhint %}

{% hint style="info" %}
Your project can use more than one Payment method.
{% endhint %}

The Platform supports the following Payment methods:

### ![](../../../.gitbook/assets/apple_icon.png) Apple

_apple_ - this method supports Apple In-App subscription. It is the standard method for iOS and macOS applications.

#### Required steps:

1. Make a Shared Secret key from iTunes Connect for In-App purchases. See the instruction:

{% page-ref page="../../../resources/how-to/untitled.md" %}

1. Add the "_apple_" method to your project settings. Example of payment method settings:

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

### ![](../../../.gitbook/assets/google_icon.svg) Google

_google_ - this method supports Google In-App subscription. It is the standard method for Android applications published in Google Play Store.

#### Required steps:

1. Create an API project from the API Access link in your Google Play console
2. Make a new service account, **save** the JSON private key that gets generated. You'll need to take this file to your server.
3. Press Done in the Play console's service account section to refresh and then grant access to the service account.
4. Get a google api client library for your server platform from [https://developers.google.com/api-client-library](https://developers.google.com/api-client-library)/.
5. Use your platform's client library to build a service interface and directly read the result of your purchase verification. 
6. Add the "_google_" method to your project settings. Example of payment method settings:

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

"_application_": "_AnchorFree-Backend/1.0_" - this parameter is constant.

"_credentials_" - this JSON block should be replaced with your JSON private key \(see step 2\).

### ![](../../../.gitbook/assets/huawei_icon.jpeg) Huawei

_huawei_ - this method supports Huawei In-App subscription. It is the standard method for Android applications published in the Huawei Store.

#### Necessary steps:

1. Set up Huawei IAP. Follow the official guideline: 

{% page-ref page="./" %}

1. Open the`agconnect-services.json` file. You need to find `client_id` and `client_secret` for the next step.
2. Add the "_huawei_" method to your project settings. Example of payment method settings:

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

1. Send a purchase request

   4.1. Make purchase as it is described in the doc:

{% page-ref page="./" %}

4.2. Parse the result and send the purchase to the server

```text
val purchaseResultInfo: PurchaseResultInfo = Iap.getIapClient(activity).parsePurchaseResultInfoFromIntent(data)
backendApi.purchase(purchaseResultInfo.inAppPurchaseData, "huawei", callback)
```

### ![](../../../.gitbook/assets/plugin_icon.webp) Custom methods

If you use another Payments service, we can make a plugin and support your service too. A new service can be one of the popular public services or your own custom service.

Requirements for the Plugin of a custom service on your side:

{% page-ref page="custom-payments-plugin-requirements.md" %}

Please contact us for any questions about Plugin.

## Actions

### Add new method

If you are going to add a new user payment method to the project, do the following:

1. Click the "![](../../../.gitbook/assets/plus_icon.jpeg)**Add**" button. You will see a form that looks like this:  

![](../../../.gitbook/assets/new_payment_method.png)

Fill the name and settings of your payment method.

1. Click "**New payments method**". The result can be seen in the table, for example:  

![](../../../.gitbook/assets/payment_methods.png)

### Edit method parameters

If you are going to change settings of an existing payment method, do the following:

1. Select a payment method and click the "![](../../../.gitbook/assets/edit_icon.png)" button. You will see a form that looks like this:  

![](../../../.gitbook/assets/edit_payment_settings.png)

1. Edit the JSON and click "**Edit payments method**". 

### Delete a method

If you are going to delete an existing payment method, do the following:

1. Select a payment method and click the "![](../../../.gitbook/assets/delete_icon.png)" button. You will see a form that looks like this:  

![](../../../.gitbook/assets/delete_payment_method.png)

1. Click "**Delete payments method**". 

