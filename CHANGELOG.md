# Changelog

All notable changes to Trakt are documented here. The format is based on
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project
adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## v1.0.0

First release of Trakt as a standalone StuxieDev project, for Jellyfin 12.x. It is based on [jellyfin-plugin-trakt](https://github.com/jellyfin/jellyfin-plugin-trakt) 33 by the Jellyfin project.

### Added
- Published from [StuxieDev/TraktPlugin](https://github.com/StuxieDev/TraktPlugin), with its own plugin ID, repository manifest and banner.

### Changed
- Built against Jellyfin 12.0.0 (`targetAbi` 12.0.0.0), so it loads on every 12.x server.

### Fixed
- Syncing and scrobbling no longer stop for good after a failed token refresh. Trakt issues a new refresh token each time one is used, and two refreshes could run at once: the second sent the already-used token, got 400 (Bad Request), and every request after that failed with 401 (Unauthorized). Refreshes now run one at a time, and a refresh that another request already did is skipped.
- When Trakt really has revoked the sign-in, the plugin now signs that user out and logs that they need to authorize again, instead of retrying the dead token on every request.
- The settings page no longer shows a user as authorized after their sign-in has gone (it only checked the token wasn't `null`, and a failed refresh left it empty).
