# Alerts

## Two ways to get alerts

| | Instant alerts, your way | Push notifications |
|---|---|---|
| **Cost** | Free | Pro |
| **How it works** | Quartermaster sets up a connection in Sonarr, Radarr or Seerr that sends straight to **your own** push service | Alerts go through Quartermaster's relay to Apple push |
| **Destinations** | ntfy (one tap, can be self-hosted), Pushover, Discord, Telegram | Your iPhone or iPad |
| **Works with the app closed** | Yes, from your push service | Yes |

Set up your own push in **Local alerts → Instant alerts, your way**. Pushover, Discord and Telegram need a short manual step in each service's **Connect** settings.

### The relay

The relay is a small Cloudflare Worker that turns service events into Apple push notifications. It only stores your device's **push token**, never your API keys, URLs or library data. It's **off by default** and fully opt-in.

### What can alert you

- **Sonarr and Radarr:** imports, failures and health warnings
- **Seerr:** new, approved and available requests

## Other alerts

| Alert | Cost | What it does |
|---|---|---|
| **Daily release digest** | Pro | A morning summary of today's releases from Radarr and Sonarr, scheduled as a real iOS notification |
| **Imports & failures** | Free | A local notification when a download finishes or fails while the app is open on screen. Nothing leaves your device |
| **Server-side alerts** | Pro | Needs QM Companion **0.1.7 or later**. Your server sends alerts using your own wording and rules |
| **Local background checks** | Free | Run when iOS allows, so they aren't instant |

## Now Playing alerts

Turn on **Push notifications** (relay), then:

| Server | Setup |
|---|---|
| **Plex** | Works through **Tautulli**, which is set up automatically |
| **Jellyfin** | Needs the official **Webhook** plugin. Quartermaster can install it, and asks first because installing briefly interrupts anyone watching |
| **Emby** | A one-time manual webhook. Tap the Emby row under Now Playing for the URL, then in Emby add a Webhook under **Dashboard → Notifications**, set the content type to `application/json`, tick **Playback** events and paste the URL |
| **Tracearr** | Not supported, because Tracearr's API is read-only. Use Tautulli or connect Jellyfin or Emby directly |

## Service alerts

**PeaNUT (UPS):** an opt-in alert when the UPS switches to battery, runs low, stops reporting or recovers.

**Uptime Kuma** *(Pro)*: a webhook sends a push when a monitor goes down and another when it recovers.

**Pulsarr:** a notification for each new request, showing the instance and quality profile.

## Fixing notifications

The **Notifications** screen warns you when push can't reach your device, or when a service is still using an old push address. It shows the fix in both cases.

If a notification never arrived, check in order:

1. Is it set up at all?
2. Is that service's switch on?
3. Has iOS notification permission been granted?
4. Open the app once to refresh an out-of-date push token. This also fixes a test push that says **Reconnecting**.
5. Remember that iOS doesn't guarantee background checks.

**"Couldn't set up"** means the service wasn't reachable at that moment. Check it connects on its own screen, then try again. For requests, make sure no other app is already using Seerr's single webhook slot.
