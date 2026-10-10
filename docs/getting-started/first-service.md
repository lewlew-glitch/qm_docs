# Add your first service

Each connection needs three things:

1. **The service type**, such as Radarr, Jellyfin or Pi-hole.
2. **An address**, for example `http://192.168.1.20:7878`. You can add an *away* address later. See [Home and away](home-and-away.md).
3. **Credentials**, usually an API key and sometimes a username and password or a token.

!!! info "Free tier"
    The free tier connects **one service, fully**, with nothing held back. Pro unlocks the rest. See [Free and Pro](free-and-pro.md).

## Where to find API keys

The steps below are for common services. Menu names can change between versions, so check the service's own documentation if something has moved.

| Service | Where to find the key |
|---|---|
| Radarr / Sonarr / Lidarr / Prowlarr / Bazarr | **Settings → General → Security → API Key** |
| SABnzbd | **Config → General → API Key** (not the NZB Key) |
| qBittorrent | No key. Use your Web UI username and password |
| NZBGet | No key. Use ControlUsername and ControlPassword |
| Deluge | Leave the username blank and enter the password only |
| Plex | Tap **Sign in with Plex** |
| UniFi | **Control Plane → Integrations** with Network scope (UniFi OS, Network 9.3+) |
| Streamystats | Your Jellyfin login |
| Unraid (7.3+) | **Settings → Management Access → API Keys**, with the **CONNECT** and **ADMIN** roles |
| Jellyfin | **Dashboard → Advanced → API Keys** |
| Emby | **Advanced → API Keys** |
| Seerr (or Jellyseerr / Overseerr) | **Settings → General → API Key** |
| Tautulli | **Settings → Web Interface → API** |
| Home Assistant | **Profile → Security → Long-lived access tokens** |
| Grafana | **Administration → Service accounts** (a *Viewer* token is enough) |

If a service still won't connect, see the [FAQ](../reference/faq.md#a-service-wont-connect).

## Search for a service

In Command Centre, you can search by name or by what a service does. For example, `dns` finds Pi-hole, AdGuard Home and Technitium, and `ups` finds PeaNUT.
