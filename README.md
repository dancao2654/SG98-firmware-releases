# SG98 Firmware Releases

Public download page for SG98 controller and remote firmware artifacts.

The source firmware repository is private. This repository is only for sharing installer bundles, device OTA files, checksums, and public hardware notes.

## Documentation

- [Hardware and communication guide](docs/hardware-and-communication.md) - supported controller/remote PCBs, purchasable hardware models, communication cases, and failover behavior.
- [Changelog](CHANGELOG.md) - public updater bundle release notes.
- [Waveshare 1.75 remote case print files](hardware/waveshare-1.75-remote-case/README.md) - STL files for the battery, magnet, and pressure-connector back-cover case.

## Downloads

Use the latest GitHub Release:

https://github.com/dancao2654/SG98-firmware-releases/releases/latest

The same full updater bundles are also committed under `bundles/` for simple
direct sharing from the public repository.

## Full Updater Bundles

- `SG98-Updater-win-x64.zip` - controller updater for Windows
- `SG98-Updater-osx-arm64.zip` - controller updater for Apple Silicon macOS
- `SG98-Remote-Updater-win-x64.zip` - remote updater for Windows
- `SG98-Remote-Updater-osx-arm64.zip` - remote updater for Apple Silicon macOS

Each zip has a matching `.md5` checksum file.

Do not cross-flash the bundles. Controller bundles are for SG98 controller hardware, and remote bundles are for SG98 remote hardware.

## Device OTA URLs

These public raw URLs are intended for device-side HTTPS OTA downloads:

- Controller OTA manifest:
  `https://raw.githubusercontent.com/dancao2654/SG98-firmware-releases/main/ota/controller-universal-s3/sg98-ota-manifest.json`
- Remote OTA manifest:
  `https://raw.githubusercontent.com/dancao2654/SG98-firmware-releases/main/ota/remote-universal-s3/sg98-ota-manifest.json`

Each OTA manifest points to the matching application firmware binary in the same folder and includes the SHA-256 hash and expected file size.
