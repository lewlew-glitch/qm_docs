# Command Centre

Command Centre covers compute, network, storage, smart home and edge. It connects to **30 services**, including Portainer, Proxmox, Unraid, TrueNAS, Pi-hole, AdGuard Home, UniFi, Home Assistant, Glances and Uptime Kuma.

Tabs: **Overview · Activity · Stack · Downloads · Stats**

## Layouts

Overview comes in six layouts. On first run, a **setup wizard** previews each one using your own stack, so you can see it before you choose.

| Layout | What you get |
|---|---|
| **Triage** | Only what needs you. Everything healthy folds away. |
| **Pipeline** | A request followed all the way to the sofa: requests → downloads → new arrivals → streams |
| **Machines** | Your stack grouped by the box it runs on, with CPU, memory, temperature and drives |
| **Glance** | Every service on one screen, as icons |
| **The mix** | What needs you, your pipeline and your machines in one scroll |
| **Classic** | Every service as a tile, as before 1.3. It stays until you pick another layout |

## Needs you

The **Needs you** section lists warnings and faults, with the fix next to each. For example:

- **Resume** a paused Pi-hole
- **Match** a stuck import *(Pro)*
- Services that are **unreachable**

Services that are running normally are collapsed into one line, such as *"5 running normally"*.

## Machines

Machine pages show **CPU, memory, temperature and drives** from any of these:
Glances · Beszel · Proxmox VE · Unraid · TrueNAS · Synology · UGREEN NAS

## Search

Search your stack by name or by function. For example, `dns` or `ups`.

## Hot bar

The hot bar holds your most-used actions, such as Radarr, Search, Downloads and Add. **Long-press any tile to pin it.** The hot bar can also appear on Entertainment Home (iPhone and iPad).

## Now Playing

Active streams from your media servers appear here.

## Containers

With [QM Companion](../companion/index.md), you can see containers, stacks, Docker volumes, available updates and recent activity. The app's container view is read-only. Starting, stopping and updating happen in Companion's own dashboard.
