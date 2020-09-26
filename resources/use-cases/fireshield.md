---
description: >-
  Fireshield feature protects users from web surfing blocking malware,
  untrusted, phishing, fraud, and online trackers website.
---

# Fireshield

Fireshield is a unique and fast technology that allows monitoring of all user's DNS requests in real-time. The main idea to get a response with full information about this domain. There is a minimal latency when checking DNS request. 

Why latency is minimal?

* Your developed VPN app has a White list. 
* The server-side has some levels of cache\(VPN node has its own cache, Fireshield server has a full database of websites\)

How can you use Fireshield technology?

* Malware and phishing protection
* Avoid getting ads

 All requests to tracker websites will be blocked.

* Parent control feature 

As a parent, you can control your kids' actions on the Internet. Fireshield knows the full information about the domain and the client application will display or not display the desired website depending on the user age.

* Government control feature

Develop your own VPN application that complies with government laws and regulations. 

* Organization control feature 

As a company owner or manager, you can limit access to a specific list of websites for your employees at work

* College and university control feature

As a principal of the college, you can limit access to a specific list of websites \(social networks\) for students during study time at college or university 

Android, iOS, and Win SDK support the Fireshield feature.

### **Technical details**

Fireshield works according to the tuned config on Pango Management Console. For example, if the user opens the untrusted website he will get the result that configured for this specific type of category.

**How to set up Fireshield config:**

1. Open Pango Management Console
2. Choose your Project 
3. Open Setting page, General tab
4. Enter valid JSON config to Config field

**Fireshield config example:**

```text
...
"fireshield": {
    "enabled": true,
    "services": [
      "bbss",
      "ip",
      "bitdefender"
    ],
    "alert_page": {
      "domain": "connect.bitdefender.net",
      "path": "safe_zone.html"
    },
    "categories": [
      {
        "category": "safe",
        "type": "proxy_peer"
      },
      {
        "category": "unsafe:malware",
        "type": "block_alert_page"
      },
      {
        "category": "unsafe:phishing",
        "type": "proxy_peer"
      },
      {
        "category": "unsafe",
        "type": "block_dns"
      },
      {
        "category": "unsafe:untrusted",
        "type": "bypass"
      },
      {
        "category": "unsafe:trackers",
        "type": "block_dns"
      },
      {
        "category": "custom",
        "type": "vpn"
      }
    ],
    "domains": {
      "unsafe:malware": [
        "franklang.ru"
      ],
      "unsafe:trackers": [
        "twitter.com"
      ],
      "unsafe:untrusted": [
        "myip.com"
      ],
      "unsafe:phishing": [
        "cnn.com"
      ],
      "custom": [
        "showmyip.com"
      ]
    }
  }
  ...
```

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key</th>
      <th style="text-align:left">Value</th>
      <th style="text-align:left">Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">enabled</td>
      <td style="text-align:left">
        <p>true</p>
        <p>false</p>
      </td>
      <td style="text-align:left">
        <p>True - Fireshield feature is ON</p>
        <p>False - Fireshield feature is OFF</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">alert_page</td>
      <td style="text-align:left">
        <p>&quot;domain&quot;: &quot;connect.bitdefender.net&quot;,</p>
        <p>&quot;path&quot;: &quot;safe_zone.html&quot;</p>
      </td>
      <td style="text-align:left">User will be redirected to this page (domain + path) if block_alert_page
        type is set up for category</td>
    </tr>
    <tr>
      <td style="text-align:left">categories</td>
      <td style="text-align:left">
        <p>{</p>
        <p>&quot;category&quot;: &quot;safe&quot;,</p>
        <p>&quot;type&quot;: &quot;proxy_peer&quot;</p>
        <p>}</p>
      </td>
      <td style="text-align:left">There is a list of categories and actions that we need to do with this
        particular category.</td>
    </tr>
    <tr>
      <td style="text-align:left">domains</td>
      <td style="text-align:left">
        <p><code>{ </code>
        </p>
        <p><code>&quot;unsafe:trackers&quot;: </code>
        </p>
        <p><code>[ &quot;twitter.com&quot; ] </code>
        </p>
        <p><code>}</code>
        </p>
      </td>
      <td style="text-align:left">There is a list of websites that we want to control ourself without using
        services</td>
    </tr>
    <tr>
      <td style="text-align:left">services</td>
      <td style="text-align:left">
        <p><code>&quot;bbss&quot;,</code>
        </p>
        <p><code> &quot;ip&quot;,</code>
        </p>
        <p><code> &quot;bitdefender&quot;</code>
        </p>
      </td>
      <td style="text-align:left">There is a services list that uses for categorizing entered domain Note: <em>ip</em> service
        should be added if you want to use <em>bitdefender </em>service</td>
    </tr>
  </tbody>
</table>

**More info about categories:**

| Name | Definition  |
| :--- | :--- |
| `"category": "safe"` | This category combines all safe \(good\) websites excluding malware, untrusted, phishing, and trackers |
| `"category": "unsafe"` | This category combines all unsafe \(bad\) websites including malware, untrusted, phishing, and trackers |
| `"category": "unsafe:malware"` | This subcategory of the unsafe category that combines just malware websites |
| `"category": "unsafe:untrusted"` | This subcategory of the unsafe category that combines just untrusted websites |
| `"category": "unsafe:trackers"` | This subcategory of the unsafe category that combines just trackers websites |
| `"category": "unsafe:phishing"` | This subcategory of the unsafe category that combines just phishing websites |
| `"category": "custom"` | This category allows you to add a custom site and find out what action you can do with it |

**Note:** It isn’t a full list of categories. It depends on connected service.

For example, for _securityzones_ service we have other categories: _unsafe:phish, unsafe:botnetcc, unsafe:porn, unsafe:badrep_

**More info about types:**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Definition</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>&quot;type&quot;: &quot;bypass&quot;</code>
      </td>
      <td style="text-align:left">It means that website go to the Internet behind, without using the VPN
        tunnel</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>&quot;type&quot;: &quot;vpn&quot;</code>
      </td>
      <td style="text-align:left">
        <p>It means that website go to the Internet through the VPN tunnel</p>
        <p><b>NOTE:</b> &quot;type&quot;: &quot;vpn&quot; doesn&apos;t support on
          iOS, we need to use only &quot;type&quot;: &quot;proxy_peer&quot;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>&quot;type&quot;: &quot;proxy_peer&quot;</code>
      </td>
      <td style="text-align:left">It means that website go to the Internet through the VPN tunnel with some
        addition Hydra implementation</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>&quot;type&quot;: &quot;block_dns&quot;</code>
      </td>
      <td style="text-align:left">It means that website will be blocked</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>&quot;type&quot;: &quot;block_alert_page&quot;</code>
      </td>
      <td style="text-align:left">
        <p>It means that website will be blocked and a tunned alert page will be
          displayed</p>
        <p>Note: It works just for HTTP websites (fo<b>r</b> example, <a href="http://franklang.ru/">franklang.ru</a>)</p>
      </td>
    </tr>
  </tbody>
</table>



