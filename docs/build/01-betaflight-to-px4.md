# 01: Migration from Betaflight to PX4

**Status:** first indoor hover successful, November 2026

## Starting point

<!-- TODO (Yannik): previous setup under Betaflight: FC, ESC, receiver, what the aircraft was used for -->

## Why PX4

<!-- TODO (Yannik): own reasons. Suggested points: GNSS navigation and missions, MAVLink telemetry, ULog data for analysis, same autopilot as used on many professional UAS -->

## What changed

| Component | Before (Betaflight) | After (PX4) |
|---|---|---|
| Flight controller | tbd | MicoAir H743 V2 |
| ESC firmware | tbd | AM32, DShot600 BiDi |
| GNSS / compass | tbd | HGLRC M100 |
| Telemetry | tbd | Holybro Telemetry Radio V3, MAVLink |
| RC link | tbd | ExpressLRS (CRSF) |
| Video | DJI O3 | removed for now |

## Build steps

<!-- Photos: ../../hardware/photos/ -->

1. Disassembly and component layout
2. Mounting FC, ESC, GNSS mast
3. Wiring (power, UARTs, GNSS/I2C, telemetry, receiver)
4. Firmware: PX4 on the FC, AM32 on the ESC

## Configuration in QGroundControl

1. Airframe: Generic Quadcopter (`SYS_AUTOSTART = 4001`)
2. Sensor orientation and calibration (gyro, accelerometer, compass, level horizon)
3. Radio setup, flight modes, arm and kill switch
4. Actuator setup: motor order, direction, DShot BiDi
5. Power: battery cells, voltage divider, capacity
6. Telemetry radio, failsafes

## Problems and solutions

| Problem | Cause | Solution |
|---|---|---|
| <!-- TODO --> | | |

## First hover

<!-- TODO (Yannik): date, location (indoor), flight mode, duration, observations -->

Parameter set: [`params/2026-11-07_01_baseline-pre-tune.params`](../../params/)
