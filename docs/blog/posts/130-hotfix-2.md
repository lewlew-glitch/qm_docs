---
date: 2026-10-20
slug: "1-3-0-hotfix-2"
categories:
  - Hotfix OTA Release
  - iOS
---

# 1.3.0 Hotfix 2

*October 2026.* A batch of your asks from the Discord, and fixes from your reports.

<!-- more -->

## Home and the Command Centre

- **Downloading:** Entertainment's Home has a **Downloading** row under Up Next while a film or episode is on its way, with its progress and time left. It has its own switch in **Customise Home**.
- **Calendar in the Command Centre:** **Customise Command Centre** can add the calendar of upcoming episodes and films to the Overview.
- **A hot bar for each world:** turn on **Match the world** in the hot bar editor, and Entertainment shows your media shortcuts while the Command Centre shows the rest.

## Films and shows

- **Specials:** a show's Specials season appears at the bottom of its seasons, even when it isn't monitored.
- **Refresh & Scan:** the **More** button on a film or show page refreshes its details and rescans its files in Radarr or Sonarr.
- **Release dates:** a film's **About** shows its cinema, digital and disc dates, and says **Expected** for any still to come.
- **Watch history:** film and episode pages show who watched and when: every play on Plex, and each person's last watch on Jellyfin and Emby.
- **Before you add:** adding a film or show puts the synopsis and the full release date right under the title.
- **Synopses in every language:** a title with no synopsis in your server's language now shows the English one, or its original language's, instead of nothing.

## Downloads

- **Any speed limit:** SABnzbd's speed menu adds **75%** and **Custom**, a slider in 5% steps that shows the speed you'll get. A limit you set elsewhere, like 80%, shows ticked. With no maximum line speed set in SABnzbd, Custom picks a real speed instead, since a percentage of nothing limits nothing.
- **Add a .torrent file:** the Add torrent sheet for qBittorrent and qui can send a `.torrent` file from Files, as well as a magnet link.
- **Easier to scan search results:** in interactive search, quality is coloured by resolution, and the size comes first so a long indexer name never hides it. The grab confirmation shows the release's full details.

## Containers and subtitles

- **Open web UI:** containers on Portainer, Dockhand, Arcane, Komodo, Synology, TrueNAS, Dozzle, Beszel and the Containers tab open their web page, whenever the platform says where it is.
- **Sync subtitle timings:** each subtitle file Bazarr has for a film or episode can be synced to the video from its page.

## Fixes

- **SSH with a key:** adding an SSH host that signs in with a key, or with Tailscale SSH, failed its Test before it ever reached the server. It now gets there, shows you the server's fingerprint to check, and signs in.
- **Clearer SSH errors:** when a server and the terminal can't agree on how to secure the connection, it now says so, and that your password or key was never tried, instead of asking you to check them.
- **Match episodes with Reduce Motion:** with Reduce Motion on, the Match episodes sheet could open only part of the way, leaving Import off the screen. It now opens fully.
