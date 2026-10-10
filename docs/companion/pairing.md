# Pair a device

There are two ways to connect Quartermaster to Companion.

## Standard setup transfer

This sends your service list and addresses to the app.

1. Sign in to Companion and open **Set up**.
2. Review each service's **local address** and optional **away address**.
3. Create the transfer and **scan it** in Quartermaster. You can also open the downloaded `.qmcompanion` file.
4. Enter the **setup code** that Companion shows separately.

!!! warning "Treat transfers as sensitive"
    A transfer **expires after three minutes** and can only be **used once**. The QR code and the `.qmcompanion` file are the same transfer. Keep them and the setup code private until they've expired or been used.

Companion codes can be scanned with either camera.

## Optional mobile connection

This gives the app a lasting connection for the live container view.

1. Deploy the **mobile Compose profile**, which serves HTTPS on port `8788`:

    ```bash
    docker compose \
      -f docker-compose.example.yml \
      -f docker-compose.mobile.yml \
      up -d --build
    ```

2. In Companion, open **Devices** and create a **pairing key** or **QR code**.
3. In Quartermaster, scan or enter it.
4. **Check that the five words** on Companion and on the phone match, then approve.

The connection is tied to **one configured HTTPS origin**. To revoke a device, remove it in **Devices**. The phone loses access immediately.

For more, see [Mobile connection](https://github.com/lewlew-glitch/qm_companion/blob/main/docs/mobile-connection.md) in the QM Companion repository.
