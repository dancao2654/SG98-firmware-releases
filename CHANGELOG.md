# Changelog

## v2026.04.28-f29f86a4

Build source commit: `f29f86a4`

Upgrade notes:

- Adds a cache-busted application URL to generated remote OTA manifests so device-side updates do not reuse stale GitHub Raw firmware binaries.
- Refreshes the public remote OTA application binary and manifests for `remote-universal-s3`.

Files:

- `ota/remote-universal-s3/sg98-ota-manifest.json`
- `ota/remote-universal-s3/sg98-flash-manifest.json`
- `ota/remote-universal-s3/flash-03-0x10000-firmware.bin`

## v2026.04.28-71159891

Build source commit: `71159891`

Upgrade notes:

- Hardens the remote home-Wi-Fi STA path using the same connection handling that fixed the controller.
- Adds USB diagnostic Wi-Fi fields for STA password length, active connect attempt, last STA event, and disconnect reason.
- Disables remote Wi-Fi modem sleep while Wi-Fi is active so saved home-network joins complete reliably.
- Refreshes the public remote OTA application binary and manifest for `remote-universal-s3`.

Files:

- `ota/remote-universal-s3/sg98-ota-manifest.json`
- `ota/remote-universal-s3/sg98-flash-manifest.json`
- `ota/remote-universal-s3/flash-03-0x10000-firmware.bin`

## v2026.04.28-6fd491b3

Build source commit: `6fd491b3`

Upgrade notes:

- Adds the polished LingLong SG-98 motor-detection screen with the generated grinder artwork.
- Refines controller and remote Wi-Fi/ESP-NOW status messaging, fallback notices, and bottom-curve network status styling.
- Improves remote idle clock visibility, charging/power-state indication, and Wi-Fi/AP connectivity behavior.
- Updates OTA download/update handling for the current controller and remote universal builds.
- Refreshes all public OTA application binaries and full first-time updater bundles for Windows x64 and Apple Silicon macOS.

Files:

- `bundles/SG98-Updater-win-x64.zip`
- `bundles/SG98-Updater-osx-arm64.zip`
- `bundles/SG98-Remote-Updater-win-x64.zip`
- `bundles/SG98-Remote-Updater-osx-arm64.zip`
- matching `.md5` checksum files
- `ota/controller-universal-s3/sg98-ota-manifest.json`
- `ota/controller-universal-s3/flash-03-0x10000-firmware.bin`
- `ota/remote-universal-s3/sg98-ota-manifest.json`
- `ota/remote-universal-s3/flash-03-0x10000-firmware.bin`

## v2026.04.28-190e8987

Build source commit: `190e8987`

Upgrade notes:

- Fixes the firmware OTA manifest resolver so both controller and remote point at the public `SG98-firmware-releases` raw URLs instead of private-source URLs.
- Fixes the remote dock clock timezone path so synced clock display uses local Pacific time instead of UTC.
- Adds a private-repo release maintenance document covering build, bundle, OTA, and public upload steps.
- Keeps generated firmware metadata clean even while tracked publish artifacts are changing during bundle generation.
- Refreshes all public OTA application binaries and full first-time updater bundles for Windows x64 and Apple Silicon macOS.

Files:

- `bundles/SG98-Updater-win-x64.zip`
- `bundles/SG98-Updater-osx-arm64.zip`
- `bundles/SG98-Remote-Updater-win-x64.zip`
- `bundles/SG98-Remote-Updater-osx-arm64.zip`
- matching `.md5` checksum files
- `ota/controller-universal-s3/sg98-ota-manifest.json`
- `ota/controller-universal-s3/flash-03-0x10000-firmware.bin`
- `ota/remote-universal-s3/sg98-ota-manifest.json`
- `ota/remote-universal-s3/flash-03-0x10000-firmware.bin`

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
