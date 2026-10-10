# The Doctor

When a download **stalls**, the Doctor works out why. It uses data from your services to explain the cause in plain English, then offers a **one-tap fix**.

The Doctor is in **Command Centre**. It moved there from Entertainment in 1.3.

## What it looks for

**Downloads and imports**

- A finished download waiting to import, or one whose import is **blocked** or **failed**
- A download that finished in SABnzbd but never reached Radarr or Sonarr
- **Stalled** or **failed** downloads
- **Indexers down**
- Health warnings and available updates from Radarr, Sonarr and the other arr apps

**Containers and hosts**

- A container that's **unhealthy**, has **crashed**, ran **out of memory** or is stuck in a **restart loop**
- A Beszel host that's down, an alert firing, or a value trending towards its limit
- A Coolify deploy that failed, or an app that's down
- A qui instance that's offline

**Drives and storage**

- A drive that's **failing** or **predicted to fail** (Scrutiny), or failing its SMART checks
- A storage pool that's **degraded** or **faulted** (TrueNAS)

**Network**

- A device that's **offline**, the **WAN down**, or one client hogging the bandwidth (UniFi)
- The **VPN down**, no forwarded port, or Gluetun missing a key

**Everything else**

- Your UPS **on battery**, **low on battery**, not reporting or needing attention (PeaNUT)
- An Uptime Kuma monitor that's **down**, or a certificate that's **invalid** or **about to expire**
- Maintainerr titles **leaving soon**, an exposed title, or a rule that has stalled

## The fixes

Depending on the problem, the Doctor offers **Import now**, **Match episodes**, **Force import**, **Retry download**, **Remove** (or **Remove, blocklist & search**), **Restart device**, **Restart tunnel** or **Re-deploy**. Each one says what it will do and asks you to confirm first.
