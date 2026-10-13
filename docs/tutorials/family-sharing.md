# Share your library with family

- **You'll end up with:** a Family & Friends profile that lets people browse your library and request titles, without touching your settings.
- **Takes:** about 5 minutes.
- **Needs:** **Pro** to set up sharing. Joining is **free**, so the people you share with don't need Pro.

## Before you start

- **Seerr** (or Jellyseerr) must be connected in Quartermaster. Radarr and Sonarr alone don't allow requests.
- Decide which **Seerr user** their requests should come from. You'll pick it as **Requests as** in step 2.

!!! info "Still on Jellyseerr or Overseerr?"
    They still work, but they're no longer maintained, so we recommend moving to **Seerr**.

## 1. Create the profile

1. Tap the **profile icon** at the top right of Home, then **Profiles**.
2. Tap **+** at the top right.
3. Under **New profile**, tap **Family & Friends**.

## 2. Set it up

| Setting | What to choose |
|---|---|
| **Name** | Anything you like, such as `Family & Friends` or a person's name |
| **Requests through** | Your Seerr service |
| **Requests as** | The Seerr user their requests are made as |

Tap **Create Family & Friends**. The new profile appears under **Profiles**.

!!! note "Your owner PIN"
    Your settings and service management stay behind your **owner PIN**. The PIN keeps honest fingers out, but it isn't device security: deleting the app removes it.

## 3. Choose how they'll connect

Quartermaster asks **How is this person connecting?**

=== "They'll use this device"

    For a shared iPad or a phone you hand across.

    Switch to their profile when you pass it over. Your **PIN** brings you back to yours. You're done, so skip the rest of this tutorial.

=== "They've got their own device"

    Send them an invite to scan or tap. Carry on with step 4.

## 4. Check where they'll connect from

Under **Before you share**, choose:

| Option | When |
|---|---|
| **On your home Wi-Fi** | They'll only use it at your house. Nothing to set up |
| **From anywhere** | Their own house, school, out and about. Quartermaster checks that every service in the profile can be reached from outside your home |

If **From anywhere** finds a service that can't leave the house, give it an away address first. See [Use Quartermaster away from home](tailscale.md).

## 5. Set a passphrase

Under **Set up their device**, enter a **passphrase** of at least 8 characters and confirm it. Then tap **Set up their device**.

The invite carries **only this profile and its services**, protected by the passphrase.

## 6. Send it to their device

=== "Scan with their phone"

    1. On **their** device, install [Quartermaster](https://apps.apple.com/gb/app/quartermaster-homelab-stack/id6779994284), open it and tap **I was given access**, then **Scan their screen**.
    2. Point it at the QR code on your screen. Larger profiles use more than one code, such as *Code 1 of 2*, so tap the arrow to show the next one.
    3. **Tell them the passphrase out loud.** Don't send it in the same message as the invite.

=== "Share as a file"

    1. Tap **Share as a file instead** and send it by AirDrop, Messages or email.
    2. On **their** device, install Quartermaster, then go to **Settings → Backup → Import** and open the file.
    3. Give them the passphrase separately.

## Tips

- Requests follow your **Seerr** settings for the **Requests as** user, so set request limits and auto-approval there.
- To change what's in their profile later, use **Edit Stack** while the Family & Friends profile is selected. **Migrate between profiles** copies services from one profile into another.
- To stop sharing, delete the Family & Friends profile, and disable or change that Seerr user's password in Seerr.
