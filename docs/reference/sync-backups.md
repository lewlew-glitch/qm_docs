# Sync and backups

Find these in **Settings → Backup & sync**.

## iCloud Sync

iCloud Sync keeps your services and settings the same across your devices, and it's protected by a **passphrase**.

- **Change the passphrase** whenever you like.
- **Forgot it?** Restart iCloud Sync from another device.
- Your config is encrypted with your passphrase and synced through **your own iCloud**. Quartermaster keeps no copy.
- **Pro isn't synced.** It follows your Apple ID. Only the date it renews or ends travels with your setup, so the Apple TV beta knows it's still active.
- The Apple TV beta gets the passphrase through your own iCloud. See [Apple TV](../platforms/apple-tv.md#pairing).

## Backups

Backups include your service connections. Your **TMDB key** is included, encrypted, in both backups and iCloud Sync.

### Export a backup *(Pro)*

1. Go to **Settings → Backup & sync → Export backup**.
2. Choose a passphrase. It's the only way back into the file, and Quartermaster keeps no copy of it.
3. Tap **Encrypt & share** and save the `.qmbackup` file somewhere safe, such as iCloud Drive.

### Restore a backup

- **On a fresh install:** choose **Restore from a backup** on the welcome screen, pick the file and enter its passphrase.
- **On a device that's already set up:** go to **Settings → Backup & sync → Import backup**, pick the file, unlock it, then choose to **merge** it with what's there or **replace** everything.

!!! note "Not included in a backup"
    The persistent QM Companion link, certificate pins and SSH host trust. Pair Companion again on the new device. Pins and host keys are learned again as you connect.

## Reset

**Delete everything & start over** removes all services, profiles, keys and settings, then restarts setup. It **can't be undone**, so export a backup first. Your Pro purchase stays on your Apple ID.
