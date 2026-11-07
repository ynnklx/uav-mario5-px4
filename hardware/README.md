# Hardware

## Bill of materials

| Component | Part | Notes |
|---|---|---|
| Frame | 5" FPV quadcopter frame | model: tbd |
| Motors | iFlight XING2 2207, 1855 KV | 14 poles (`MOT_POLE_COUNT = 14`) |
| Propellers | tbd | baseline for the propeller comparison |
| Flight controller | MicoAir H743 V2 | STM32H743, onboard compass QMC5883L |
| ESC | MicoAir 55 A, AM32 | bidirectional DShot600, 1000 µF capacitor on battery pads |
| GNSS / compass | HGLRC M100-5883 | QMC5883 compass |
| Telemetry radio | Holybro Telemetry Radio V3, 433 MHz | MAVLink to QGroundControl |
| RC receiver | ExpressLRS | CRSF protocol (`RC_INPUT_PROTO = 6`) |
| Battery | 6S 1300 mAh LiPo | |
| Video | DJI O3 Air Unit | currently removed |

## Weights

| Configuration | Mass |
|---|---|
| Dry (no battery) | tbd |
| With 6S 1300 mAh LiPo | tbd |

## Wiring

Wiring diagram: tbd (`hardware/wiring.png`)

## Photos

Naming: `YYYY-MM-DD_NN_short-description.jpg`, resized to max. 1600 px, EXIF data (incl. GPS) removed.

| File | Content |
|---|---|
| [`2026-11-04_01_components.jpg`](photos/2026-11-04_01_components.jpg) | New components: ESC, FC, telemetry radio, GNSS, ELRS receiver, motors, DJI O3 |
| [`2026-11-04_02_frame-parts.jpg`](photos/2026-11-04_02_frame-parts.jpg) | Frame stripped down |
| [`2026-11-04_03_esc-capacitor.jpg`](photos/2026-11-04_03_esc-capacitor.jpg) | ESC with capacitor |
| [`2026-11-04_04_esc-motors-mounted.jpg`](photos/2026-11-04_04_esc-motors-mounted.jpg) | ESC mounted, motors soldered |
| [`2026-11-04_05_fc-gnss-telemetry-wiring.jpg`](photos/2026-11-04_05_fc-gnss-telemetry-wiring.jpg) | FC, GNSS and telemetry wiring |
| [`2026-11-04_06_assembled.jpg`](photos/2026-11-04_06_assembled.jpg) | Assembled with battery |
