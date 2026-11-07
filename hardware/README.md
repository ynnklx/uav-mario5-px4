# Hardware

## Bill of materials

| Component | Part | Notes |
|---|---|---|
| Frame | 5" FPV quadcopter frame | model: tbd |
| Motors | iFlight XING2 2207, 1855 KV | 14 poles (`MOT_POLE_COUNT = 14`) |
| Propellers | tbd | baseline for the propeller comparison |
| Flight controller | MicoAir H743 V2 | STM32H743 |
| ESC | MicoAir 55 A, AM32 | bidirectional DShot600 |
| GNSS / compass | HGLRC M100 | |
| Telemetry radio | Holybro Telemetry Radio V3 | MAVLink to QGroundControl |
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

Build photos go into [`photos/`](photos/). Naming: `YYYY-MM-DD_short-description.jpg`, resized to max. 1600 px, EXIF data removed.
