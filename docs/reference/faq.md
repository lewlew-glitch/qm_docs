# FAQ

Answers to the questions we get most on [Discord](https://discord.gg/ecFz4WsVVB). For error codes, see [Error codes](error-codes.md).

## Connecting and networking

??? question "What do the four connection test stages mean?"
    The test checks **Address → Reachable → Authenticated → Version**, in that order, and stops at the first failure. The `QM-` code it shows tells you exactly which layer to fix. See [Error codes](error-codes.md).

??? question "It fails at Authenticated. Is my address wrong?"
    No. The host answered fine.

    - **401:** the key is wrong or mistyped. Copy it again.
    - **403:** a proxy or Cloudflare Access is stripping the key, or the key doesn't have permission.

??? question "It fails at Reachable. Why can't it reach the service?"
    There was no HTTP answer at all. Check that:

    - `http` vs `https` matches what the service uses
    - you're on a network that can see it (Wi-Fi or Tailscale)
    - the port is right

    Your first LAN connection also needs **Settings → Quartermaster → Local Network** turned on in iOS.

??? question "Where do I add another network or IP range after setup?"
    Tap the **profile icon** (top right), then the **key icon**. You can add, edit or remove ranges at any time without a reset. A range only decides "is this my network". It doesn't affect whether a service is reachable.

??? question "How does it choose between the home and away address?"
    It always prefers the local address and only falls back to the remote one when local fails. A badge shows which it's using: **On your network**, **Remote**, **Via Tailscale** or **Unreachable**. See [Home and away](../getting-started/home-and-away.md).

??? question "What does setting a Home Wi-Fi (SSID) do?"
    When you're on that exact Wi-Fi network, the app uses the local address straight away without testing first. Reading the Wi-Fi name needs **Location** permission. If you skip it, the app just tests the address instead.

??? question "How do I reach my stack from anywhere with Tailscale?"
    Install Tailscale on your phone and your server, then use the server's `100.x` IP or MagicDNS name as the remote address.

    !!! note
        SABnzbd needs that hostname added to its whitelist, or it returns 403. See [SABnzbd won't connect](#a-service-wont-connect).

??? question "What's the difference between Cloudflare Tunnel and Cloudflare Access?"
    - **Tunnel** is just another address and works normally.
    - **Access** is a login gate that blocks the API (`QM-EDGE-01`). To fix it, create an Access **service token** and save its `CF-Access-Client-Id` and `CF-Access-Client-Secret` headers once per domain in your profile's credentials (profile icon → **Profiles** → **key icon** → **Edge access by domain**). Every service on that domain then uses them automatically. See [Get past Cloudflare Access](../tutorials/cloudflare-access.md).

??? question "My service has a self-signed certificate. How do I trust it?"
    Many self-hosted consoles ship with a self-signed certificate, such as Proxmox on `:8006`, Portainer on `:9443` and UniFi. iOS won't accept one automatically, so the first connection fails at **Reachable** with a TLS error. When it's a certificate Quartermaster can pin, it offers a **trust prompt** (`QM-TLS-02`) instead.

    The prompt shows the certificate's **SHA-256 fingerprint**, plus its issuer, subject and expiry. Check the fingerprint against what your server actually presents, then tap **Trust** to pin that exact certificate. From then on the connection is only trusted while the certificate keeps matching. This is *trust on first use*, the same model SSH uses.

    !!! warning "TrueNAS"
        TrueNAS can't use the trust prompt, because its WebSocket connections can't use certificate pinning. Use HTTPS with a certificate your device already trusts.

        Quartermaster **blocks plain-HTTP TrueNAS API-key connections** before sending the key, because TrueNAS can revoke keys it receives insecurely. If you use a reverse proxy, make its connection to TrueNAS HTTPS too. A public HTTPS address alone doesn't secure that leg.

??? question "Why does it warn that the certificate changed?"
    The pinned certificate no longer matches (`QM-TLS-03`). Usually that's a renewed certificate or a rebuilt container, but it could mean someone is intercepting the connection. Only trust it again if you were expecting the change.

??? question "It connects but fails with 404 or a Version error. Is the service down?"
    Not necessarily.

    - **404** is often a missing subpath in your URL. Add it, for example `/radarr`.
    - **A Version error** means a proxy or SSO login page is answering instead of the service. Point the address directly at the service.

??? question "What does “Cloudflare is rate-limiting, backed off” (QM-EDGE-02) mean?"
    The app is deliberately backing off so Cloudflare doesn't block your address. Relax bot protection for that hostname, or connect over Tailscale or your LAN instead.

??? question "Connects at home but not away (or the other way round)?"
    The missing address, local or external, needs to be added or corrected in that service's connection settings. For remote access without opening ports, use Tailscale or a Cloudflare Tunnel.

??? question "Do I have to expose my servers to the internet?"
    No. At home the app talks over your LAN, and nothing needs to face the internet. For access from anywhere without opening ports, add a Tailscale or Cloudflare Tunnel address.

## A service won't connect

??? question "Radarr, Sonarr, Prowlarr, Lidarr or Bazarr rejects the connection"
    These use an **API key** (**Settings → General → Security**), not a username and password.

    - **401:** wrong key
    - **404:** missing URL Base or subpath
    - **403:** something in front of the service is stripping the key

??? question "Plex won't sign in, or sharing says I'm not the owner"
    Tap **Sign in with Plex**. It uses Plex's official PIN sign-in, so you don't need a manual token. For sharing or invite errors, sign in with the account that actually owns the server.

??? question "Jellyfin or Emby rejects my key (or I don't have one)"
    They need a **server API key**, not your login. An admin creates one under **Advanced → API Keys**. If a proxy strips the header, add `Authorization: MediaBrowser Token="<key>"` as a custom header under **Advanced**.

??? question "SABnzbd won't connect"
    Use the full **API Key** (**Config → General**), not the NZB Key.

    "Blocked this hostname" comes from SABnzbd's DNS-rebinding protection. Add your hostname to `host_whitelist` in **Config → Special**.

??? question "qBittorrent won't connect"
    There's no API key. Sign in with your **Web UI username and password**, and turn on the Web UI first under **Tools → Options**.

??? question "Deluge shows Authenticated with a cross, but its log says login succeeded"
    Your password is fine. Leave the username **blank** and enter only the password. The session cookie isn't carrying over, which is a known issue we're fixing. In the meantime, connect directly to `host:8112` rather than through a proxy.

??? question "NZBGet won't connect"
    NZBGet uses HTTP Basic auth with the **ControlUsername** and **ControlPassword** from NZBGet's settings. The defaults are `nzbget` / `tegbzn6789`, so change them. Check that any proxy passes Basic credentials through.

??? question "Tautulli won't connect"
    The API key is under **Settings → Web Interface → API**. A blank version number just means no Plex server is linked yet. It isn't a connection fault.

??? question "UniFi won't connect"
    You need **UniFi OS with Network 9.3 or later**. Create the key under **Control Plane → Integrations** with **Network** scope. A Site Manager cloud key won't work. Expect a self-signed certificate trust prompt.

??? question "Streamystats won't connect or shows no data"
    Streamystats uses your **Jellyfin login**, not its own key, so a Streamystats problem is often a Jellyfin login problem. Deep Stats also needs the Jellyfin account to be an admin.

??? question "Glances connected, but the Docker card shows no containers"
    Glances needs the Docker socket mounted. Add this to the container and restart it:

    ```
    -v /var/run/docker.sock:/var/run/docker.sock:ro
    ```

    If Portainer or Dockhand is connected, it's used as the container source instead.

??? question "How do I connect Unraid?"
    You need **Unraid 7.3 or later**.

    1. In Unraid, go to **Settings → Management Access → API Keys**.
    2. Create a key with the **CONNECT** and **ADMIN** roles.
    3. In Quartermaster, add Unraid with your server's address and paste the key.

??? question "Unraid refuses to start or stop a container or VM"
    Quartermaster shows the reason, including which permission is missing. Check the API key has the **CONNECT** and **ADMIN** roles under **Settings → Management Access → API Keys**.

??? question "My key is definitely correct, but I get a 403 or a login page"
    It's not your key. A proxy or edge service (Cloudflare Access, Authelia, nginx) is intercepting the request. Add a bypass rule for the API, or send the proxy's own credentials as custom headers under **Advanced**.

??? question "AdGuard Home on a router (GL.iNet) has no username or password"
    Leave both fields empty and tap **Test**. Router-hosted AdGuard Home is open by default. Only fill in credentials if you set up your own login.

??? question "Which Gluetun API routes does Quartermaster need?"
    - `GET /v1/vpn/status`
    - `GET /v1/publicip/ip`
    - `GET /v1/openvpn/portforwarded`
    - `GET /v1/version`

    Add `PUT /v1/vpn/status` if you want the restart button to work.

??? question "Can I get a terminal for my Proxmox VMs and containers?"
    Not in the app yet. Use **Open console in browser** from each VM's or container's row menu. You need to already be signed in to Proxmox in that browser.

??? question "How do I connect a machine over SSH?"
    Add an **SSH** service and fill in:

    - **Host:** the machine's LAN IP or private DNS name. You can tap one of your saved addresses to fill it in.
    - **Port:** usually `22`
    - **Username:** the account you'd type after `ssh`, as in `root@tower`
    - **Sign in with:** **Password**, **Key** or **Tailscale**. A key is safer wherever your server allows one. Passwords are kept in the device keychain and only sent to that host.

    For access when you're away, add a **remote** host under **Remote access**, such as a Tailscale address, a VPN or a forwarded TCP port.

??? question "Why does SSH ask about a host key the first time I connect?"
    That fingerprint is the only thing that proves the machine answering is really your server, and not something sitting in the middle of the connection. Quartermaster won't connect to a host it hasn't been told to trust, and there's no option to accept whatever turns up.

    Check it rather than tapping through. On the server, run:

    ```
    ssh-keygen -lf /etc/ssh/ssh_host_*_key.pub
    ```

    Find the `SHA256:` line for the key type the app shows. It must match character for character. Tap **Trust and connect**, and you won't be asked again for that host and port. After that, a different key **stops the connection**. If you weren't expecting the key to change, don't trust it.

??? question "Can I sign in with a key, and why is my RSA key refused?"
    Keys work, but only **ed25519** keys at the moment. Paste the **private** key (the file that begins with `-----BEGIN OPENSSH PRIVATE KEY-----`, not the `.pub` one) and add its passphrase if it has one. Passwords work too, if your server still allows them.

    RSA isn't supported yet. The SSH library Quartermaster uses, Apple's swift-nio-ssh, doesn't implement RSA, and the alternative relies on an unreviewed fork that changes how host identity is checked. That isn't something to route a root password through, so the app says so plainly rather than failing vaguely.

    Making an ed25519 key takes one line:

    ```
    ssh-keygen -t ed25519 -C "iphone"
    ```

    Add the public half to `~/.ssh/authorized_keys` on the server, then paste the private half into Quartermaster. Consider giving the phone its own key rather than reusing your desktop's, so you can revoke it on its own.

??? question "It says the server and the terminal couldn't agree on how to secure the connection"
    That happens **before** any sign-in, so your password or key was never tried and isn't the problem.

    The terminal supports a small set of modern algorithms: **Curve25519** or **ECDH** key exchange, **AES-GCM** encryption, and **Ed25519** or **ECDSA** host keys. A standard OpenSSH server offers all of them. A server hardened down to other algorithms, or a **Dropbear** server on a router or small device, may share none of them.

    To see what your server offers, run this on it:

    ```
    sshd -T | grep -E '^(ciphers|kexalgorithms|hostkeyalgorithms) '
    ```

    If AES-GCM, Curve25519 or Ed25519 is missing, adding it back (usually in a file under `/etc/ssh/sshd_config.d/`) lets the terminal connect. The server's own log says the same from its side: a line starting `Unable to negotiate` names exactly what it couldn't match.

??? question "Where does my SSH password or key actually live?"
    In the iPhone's **keychain**, like every other credential in the app, and never in ordinary app storage. It's sent to one place only, the server you added it for, over the encrypted SSH connection. There's no account, no relay and no server of ours involved, and nothing about a session leaves your phone.

    Only the part that has to reach the native SSH code does so, and only in memory for the connection being made. Commands you've run are kept on the device for the history list, with anything that looks like a credential removed.

??? question "What can the terminal do, and what can't it?"
    It opens a real SSH session and runs commands you type or save, showing their output. That covers most of what people reach for a laptop to do: restart a container, check a disk, tail a log, run an update.

    It's a **console, not a full terminal emulator**, so it won't run anything that takes over the whole screen. `htop`, `top`, `vim`, `nano` and `less` are detected and reported as needing a full terminal, rather than drawn as nonsense.

    Each command runs **in its own session**, so nothing carries over from one to the next. That means `cd` doesn't persist: run `cd /var/log` on its own and the next command still starts in your home directory. Chain them instead:

    ```
    cd /var/log && tail -n 50 syslog
    ```

    The upside is that a stuck command can never affect the next one, and **Stop** really stops what's running rather than leaving it orphaned on the server.

    Open **Commands** for an **Interactive shell**, or run a one-tap command:

    - Show free space, memory use, or uptime and load
    - Show the busiest processes, failed services, or who is signed in
    - Show a disk SMART report
    - Check for updates on Debian or Ubuntu, or on Fedora or RHEL (these install nothing)
    - **Restart a service** or **Reboot the host**, marked :warning: because they interrupt what's running

??? question "Can I use SSH through Cloudflare Access?"
    No. Cloudflare Access SSH hostnames that need the `cloudflared` client aren't supported. Use a direct address instead: Tailscale, Cloudflare WARP, a VPN or private route, or a forwarded TCP port.

## Notifications and alerts

??? question "How do notifications work? What are my options?"
    There are two paths:

    1. **Instant alerts, your way** *(free)*. Quartermaster sets up a connection in Sonarr, Radarr or Seerr that sends straight to your own **ntfy**, **Pushover**, **Discord** or **Telegram**.
    2. **Push notifications** *(Pro)*. Alerts go through Quartermaster's relay and arrive even when the app is closed.

    See [Alerts](../worlds/alerts.md).

??? question "How do I set up instant alerts through my own push service?"
    Go to **Settings → Notifications → Instant alerts, your way**. ntfy is set up in one tap, and you can self-host it for full privacy. Pushover, Discord and Telegram need a short manual step in each service's own **Connect** settings.

??? question "What is the relay, and is it private?"
    It's a small Cloudflare Worker that turns service events into Apple push notifications. It only stores your device's push token, **never** your API keys, URLs or library data. It's off by default, needs Pro and is fully opt-in.

??? question "Which services and events can alert me right now?"
    - **Relay:** Sonarr and Radarr imports, failures and health warnings. Seerr new, approved and available requests.
    - **Your own push:** the same services, set up in one tap with sensible defaults.

??? question "A notification never arrived. What should I check?"
    In order:

    1. Is it set up at all?
    2. Is that service's switch on?
    3. Has iOS notification permission been granted?
    4. Open the app once to refresh an out-of-date push token.
    5. Remember that iOS doesn't guarantee background checks.

??? question "I switched a service on but got “Couldn't set up”"
    The service wasn't reachable at that moment. Check it connects on its own screen first, then try again. For requests, make sure no other app is already using Seerr's single webhook slot.

??? question "Test push says “Reconnecting”, or the device token refreshed"
    Apple issued a new push token (after an update or restore) and the relay still has the old one. Just open Quartermaster once and it registers again automatically.

??? question "How do I get a live Now Playing card or alert when someone starts watching?"
    Turn on **Push notifications** (relay).

    - **Plex:** works through **Tautulli**, which is set up automatically.
    - **Jellyfin:** needs its free **Webhook** plugin, which Quartermaster can install for you.
    - **Emby:** needs a one-time manual webhook.

??? question "Jellyfin Now Playing wants a plugin and a restart. Is that safe?"
    Yes. Quartermaster only adds the official Webhook plugin and nothing else changes. It asks first, because installing it briefly interrupts anyone who's watching.

??? question "How do I add the Emby Now Playing webhook by hand?"
    Tap the **Emby** row under Now Playing to get the exact URL. Then in Emby:

    1. Go to **Dashboard → Notifications** and add a **Webhook**.
    2. Set the content type to `application/json`.
    3. Tick **Playback** events.
    4. Paste the URL.

??? question "Can Quartermaster get Now Playing alerts from Tracearr?"
    Not Now Playing alerts. Tracearr's API is read-only, so connect Tautulli (for Plex), or Jellyfin or Emby directly. With **QM Companion** you can still get Tracearr's **rule violations and server status** as alerts: see [From your Companion](../worlds/alerts.md#from-your-companion).

??? question "What is the daily release digest?"
    A **Pro** morning summary of what's releasing today, from Radarr and Sonarr. It's scheduled as a real iOS notification, so it arrives reliably even when the app is closed.

??? question "What are “Imports & failures” foreground alerts?"
    A local notification when a download finishes or fails while the app is open on screen. You don't need to set anything up in your services, and nothing leaves your device.

??? question "Do I need Pro for notifications?"
    Relay push and the daily digest need Pro. Your own push (ntfy, Pushover, Discord, Telegram) and the foreground "Imports & failures" alerts are free.

## Downloads, Discover and Home

??? question "How do I move a download up or down the queue?"
    Open the row's **⋯** menu and choose **Move to top**, **up**, **down** or **to bottom**. This works for SABnzbd, NZBGet, qBittorrent, Transmission and Deluge. It only appears on items that have a queue position.

??? question "qBittorrent downloads show no Move options"
    Turn on **Torrent Queueing** in qBittorrent's options (**Downloads** or **BitTorrent**, depending on version), then reconnect. Without it, qBittorrent doesn't report a queue position.

??? question "How does queue order work for SABnzbd and NZBGet?"
    The list order is the queue: the top item downloads next. The Move options shift its position. There's no separate priority number to set.

??? question "What's the difference between the two Discover decks?"
    - **My Library:** swipe through what you already own, ranked by your taste.
    - **New to You:** recommends titles you don't have yet, built from your taste profile using Seerr or TMDB.

??? question "I picked two genres and got fewer titles. Is that a bug?"
    No, that's intended. Genres combine with **AND**, so each extra genre narrows the deck. Deselect a genre to broaden it again.

??? question "What does the Both / Movies / Series toggle do?"
    It filters the deck. **Both** mixes films and series, **Movies** uses Radarr only and **Series** uses Sonarr only. It applies to both Discover decks.

??? question "Now Playing is empty even though something's streaming"
    For Plex, Jellyfin and Emby, sessions only show for the **server owner's** account or token. A shared or managed-user connection returns nothing, so switch to the owner's account.

??? question "Tapping a Plex poster opens Plex's home screen, not the title"
    Plex's own "Who's watching?" picker swallows the link. In Quartermaster, go to **Settings → Media & Reader** and set **Open in Plex** to **Web**, which opens the title directly.

??? question "Why does Home say “Now Playing · Plex” instead of just “Now Playing”?"
    When more than one source is streaming at once, each card is labelled with its source. With one active source there's no label.

??? question "UniFi shows 0.00 Mbps for a client"
    One client at 0 usually just means it's idle right now. If every client shows 0, your console's firmware doesn't provide the older per-client speed data.

??? question "What is the Most Active card in UniFi?"
    It ranks your highest-bandwidth devices as usage bars. It shows live speed when they're active and falls back to session totals when idle. Tap a row for that device's details.

## Pro, privacy and the basics

??? question "What do I get free, and what needs Pro?"
    **Free:** one service, one profile and the full Demo mode.

    **Pro:** unlimited services and profiles, the Discover deck, Coming Soon on Home and the combined calendar, the Stuck Download Doctor, full stats, encrypted backups and custom icons.

    See [Free and Pro](../getting-started/free-and-pro.md).

??? question "How much is Pro, and what's the difference between the plans?"
    You can buy a **one-time lifetime unlock** or an **auto-renewing subscription**. Every plan unlocks exactly the same features, and there are no separate tiers. Pick lifetime if you're staying long term, or monthly to try it out. See [Pricing](../getting-started/free-and-pro.md#pricing).

??? question "Does Quartermaster collect any data about me or my servers?"
    No. It's purely a client, with no analytics, no telemetry and no server behind it. It only talks to the services you set up, and nothing about your stack is sent to us or anyone else. The optional [relay](#notifications-and-alerts) only stores a push token.

??? question "Where are my API keys and passwords stored?"
    In the **iOS Keychain**, never in unencrypted app storage. Keys are also removed from all diagnostic logs.

??? question "Can I try the app before connecting my servers?"
    Yes. **Demo mode** fills the app with realistic sample data. It runs entirely on your device, makes no network calls and touches no secrets. Turn it on with **Settings → Explore with sample data**, or when you first open the app.

??? question "I didn't buy Pro. What happens to the extra services I added?"
    They're kept, not deleted. One service and one profile stay usable. The rest show as locked, with their settings and keys saved untouched until you unlock Pro.

??? question "What are profiles, and when would I use more than one?"
    A profile is a self-contained stack: its services, addresses, Wi-Fi name and proxy domains. Use separate profiles for separate setups, such as your home and a family member's. Free includes one profile, and Pro is unlimited.

??? question "What are the worlds?"
    **Entertainment** is media: films, shows, downloads and requests. **Command Centre** is infrastructure: containers, DNS, UniFi and NAS. **QM Reader** is books and audiobooks. The switcher at the top of Home moves between them. See [Worlds](../worlds/index.md).

??? question "I have a new phone or reinstalled. How do I get Pro back?"
    Go to **Settings → Restore purchase**. If it says "Nothing to restore", check you're signed in with the same Apple ID that bought Pro.

??? question "How do I completely reset the app?"
    Go to **Settings → Backup & sync → Delete everything & start over**. This wipes all services, keys and settings and **can't be undone**, so export a backup first. Your Pro purchase stays on your Apple ID.

??? question "How do I cancel the subscription or get a refund?"
    Apple manages both. To cancel, go to **App Store → your Apple ID → Subscriptions → Quartermaster Pro → Cancel**. For refunds, use [reportaproblem.apple.com](https://reportaproblem.apple.com).

??? question "Does it work on Mac? Is there an Apple TV app?"
    It runs on Apple silicon Macs as the same app, with a sidebar layout. The Apple TV app is in beta. See [Platforms](../platforms/index.md).