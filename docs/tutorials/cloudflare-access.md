# Get past Cloudflare Access

- **You'll end up with:** a service behind Cloudflare Access that Quartermaster can connect to.
- **Takes:** about 10 minutes.

Cloudflare Access puts a login page in front of your service. That's great in a browser, but it blocks apps, so Quartermaster fails with **`QM-EDGE-01`**. The fix is a **service token**: a key that lets Quartermaster past the login page without weakening it for anyone else.

!!! info "Using Cloudflare Tunnel without Access?"
    A plain Tunnel is just another address and works normally. You only need this guide if there's an Access login page.

## 1. Create a service token

1. In the [Cloudflare dashboard](https://one.dash.cloudflare.com), go to **Zero Trust → Access → Service auth → Service Tokens**.
2. Click **Create Service Token** and name it, for example `Quartermaster`.
3. Copy the **Client ID** and **Client Secret**.

!!! warning
    Cloudflare only shows the **Client Secret** once. Copy it before you leave the page.

## 2. Allow the token on your application

1. Go to **Access → Applications** and open the application that protects your service.
2. Add a policy with the action **Service Auth**.
3. Under **Include**, choose **Service Token** and pick the token you just made.
4. Save.

## 3. Save the headers in Quartermaster

You only do this once per domain. Every service on that domain then uses them automatically.

1. Tap the **profile icon** at the top right of Home, then **Profiles**.
2. Tap the **key icon** on your profile to open its credentials.
3. Scroll to **Edge access by domain** and tap **Add domain**.
4. Enter your domain, for example `example.com`. The two header names are already filled in, so just paste the values:

    | Header name | Value |
    |---|---|
    | `CF-Access-Client-Id` | Your Client ID |
    | `CF-Access-Client-Secret` | Your Client Secret |

5. Tap **Save**.
6. Open a service on that domain and tap **Test**. Its **Cloudflare Access** dropdown shows the saved domain. You can also pick it there when adding a new service.

## If it still fails

??? question "Still QM-EDGE-01, or a login page"
    - Check the policy action is **Service Auth**, not **Allow**.
    - Check the token is included in **that** application's policy.
    - Check both headers are spelled exactly as above.
    - Check the service's address is on the domain you saved, and that its **Cloudflare Access** dropdown doesn't say **None**.

??? question "“Cloudflare is rate-limiting, backed off” (QM-EDGE-02)"
    Cloudflare's bot protection is slowing Quartermaster down, so the app backs off to keep your address from being blocked. Relax bot protection for that hostname, or connect over [Tailscale](tailscale.md) instead.

!!! note "SSH"
    This doesn't work for SSH. Cloudflare Access SSH hostnames that need the `cloudflared` client aren't supported. Use Tailscale, WARP, a VPN or a forwarded port.
