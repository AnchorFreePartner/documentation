# Why DNS Leak tests often indicate positive result?

Most DNS Leak services check address of recursive resolver for leak detection purposes. They show positive result when it is detects public DNS resolver or DNS resolver from different network from the client. Though it will be positive when there is actually client side DNS Leak, there is also possible to have false positive detection. 

We use Cloudflare recursive DNS resolvers on our VPN servers - DNS requests sent to them are anonymized and cannot be associated with specific client of VPN service. It is actually can be more secure in some cases then do recursive resolving directly from our servers - additional caching level mixing anonymized DNS requests from our customers with a lot of Cloudflare users worldwide.

