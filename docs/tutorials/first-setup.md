# Your first setup

- **You'll end up with:** Quartermaster connected to Radarr (or Sonarr), tested and saved.
- **Takes:** about 5 minutes.

!!! tip "Just looking?"
    Turn on **Demo mode** at first launch or in Settings to explore with sample data first. It runs entirely on your phone.

## 1. Get the API key

In Radarr, go to **Settings → General → Security** and copy the **API Key**. Sonarr is in the same place.

## 2. Add the service

1. Tap the **profile icon** at the top right of Home (the house, by default).
2. Tap **Profiles**, then **Edit Stack**.
3. Tap **+** at the top right.
4. Choose **Radarr**.

**Edit Stack** is also where you edit or remove services later. Tap any service in the list to open it.

## 3. Fill in the connection

### Label

A name you'll recognise, such as `Radarr`.

### Local address

How to reach Radarr on your home network.

| Field | What to enter |
|---|---|
| **Scheme** | `http`, unless Radarr itself serves HTTPS |
| **Host** | Radarr's LAN IP, for example `192.168.1.50`. Tap one of your saved addresses to fill it in |
| **Port** | Already filled in for Radarr (`7878`). Clear it only if you go through a reverse proxy on 443 or 80 |
| **URL Base** *(optional)* | Only if Radarr sits behind a reverse proxy at a subpath, such as `/radarr` |

### API key

Paste the key from step 1.

!!! info "First time on your network"
    iOS asks for **Local Network** permission the first time. Allow it, or Quartermaster can't reach anything at home. If you said no, turn it on in **Settings → Quartermaster → Local Network**.

### Remote access *(optional)*

Your local address is always tried first. Add a remote address here to use Radarr when you're away:

| Field | What to enter |
|---|---|
| **Local only** | Turn on if you **don't** want Radarr away from home. It just keeps "unavailable" warnings quiet, and doesn't change how Quartermaster connects |
| **Scheme** | Usually `https` for a public hostname |
| **Host** | Your public hostname or Tailscale address, for example `radarr.example.com`. Tap a saved domain to fill it in, then edit the subdomain |
| **Port** | Usually **blank**, because a reverse proxy uses 443 or 80. Set it only for a direct port |

Using Tailscale? See [Use Quartermaster away from home](tailscale.md).

### Home Wi-Fi *(optional)*

Enter your **Network name (SSID)**, or tap **Use current network** while you're at home. On that Wi-Fi, Quartermaster uses the local address straight away. Reading the network name needs **Location** access.

### Cloudflare Access *(optional)*

Only if Radarr is behind a Cloudflare Access login page. Pick the Access headers you saved for its domain. See [Get past Cloudflare Access](cloudflare-access.md).

### Advanced

**Authentication & TLS** holds extra sign-in and certificate options. Most people can leave it alone.

## 4. Test it

Tap **Test**. Quartermaster checks four stages in order and stops at the first one that fails:

**Address → Reachable → Authenticated → Version**

| Stops at | Usually means |
|---|---|
| **Reachable** | Wrong `http`/`https`, wrong port, or you're not on your home network |
| **Authenticated** | **401:** the key was mistyped. **403:** something in front of Radarr is blocking it |
| **Version** | A login page or proxy answered instead of Radarr, or the URL needs a subpath such as `/radarr` |

The `QM-` code shown tells you exactly what to fix. See [Error codes](../reference/error-codes.md).

## 5. Save

Tap **Save**. Radarr now shows a badge saying how it's connected, such as **On your network**.

!!! tip "Save time on the next service"
    Your profile can store things every service shares: your server addresses, home Wi-Fi, reverse-proxy domains and sign-ins. New services then fill them in for you. See [Profile credentials](../getting-started/home-and-away.md#profile-credentials).

## Next

- [Use Quartermaster away from home](tailscale.md)
- The free tier connects **one** service fully. To add more, see [Free and Pro](../getting-started/free-and-pro.md).
