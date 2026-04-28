# Changelog

## v2026.04.28-79aafbf3

Build source commit: `79aafbf3`

Upgrade notes:

- Adds OTA-capable controller and remote firmware builds.
- Adds public OTA manifest and application binary files for device-side HTTPS download.
- Keeps full first-time updater bundles available for Windows x64 and Apple Silicon macOS.
- Improves the firmware About page so version, build, OTA slot, and update information are readable as a real child page.
- Includes the latest controller/remote communication, wireless, menu, and remote UI fixes from the private firmware source.

Files:

- `SG98-Updater-win-x64.zip`
- `SG98-Updater-osx-arm64.zip`
- `SG98-Remote-Updater-win-x64.zip`
- `SG98-Remote-Updater-osx-arm64.zip`
- matching `.md5` checksum files
- `ota/controller-universal-s3/sg98-ota-manifest.json`
- `ota/controller-universal-s3/flash-03-0x10000-firmware.bin`
- `ota/remote-universal-s3/sg98-ota-manifest.json`
- `ota/remote-universal-s3/flash-03-0x10000-firmware.bin`

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
