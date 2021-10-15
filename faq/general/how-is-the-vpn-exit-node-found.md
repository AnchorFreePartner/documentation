# How is the VPN exit node found?

From the client standpoint It is managed externally through the configuration file.

Clients request VPN servers from our backend API. We have dynamic discovery which provides five VPN servers (exit nodes) to clients based on client information, geoip, configured discovery rules and realtime server load.
