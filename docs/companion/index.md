# QM Companion

QM Companion is a **free, open-source** (MIT) app you run on your own server alongside Docker. It gives Quartermaster a live view of your containers and helps you set up new devices.

[:fontawesome-brands-github: View on GitHub](https://github.com/lewlew-glitch/qm_companion){ .md-button }

## What it does

- **Live view in the app:** containers, stacks, Docker volumes, available updates and recent activity. In the app this view is **read-only**.
- **Web dashboard:** containers, stacks, images, volumes, networks, events, logs and resource use.
- **Control:** start, stop or update containers from **Companion's own dashboard**. This only works once you've given Companion Docker write access. See [Docker access profiles](docker-access.md).
- **Setup transfer:** send your service list and addresses to the app with a QR code or file. See [Pair a device](pairing.md).
- **Stack handover:** a fresh install takes your whole service list in one go. See [Stack handover](stack-handover.md).
- **Server-side alerts** *(Pro, 0.1.7+)*. See [Alerts](../worlds/alerts.md).

## How it connects

1. Install Companion on your server, reachable on your home network or over Tailscale.
2. Pair your phone once. You approve it by matching **five words** shown on the server and the phone.
3. The credential is stored in the phone's **keychain**. Revoke it on the server and the phone loses access immediately.

After setup, the app talks to the server **directly**. Nothing goes through a relay.

## Ports

| Port | Purpose |
|---|---|
| `8787` | Web panel. Use HTTP only on a trusted network, or put it behind an HTTPS reverse proxy |
| `8788` | HTTPS for the optional mobile profile |

[Install QM Companion :octicons-arrow-right-24:](install.md){ .md-button .md-button--primary }
