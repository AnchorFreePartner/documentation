# VPN Bypass list

Some traffic \(by domain\) can go to the internet directly outside the VPN tunnel.  To access the feature, add domains to this Bypass list.

## Actions

### Manually adding a Single domains

If you are going to add one domain to the Bypass list of you project you need to do next steps:

1. Click button "![](../../.gitbook/assets/plus_icon.jpeg)**Add**". A new line without a domain will be generated in the list of domains.

![](../../.gitbook/assets/add_url_bypasslist.png)

  2. Enter the domain and then click on the **Add** button. The domain will then be moved to the bottom of the list.

{% hint style="info" %}
 You can use special characters "\*". Example: 

* `*.google.com` — all domains google.com
* `*.exploit.*` — all domains containing the`exploit`string
{% endhint %}

{% hint style="warning" %}
if your domain will be incorrect, you will see the error message "**Domain is not valid**".  
{% endhint %}

  3. Repeat step 2 and 3 for other domains 

  4. Select the **Save** button so that the changes that were made are retained. As a result, you will see the form for approval new Bypass list.  

![](../../.gitbook/assets/save_bypasslist.png)

  5. Click the button **Save** for approval all changes you new VPN Bypass list. Like result you will see the form with the result of the Bypass list changes like this:  

![](../../.gitbook/assets/bypasslist_changes.png)

  6. You can close it \(click the button "**Close**"\) or download this log \(click the button "**Download**"\).

### **Adding Multiple domains**

  1. To add multiple domains, generate a text file with domains on each line. For example:

```text
testURL2.com
example2.mm
example4.mn
!@#.fg
fhgk.com
```

  2. Click on ![](../../.gitbook/assets/upload_icon.png) **Upload** and select the text file. You will see all domains in your Bypass list:

![](../../.gitbook/assets/upload_bypasslist.png)

{% hint style="warning" %}
if any domain is incorrect, you will see the error message "**Domain is not valid**" \(see domain _!@\#.fg_ in the screenshot\).
{% endhint %}

  3. Select the **Save** button so that the changes that were made are retained. As a result, you will see the form for approval new Bypass list.  

![](../../.gitbook/assets/save_bypasslist.png)

  5. Click the button **Save** for approval all changes you new VPN Bypass list. Like result you will see the form with the result of the Bypass list changes like this:   

![](../../.gitbook/assets/log_vith_error_bypasslist.png)

{% hint style="info" %}
The incorrect domain not included to the new Bypass list \(see screenshot\).
{% endhint %}

  6. You can close it \(click the button "**Close**"\) or download this log \(click the button "**Download**"\).

### **Deleting a domain**

  1. Click on the ![](../../.gitbook/assets/delete_icon.png)trash can that is one the line of the site that needs to be removed. 

  2. Select the **Save** button so that the changes that were made are retained. As a result, you will see the form for approval new Bypass list.  

![](../../.gitbook/assets/save_bypasslist.png)

  5. Click the button **Save** for approval all changes you new VPN Bypass list. Like result you will see the form with the result of the Bypass list changes like this:   

![](../../.gitbook/assets/save2_bypasslist.png)

  6. Click the button "**Close**".

### **Search**

If there are a large number of domains in the bypass list, the![](../../.gitbook/assets/search_icon.png)**Search domains** feature can be used to determine if the domain already exists in the list.

### **Download** 

If a list of the bypass is desired, click on ![](../../.gitbook/assets/download_icon.webp) **Download** and the list of the domains will be downloaded to your device.

