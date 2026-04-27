# Waveshare 1.75 Remote Case Print Files

This folder contains the current 3D-print back-cover case concept for the SG98 remote built around the Waveshare `ESP32-S3-Touch-AMOLED-1.75` board.

The case sits below the remote, locates the remote into a deep open-sided round upper socket, and covers the battery and pressure-sensor wiring behind the remote. The body is intentionally narrower than the remote so the USB-C and button sides stay exposed.

## Printable STL Files

Use these files for printing:

| File | Purpose |
| --- | --- |
| [`print_files/sg98_remote_backcover_shell.stl`](print_files/sg98_remote_backcover_shell.stl) | Main lower shell with the deep remote socket, wiring cavity, recessed pressure-connector bay, and bottom-lid snap slots. |
| [`print_files/sg98_remote_backcover_bottom_lid.stl`](print_files/sg98_remote_backcover_bottom_lid.stl) | Snap-in bottom lid with an internal recessed pocket for a `10 x 60 x 1.5 mm` magnet strip. |
| [`print_files/sg98_pressure_socket_snap_cover.stl`](print_files/sg98_pressure_socket_snap_cover.stl) | Optional snap cover for the recessed pressure connector when the sensor cable is not attached. |

The printable STLs contain only the plastic case parts.

## Preview Files

- [`sg98_remote_case_preview.png`](sg98_remote_case_preview.png): case layout preview.
- [`sg98_remote_case_preview.svg`](sg98_remote_case_preview.svg): vector case preview.
- [`sg98_pressure_connector_recess_mockup.png`](sg98_pressure_connector_recess_mockup.png): recessed connector mockup.
- [`sg98_pressure_connector_recess_mockup.svg`](sg98_pressure_connector_recess_mockup.svg): vector connector mockup.
- [`preview_files/sg98_remote_backcover_fit_check_assembly_NOT_FOR_PRINT.stl`](preview_files/sg98_remote_backcover_fit_check_assembly_NOT_FOR_PRINT.stl): preview-only fit-check assembly with a dummy remote body.

Do not print the `NOT_FOR_PRINT` assembly STL as the final case. It exists only to show how the remote sits in the socket.

## Source Dimensions

- Waveshare module outside diameter: `48.96 mm`
- Visible display area: `44.16 mm`
- Round PCB reference: `46.0 mm`
- Vendor total module height: `10.4 mm`
- Battery: `25.5 x 37.0 x 4.3 mm`
- Magnet strip: `10.0 x 60.0 x 1.5 mm`
- Back-cover body: `44.0 x 70.0 mm`

## Pressure Connector

The pressure connector bay is designed for a compact detachable 3-pin connector instead of a hardwired sensor cable.

Recommended connector concept:

- Remote/case side: recessed female panel-mount connector.
- Sensor cable side: matching male plug.
- Current CAD target: compact 3-pin M5 A-coded pair.
- Connector pocket: about `22.0 x 10.0 mm`.
- Center bore: about `5.8 mm`.
- Connector mounting plane: about `4.0 mm` behind the outer lip.

Connector pins:

- `SUP / +5V`
- `OUT / pressure signal`
- `GND`

Use a keyed or locking connector so the sensor cannot be reversed. Measure the exact connector body, nut, and solder-cup clearance before final printing; this is still a fit-check design.

## Battery And Charging

The LiPo battery stays on the Waveshare board battery connector. Do not wire the battery to the pressure connector or to the H2 header.

USB-C charging is handled by the board PMIC. If adding external 5V charging contacts, wire them only to:

- `H2 pin 8 = VBUS / +5V`
- `H2 pin 7 = GND`

## Print Notes

- Treat these files as a first fit-check prototype.
- Start with PLA or PETG at `0.2 mm` layer height.
- Use 3 walls and 20-30% infill.
- Print the bottom lid with the smooth outside face on the bed and the magnet pocket/snaps upward.
- Print the main shell with supports enabled for the internal overhangs.
- PETG is preferred over brittle PLA for snap tabs.
- If the snap tabs are too tight, sand the four tabs slightly instead of forcing the lid.
- Put thin foam or Kapton between the battery pouch and PCB.
- Do not clamp the battery pouch tightly; keep at least `0.5-0.7 mm` height clearance.
