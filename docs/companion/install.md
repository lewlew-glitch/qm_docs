# Install QM Companion

!!! info "Before you start"
    You need Docker with Compose on the host and `openssl` to generate secrets. Read the [security model](security.md) before you expose the panel or turn on Docker writes.

!!! tip "On Unraid?"
    Install from Community Applications instead. Follow the [Install QM Companion on Unraid](../tutorials/companion-unraid.md) tutorial.

## 1. Clone the repository

```bash
git clone https://github.com/lewlew-glitch/qm_companion.git
cd qm_companion
```

## 2. Edit the Compose file

Open `docker-compose.example.yml` and:

- [ ] Set the published address for port **8787**
- [ ] Set `QM_HOST`
- [ ] Replace the example service config paths with real paths on your server

!!! warning "Mount single files"
    Mount individual config files only. **Don't** mount a whole app-data parent directory.

## 3. Create secrets

For a **new** installation only, create a gitignored `.env`. This snippet won't overwrite an existing file:

```bash
if [ -e .env ]; then
  printf 'Refusing to replace existing .env\n' >&2
  false
else
  umask 077
  {
    printf 'SECRET_KEY=%s\n' "$(openssl rand -hex 32)"
    printf 'QM_PROXY_KEY=%s\n' "$(openssl rand -hex 32)"
  } > .env
  chmod 600 .env
fi
```

Check the values and the Compose file without printing your secrets:

```bash
(
  set -a
  . ./.env
  set +a
  test "${#SECRET_KEY}" -eq 64 &&
    test "${#QM_PROXY_KEY}" -ge 32 &&
    test "$SECRET_KEY" != "$QM_PROXY_KEY"
) && docker compose -f docker-compose.example.yml config --quiet
```

## 4. Start Companion

This starts the read-only profile:

```bash
docker compose -f docker-compose.example.yml up -d --build
```

## 5. Claim the owner account

Open `http://<server-address>:8787` and claim the owner account.

If you didn't set `SETUP_TOKEN`, the first-run token is in the log:

```bash
docker compose -f docker-compose.example.yml logs companion
```

Then turn on **two-factor authentication** and save your **recovery codes**.

## Environment variables

