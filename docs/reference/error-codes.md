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

### Reachability

| Code | Meaning | What to do |
|---|---|---|
| `QM-NET-01` | Can't reach the host: DNS failed, the connection was refused, or the host is unreachable | Check the address, port and network. See [Reachable](faq.md#connecting-and-networking) |
| `QM-NET-02` | Timed out | The host is slow or blocked. Check firewalls and VPNs |

### TLS

| Code | Meaning | What to do |
|---|---|---|
| `QM-TLS-01` | Self-signed, and can't be pinned | Use `http://` (not for TrueNAS) or a real certificate |
| `QM-TLS-02` | Self-signed, but can be pinned | Check the SHA-256 fingerprint in the trust prompt and tap **Trust**. See [self-signed certificates](faq.md#connecting-and-networking) |
| `QM-TLS-03` | A pinned certificate changed | Only trust it again if you expected the change, such as a renewed certificate or rebuilt container |

### Auth and content

| Code | Meaning | What to do |
|---|---|---|
| `QM-AUTH-01` | The key or Web UI login was rejected | Copy the key again. Make sure it's the right kind (for example SABnzbd's API Key, not its NZB Key) |
| `QM-HTTP-01` | An unexpected HTTP response, often a wrong URL or a missing subpath | Add the URL Base, for example `/radarr` |
| `QM-HTTP-02` | The service or its proxy returned HTTP 429, and the app backed off | Wait a moment, or relax rate limiting on the service or proxy |
| `QM-DATA-01` | A page came back that wasn't the service's API, usually a login or proxy page | Point the address directly at the service, or add a bypass for the API |

### Edge

| Code | Meaning | What to do |
|---|---|---|
| `QM-EDGE-01` | A Cloudflare Access challenge answered instead of the service | Save an Access service token's headers under **Profiles → key icon → Edge access by domain**. See [the tutorial](../tutorials/cloudflare-access.md) |
| `QM-EDGE-02` | Cloudflare is rate-limiting, and the app backed off | Relax bot protection for that hostname, or connect over Tailscale or your LAN |

### Outside the connection test

| Code | Meaning | What to do |
|---|---|---|
| `QM-URL-01` | The address isn't a valid URL | Check the format, for example `http://192.168.1.20:7878` |
| `QM-OPEN-01` | A deep link into a media server didn't resolve | Check the media server's app is installed. For Plex, try **Settings → Media & Reader → Open in Plex → Web** |
