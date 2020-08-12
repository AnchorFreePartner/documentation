# VPN Bypass list

Some traffic \(by domain\) can avoid the VPN tunnel and go to the Internet directly. To access the feature, add domains to this Bypass list.

## Actions

### Manually adding a single Domain

If you are going to add one domain to the Bypass list of your project, do the following:

1. Click "![](../../.gitbook/assets/plus_icon.jpeg)**Add**". A new line without a domain will be created in the list of domains.

![](../../.gitbook/assets/add_url_bypasslist.png)

  2. Enter the domain and then click **Add**. The domain will then be moved to the bottom of the list.

{% hint style="info" %}
 You can use special characters like "\*". For example: 

* `*.google.com` — all domains google.com
* `*.exploit.*` — all domains containing the`exploit`string
{% endhint %}

{% hint style="warning" %}
if your domain is incorrect, you will get the error message "**Domain is not valid**".  
{% endhint %}

  3. Repeat steps 2 and 3 for other domains.

  4. Click **Save** so that the changes are saved. As a result, you will see the form for approval of a new Bypass list.  

![](../../.gitbook/assets/save_bypasslist.png)

  5. Click **Save** to save all changes to your new VPN Bypass list, and then you will see the following window:  

![](../../.gitbook/assets/bypasslist_changes.png)

  6. You can close it \(click **Close**\) or download this log \(click **Download**\).

### **Adding multiple Domains**

  1. To add multiple domains, create a text file with domains in each line, for example:

```text
testURL2.com
example2.mm
example4.mn
!@#.fg
fhgk.com
```

  2. Click ![](../../.gitbook/assets/upload_icon.png) **Upload** and select the text file. You will see all domains in your Bypass list:

![](../../.gitbook/assets/upload_bypasslist.png)

{% hint style="warning" %}
If a domain is incorrect, you will see the error message "**Domain is not valid**" \(see domain _!@\#.fg_ in the screenshot above\).
{% endhint %}

  3. Click **Save** to save the changes. As a result, you will see a form of approval:  

![](../../.gitbook/assets/save_bypasslist.png)

  5. Click **Save** to save all changes to you new VPN Bypass list. As a result, you will see a form with the changes, for example:   

![](../../.gitbook/assets/log_vith_error_bypasslist.png)

{% hint style="info" %}
The incorrect domain will not be included in the new Bypass list \(see screenshot above\).
{% endhint %}

  6. You can close it \(click **Close**\) or download this log \(click **Download**\).

### **Deleting a domain**

  1. Click the ![](../../.gitbook/assets/delete_icon.png)button in the same line with a domain you want to remove. 

  2. Click **Save**. As a result, you will see a form of approval:  

![](../../.gitbook/assets/save_bypasslist.png)

  5. Click **Save** again. You will receive a verification form:   

![](../../.gitbook/assets/save2_bypasslist.png)

  6. Click **Close**.

### **Search**

If there is a large number of domains in the bypass list, the![](../../.gitbook/assets/search_icon.png)**Search domains** feature can be used to find a desired domain in the list.

### **Download** 

Click ![](../../.gitbook/assets/download_icon.webp) **Download**, and the list of domains will be downloaded to your device.

