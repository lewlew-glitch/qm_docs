# Use Quartermaster away from home

- **You'll end up with:** your services working on mobile data or any Wi-Fi, without opening ports on your router.
- **Takes:** about 10 minutes.
- **You need:** a free [Tailscale](https://tailscale.com) account.

Quartermaster always tries a service's **local** address first. If that fails, it uses the **remote** address. Tailscale gives your server a private address that works from anywhere.

## 1. Put Tailscale on your server

=== "Linux"

    ```bash
    curl -fsSL https://tailscale.com/install.sh | sh
    sudo tailscale up
    ```

    Open the link it prints and sign in.

=== "Unraid"

    Install **Tailscale** from **Apps**, open it and sign in.

=== "Synology / other NAS"

    Install the **Tailscale** package from your NAS's package centre and sign in.

## 2. Put Tailscale on your iPhone

Install **Tailscale** from the App Store and sign in with the **same account**. Turn it on.

## 3. Find your server's Tailscale address

In the [Tailscale admin console](https://login.tailscale.com/admin/machines), find your server. Copy either:

- its **`100.x.y.z`** address, or
- its **MagicDNS name**, such as `tower.tailnet-name.ts.net`. This is easier to remember.

## 4. Add it as the remote address

For each service in Quartermaster:

1. Open the service and go to **Remote access**.
2. Make sure **Local only** is **off**.
3. Set **Scheme** to `http`, unless the service itself serves HTTPS.
4. Enter the Tailscale address as the **Host**, and the same **Port** the service uses at home.
5. Tap **Test**, then **Save**.

!!! tip "Or use Tailscale for the local address"
    Quartermaster also accepts a Tailscale hostname as the **local** address. When you're away it uses whichever address answers, including the local one over Tailscale.

!!! tip "Home Wi-Fi"
    Set your **Home Wi-Fi (SSID)** as well, or tap **Use current network** while you're at home. On that Wi-Fi, Quartermaster uses the local address straight away. Reading the network name needs **Location** permission.

## 5. Try it

Turn off Wi-Fi on your phone, leave Tailscale on, and open Quartermaster. The service should show **Via Tailscale**.

## If something doesn't connect

??? question "SABnzbd returns 403 over Tailscale"
    SABnzbd blocks hostnames it doesn't know. In SABnzbd, go to **Config → Special** and add your MagicDNS name to `host_whitelist`, then restart SABnzbd.

??? question "It still shows Unreachable"
    - Check Tailscale is **on** in the iPhone app.
    - Check the service listens on all interfaces, not just `127.0.0.1`.
    - Check the port is the one the service uses on the server itself.

!!! note "SSH"
    SSH services can also **Sign in with Tailscale**, which uses Tailscale SSH instead of a password or key.
