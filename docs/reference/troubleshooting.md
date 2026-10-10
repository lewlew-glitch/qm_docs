# Troubleshooting

For service-specific problems, see the [FAQ](faq.md#a-service-wont-connect). For `QM-` codes, see [Error codes](error-codes.md).

??? question "A service shows as Unreachable"
    - Are you on the network the address belongs to? Check the [local and away addresses](../getting-started/home-and-away.md).
    - Open the address in Safari on the same device.
    - If you're away, check that Tailscale or your VPN is connected.
    - Make sure the API key hasn't been regenerated on the service.
    - For a self-signed certificate, trust it after checking the fingerprint.

??? question "Push notifications don't arrive"
    Open the **Notifications** screen. It warns you when push can't reach the device or a service is using an old push address, and shows the fix. Local checks only run when iOS allows, so they're never instant.

??? question "A download is stuck"
    Open the [Doctor](../worlds/doctor.md) in Command Centre for a plain-English diagnosis and a one-tap fix.

??? question "Unraid refuses to start or stop a container or VM"
       Quartermaster shows the reason and the permission you need to change on Unraid. Check the API key has the **CONNECT** and **ADMIN** roles under **Settings → Management Access → API Keys**. Unraid 7.3 or later is required.

??? question "I can't start or stop containers in the app"
    That's intended. The app's container view is read-only. Control containers from QM Companion's dashboard, with a [Management profile](../companion/docker-access.md) installed and the active mode raised.

??? question "Companion's first-run token is missing"
    If `SETUP_TOKEN` isn't set, the token is printed to the log until an owner exists:

    ```bash
    docker compose -f docker-compose.example.yml logs companion
    ```

??? question "Companion credentials stopped working after an upgrade"
    `SECRET_KEY` probably changed. Stored credentials can only be read with the original key, so restore your old `.env`.

??? question "The setup transfer QR code doesn't work"
    Transfers **expire after three minutes** and can only be **used once**. Create a new one.

Still stuck? Ask on [Discord](https://discord.gg/ecFz4WsVVB).
