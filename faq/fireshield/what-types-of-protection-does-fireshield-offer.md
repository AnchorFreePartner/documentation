# What types of protection does Fireshield offer?

### Protection against malicious domains

Fireshield provides a decent level of protection against malicious domains \(same as DNS servers with RPZ blocklists\), but Fireshield is also able to block specific ports and protocols.

### Protection against malicious bare IP addresses

DNS blacklists are not able to protect in this case, but Fireshield has the full capability to block bare malicious IP.

Example: site example.com, which not in any blacklists got hacked and adversary injected an iframe or a redirect to the malicious site [http://123.123.123.123](http://123.123.123.123) with an exploit pack. IP address 123.123.123.123 is in the blacklists, but DNS infrastructure and DNS blocklists are not able to intercept and block this request, because the client will not perform any DNS resolving before sending requests to [http://123.123.123.123](http://123.123.123.123).

Fireshield will intercept TCP connection to 123.123.123.123:80 and check this IP address in blacklists before allowing this connection.

### Protection against malicious IP under safe domains

Fireshield currently is not able to detect such cases in bypass mode, because domain resolution and categorization \(blacklist checking\) performs in parallel to reduce latency and we do it only once for the domain. After the client receives information that example.com is safe and information that example.com resolves to 172.16.254.2 it performs connection without additional checks for that IP address.

However, in the full VPN mode, we are able to block connection to this IP address on the server-side. Fireshield client can also do categorization after resolving \(feature enhancement in development\).

Example: a malicious party with domain bad.com \(IP address 172.16.254.2\) got blacklisted, both domain bad.com and IP address 172.16.254.2. To bypass blacklisting, new domain bad2.com registered with the same IP address 172.16.254.2.  


