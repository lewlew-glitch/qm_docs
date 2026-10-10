# Error codes

## Connection test

When you test a service, Quartermaster checks four stages in order and **stops at the first failure**:

| Stage | What it checks | If it fails |
|---|---|---|
| **Address** | The URL is valid | Fix the typo or format (`QM-URL-01`) |
| **Reachable** | Something answers over HTTP | Check `http` vs `https`, the port, your network or Tailscale, and iOS **Local Network** permission |
| **Authenticated** | The key or login is accepted | **401:** wrong key. **403:** a proxy is stripping the key, or it lacks permission |
| **Version** | The real service answered | A proxy or SSO login page answered instead. Point the address directly at the service |

## QM- codes

| Code | Meaning | What to do |
|---|---|---|
| `QM-NET-01` | Unreachable | Check the address, port and network. See [Reachable](faq.md#connecting-and-networking) |
| `QM-NET-02` | Timed out | The host is slow or blocked. Check firewalls and VPNs |
| `QM-TLS-01` | Self-signed certificate | Check the fingerprint and tap **Trust**, or use `http://` |
| `QM-TLS-02` | Self-signed certificate | Check the fingerprint and tap **Trust**, or use `http://` |
| `QM-TLS-03` | Pinned certificate changed | Only trust it again if you expected the change, such as a renewed certificate or rebuilt container |
| `QM-AUTH-01` | Key or login rejected | Copy the key again. Make sure it's the right kind (for example SABnzbd's API Key, not its NZB Key) |
| `QM-HTTP-01` | Wrong URL or missing subpath | Add the URL Base, for example `/radarr` |
| `QM-DATA-01` | The wrong page came back | A proxy or login page is answering. Point the address directly at the service |
| `QM-EDGE-01` | Blocked by Cloudflare Access | Add an Access service token as `CF-Access-Client-Id` and `CF-Access-Client-Secret` headers under **Advanced** |
| `QM-EDGE-02` | Cloudflare rate limiting | The app is backing off. Relax bot protection, or connect over Tailscale or your LAN |
| `QM-URL-01` | Invalid URL | Check the format, for example `http://192.168.1.20:7878` |
| `QM-OPEN-01` | A deep link failed to open | Check that the target app is installed |

!!! todo
    Add the difference between `QM-TLS-01` and `QM-TLS-02`.
