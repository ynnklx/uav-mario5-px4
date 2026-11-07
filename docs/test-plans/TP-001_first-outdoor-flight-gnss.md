# TP-001: First outdoor flight and GNSS verification

| | |
|---|---|
| Status | planned |
| Parameter set | `params/2026-11-05_01_baseline-pre-tune.params` |
| Location | outdoor, open field, EU open category A3 |
| Weather limits | wind max. 5 m/s, no rain |
| Battery | 6S 1300 mAh LiPo, fully charged |

## Objective

1. Verify GNSS and compass function outdoors. Indoors the GNSS did not work properly.
2. Verify Altitude and Position mode.
3. Record a baseline log for the tuning work: hover throttle, vibration, rate controller tracking.

## Background: GNSS configuration

`GPS_1_GNSS = 63` enables all six constellation bits (GPS, SBAS, Galileo, BeiDou, GLONASS, NavIC). The HGLRC M100 is based on a u-blox M10 receiver, which tracks up to four constellations concurrently; NavIC is not among its supported systems. Whether this setting has an effect is to be checked in this test.

| Run | `GPS_1_GNSS` | Systems |
|---|---|---|
| A | 63 | as configured |
| B | 0 | receiver default |

## Pre-flight checks

- [ ] Failsafes reviewed: RC loss → Return after 0.5 s (`NAV_RCL_ACT = 2`), return altitude 30 m, low battery → warning only (`COM_LOW_BAT_ACT = 0`)
- [ ] Arm switch, kill switch and flight mode switch checked on the ground
- [ ] Telemetry link to QGroundControl stable
- [ ] Logging active (SD card, `SDLOG_MODE = 0`: from arming to disarming)

## Procedure

For each run (A, B):

1. Power on, aircraft stationary. Note time to 3D fix, number of satellites, HDOP/EPH in QGroundControl.
2. Check heading in QGroundControl against the real heading of the aircraft.
3. Take off in **Stabilized**, hover at 2 to 3 m for 30 to 60 s.
4. Switch to **Altitude**: hover, small climbs and descents.
5. Switch to **Position**, only if GNSS fix is good: hover without stick input for 30 s, then short movements in all directions.
6. Land, disarm.

## Data to record

| Value | Source |
|---|---|
| Time to 3D fix, satellites, EPH | QGroundControl, ULog |
| Heading deviation | QGroundControl vs. reality |
| Position hold drift | ULog |
| Hover throttle (learned) | ULog, `MPC_THR_HOVER` estimate |
| Vibration levels | ULog / Flight Review |
| Battery voltage after landing | multimeter / QGroundControl |

## Success criteria

- 3D fix with at least 6 satellites and EPH below 3 m (`EKF2_REQ_NSATS`, `EKF2_REQ_EPH`)
- Heading plausible, no toilet bowling in Position mode
- Position mode holds without stick input
- No noticeable oscillation in any mode

## Abort criteria

- Oscillation or unexpected attitude change → switch to Stabilized, land
- Toilet bowling or drift in Position → switch to Altitude or Stabilized, land
- Loss of telemetry or RC link
- Battery below 3.5 V/cell under load

## Out of scope

- DJI O3 Air Unit: not installed, not needed for this project.
