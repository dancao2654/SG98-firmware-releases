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

Current version: **2026.10.25.1**, build source `e9995562`.

| Platform | Controller | Remote |
| --- | --- | --- |
| Windows x64 | [Download](https://github.com/dancao2654/SG98-firmware-releases/releases/download/v2026.10.25.1-e9995562/SG98-Updater-2026.10.25.1-win-x64.zip) | [Download](https://github.com/dancao2654/SG98-firmware-releases/releases/download/v2026.10.25.1-e9995562/SG98-Remote-Updater-2026.10.25.1-win-x64.zip) |
| Intel Mac | [Download](https://github.com/dancao2654/SG98-firmware-releases/releases/download/v2026.10.25.1-e9995562/SG98-Updater-2026.10.25.1-osx-x64.zip) | [Download](https://github.com/dancao2654/SG98-firmware-releases/releases/download/v2026.10.25.1-e9995562/SG98-Remote-Updater-2026.10.25.1-osx-x64.zip) |
| Apple Silicon Mac | [Download](https://github.com/dancao2654/SG98-firmware-releases/releases/download/v2026.10.25.1-e9995562/SG98-Updater-2026.10.25.1-osx-arm64.zip) | [Download](https://github.com/dancao2654/SG98-firmware-releases/releases/download/v2026.10.25.1-e9995562/SG98-Remote-Updater-2026.10.25.1-osx-arm64.zip) |

Each zip has a matching `.md5` compatibility checksum. SHA-256 values are in
`bundles/SHA256SUMS-2026.10.25.1.txt` and the release manifest. Previous bundle
filenames and OTA binaries are preserved.

TSE-family support follows the family manual and is not yet validated on the
TSE-B-D-100-KFM hardware. Read the [TSE setup guide](docs/TSE-Servo-Setup.md)
before use. Existing input safety settings are not automatically remapped;
incompatible settings keep the drive NOT READY. Shared ramp mapping and
automatic torque calibration are not implemented for TSE.

Do not cross-flash the bundles. Controller bundles are for SG98 controller hardware, and remote bundles are for SG98 remote hardware.

## Device OTA URLs

These public raw URLs are intended for device-side HTTPS OTA downloads:

The controller, universal remote, and Waveshare 1.75 remote OTA channels are
paired at **2026.10.27.1** (`438efcc3-dirty`). This validation build includes
the remote's graphical System Update screen and the captured KFM detection
signature. KFM motor run control is not hardware-validated; do not treat
successful detection as authorization to run an uncommissioned drive.

- Controller OTA manifest:
  `https://raw.githubusercontent.com/dancao2654/SG98-firmware-releases/main/ota/controller-universal-s3/sg98-ota-manifest.json`
- Remote OTA manifest:
  `https://raw.githubusercontent.com/dancao2654/SG98-firmware-releases/main/ota/remote-universal-s3/sg98-ota-manifest.json`
- Waveshare 1.75 remote OTA manifest:
  `https://raw.githubusercontent.com/dancao2654/SG98-firmware-releases/main/ota/remote-waveshare-175/sg98-ota-manifest.json`

Each OTA manifest points to the matching application firmware binary in the same folder and includes the SHA-256 hash and expected file size.
