# What type of traffic Aura Protection and Fireshield is able to handle?

Aura Protect and Aura Fireshield capture all traffic routed to the TUN device. They can force DNS to use certain DNS servers, encrypt all user traffic and send it through the tunnel to the VPN concentrator, etc.

To provide selective routing and improve performance, Aura VPN products can selectively terminate specified traffic (for instance, TCP) on the local transparent proxy. This smart local proxy can then make a decision on how to route each content request: block, bypass or send to the remote secure proxy. All traffic not intercepted by this smart local proxy can also be either sent through the VPN tunnel or bypassed, but smart proxy provides a finer granularity of control.
