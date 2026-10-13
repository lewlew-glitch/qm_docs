# Apple TV *(beta)*

Quartermaster for Apple TV is in **beta through TestFlight**, with testers from the Discord. It isn't on the App Store yet.

[Ask to join on Discord](https://discord.gg/ecFz4WsVVB){ .md-button .md-button--primary }

Report bugs in **#tvos-bug-reports**, ideally with a photo or video.

## Requirements

- **tvOS 18** or later
- **Jellyfin**, **Plex**, or **Emby**, with **Seerr** for requests
- An iPhone running **Quartermaster 1.3** with **iCloud Sync** turned on
- The Apple TV signed in to the **same Apple Account** as the iPhone
- **Pro**. During the beta, access follows the Pro subscription on the iPhone that set it up. After release, the app will be free to download, and Pro will unlock it.

## Pairing

1. On the Apple TV, open Quartermaster and choose **Set Up from iPhone**. It shows a **six-digit code** and a **QR code**. The code changes every ten minutes.
2. On the iPhone, go to **Settings → Apple TV** (also in **Backup & sync**).
3. Enter the code, or tap **Scan QR code**, then tap **Find Apple TV**.
4. The sync passphrase goes to the Apple TV through **your iCloud**, never through Quartermaster's servers.

An Apple TV you've already set up shows on this screen once it opens Quartermaster. That can take a minute to come through iCloud.

If you don't have an iPhone set up, choose **Try the Demo** on the Apple TV's welcome screen.

## Oracle player

**Oracle** is the default player in the beta. It plays the **original file** from Jellyfin, Emby or Plex with no server-side conversion. It's built on FFmpeg 8.1 together with Apple TV's own decoders and renderers.

| | Support |
|---|---|
| **Containers** | MKV, MP4, transport streams |
| **Video** | HEVC and H.264 (hardware). VC-1 and MPEG-2 (software). Deinterlaces interlaced recordings |
| **HDR** | HDR10, Dolby Vision profiles 5 and 8.1 passed through. Profile 7 converted to 8.1 on the fly |
| **Audio** | Dolby Digital and Dolby Digital Plus (Apple decoders). TrueHD, DTS, DTS-HD MA and FLAC decoded to multichannel PCM |
| **Subtitles** | Styled text, including ASS and SSA. PGS and VobSub shown as-is. Forced lines appear even with subtitles off |

**Controls:** Swipe down for audio, subtitles, chapters and **Playback Info** (decoder, HDR format, audio path). Scrubbing shows previews, intros can be skipped and Up Next plays the next episode.

**Server sync:** The Apple TV shows up in Jellyfin's Now Playing. Position and watched status sync back to the server.

**Fallback:** You can choose Apple's own player in Settings. Files Oracle can't play go to Apple's player automatically.

## Profiles

- Every Jellyfin or Emby account gets its own profile.
- Admins sign in with a **4-digit PIN**.
- Other users only see what their account can access.
- Each profile can set its own icon, theme (Automatic, Light or Dark), accent colour and text size (three options).

## Home

Up Next, downloads, upcoming titles, shelves, and browsing by genre and decade.

- **Requests** go through Seerr and follow its hide settings. You can choose seasons.
- **Deleting** films, series or seasons needs delete permission on the user's Jellyfin account. Items are disabled in Sonarr first so they don't download again.

## Command Centre *(admins only)*

Shows tiles, machines, Now Playing, downloads and requests, with problems at the top. **Keep on Screen** keeps it visible. The **Calendar** is also admin-only.

Servers with **self-signed certificates** can be trusted once you've checked the fingerprint.
