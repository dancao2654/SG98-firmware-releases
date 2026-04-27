# SG98 Hardware And Communication Guide

This document covers the public release bundles, the expected controller and remote hardware, and the normal communication and recovery behavior between the SG98 remote and controller.

The firmware source is private. The updater bundles in this release repository are the supported public installer path.

## Hardware Requirements

### Controller

Use the controller updater bundle only on SG98 controller-compatible ESP32-S3 hardware.

Required controller hardware:

- ESP32-S3 based controller target supported by the SG98 controller firmware.
- SG98-compatible controller pinout or carrier PCB.
- Supported motor-driver wiring and firmware profile, such as the SG98 JMC, RT, or KRS motor-driver configuration.
- Stable controller power supply sized for the controller, display, motor-driver interface, and any attached peripherals.
- USB connection for firmware update and service access.

Supported controller styles:

- Full-size controller with local display, buttons, and encoder.
- Headless controller with no local UI. A headless controller must keep a recoverable radio path, so firmware prevents unrecoverable radio-off states.

Optional controller hardware:

- Local screen, side buttons, and encoder on full-size builds.
- BLE scale for grind-by-weight operation.
- Home Wi-Fi access for setup, web UI, time sync, and environment sync.

### Remote

Use the remote updater bundle only on SG98 remote-compatible ESP32-S3 handheld hardware.

Required remote hardware:

- ESP32-S3 based SG98 remote target supported by the SG98 remote firmware.
- Supported round display and touch/input hardware for the selected SG98 remote build.
- Supported run/menu controls.
- USB connection for firmware update and service access.

Supported remote features depend on the specific SG98 remote hardware:

- Touch screen and/or rotary input.
- Battery, USB power, and charging status display.
- Motion sensor for wake and screen orientation where present.
- Pressure sensor input and BLE transducer/profiler mode where wired and enabled.

### Update Bundle Selection

| Bundle | Use on | Host computer |
| --- | --- | --- |
| `SG98-Updater-win-x64.zip` | SG98 controller | Windows x64 |
| `SG98-Updater-osx-arm64.zip` | SG98 controller | Apple Silicon macOS |
| `SG98-Remote-Updater-win-x64.zip` | SG98 remote | Windows x64 |
| `SG98-Remote-Updater-osx-arm64.zip` | SG98 remote | Apple Silicon macOS |

Each zip has a matching `.md5` checksum file in the same release.

## Communication Scheme

The SG98 system is designed around a low-resource remote-to-controller link, with Wi-Fi used mainly for setup, web access, and recovery.

### Default Link: ESP-NOW

The normal parked state is ESP-NOW:

- Controller radio state: `Wi-Fi disabled` in the user menu.
- Remote radio state: ESP-NOW remote link.
- Wi-Fi AP and home Wi-Fi client are off.
- Remote commands, status polling, menu reads/writes, heartbeats, and environment sync all use ESP-NOW frames.

ESP-NOW is the preferred final state whenever a remote and controller are paired and operating normally.

### Discovery And Pairing

On a fresh pair or after recovery:

1. The remote sends `DISCOVER` over ESP-NOW while scanning for a controller.
2. The controller answers with a peer frame containing controller identity, target, MAC address, and channel.
3. The remote locks onto that controller peer and continues with normal command/status traffic.
4. Once the link is healthy, both sides stay in the ESP-NOW parked state unless Wi-Fi is intentionally enabled for setup or web access.

### Command And Status Frames

The SG98 remote protocol is text framed. The main frames include:

| Frame | Direction | Purpose |
| --- | --- | --- |
| `DISCOVER` | Remote to controller | Find a controller over ESP-NOW. |
| `PEER` | Controller to remote | Tell the remote the controller identity, MAC, target, and radio channel. |
| `START`, `STOP`, `IDLE`, `IDLE_GBW` | Remote to controller | Control grinder state. |
| `SET_RPM`, `SET_WEIGHT` | Remote to controller | Send grind speed and target weight values. |
| `GET_STATUS`, `STAT` | Both directions | Poll and report controller state, motor state, scale state, RPM, weight, Wi-Fi status, and menu state. |
| `GET_MENU`, `SET_MENU`, `MENU` | Both directions | Read and update controller menu values. |
| `ACTION` | Remote to controller | Trigger named controller actions. |
| `HEARTBEAT` | Remote to controller | Keep the link alive and prove remote presence. |
| `GET_ENV`, `ENV` | Both directions | Share time, weather, and location environment data. |
| `WIFI` | Remote to controller | Send Wi-Fi SSID/password setup data over the SG98 protocol. |

Wi-Fi credentials are hex-encoded inside the protocol frame before being sent across the link.

### Wi-Fi Setup And Web UI

When Wi-Fi is enabled from the controller menu:

- The controller opens its Wi-Fi setup/web session.
- The controller AP is reachable at `http://192.168.4.1` when the phone/tablet/computer is connected to the SG98 controller AP.
- Wi-Fi is treated as a temporary setup/control session, not the preferred parked state.
- ESP-NOW remote control is paused during the temporary Wi-Fi session and resumes when the controller parks back to ESP-NOW.
- After home Wi-Fi is connected and internet/environment sync completes, the controller shuts down the Wi-Fi session and parks back in ESP-NOW.
- If the Wi-Fi session is idle for 10 minutes, the controller also parks back in ESP-NOW.

