# Docker access profiles

The **installed profile** sets the most Companion can ever do. Within that limit, the **active mode** is chosen in the dashboard.

| Profile | Compose files | Installed maximum |
|---|---|---|
| **Read only** | `docker-compose.example.yml` | Discovery, status and logs |
| **Management** | adds `docker-compose.management.yml` | Docker writes, without container exec |
| **Management + shell** | adds `docker-compose.shell.yml` | Docker writes and container exec |

Every profile **starts in Read only mode**. To go higher, the owner raises the mode from **Docker access**, up to the installed maximum.

=== "Read only"

    ```bash
    docker compose -f docker-compose.example.yml up -d --build
    ```

=== "Management"

    ```bash
    docker compose \
      -f docker-compose.example.yml \
      -f docker-compose.management.yml \
      up -d --build
    ```

=== "Management + shell"

    ```bash
    docker compose \
      -f docker-compose.example.yml \
      -f docker-compose.management.yml \
      -f docker-compose.shell.yml \
      up -d --build
    ```

!!! warning "Keep the file order"
    Use the same Compose file order every time you recreate the installation. If you use the [mobile profile](pairing.md#optional-mobile-connection), put `docker-compose.mobile.yml` **after** any file that changes `ports`.

!!! danger "Management grants broad authority"
    With a Management profile installed, the Companion process has broad Docker authority **even when the active mode is lower**. Install only the profile you need.

For full details, see [Docker access](https://github.com/lewlew-glitch/qm_companion/blob/main/docs/docker-access.md) in the QM Companion repository.