| Variable | Required | Notes |
|---|:---:|---|
| `SECRET_KEY` | :material-check: | 64 hex characters. **Keep it the same across upgrades.** If you lose it, stored credentials can't be read. |
| `QM_PROXY_KEY` | :material-check: | At least 32 characters. Must be different from `SECRET_KEY`. Shared with the QM socket proxy. Not needed if you use [your own proxy](#socket-proxy). |
| `QM_HOST` | :material-check: | The LAN or Tailscale address of your server that the phone can reach. Use a **host only**, with no scheme, port or path. For example `192.168.1.50` or `myserver.tailnet-name.ts.net`, but not `http://192.168.1.50:8787`. |
| `QM_REMOTE_HOST` | | Optional. A hostname or Tailscale address suggested for away routes. |
| `SETUP_TOKEN` | | Optional. If it isn't set, a first-run token is logged until an owner exists. |

## Next steps

- [Choose a Docker access profile](docker-access.md)
- [Pair your phone](pairing.md)

## Installing on Unraid

QM Companion is in Unraid's **Community Applications**. For step-by-step instructions, follow the [Install QM Companion on Unraid](../tutorials/companion-unraid.md) tutorial. This section is the reference for every template setting.

It runs as **two containers**: a Docker socket proxy and Companion itself. Companion never touches the Docker socket directly.

### Socket proxy

You can use the QM proxy or your own. Either works.

=== "qm-socket-proxy (recommended)"

    Install **qm-socket-proxy** from Community Applications. It's locked down to only what Companion needs.

    - Set `QM_PROXY_KEY` on the proxy: at least 32 characters, different from `SECRET_KEY`.
    - Set Companion's **Proxy key** to the **same** value.

=== "Your own Docker socket proxy"

    Already run a Docker socket proxy? Point Companion at it instead. You **don't need `QM_PROXY_KEY`**, so leave Companion's **Proxy key** blank.

    Your proxy must allow **read** access to:

    - containers
    - events
    - images
    - networks
    - system and info
    - volumes
    - ping

    To start, stop or update containers, it also needs **POST** access, and **EXEC** for shell access. Set Companion's **Docker access limit** to match: `read`, `manage` (POST) or `shell` (EXEC).

Companion reaches the proxy by its **container name**, so its **Docker host** is `tcp://<proxy-container-name>:2375`, for example `tcp://dockersocket:2375`.

!!! warning "Same network, no published port"
    Put the proxy and Companion on the **same custom Docker network**. Unraid's default `bridge` network doesn't let containers find each other by name. **Don't publish port 2375** on the host.

### Template settings

#### Required

| Setting | Variable | What to enter |
|---|---|---|
| **WebUI port** | `8787` | The host port for the web panel. Change it if 8787 is taken |
| **Appdata** | `/data` | Leave as `/mnt/user/appdata/qm-companion`. This holds Companion's encrypted state, so back it up |
| **Encryption key** | `SECRET_KEY` | 64 hex characters. Generate it once with `openssl rand -hex 32` |
| **Server address** | `QM_HOST` | Your Unraid server's LAN or Tailscale address, as a host only, for example `192.168.1.50`. No `http://`, port or path |
| **Docker access limit** | `DOCKER_ACCESS_MAX` | `read`, `manage` or `shell`. Keep `read` unless your proxy allows POST (manage) or EXEC (shell) |
| **Bind address** | `BIND_ADDRESS` | Leave as `0.0.0.0` so Unraid's port mapping works |
| **Docker host** | `DOCKER_HOST` | `tcp://<proxy-container-name>:2375`, from step 1 |
| **Proxy key** | `QM_PROXY_KEY` | **qm-socket-proxy only:** the same key you set on the proxy. Leave it blank if you use your own proxy |
| **Trusted reverse proxy** | `TRUST_PROXY` | `false`, unless the panel is behind a trusted HTTPS reverse proxy |

#### Mobile connection

These settings power the [mobile connection](pairing.md#optional-mobile-connection).

| Setting | Variable | What to enter |
|---|---|---|
| **Mobile API** | `MOBILE_API_ENABLED` | `true` to turn on the mobile connection |
| **Mobile enrolment** | `MOBILE_ENROLMENT_ENABLED` | `true` to allow pairing new devices |
| **Mobile bind IP** | `QM_MOBILE_BIND_IP` | Your Unraid server's IP, for example `192.168.1.50` |
| **Advertised origin** | `QM_ADVERTISED_ORIGIN` | The HTTPS address phones use, for example `https://192.168.1.50:8788` |
| **Mobile port** | `8788` | The host port for the mobile connection |

#### Optional

| Setting | Variable | What to enter |
|---|---|---|
| **Away address** | `QM_REMOTE_HOST` | A hostname or Tailscale address suggested for away routes |
| **Marketplace bind roots** | `DOCKER_DEPLOY_BIND_ROOTS` | Host folders Marketplace deployments may bind-mount. Leave blank to allow named volumes only |
| **Marketplace bind address** | `DOCKER_DEPLOY_BIND_ADDRESS` | The host address used for ports published by Marketplace deployments |

#### Service configs

Map each service's config file so Companion can read it for [setup transfers](pairing.md). Every one is optional, so only fill in the services you run.

| Service | File | Typical Unraid path |
|---|---|---|
| Radarr | `config.xml` | `/mnt/user/appdata/radarr/config.xml` |
| Sonarr | `config.xml` | `/mnt/user/appdata/sonarr/config.xml` |
| Lidarr | `config.xml` | `/mnt/user/appdata/lidarr/config.xml` |
| Prowlarr | `config.xml` | `/mnt/user/appdata/prowlarr/config.xml` |
| Bazarr | `config.yaml` | `/mnt/user/appdata/bazarr/config/config.yaml` |
| SABnzbd | `sabnzbd.ini` | `/mnt/user/appdata/sabnzbd/sabnzbd.ini` |
| Seerr / Jellyseerr | `settings.json` | `/mnt/user/appdata/jellyseerr/settings.json` |
| Overseerr | `settings.json` | `/mnt/user/appdata/overseerr/settings.json` |
| Tautulli | `config.ini` | `/mnt/user/appdata/tautulli/config.ini` |
| Jackett | `ServerConfig.json` | `/mnt/user/appdata/jackett/Jackett/ServerConfig.json` |
| NZBHydra2 | `nzbhydra.yml` | `/mnt/user/appdata/nzbhydra2/nzbhydra.yml` |

The exact path depends on how each app was installed, so check its appdata folder.

!!! warning "Single files only"
    Map each config **file** on its own. Don't map `/mnt/user/appdata` or a whole app folder.

### Updating

Update both containers from the **Docker** tab like any other Community Apps containers. Your settings are kept.

!!! warning "Keep your SECRET_KEY"
    Never change **Encryption key** (`SECRET_KEY`) when you edit the template. Companion needs it to read the credentials it has already stored.
