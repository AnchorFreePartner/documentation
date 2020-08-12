---
description: >-
  We need to be assured that Platform can restrict access to our data, and is
  only used by our users. How will this be accomplished?
---

# How the Platform restricts access to our data?

Our Platform is a multi-tenant system. Each project data is isolated and direct access is needed to work with the project data. There are 2 APIs for working with users' data of a project:

* \*\*\*\*[**User API**](https://backend.northghost.com/doc/user/index.html)  - this API is included into SDK and is useful in application client side. User API gives a user access to his data only. The key to data access is the "_access token_". Each user device should be registered in the project and get a unique "access token" \(`POST`[`/user/login`](https://backend.northghost.com/doc/user/index.html#!/user-controller/loginDevice)\). 

  SDK uses the device keychain to save the "_access token_" from theft.

* \*\*\*\*[**Partner API**](https://backend.northghost.com/doc/partner/index.html) - this API is used to manage all project data. This API is used in our Platform Console and can be used for any integration with your systems. Access the Partner API is implemented by login and password \(`POST`[`/partner/login`](https://backend.northghost.com/doc/partner/index.html#!/partner-controller/login)\). Where: the login is the _Project ID_, the password is the project _Private Key_. The _Private Key_ can be found in the _Settings_ of your project. Only the project members can see this _Private Key_ and have access to the project data. To manage the project members, see next document:

{% page-ref page="../../console-details/project-settings/members.md" %}

\_\_





