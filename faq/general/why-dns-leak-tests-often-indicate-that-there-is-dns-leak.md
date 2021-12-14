# Why DNS Leak tests often indicate positive result?

Most DNS Leak services check the address of the recursive resolver for leak detection purposes. They report a positive result when the system detects a public DNS resolver or DNS resolver from a different network. Though it will be positive when there is a client-side DNS Leak, it is also possible to have false-positive detections.

We use Cloudflare and Google recursive DNS resolvers on our VPN servers - DNS requests sent to them are anonymized and cannot be associated with a specific client of VPN service. It can be more secure than using recursive resolving directly from our servers. Additional caching level mixing anonymized DNS requests from our customers with other Cloudflare or Google users worldwide.
