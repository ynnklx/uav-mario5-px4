# 01: From Betaflight via ArduPilot to PX4

**Period:** 2026-11-01 to 2026-11-05
**Result:** aircraft rebuilt on a new flight stack, all systems working, first indoor hover successful

The aircraft started as a Betaflight FPV quad. The goal was to learn ArduPilot, MAVLink and QGroundControl on the existing hardware first and then move to PX4 on a flight controller with enough resources for a full autopilot.

## Stage 1: Betaflight (starting point)

| Component | Part |
|---|---|
| Flight controller | SpeedyBee F405 V4 |
| ESC | 4-in-1, J-H-40, Bluejay 0.21.0, 48 kHz |
| Video | DJI O3 (DisplayPort OSD) |
| Receiver | ExpressLRS (CRSF) |
| GNSS | GEP-M10, no compass |
| Battery | 6S 1300 mAh |

Full configuration backup before reflashing: [`params/legacy/2026-11-01_betaflight_speedybeef405v4_cli-dump.txt`](../../params/legacy/)

## Stage 2: ArduPilot on the existing F405 (2026-11-01)

ArduCopter 4.7.2 was flashed via DFU on the SpeedyBee F405 V4. The Betaflight backup was kept so the FC could be reverted at any time.

### Setup

- **Motor order:** outputs did not match the ArduPilot X layout. Solved with `FRAME_TYPE = 1` and remapping (`SERVO1_FUNCTION = 35`, `SERVO3_FUNCTION = 33`). Order and direction (props in) verified.
- **DShot:** DShot300 with Bluejay EDT, bidirectional (`SERVO_DSHOT_ESC = 4`, `SERVO_BLH_BDMASK = 15`, `SERVO_BLH_POLES = 14`).
- **No compass:** `COMPASS_ENABLE = 0`, yaw from the GSF estimator (`EK3_SRC1_YAW = 8`). Loiter only available after a few metres of straight flight.

### Problems and solutions

| Problem | Cause | Solution |
|---|---|---|
| "EKF3 not enough memory" | RAM limit of the F405 | `LOG_FILE_BUFSIZE = 8`, `TERRAIN_ENABLE = 0`, `SRTL_POINTS = 0`, `SERIAL5_PROTOCOL = -1`, `EK3_IMU_MASK = 1` |
| Pre-arm failure | `EK3_ENABLE` was 0 (stock) | `EK3_ENABLE = 1` |
| Pre-arm demanded GPS position | `FENCE_AUTOENABLE = 1` despite `FENCE_ENABLE = 0` | `FENCE_AUTOENABLE = 0` |
| Log deleted after flight | SD card had a 256 MB partition, combined with `LOG_FILE_MB_FREE = 500` | card reformatted (FAT32, MBR) |

### Flight 1 (log 0): oscillation

The aircraft hovered at only **~4 % throttle**, so the motors ran close to their minimum and control authority was poor. Rough estimate: thrust-to-weight ratio around 20:1. Vibration levels were very low.

Starting values for a 5" quad were then set: `INS_GYRO_FILTER = 75`, `FLTD/FLTT = 38`, rate P/I = 0.07, D = 0.0018, `MOT_THST_EXPO = 0.5`, `MOT_THST_HOVER = 0.125`, `MOT_SPIN_ARM/MIN = 0.05/0.08`, logging at 400 Hz.

Parameter sets: [`params/legacy/`](../../params/legacy/) (stock and pre-tune)

### Flight 2 (log 1): stable, but drift

- Controller stable, no oscillation.
- **Drift to the front left.** The motor RPM data showed the cause: front left motor ~7,750 rpm, rear right ~5,550 rpm and at minimum 38 % of the time. The centre of gravity was offset to the front left.
- Barometer read -3 m during hover (prop wash), triggering baro glitch errors.

### Lessons from stage 2

- The F405 is at its limit with ArduPilot: RAM forced EKF and logging features to be cut.
- Without a compass, position modes are limited.
- RPM telemetry is a useful diagnostic tool, not only an input for notch filters.
- The baro needs shielding from prop wash.

## Stage 3: new stack and PX4 (2026-11-04 to 2026-11-05)

### What changed

| Component | Before | After |
|---|---|---|
| Flight controller | SpeedyBee F405 V4 | MicoAir H743 V2 (onboard compass QMC5883L) |
| ESC | J-H-40, Bluejay | MicoAir 55 A, AM32 |
| Motor protocol | DShot300 BiDi | DShot600 BiDi |
| GNSS / compass | GEP-M10, no compass | HGLRC M100-5883 (GNSS + QMC5883 compass) |
| Telemetry | not installed | Holybro Telemetry Radio V3 (433 MHz), MAVLink |
| Receiver | ExpressLRS | unchanged |
| Video | DJI O3 | removed for now |
| Autopilot | ArduCopter 4.7.2 | PX4 1.17.0 |

### Build

| | |
|---|---|
| ![Components](../../hardware/photos/2026-11-04_01_components.jpg) | ![Frame parts](../../hardware/photos/2026-11-04_02_frame-parts.jpg) |
| New components before assembly | Frame stripped down |
| ![ESC with capacitor](../../hardware/photos/2026-11-04_03_esc-capacitor.jpg) | ![ESC and motors](../../hardware/photos/2026-11-04_04_esc-motors-mounted.jpg) |
| ESC with 1000 µF capacitor on the battery pads | ESC mounted, motor leads soldered |
| ![FC, GNSS, telemetry](../../hardware/photos/2026-11-04_05_fc-gnss-telemetry-wiring.jpg) | ![Assembled](../../hardware/photos/2026-11-04_06_assembled.jpg) |
| FC stacked, GNSS and telemetry radio connected | Assembled, battery on top |

<!-- TODO (Yannik): notes on wiring and UART assignment, anything that went wrong during assembly -->

### Configuration in QGroundControl

1. Airframe: Generic Quadcopter (`SYS_AUTOSTART = 4001`)
2. Board orientation: yaw 180° (`SENS_BOARD_ROT = 4`)
3. Sensor calibration: gyro, accelerometer, two magnetometers, level horizon
4. Radio: CRSF (`RC_INPUT_PROTO = 6`), arm switch on channel 5, kill switch on channel 6, flight mode channel 8 (Stabilized / Altitude / Position)
5. Actuators: motor order and direction checked, DShot600 bidirectional, 14 poles
6. Power: 6S, 1300 mAh
7. Telemetry radio on MAVLink, failsafe on RC loss: Return

<!-- TODO (Yannik): problems during PX4 setup and how they were solved -->

### First hover

<!-- TODO (Yannik): date, indoor location type, flight mode, duration, observations -->

Parameter set: [`params/2026-11-05_01_baseline-pre-tune.params`](../../params/2026-11-05_01_baseline-pre-tune.params)

## Open points carried over

- Centre of gravity: check battery position (front-left offset seen in stage 2)
- Baro: cover with open-cell foam
- Hover throttle: very high thrust-to-weight ratio, relevant for tuning and the hover thrust estimate
- RPM-based notch filter, now possible on the H743
- Autotune
