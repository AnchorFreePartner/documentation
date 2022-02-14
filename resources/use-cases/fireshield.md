---
description: >-
  Fireshield feature protects users from web surfing blocking malware,
  untrusted, phishing, fraud, and online trackers website.
---

# Fireshield

Fireshield is a unique and fast technology that allows monitoring of all user's DNS requests in real-time. The main idea to get a response with full information about this domain. There is a minimal latency when checking DNS request.&#x20;

Why latency is minimal?

* Your developed VPN app has a White list.&#x20;
* The server-side has some levels of cache(VPN node has its own cache, Fireshield server has a full database of websites)

How can you use Fireshield technology?

* Malware and phishing protection
* Avoid getting ads

&#x20;All requests to tracker websites will be blocked.

* Parent control feature&#x20;

As a parent, you can control your kids' actions on the Internet. Fireshield knows the full information about the domain and the client application will display or not display the desired website depending on the user age.

* Government control feature

Develop your own VPN application that complies with government laws and regulations.&#x20;

* Organization control feature&#x20;

As a company owner or manager, you can limit access to a specific list of websites for your employees at work

* College and university control feature

As a principal of the college, you can limit access to a specific list of websites (social networks) for students during study time at college or university&#x20;

Android, iOS, and Win SDK support the Fireshield feature.

### **Technical details**

Fireshield works according to the tuned config on Aura Management Console. For example, if the user opens the untrusted website he will get the result that is configured for this specific type of category.

**How to set up Fireshield config:**

1. Open Aura Management Console
2. Choose your Project&#x20;
3. Open Setting page, General tab
4. Enter valid JSON config to Config field

**Fireshield config example:**

```
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

| Key         | Value                                                                                                                    | Notes                                                                                                                                          |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| enabled     | <p>true</p><p>false</p>                                                                                                  | <p>True - Fireshield feature is ON</p><p>False - Fireshield feature is OFF</p>                                                                 |
| alert\_page | <p>"domain": "connect.bitdefender.net", </p><p>"path": "safe_zone.html"</p>                                              | User will be redirected to this page (domain + path) if block\_alert\_page type is set up for category                                         |
| categories  | <p>{ </p><p>"category": "safe",</p><p> "type": "proxy_peer" </p><p>}</p>                                                 | There is a list of categories and actions that we need to do with this particular category.                                                    |
| domains     | <p><code>{</code> </p><p><code>"unsafe:trackers":</code> </p><p><code>[ "twitter.com" ]</code> </p><p><code>}</code></p> | There is a list of websites that we want to control ourself without using services                                                             |
| services    | <p><code>"bbss",</code></p><p> <code>"ip",</code></p><p> <code>"bitdefender"</code></p>                                  | There is a services list that uses for categorizing entered domain Note: _ip_ service should be added if you want to use _bitdefender_ service |

**More info about categories:**

| Name                             | Definition                                                                                            |
| -------------------------------- | ----------------------------------------------------------------------------------------------------- |
| `"category": "safe"`             | This category combines all safe (good) websites excluding malware, untrusted, phishing, and trackers  |
| `"category": "unsafe"`           | This category combines all unsafe (bad) websites including malware, untrusted, phishing, and trackers |
| `"category": "unsafe:malware"`   | This subcategory of the unsafe category that combines just malware websites                           |
| `"category": "unsafe:untrusted"` | This subcategory of the unsafe category that combines just untrusted websites                         |
| `"category": "unsafe:trackers"`  | This subcategory of the unsafe category that combines just trackers websites                          |
| `"category": "unsafe:phishing"`  | This subcategory of the unsafe category that combines just phishing websites                          |
| `"category": "custom"`           | This category allows you to add a custom site and find out what action you can do with it             |

**Note:** It isn’t a full list of categories. It depends on connected service.

For example, for _securityzones_ service we have other categories: _unsafe:phish, unsafe:botnetcc, unsafe:porn, unsafe:badrep_

**More info about types:**

| Name                         | Definition                                                                                                                                                                                                        |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `"type": "bypass"`           | It means that website go to the Internet behind, without using the VPN tunnel                                                                                                                                     |
| `"type": "vpn"`              | <p>It means that website go to the Internet through the VPN tunnel</p><p><strong>NOTE:</strong> "type": "vpn" doesn't support on iOS, we need to use only "type": "proxy_peer"</p>                                |
| `"type": "proxy_peer"`       | It means that website go to the Internet through the VPN tunnel with some addition Hydra implementation                                                                                                           |
| `"type": "block_dns"`        | It means that website will be blocked                                                                                                                                                                             |
| `"type": "block_alert_page"` | <p>It means that website will be blocked and a tunned alert page will be displayed</p><p>Note: It works just for HTTP websites (fo<strong>r</strong> example, <a href="http://franklang.ru">franklang.ru</a>)</p> |

