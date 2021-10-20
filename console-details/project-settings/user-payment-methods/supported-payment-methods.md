# Supported payment methods

## Payment methods in your project

{% hint style="info" %}
Your project can use more than one payment method
{% endhint %}

The Platform supports the following payment methods:

### ![](../../../.gitbook/assets/apple\_icon.png) Apple

_apple_ - this method supports Apple In-App subscription. It is the standard method for iOS and macOS applications.

#### Required steps:

1. Make a Shared Secret key from iTunes Connect for In-App purchases. See the instruction:

{% content-ref url="../../../resources/how-to/untitled.md" %}
[untitled.md](../../../resources/how-to/untitled.md)
{% endcontent-ref %}

1. Add the "_apple_" method to your project settings. Example of payment method settings:

```
{
  "url": "https://buy.itunes.apple.com/verifyReceipt",
  "bundle": "com.youapps.vpnapp",
  "password": "3e646cc01cd56ce1b051888bacc0ffa4"
}
```

"_URL_" - URL for purchase receipt verification. Standard URL - "[_https://buy.itunes.apple.com/verifyReceipt_](https://buy.itunes.apple.com/verifyReceipt)".

"_bundle_" - the bundle of your iOS or macOS application. You can found it in your [appstoreconnect.apple.com](https://appstoreconnect.apple.com).

"_password_" - Shared Secret key from iTunes Connect for In-App Purchase (see step 1)

### ![](../../../.gitbook/assets/google\_icon.svg) Google

_google_ - this method supports Google In-App subscription. It is the standard method for Android applications published in Google Play Store.

#### Required steps:

1. Create an API project from the API Access link in your Google Play console
2. Make a new service account, **save** the JSON private key that gets generated. You'll need to take this file to your server.
3. Press Done in the Play console's service account section to refresh and then grant access to the service account.
4. Get a google API client library for your server platform from [https://developers.google.com/api-client-library](https://developers.google.com/api-client-library)/.
5. Use your platform's client library to build a service interface and directly read the result of your purchase verification.&#x20;
6. Add the "_google_" method to your project settings. Example of payment method settings:

```
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

"_credentials_" - this JSON block should be replaced with your JSON private key (see step 2).

### ![](../../../.gitbook/assets/huawei\_icon.jpeg) Huawei

_huawei_ - this method supports Huawei In-App subscription. It is the standard method for Android applications published in the Huawei Store.

#### Necessary steps:

1. Set up Huawei IAP. Follow the official guideline:&#x20;

{% content-ref url="./" %}
[.](./)
{% endcontent-ref %}

1. Open the`agconnect-services.json` file. You need to find `client_id` and `client_secret` for the next step.
2. Add the "_huawei_" method to your project settings. Example of payment method settings:

```
{
  "url": "https://subscr-dre.iap.hicloud.com",
  "client_id": "101123456",
  "client_secret": "8970db64cd9f11234567890c98eb80977393aadf553517aff812345678908bff"
}
```

"_URL_" - URL for purchase receipt verification. The standard URL of Huawei Store is "[_https://subscr-dre.iap.hicloud.com_](https://subscr-dre.iap.hicloud.com)".

"_client\_id_" - client id, can be found in `agconnect-services.json`

"client\_secret" - client secret, can be found in `agconnect-services.json`

1.  Send a purchase request

    4.1. Make a purchase as it is described in the doc:

{% content-ref url="./" %}
[.](./)
{% endcontent-ref %}

4.2. Parse the result and send the purchase to the server

```
val purchaseResultInfo: PurchaseResultInfo = Iap.getIapClient(activity).parsePurchaseResultInfoFromIntent(data)
backendApi.purchase(purchaseResultInfo.inAppPurchaseData, "huawei", callback)
```

### ![](../../../.gitbook/assets/plugin\_icon.webp) Custom methods

If you use another Payments service, we can make a plugin and support your service too. A new service can be one of the popular public services or your own custom service.

Requirements for the Plugin of a custom service on your side:

{% content-ref url="custom-payments-plugin-requirements.md" %}
[custom-payments-plugin-requirements.md](custom-payments-plugin-requirements.md)
{% endcontent-ref %}

Please contact us with any questions about the payment plugins
