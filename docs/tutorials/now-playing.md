# Now Playing alerts

- **You'll end up with:** a live Now Playing card, and an alert when someone starts watching.
- **Takes:** about 5 minutes.
- **Needs:** Pro, with **Push notifications** turned on.

## 1. Turn on Push notifications

Turn on **Push notifications** in Quartermaster. They use Quartermaster's relay, which only stores your device's push token, never your keys, URLs or library data. See [The relay](../worlds/alerts.md#push-notifications).

## 2. Connect your media server

Use the **server owner's** account or token. A shared or managed user returns no sessions.

=== "Plex"

    Plex works through **Tautulli**.

    1. Connect **Tautulli** in Quartermaster. Its API key is under **Settings → Web Interface → API** in Tautulli.
    2. That's it. Quartermaster sets up the Tautulli notification automatically.

=== "Jellyfin"

    Jellyfin needs its official **Webhook** plugin, and Quartermaster can install it for you.

    1. When Quartermaster offers to install the plugin, accept.
    2. Jellyfin restarts to finish installing it.

    !!! warning
        The restart briefly interrupts anyone who's watching, so do it at a quiet time. Quartermaster only adds the Webhook plugin and changes nothing else.

=== "Emby"

    Emby needs a one-time manual webhook.

    1. In Quartermaster, tap the **Emby** row under **Now Playing** and copy the URL.
    2. In Emby, go to **Dashboard → Notifications** and add a **Webhook**.
    3. Set the content type to `application/json`.
    4. Tick **Playback** events.
    5. Paste the URL and save.

## 3. Try it

Start playing something. The Now Playing card appears, and you get an alert.

## If nothing shows

??? question "Now Playing is empty even though something's streaming"
    You've probably connected with a shared or managed user. Reconnect with the **server owner's** account.

??? question "Can I use Tracearr instead?"
    No. Tracearr's API is read-only. Use Tautulli for Plex, or connect Jellyfin or Emby directly.

??? question "The test push says “Reconnecting”"
    Apple issued a new push token, for example after an update or restore. Open Quartermaster once and it registers again automatically.
