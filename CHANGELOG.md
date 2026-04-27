# Changelog

## v2026.04.27-ef29982

Build source commit: `ef29982`

Upgrade notes:

- Adds the new controller `Wireless` submenu with `WiFi`, `ESP-NOW`, and `Radio Off` modes.
- Moves network information and network reset into the `Wireless` menu.
- Applies the polished main-menu visual treatment to controller submenus.
- Adds opportunistic environment sync between controller and remote: if one side has valid time/weather data and the other side does not, the next normal communication can share it.
- Refreshes the remote universal firmware package and controller firmware package.
- Includes regenerated Windows x64 and Apple Silicon macOS updater bundles for controller and remote.

Files:

- `SG98-Updater-win-x64.zip`
- `SG98-Updater-osx-arm64.zip`
- `SG98-Remote-Updater-win-x64.zip`
- `SG98-Remote-Updater-osx-arm64.zip`
- matching `.md5` checksum files

## v2026.04.27-388014f

Build source commit: `388014f`

- Initial public updater bundle release.
- Added hardware and communication guide.
- Added Waveshare 1.75 remote case print files.
