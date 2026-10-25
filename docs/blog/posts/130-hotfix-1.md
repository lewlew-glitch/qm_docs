---
date: 2026-10-10
slug: "1-3-0-hotfix-1"
categories:
  - Hotfix OTA Release
  - iOS
---

# 1.3.0 Hotfix 1

*October 2026.* Easier show pages, a better Up Next, and fixes from your reports since 1.3 came out.

<!-- more -->

## Show pages

- **Seasons fold open:** each season is one row, newest first. Tap it to open its episodes right there, as stills or as a list, with **Search** and **Monitored** at the top. In the list, hold an episode for Search and Monitor.
- **Episode ratings:** episodes show their TMDB rating, through Seerr or your TMDB key, or the rating your Jellyfin or Emby server holds.
- **Watched, favourites and collections:** on a film or series page, the button beside Search marks it watched or unwatched, and on Jellyfin or Emby adds it to your favourites or to a collection. Plex gets watched and unwatched.
- **History by episode:** a show's download history shows the five episodes with the newest activity, one short row each, then **Show more**. Each episode's page now has its own history too.

## Home

- **Round the spotlight:** swipe on from the last title in the spotlight to go back to the first.
- **Tap for details:** tapping a card in Up Next opens the film or episode instead of starting it. Press and hold a card for **Resume** or **Play**.
- **Continue Watching and Up Next:** what you're partway through and the next episodes of the shows you're watching now have a row each, so a long list of one never hides the other. Each has its own switch in **Customise Home**. Your Tonight picks sit in Up Next.
- **Seerr's hide settings:** if Seerr is set to hide titles you already have, titles on your blocklist or titles already requested, Trending now, the Discover rows and Browse leave them out too. Hiding requested titles needs Seerr 3.5 or later.
- **Customise from Home:** Entertainment now ends with **Customise Home** and **Customise Tabs**, as the Command Centre does.

## Calendar

- **Which episodes:** when several episodes of a show come out on the same day, the calendar and Home's upcoming row now say which ones, like S01E01-09, instead of just how many.

## Alerts

- **Release name:** custom alert wording for Sonarr and Radarr can include the full release name, as Sonarr and Radarr show it in History. It fills in once a QM Companion update adds it.

## Fixes

- **App icons:** the Blackout and Bronze app icons were the wrong way round. Each now sets its own icon, and if you picked one before, the tick moves to the icon you actually have.
- **Typing in forms:** forms and sheets no longer jump up and down while you type a username and password.
- **Streamystats unlock:** the `SESSION_SECRET` field no longer offers a Strong Password or to save it to Passwords.
