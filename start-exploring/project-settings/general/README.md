---
description: Show us the project settings.
---

# General

### General parameters

* **Private Key** - the password of the Partner API.

For 'Login' you should use the Project ID. You can see the Project ID on the top left side like "_afdemo_" in this example:

![](../../../.gitbook/assets/image%20%283%29.png)

* **Company name** - text field with a company name of owner this project.
* **Type** - the project type. 
* **URL** - base URL of Platform. Often this URL blocked by governments. We recommend to cover this URL, see example:

{% page-ref page="../../../resources/faq/aws-cloudfront-distribution.md" %}

* **Bandwidth type** - The type of bandwidth limitation. By default, the type is "_By user_". It means the Platform will calculate the bandwidth amount like the sum of all a user devices bandwidth. Another Bandwidth type is "_By device_". The Platform will calculate the bandwidth amount separately per each user device. For details, connect to us.
* **Default Bandwidth limit \(Mb\)** -  you can use this parameter for set the daily bandwidth limit for new registered users. For example, if you set "100", new registered users will have 100MB daily limit. If this parameter will empty, new registered users will have unlimited daily limit.
* **Default License** - you can select default license for new registered users. Exist the list of licenses:

![](../../../.gitbook/assets/image%20%282%29.png)

Each license includes 2 parameters. The first parameter is the devices limit, the second parameter - the concurrent sessions limit \(not used more\). For example, the license "20-100" gives to user limits: 20 devices and 100 concurrent sessions. The "_default_" license gives to user unlimited devices and unlimited concurrent sessions.

* **Config** - you can see and change the specific project parameters \(JSON format\). Details:

{% page-ref page="project-config-description-json-format.md" %}

* **Optimal location** - the parameter switch on or switch off the "Optimal location" for this project. By default, this parameter switched on \("_enabled_"\). As a result, your application can ask credentials without parameter "location". The Platform will provide optimal \(nearest\) VPN-nodes for connecting. If this parameter "disabled", you should set location for any request of credentials. The request for credentials without the location parameter will return the error.
* **Network template** - not used more.
* **Description** - text description of the project. 
* **Icon** - you can set the icon for the project. You can see this icon in the projects list.

### Actions

* Upload image - 
* Save changes - 
* Delete project - 

