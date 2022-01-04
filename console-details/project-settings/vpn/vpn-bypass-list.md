---
description: Configure domains available directly (without using VPN) by project users
---

# VPN Bypass list

Some traffic (by domain) can avoid the VPN tunnel and go to the Internet directly. To access the feature, add domains to this Bypass list.

## Actions

### Manually adding a single domain

If you are going to add one domain to the Bypass list of your project, do the following:

1. Click "![](../../../.gitbook/assets/plus\_icon.jpeg)**Add**". A new line without a domain will be created in the list of domains.

![VPN Bypass list overview](../../../.gitbook/assets/add\_url\_bypasslist.png)

&#x20; 2\. Enter the domain and then click **Add**. The domain will then be moved to the bottom of the list.

{% hint style="info" %}
&#x20;You can use special characters like "\*". For example:&#x20;

* `*.google.com` — all domains google.com
* `*.exploit.*` — all domains containing the`exploit`string
{% endhint %}

{% hint style="warning" %}
if your domain is incorrect, you will get the error message "**Domain is not valid**". &#x20;
{% endhint %}

&#x20; 3\. Repeat steps 2 and 3 for other domains.

&#x20; 4\. Click **Save** so that the changes are saved. As a result, you will see the form for approval of a new Bypass list. &#x20;

![Save domain list dialog](../../../.gitbook/assets/save\_bypasslist.png)

&#x20; 5\. Click **Save** to save all changes to your new VPN Bypass list, and then you will see the following window: &#x20;

![Successful domain list save dialog](../../../.gitbook/assets/bypasslist\_changes.png)

&#x20; 6\. You can close it (click **Close**) or download this log (click **Download**).

### **Adding multiple Domains**

&#x20; 1\. To add multiple domains, create a text file with domains in each line, for example:

```
testURL2.com
example2.mm
example4.mn
!@#.fg
fhgk.com
```

&#x20; 2\. Click ![](../../../.gitbook/assets/upload\_icon.png) **Upload** and select the text file. You will see all domains in your Bypass list:

![Multiple domains bypass list](../../../.gitbook/assets/upload\_bypasslist.png)

{% hint style="warning" %}
If a domain is incorrect, you will see the error message "**Domain is not valid**" (see domain _!@#.fg_ in the screenshot above).
{% endhint %}

&#x20; 3\. Click **Save** to save the changes. As a result, you will see a form of approval: &#x20;

![Save domain list dialog](../../../.gitbook/assets/save\_bypasslist.png)

&#x20; 5\. Click **Save** to save all changes to you new VPN Bypass list. As a result, you will see a form with the changes, for example:  &#x20;

![Successful domain list save dialog](../../../.gitbook/assets/log\_vith\_error\_bypasslist.png)

{% hint style="info" %}
The incorrect domain will not be included in the new Bypass list (see screenshot above).
{% endhint %}

&#x20; 6\. You can close it (click **Close**) or download this log (click **Download**).

### **Deleting a domain**

&#x20; 1\. Click the ![](../../../.gitbook/assets/delete\_icon.png)button in the same line with a domain you want to remove.&#x20;

&#x20; 2\. Click **Save**. As a result, you will see a form of approval: &#x20;

![Save domain list dialog](../../../.gitbook/assets/save\_bypasslist.png)

&#x20; 5\. Click **Save** again. You will receive a verification form:  &#x20;

![Successful domain list save dialog](../../../.gitbook/assets/save2\_bypasslist.png)

&#x20; 6\. Click **Close**.

### **Search**

If there is a large number of domains in the bypass list, the![](../../../.gitbook/assets/search\_icon.png)**Search domains** feature can be used to find a desired domain in the list.

### **Download**&#x20;

Click ![](../../../.gitbook/assets/download\_icon.webp) **Download**, and the list of domains will be downloaded to your device.
