# Home and away

Every service can have two addresses:

| Address | Used when | Example |
|---|---|---|
| **Local** | You're on your home network | `http://192.168.1.20:8096` |
| **Away** *(optional)* | You're anywhere else | `https://jellyfin.example.com` or a Tailscale address |

Quartermaster **always prefers the local address** and only falls back to the away address when local fails. A badge shows which one it's using:

| Badge | Meaning |
|---|---|
| **On your network** | Using the local address |
| **Remote** | Using the away address |
| **Via Tailscale** | Using a Tailscale address |
| **Unreachable** | Neither address answered |

## Home Wi-Fi

Set your **Home Wi-Fi (SSID)**. When you're on that exact network, the app uses the local address straight away without testing it first. Reading the Wi-Fi name needs **Location** permission. Without it, the app just tests the address instead.

## Network ranges

To add or change the IP ranges that count as "home", tap the **profile icon** (top right), then the **key icon**. You can change them at any time without a reset. A range only decides whether you're on your network. It doesn't affect whether a service is reachable.

!!! info "First LAN connection"
    iOS asks for **Local Network** permission the first time. If you said no, turn it on in **Settings → Quartermaster → Local Network**.

## Options for remote access

=== "Tailscale"

    Install Tailscale on your server and on your device, then use the server's `100.x` IP or MagicDNS name as the away address. Nothing is exposed to the internet.

    SABnzbd needs that hostname added to `host_whitelist` in **Config → Special**, or it returns 403.

=== "Reverse proxy"

    Put the service behind a reverse proxy with HTTPS, such as Caddy, Traefik, Nginx Proxy Manager or a Cloudflare Tunnel. Use the public HTTPS URL as the away address.

    A **Cloudflare Tunnel** works like any other address. **Cloudflare Access** blocks the API (`QM-EDGE-01`). To get past it, add an Access service token as `CF-Access-Client-Id` and `CF-Access-Client-Secret` custom headers under **Advanced**. The same applies to Authelia and other login gates: add a bypass rule, or send the proxy's credentials as headers.

=== "VPN"

    With WireGuard or another VPN back to your home network, the local address often works for both. Add an away address only if your VPN resolves names differently.

!!! warning
    Don't expose services to the internet over plain HTTP. Use HTTPS or a private network such as Tailscale.

## QM Companion addresses

When you create a [setup transfer](../companion/pairing.md) in QM Companion, you review each service's local and optional away address before sending it to the phone.
