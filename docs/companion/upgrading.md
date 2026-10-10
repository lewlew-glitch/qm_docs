# Upgrading

1. **Keep your existing `.env` and `SECRET_KEY`.** Skip the `.env` creation step. Changing `SECRET_KEY` makes stored credentials unreadable.
2. Pull the latest code and rebuild using the **same Compose files in the same order** as before:

    ```bash
    git pull
    docker compose -f docker-compose.example.yml up -d --build
    ```

    Add your `management`, `shell` or `mobile` files in the same order you installed them.

!!! tip
    Server-side custom alerts need Companion **0.1.7 or later**.

## Development

Requires Node.js 24 or newer.

```bash
npm ci
npm test
node verify.mjs
```
