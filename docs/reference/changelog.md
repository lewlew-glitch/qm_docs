# What's new

## 1.3.0 Hotfix 2

*October 2026.* A batch of your asks from the Discord, and fixes from your reports.

### Home and the Command Centre

- **Downloading:** Entertainment's Home has a **Downloading** row under Up Next while a film or episode is on its way, with its progress and time left. It has its own switch in **Customise Home**.
- **Calendar in the Command Centre:** **Customise Command Centre** can add the calendar of upcoming episodes and films to the Overview.
- **A hot bar for each world:** turn on **Match the world** in the hot bar editor, and Entertainment shows your media shortcuts while the Command Centre shows the rest.

### Films and shows

- **Specials:** a show's Specials season appears at the bottom of its seasons, even when it isn't monitored.
- **Refresh & Scan:** the **More** button on a film or show page refreshes its details and rescans its files in Radarr or Sonarr.
- **Release dates:** a film's **About** shows its cinema, digital and disc dates, and says **Expected** for any still to come.
- **Watch history:** film and episode pages show who watched and when: every play on Plex, and each person's last watch on Jellyfin and Emby.
- **Before you add:** adding a film or show puts the synopsis and the full release date right under the title.
- **Synopses in every language:** a title with no synopsis in your server's language now shows the English one, or its original language's, instead of nothing.

### Downloads

- **Any speed limit:** SABnzbd's speed menu adds **75%** and **Custom**, a slider in 5% steps that shows the speed you'll get. A limit you set elsewhere, like 80%, shows ticked. With no maximum line speed set in SABnzbd, Custom picks a real speed instead, since a percentage of nothing limits nothing.
- **Add a .torrent file:** the Add torrent sheet for qBittorrent and qui can send a `.torrent` file from Files, as well as a magnet link.
- **Easier to scan search results:** in interactive search, quality is coloured by resolution, and the size comes first so a long indexer name never hides it. The grab confirmation shows the release's full details.

### Containers and subtitles

- **Open web UI:** containers on Portainer, Dockhand, Arcane, Komodo, Synology, TrueNAS, Dozzle, Beszel and the Containers tab open their web page, whenever the platform says where it is.
- **Sync subtitle timings:** each subtitle file Bazarr has for a film or episode can be synced to the video from its page.

### Fixes

- **SSH with a key:** adding an SSH host that signs in with a key, or with Tailscale SSH, failed its Test before it ever reached the server. It now gets there, shows you the server's fingerprint to check, and signs in.
- **Clearer SSH errors:** when a server and the terminal can't agree on how to secure the connection, it now says so, and that your password or key was never tried, instead of asking you to check them.
- **Match episodes with Reduce Motion:** with Reduce Motion on, the Match episodes sheet could open only part of the way, leaving Import off the screen. It now opens fully.

## 1.3.0 Hotfix 1

*October 2026.* Easier show pages, a better Up Next, and fixes from your reports since 1.3 came out.

### Show pages

- **Seasons fold open:** each season is one row, newest first. Tap it to open its episodes right there, as stills or as a list, with **Search** and **Monitored** at the top. In the list, hold an episode for Search and Monitor.
- **Episode ratings:** episodes show their TMDB rating, through Seerr or your TMDB key, or the rating your Jellyfin or Emby server holds.
- **Watched, favourites and collections:** on a film or series page, the button beside Search marks it watched or unwatched, and on Jellyfin or Emby adds it to your favourites or to a collection. Plex gets watched and unwatched.
- **History by episode:** a show's download history shows the five episodes with the newest activity, one short row each, then **Show more**. Each episode's page now has its own history too.

### Home

- **Round the spotlight:** swipe on from the last title in the spotlight to go back to the first.
- **Tap for details:** tapping a card in Up Next opens the film or episode instead of starting it. Press and hold a card for **Resume** or **Play**.
- **Continue Watching and Up Next:** what you're partway through and the next episodes of the shows you're watching now have a row each, so a long list of one never hides the other. Each has its own switch in **Customise Home**. Your Tonight picks sit in Up Next.
- **Seerr's hide settings:** if Seerr is set to hide titles you already have, titles on your blocklist or titles already requested, Trending now, the Discover rows and Browse leave them out too. Hiding requested titles needs Seerr 3.5 or later.
- **Customise from Home:** Entertainment now ends with **Customise Home** and **Customise Tabs**, as the Command Centre does.

### Calendar

- **Which episodes:** when several episodes of a show come out on the same day, the calendar and Home's upcoming row now say which ones, like S01E01-09, instead of just how many.

### Alerts

- **Release name:** custom alert wording for Sonarr and Radarr can include the full release name, as Sonarr and Radarr show it in History. It fills in once a QM Companion update adds it.

### Fixes

- **App icons:** the Blackout and Bronze app icons were the wrong way round. Each now sets its own icon, and if you picked one before, the tick moves to the icon you actually have.
- **Typing in forms:** forms and sheets no longer jump up and down while you type a username and password.
- **Streamystats unlock:** the `SESSION_SECRET` field no longer offers a Strong Password or to save it to Passwords.

## 1.3

### New Entertainment Home
- A full-screen spotlight with resume, play and open buttons. Pull down to expand it.
- Rows only appear when they have content. Browsing rows skip titles you own.
- **Customise Home**: turn rows on or off, and get Trending from Jellyseerr or TMDB.
- Choose whose titles appear in Up Next and Continue Watching (Jellyfin and Emby).
- Intro skipping, and Up Next autoplay for up to three episodes.

### Command Centre layouts
- Six layouts (Triage, Pipeline, Machines, Glance, The mix, Classic) with a setup wizard.
- **Needs you**, with fixes inline. Machine pages. Search by function.
- Now Playing and a pinnable **hot bar**.

### QM Reader
- A third world for BookOrbit and Grimmory, with a native EPUB and PDF reader and audiobooks.

### Alerts
- Server-side custom alerts (Pro, Companion 0.1.7+).
- PeaNUT UPS alerts, Uptime Kuma down and recovery pushes (Pro) and Pulsarr request pushes.
- The Notifications screen now diagnoses push problems.

### New connections
Grafana · Uptime Kuma · PeaNUT · Pulsarr · Grimmory (64 services in total)

### Smaller changes
- A world slider with previews (iPhone and iPad).
- Entertainment tabs are now Home, Movies, Shows, Discover and Search. Stack, Stats, Downloads, Containers and the Doctor moved to Command Centre.
- Open the app where you left off or in a chosen world.
- Better behaviour at large text sizes.
- Restart iCloud Sync from another device, and change the passphrase.
- TMDB key included in backups and sync.
- Mac: the new Home, layouts and wizard in the sidebar, and two-column layouts.

### Fixes
- Search adds to the root folder you select.
- Jellyfin Now Playing no longer drops live streams when the server clock runs slow.
- Unraid explains refused actions.
- Maintainerr's *Keep forever* updates Leaving Soon immediately.
- Sheets no longer jump back when swiped down, and clicking beside a sheet closes it (Mac and iPad).
- Companion codes work with either camera.
