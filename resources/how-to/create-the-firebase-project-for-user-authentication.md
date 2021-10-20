# Create a Firebase project for User Authentication

## Introduction to Firebase

Firebase was developed in 2011 to create and provide support for mobile and web applications. Later on, in 2014, it was acquired by Google. It gives you a number of facilities that can be used for the fast development of your applications. So, all you need to do is build applications quickly without thinking of managing infrastructure. There are a few products of Firebase that can be used in any applications but we will talk about _**Authentication**_ (It is used to authenticate the users of your applications).

## **Login and Authentication in Firebase**

Firebase authentication is used to authenticate the users of applications in a very easy manner. Not only for the users but for the developers also, it provides a very easy flow for the authentication and login process that is present in almost every application.

{% hint style="info" %}
Firebase supports authentication using email and password, phone numbers or even you can use facebook, google, twitter, github, etc.
{% endhint %}

To authenticate your users, all you need to do is get the authentication credentials from the user and then pass this credential to the Firebase Authentication SDK. These credentials can be email-password or mobile number or any token from identity providers like facebook, google, twitter, github, etc. After passing the credentials, Firebase will verify the credentials and in return, you will get a response that tells you if the authentication is successful or not.

This response you should use as parameter "_token_" of POST [`/user/purchase`](https://backend.northghost.com/doc/user/index.html#!/user-controller/sendPurchase) (same method in SDK) and `"type" = "firebase"`.

To use Firebase Authentication in our application and Platform project, you need to create a Firebase project and add this project to the Platform project as the Auth method. Following are the steps that are used to do it:

**Step 1:** Open the [Firebase Website](https://firebase.google.com) and login into it.

**Step 2:** After login, click on the "**Go To Console**" button that is present on the upper right side of the website. &#x20;

![](../../.gitbook/assets/firebase-login.png)

**Step 3:** If you don't have Firebase project for your application, click on "**Add Project**". &#x20;

![](../../.gitbook/assets/firebase-add-project.png)

**Step 4:** Enter the required details of the project and click on submit. &#x20;

![](../../.gitbook/assets/firebase-project-details.jpg)

**Step 5:** After creating a project, you will see the below image of your project dashboard. &#x20;

![](../../.gitbook/assets/firebase-dashboard.jpg)

Here, all the services of Firebase are shown and you can use any of them.

**Step 6:** In this blog, we are interested in the authentication part, so click on the "**Authentication**" button and then switch to "**Sign-in method**" tab. &#x20;

![](../../.gitbook/assets/firebase-signin-methods.jpg)

**Step 7:** In our example, we will sign-in by email. So, click on the edit button next to the "**Email/Password**" option and you will see the below screen. &#x20;

![](../../.gitbook/assets/firebase\_signin\_method.png)

{% hint style="info" %}
You can use any available sign-in method available in Firebase Authentication.
{% endhint %}

**Step 8:** Enable Email/Password sign-in and click on "**Save**". You are done with the Firebase part.

**Step 9: **Open Firebase project settings: &#x20;

![](../../.gitbook/assets/firebase\_settings.png)

**Step 10:** Found "_Web API Key_", for example  `Web API Key: "AIzaSyBAw-hTjky776yqQccP987654dbJas_Lb0"` and set it in to auth settings your "_firebase_" auth method in your Platform project:

```
{
   "firebase_api_key": "AIzaSyBAw-hTjky776yqQccP987654dbJas_Lb0"
}
```

see details:

{% content-ref url="../../console-details/project-settings/user-authentification-methods/" %}
[user-authentification-methods](../../console-details/project-settings/user-authentification-methods/)
{% endcontent-ref %}

**Step 11: **add the Firebase Authentication to your application. See official documentation:

{% content-ref url="create-the-firebase-project-for-user-authentication.md" %}
[create-the-firebase-project-for-user-authentication.md](create-the-firebase-project-for-user-authentication.md)
{% endcontent-ref %}

