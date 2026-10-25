# Changelog

All notable changes to Trakt are documented here. The format is based on
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/). The plugin is pre-stable, so it uses
[Semantic Versioning](https://semver.org) on `0.x.y` for now. Its first stable release will be its
first [Date Versioning](https://datevers.ing) release (`YY.MM.DD`, the UTC release date, with `-1`,
`-2`… for later releases the same day), and every release after that will be a Date Version too.
There will be no v1.0.0. Jellyfin shows each version with a fourth part: `0.2.0` is `0.2.0.0`.
Releases before v0.2.0 were first published with other numbers; each says which.

## v0.2.0

### Added
- `tests/run.sh` checks `VERSION.md`, the newest changelog heading, the version in `Directory.Build.props` and `meta.json`, and the versioning rules below. The release workflow runs it before building.

### Changed
- The plugin is pre-stable, so it's versioned with SemVer `0.x.y` until its first stable release, which will be its first [Date Versioning](https://datevers.ing) release (there will be no v1.0.0). The earlier releases have been relabelled: v1.0.0 is now v0.1.0, and v26.10.23 is now v0.1.1. Their GitHub releases and the plugin repository now use the new numbers, with each zip rebuilt from its tag to carry its new version. `commit.sh` / `commit.bat` and the release workflow accept `0.x.y` versions as well as Date Versions, and refuse `0.x.y` once a Date Version has been released.
- In Jellyfin this release is version `0.2.0.0`. If you installed v26.10.23 (shown as `26.10.23.0`) or a 1.x release, Jellyfin sees that as the newer version and won't offer this one as an update: uninstall the plugin, restart, and install it again from the catalogue. Your settings are kept.

## v0.1.1

_Released 2026-10-23 as v26.10.23._

### Changed
- Versions now follow [Date Versioning](https://datevers.ing): the UTC release date as `YY.MM.DD`, with `-1`, `-2`… for later releases the same day. Jellyfin shows this release as `26.10.23.0` and treats it as an update from v1.0.0, so nothing needs reinstalling. `commit.sh`/`commit.bat` now refuse to tag anything that isn't a real, non-future Date Version.

## v0.1.0

_Released 2026-09-29 as v1.0.0._

First release of Trakt as a standalone StuxieDev project, for Jellyfin 12.x. It is based on [jellyfin-plugin-trakt](https://github.com/jellyfin/jellyfin-plugin-trakt) 33 by the Jellyfin project.

### Added
- Published from [StuxieDev/TraktPlugin](https://github.com/StuxieDev/TraktPlugin), with its own plugin ID, repository manifest and banner.

### Changed
- Built against Jellyfin 12.0.0 (`targetAbi` 12.0.0.0), so it loads on every 12.x server.

### Fixed
- Syncing and scrobbling no longer stop for good after a failed token refresh. Trakt issues a new refresh token each time one is used, and two refreshes could run at once: the second sent the already-used token, got 400 (Bad Request), and every request after that failed with 401 (Unauthorized). Refreshes now run one at a time, and a refresh that another request already did is skipped.
- When Trakt really has revoked the sign-in, the plugin now signs that user out and logs that they need to authorize again, instead of retrying the dead token on every request.
- The settings page no longer shows a user as authorized after their sign-in has gone (it only checked the token wasn't `null`, and a failed refresh left it empty).