If the phone captive portal does not open automatically, connect to the SG98 AP and manually open:

```text
http://192.168.4.1
```

### User-Facing Radio Controls

| UI wording | Internal behavior | Normal use |
| --- | --- | --- |
| Wi-Fi disabled | ESP-NOW parked state | Lowest resource mode for remote/controller operation. |
| Wi-Fi enabled | Temporary Wi-Fi setup/web session | Configure home Wi-Fi, use web UI, sync time/weather, then return to ESP-NOW. |
| Radio off | All radio disabled | Full-size controller local-only use. Not allowed on headless builds. |

ESP-NOW is intentionally presented as `Wi-Fi disabled` because users normally care whether phone/web Wi-Fi is open. Internally, this is still the normal remote-control radio path.

## Connection And Failover Cases

| Case | Controller behavior | Remote behavior | Failover protection | Final expected state |
| --- | --- | --- | --- | --- |
| Fresh controller and remote, no saved Wi-Fi | Boots into ESP-NOW parked state. | Scans with ESP-NOW discovery. | Remote repeats discovery until a controller answers. | Remote and controller linked by ESP-NOW, Wi-Fi off. |
| Full-size controller used alone | Remains locally usable with screen/buttons/encoder. | Not required. | Local controls can enable Wi-Fi or radio off as needed. | User-selected local state. |
| Headless controller boots with no remote nearby | Starts in ESP-NOW and waits for valid remote traffic. | Offline or out of range. | If no remote traffic is heard for about 60 seconds, controller opens Wi-Fi recovery. | Recovery AP/web session available, then ESP-NOW after recovery. |
| Remote goes out of range after a healthy link | Tracks last valid ESP-NOW command/heartbeat. | Becomes silent. | Headless controller opens Wi-Fi recovery after about 60 seconds of silence. | Recovery AP/web session, then ESP-NOW after remote returns. |
| Remote link is lost while grinding/running | Controller keeps motor safety locally. | Becomes silent. | Headless remote deadman stops motor states after about 7.5 seconds without remote traffic, then network recovery can open Wi-Fi if silence continues. | Safe idle/recovery, then ESP-NOW after relink. |
| User enables Wi-Fi for setup | Starts AP/web setup session at `192.168.4.1`. | Remote link waits for the controller to park back to ESP-NOW. | Wi-Fi session has an idle timeout and does not persist as the default boot state. | Back to ESP-NOW after internet sync or 10-minute idle timeout. |
| Home Wi-Fi setup completes | Connects to home Wi-Fi and syncs internet time/weather when available. | Receives environment data after ESP-NOW resumes. | After sync is complete, controller closes Wi-Fi to avoid resource hogging. | ESP-NOW parked state. |
| Captive portal does not pop up | AP still serves the setup page when Wi-Fi session is active. | Not required. | User can manually browse to `http://192.168.4.1`. | Setup page opens, then ESP-NOW after setup/sync. |
| Remote has saved Wi-Fi but cannot find ESP-NOW peer | Controller may be on recovery/web session or unreachable. | Remote tries ESP-NOW first, then recovery paths where available. | Remote returns to ESP-NOW once a peer is discovered again. | ESP-NOW parked state. |
| User selects Radio off on full-size controller | Radio is disabled. | Remote cannot control while radio is off. | Allowed only because local UI exists to recover. | Local-only until user re-enables Wi-Fi or ESP-NOW. |
| Radio off requested on headless controller | Request is rejected or sanitized. | Remote remains the recovery path. | Firmware avoids stranding a controller with no local UI. | Wi-Fi recovery or ESP-NOW, never unrecoverable radio off. |

## Failover Protections

The firmware includes several protections so a controller is not stranded:

- Boot recovery for headless controllers: if no valid ESP-NOW remote traffic appears within about 60 seconds, Wi-Fi recovery opens.
- Remote-lost recovery for headless controllers: if a previously linked remote goes silent for about 60 seconds, Wi-Fi recovery opens.
- Running-state deadman: a headless controller stops motor states after about 7.5 seconds without expected remote traffic.
- Wi-Fi idle parking: a Wi-Fi setup/web session parks back to ESP-NOW after 10 minutes of no web activity.
- Internet-sync parking: after home Wi-Fi is configured and time/weather sync completes, Wi-Fi closes and the controller returns to ESP-NOW.
- Headless radio-off guard: headless builds reject or sanitize radio states that would remove both local and wireless recovery paths.
- Boot sanitization: temporary web states are not treated as permanent boot destinations; the firmware prefers ESP-NOW on normal startup.

## Quick Troubleshooting

| Symptom | What to try |
| --- | --- |
| Phone joins SG98 AP but no captive portal appears | Open `http://192.168.4.1` manually. |
| Controller seems stuck in Wi-Fi setup | Complete home Wi-Fi setup and wait for sync, wait for the 10-minute idle timeout, or reboot to return to ESP-NOW. |
| Remote cannot find controller | Keep both devices close, reboot the controller, and allow discovery/recovery time. A headless controller should open Wi-Fi recovery if it hears no remote traffic. |
| Full-size controller is in Radio off | Use the local controller UI to re-enable Wi-Fi or return to `Wi-Fi disabled` for ESP-NOW operation. |
| Wrong updater bundle was selected | Stop before flashing. Use controller bundles only for controller hardware and remote bundles only for remote hardware. |
