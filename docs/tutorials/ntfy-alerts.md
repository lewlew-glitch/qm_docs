# Free instant alerts with ntfy

- **You'll end up with:** a notification on your phone when Sonarr or Radarr imports something, fails or has a health warning, and when Seerr gets a request.
- **Takes:** about 5 minutes.
- **Cost:** free. No Pro needed.

With this setup, alerts go **straight from your services to ntfy**. Quartermaster sets up the connection but isn't in the path, so they arrive even when the app is closed.

## 1. Install ntfy on your iPhone

Install **ntfy** from the App Store and allow notifications.

!!! tip "Self-host for full privacy"
    You can run your own ntfy server instead of using ntfy.sh:

    ```bash
    docker run -d --name ntfy -p 8090:80 binwiederhier/ntfy serve
    ```

    Then add your server in the ntfy app's settings.

## 2. Set up ntfy in Quartermaster

1. Go to **Settings → Notifications → Instant alerts, your way** and choose **ntfy**.
2. Under **Your ntfy**, check the settings:

    | Setting | What to enter |
    |---|---|
    | **Server** | Leave it as `https://ntfy.sh`, or point it at your own server |
    | **Topic** | Quartermaster creates a random topic for you, such as `qm-ypwma6ptdd`. Tap **New topic** for a different one |
    | **Token** *(optional)* | Only if your ntfy topic is protected and needs a token |

3. Tap **Save**.

!!! warning "Topic names on ntfy.sh are public"
    Anyone who knows a topic name on ntfy.sh can read it. Keep the random topic Quartermaster made, don't share it, or self-host ntfy.

## 3. Subscribe on your phone

Under **Get it on your phone**, Quartermaster shows the full topic address, for example `https://ntfy.sh/qm-ypwma6ptdd`.

1. Open the **ntfy** app and tap **+** to subscribe to a topic.
2. Enter the topic name. If you use your own server, add it as the server first.
3. Back in Quartermaster, tap **Send test**. It should arrive within seconds.

## 4. Connect your services

Under **Your services**, switch on the ones you want alerts from: Sonarr, Radarr and Seerr. It shows how many are connected, such as *2 of 3 wired to your ntfy*.

Quartermaster adds the ntfy connection to each service for you, with sensible defaults. To check, grab something in Radarr and wait for the alert.

## If something doesn't work

??? question "I got “Couldn't set up”"
    The service wasn't reachable at that moment. Check it connects on its own screen in Quartermaster, then try again. For Seerr, make sure no other app is already using its single webhook slot.

??? question "Nothing arrives"
    - Check the ntfy app has notification permission.
    - Check you're subscribed to the right topic, on the right server.
    - In Sonarr or Radarr, open **Settings → Connect**. The ntfy connection should be listed there, and you can test it.

## Other services

**Pushover**, **Discord** and **Telegram** work the same way, but need one short manual step in each service's **Settings → Connect**. **Gotify** and **Apprise** are coming soon.

For alerts through Apple push, with no extra app, see [Alerts](../worlds/alerts.md). That needs Pro.
