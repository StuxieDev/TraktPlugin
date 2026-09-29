<p align="center">
  <img src="assets/logo.svg" alt="Trakt plugin logo" width="360">
</p>

# Trakt – Jellyfin Plugin

Syncs your [Jellyfin](https://jellyfin.org/) library and watch states with [trakt.tv](https://trakt.tv), and scrobbles what you watch as you watch it.

Built for **Jellyfin 12**.

## Installation

Add the plugin repository in Jellyfin under **Dashboard → Plugins → Repositories → +** :

```
https://github.com/StuxieDev/TraktPlugin/releases/latest/download/manifest.json
```

Then install **Trakt** from the plugin catalogue and restart Jellyfin.

**Moving from Jellyfin's official Trakt plugin:** uninstall it first, then install this one and restart. Both use the same settings file, so your settings and linked users carry over. This plugin has its own plugin ID, so the official repository can't "update" over it. If Trakt had stopped accepting your sign-in, authorize again in the plugin settings.

### Requirements

- Jellyfin 12.0 or newer
- A [trakt.tv](https://trakt.tv) account

## Setup

1. Open **Dashboard → Plugins → Trakt**.
2. Pick the Jellyfin user, select **Authorize Device**, and enter the code shown at [trakt.tv/activate](https://trakt.tv/activate).
3. Choose which libraries to sync and what to scrobble, then save.

Syncing runs as scheduled tasks under **Trakt** in **Dashboard → Scheduled Tasks**; scrobbling happens live during playback.

## Build from source

```bash
dotnet build Trakt/Trakt.csproj -c Release
```

See [CONTRIBUTING.md](CONTRIBUTING.md) for development and release details.

## Credits

Based on [jellyfin-plugin-trakt](https://github.com/jellyfin/jellyfin-plugin-trakt) by the Jellyfin project and contributors. Maintained by [StuxieDev](https://github.com/StuxieDev) as a standalone project, for Jellyfin 12. Uses the [Trakt API](https://trakt.docs.apiary.io/); not affiliated with trakt.tv.

© Leo Ridgwell (StuxieDev) for changes made since the original. Licensed under the [MIT License](LICENSE.md), like the code it's based on.
