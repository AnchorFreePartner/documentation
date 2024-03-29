---
description: How to avoid blockage of backend.northghost.com domain
---

# AWS CloudFront Distribution of the Platform URL

Sometimes backend.northghost.com domain gets blocked by certain resources. To avoid that and make our app available globally, we need to hide backend.northghost.com under an AWS CloudFront Distribution.

1. Select CloudFront from the list of services in your [AWS Console](https://aws.amazon.com) or, simply type CloudFront into the AWS services search field on the main page.    &#x20;

![](../../.gitbook/assets/aws\_console.png)

&#x20;   2\. Then select **Create Distribution**. &#x20;

![](../../.gitbook/assets/cloudfront\_distribution.png)

&#x20;   3\. In the **Web** section select **Get Started**. &#x20;

![](../../.gitbook/assets/cloudfront\_web\_section.png)

&#x20;  4\. **Create Distribution** form:

A. **Origin Settings** part.

1. Type **backend.northghost.com** into the **Origin Domain Name** field.
2. Select **HTTPS Only** option in the **Origin protocol Policy**.
3. Leave the rest of the **Origin Settings** by default. &#x20;

![](../../.gitbook/assets/cloudfront\_origin\_settings.png)

B. Scroll down for **Default Cache Behavior Settings** part.

1. In **Viewer Protocol Policy** select **Redirect HTTP to HTTPS**.
2. In **Allowed HTTP Methods** select **GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE**.
3. In **Cache Based on Selected Request Headers** select **Whitelist**.
4. In **Whitelist Headers** add **Accept** and **Authorization** headers.
5. In **Forward Cookies** select **All**.
6. In **Query String Forwarding and Caching** select **Forward all, cache based on whitelist**. &#x20;

![](../../.gitbook/assets/cloudfront\_settings.png)

C. Leave by default **Distribution Settings** part.

D.   Scroll down and hit **Create Distribution** button .

It takes AWS about 10 minutes to create a distribution. Once it is complete you can find your CloudFront Distribution by clicking on your newly created distribution from the list and looking up its domain name. &#x20;

![](../../.gitbook/assets/cloudfront\_create\_distribution.png)

So next time, when you are using SDK, input newly generated distribution link as a base URL instead of backend.northghost.com. This will help to avoid blockage by 3rd parties resources.
