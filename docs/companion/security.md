# Security

## Account

- A single **owner** account
- **Two-factor authentication**
- **Session revocation**
- **Recovery codes**

## Network exposure

- Plain HTTP on port `8787` should only be used on a **trusted private network**.
- To expose the panel any further, put Companion **behind a trusted HTTPS reverse proxy**.
- The mobile connection uses HTTPS on `8788` and is tied to one origin.

## What Companion can see

!!! danger "Docker inspection exposes a lot"
    Docker inspection can reveal container metadata, mounts, network layout and **credentials stored in environment variables**. A read-only file mount still lets Companion **read** that file.

- Mount **individual config files**, not whole app-data folders.
- Install the **lowest Docker access profile** you need. See [Docker access profiles](docker-access.md).

## Reporting vulnerabilities

Read the [security model](https://github.com/lewlew-glitch/qm_companion/blob/main/docs/security-model.md) before you expose the panel or turn on Docker writes. Report vulnerabilities as described in [SECURITY.md](https://github.com/lewlew-glitch/qm_companion/blob/main/SECURITY.md).

## Verifying an install

You can check a running, initialised instance with the verification script (Node.js 24+):

```bash
node prove_secure.mjs
QM_SESSION=<current-qm_sess-value> node prove_secure.mjs
```

Docker writes, registry behaviour, reverse-proxy buffering and NAS permissions should be tested in your own environment.
