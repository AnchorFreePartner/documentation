---
description: >-
  We need to be assured that Platform can restrict access to our data, and only
  used by our users. How will they accomplish?
---

# How the Platform restrict access to our data?

Our Platform is a multi-tenant system. Each project data isolated and need access to work with project data. There are 2 API for work with users data of a project:

* \*\*\*\*[**User API**](https://backend.northghost.com/doc/user/index.html)  - this API included to SDK and useful in application client-side. User API gives a user access to his data only. The key to data access is the "_access token_". Each user device should be registered in the project and get a unique "access token" \(`POST`[`/user/login`](https://backend.northghost.com/doc/user/index.html#!/user-controller/loginDevice)\). 

  SDK uses the device keychain to save the "_access token_" for any discredit.

* \*\*\*\*[**Partner API**](https://backend.northghost.com/doc/partner/index.html) - this API attended to manage all project data. This API we are using in our Platform Console and you can use for any integration with your systems. Access to the Partner API implemented by login and password \(`POST`[`/partner/login`](https://backend.northghost.com/doc/partner/index.html#!/partner-controller/login)\). Where: the login is the _Project ID_, the password is the project _Private Key_. The _Private Key_ you can see in the _Settings_ of your project. Only project members can see this _Private Key_ and have access to project data. You can manage the project members, see next document:

{% page-ref page="../../console-details/project-settings/members.md" %}

\_\_





