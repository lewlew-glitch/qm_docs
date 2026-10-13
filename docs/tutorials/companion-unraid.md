# Install QM Companion on Unraid

- **You'll end up with:** your containers, stacks and updates in Quartermaster, and your phone paired.
- **Takes:** about 15 minutes.
- **You need:** Unraid with Community Applications installed.

## 1. Generate your keys

In the Unraid **Terminal** (the **>_** icon at the top right), run this and keep the result somewhere safe:

```bash
openssl rand -hex 32
```

That's your **`SECRET_KEY`**. **Never change it later.** Companion needs it to read what it has saved.

If you'll use the QM socket proxy in step 2, run it a second time for your **`QM_PROXY_KEY`**.

## 2. Set up a socket proxy

Companion never touches the Docker socket directly. It goes through a socket proxy, which can be the QM one or your own.

=== "qm-socket-proxy (recommended)"

    1. Go to **Apps**, search for **qm-socket-proxy** and click **Install**.
    2. Set **`QM_PROXY_KEY`** to your second key.
    3. Put it on a **custom Docker network**. Unraid's default `bridge` network doesn't let containers find each other by name.
    4. Click **Apply**.

=== "Your own Docker socket proxy"

    Already run one? Use it, and skip `QM_PROXY_KEY` entirely.

    1. Check it allows **read** access to containers, events, images, networks, system and info, volumes and ping. It also needs **POST** to start, stop or update containers, and **EXEC** for shell. See [Socket proxy](../companion/install.md#socket-proxy) for details.
    2. Make sure it's on a **custom Docker network** that Companion can join.

Either way, note the proxy's **container name** on the **Docker** tab, for example `dockersocket`. You'll need it in the next step.

## 3. Install QM Companion

Go to **Apps**, search for **QM Companion** and click **Install**. Fill in at least:

| Setting | Enter |
|---|---|
| **Encryption key** (`SECRET_KEY`) | Your first key |
| **Proxy key** (`QM_PROXY_KEY`) | **QM proxy:** your second key, the same as the proxy. **Your own proxy:** leave blank |
| **Server address** (`QM_HOST`) | Your Unraid IP, host only, for example `192.168.1.50` |
| **Docker host** (`DOCKER_HOST`) | `tcp://<proxy-container-name>:2375`, for example `tcp://dockersocket:2375` |
| **Docker access limit** | `read` to start with. Only raise it if your proxy allows POST or EXEC |
| **Network type** | The same custom network as the proxy |

Optionally, map your services' config files, such as `/mnt/user/appdata/radarr/config.xml`, so Companion can hand their details to your phone in step 5. Map **single files** only.

Click **Apply**. Every setting is explained in [Template settings](../companion/install.md#template-settings).

## 4. Claim the owner account

1. Open `http://<unraid-ip>:8787`.
2. If it asks for a setup token, click the Companion icon on the **Docker** tab, choose **Logs** and copy the token.
3. Create the owner account, then turn on **two-factor authentication** and save your **recovery codes**.

## 5. Pair your phone

1. In Companion, open **Set up**.
2. Check each service's **local** address and optional **away** address.
3. Create the transfer and **scan the QR code** in Quartermaster.
4. Enter the **setup code** Companion shows.

!!! warning
    The QR code expires after **three minutes** and only works **once**. Keep it and the setup code private.

## 6. Check it worked

Quartermaster's Command Centre now shows a **QM Companion** card, such as *"32 running, 2 stopped"*.

## Next

- To start, stop and update containers from Companion's dashboard, raise the **Docker access limit**. See [Docker access profiles](../companion/docker-access.md).
- [Pair a device](../companion/pairing.md) covers the optional mobile connection.
