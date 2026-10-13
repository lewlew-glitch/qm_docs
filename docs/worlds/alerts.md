# Alerts

Quartermaster runs no servers by default, so your stack, keys and data stay on your devices. Find every option in **Settings → Notifications**:

| Option | Cost | How alerts reach you |
|---|---|---|
| [**Push notifications**](#push-notifications) | Pro | Apple notifications through Quartermaster's relay, even when the app is closed |
| [**Instant alerts, your way**](#instant-alerts-your-way) | Free | Your services push straight to your own ntfy, Pushover, Discord or Telegram |
| [**Local alerts**](#local-alerts) | Free, except the daily digest (Pro) | On this device: foreground alerts, the daily digest and server thresholds |
| [**From your Companion**](#from-your-companion) | Pro | Your own server sends the alerts, with the wording and rules you choose |

## Push notifications

Traditional Apple notifications delivered through **Quartermaster's relay**, so they reach your phone even when the app is closed.

The relay is **off until you turn it on**. It forwards each alert and keeps **only your device's push token**, never your keys, URLs or library.

Turn on **Push notifications**, then choose which services can reach you:

- **Sonarr** and **Radarr:** imports, failures and health warnings. If [QM Companion alerts](#from-your-companion) are on, Companion sends these instead, and you manage them there.
- **Seerr:** a nudge when someone makes a request, or one is approved and ready to watch. Set up for you.
- **Now playing alerts:** a notification each time someone starts watching. On a busy server these can add up. See [Now Playing alerts](../tutorials/now-playing.md).

## Instant alerts, your way

Your services push **straight to your own channel**, never through Quartermaster's relay. This is the most reliable free option.

For **ntfy**, Quartermaster can set it up for you. Follow [Free instant alerts with ntfy](../tutorials/ntfy-alerts.md).

For the others, add the connection in each service yourself:

=== "ntfy (manual)"

    1. Install the **ntfy** app, then subscribe to a topic on your server (`ntfy.sh`, or your own such as `https://ntfy.example.com`).
    2. **Sonarr / Radarr → Settings → Connect:** add a **Webhook** (or Custom Script) pointed at your topic URL, such as `https://ntfy.sh/<topic>`, firing on Grab, Download and Import.
    3. **SABnzbd → Config → Notifications:** enable a provider (Apprise works well) pointed at the same topic.
    4. Protected topic? Add your ntfy access token as an `Authorization` header.

=== "Pushover"

    A simple paid push service. Hosted, but reliable and quick to set up.

    1. **Sonarr / Radarr → Settings → Connect → Pushover** (built in): enter your user key and an API token.
    2. **SABnzbd → Config → Notifications → Pushover.**

=== "Discord"

    Pushes to a Discord channel you control, through a webhook.

    1. **In Discord:** Channel settings → Integrations → Webhooks. Create one and copy its URL.
    2. **Sonarr / Radarr → Settings → Connect → Discord** (built in): paste the webhook URL.
    3. **SABnzbd:** through Apprise (`discord://`) or a notification script.

=== "Telegram"

    A free bot pushes to your Telegram chat.

    1. Create a bot with **@BotFather** to get a token, and find your chat ID.
    2. **Sonarr / Radarr → Settings → Connect → Telegram** (built in): enter the bot token and chat ID.
    3. **SABnzbd:** through Apprise (`tgram://`) or a notification script.

**Gotify** and **Apprise** are coming soon.

## Local alerts

Alerts that run on your device, never through Quartermaster's relay.

| Alert | What it does |
|---|---|
| **Imports & failures** | A local alert the moment a download finishes or fails, while the app is open |
| **Daily release digest** *(Pro)* | Each morning, a summary of what's releasing or airing today. It lives under Local alerts but needs Pro |
| **Server thresholds** | Storage, CPU, temperature and memory alerts. Needs **Glances** |

!!! note "Background checks aren't guaranteed"
    Background checks happen occasionally, when iOS allows. They're handy for slow things like storage filling up, but not guaranteed. For reliable alerts, use [Instant alerts, your way](#instant-alerts-your-way).

## From your Companion

*Pro, with QM Companion 0.1.7 or later.* Your own server sends the alerts, with the wording and rules you choose. Open it from **Settings → Notifications → From your Companion**.

### This iPhone

- **Alerts are on** shows when the last alert was delivered.
- **Send a test alert** checks the whole path from your Companion to this phone.
- **Stop alerts on this iPhone.**

### Your connections

Switch alerts on for **Sonarr**, **Radarr** and **Seerr**. Tap Sonarr or Radarr to choose exactly which alerts it sends:

| Alert | |
|---|---|
| **Imports** | When something is imported |
| **Grabs** | When a release is grabbed |
| **Needs attention** | When something needs you, such as a stuck import |
| **Health issues** | When the app reports a health problem |
| **Health restored** | When that problem clears |
| **App updates** | When an update is available |

Tap any alert to change its wording. Custom wording can include the full **release name**, as Sonarr and Radarr show it in History.

Each service's page also shows the **address** Quartermaster wrote into that service for you, and when the last alert arrived. **New address** makes a new secret address and writes it into the service, which is useful if the old one leaked.

### Other sources

**Add a source** to send alerts from:

- **Tracearr:** rule violations and server status
- **Uptime Kuma:** monitors going down and coming back
- **Anything else:** scripts, backups or any tool that can send a webhook

### History

**History** lists every alert your Companion sent or held back.

## Fixing notifications

The **Notifications** screen warns you when push can't reach your device, or when a service is still using an old push address. It shows the fix in both cases.

If a notification never arrived, check in order:

1. Is it set up at all?
2. Is that service's switch on?
3. Has iOS notification permission been granted?
4. Open the app once to refresh an out-of-date push token. This also fixes a test push that says **Reconnecting**.
5. Remember that iOS doesn't guarantee background checks.

**"Couldn't set up"** means the service wasn't reachable at that moment. Check it connects on its own screen, then try again. For requests, make sure no other app is already using Seerr's single webhook slot.
