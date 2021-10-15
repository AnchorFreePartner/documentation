# Do we need to perform endpoint health checks?

**Client**: neither VPN client nor routing rules shut down on themselves. If VPN conn goes down, traffic is still contained in buffers / TUN, and reconnect attempts are made. If they are unsuccessful, error is returned, but traffic is still contained (routing rules are still applied)

**Server**: we already have extensive monitoring and continuous testing of VPN servers on our side, any endpoint not functioning properly excluded from server discovery.
