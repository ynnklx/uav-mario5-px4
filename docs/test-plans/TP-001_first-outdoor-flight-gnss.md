# TP-001: First outdoor flight and GNSS verification

| | |
|---|---|
| Status | planned |
| Parameter set | `params/2026-11-07_02_outdoor-failsafe-dshot300.params` |
| Location | outdoor, open field, EU open category A3 |
| Weather limits | wind max. 5 m/s, no rain |
| Battery | 6S 1300 mAh LiPo, fully charged |

## Objective

1. Verify GNSS and compass function outdoors. Indoors the GNSS did not work properly.
2. Verify Altitude and Position mode.
3. Record a baseline log for the tuning work: hover throttle, vibration, rate controller tracking.

## Background: GNSS configuration

Indoors the GNSS did not work properly. In parameter set 01, `GPS_1_GNSS = 63` enabled all six constellation bits, including NavIC, which the u-blox M10 in the HGLRC M100 does not support. Parameter set 02 uses the receiver default (`GPS_1_GNSS = 0`). This test checks whether the GNSS works correctly outdoors with this setting.

## Pre-flight checks

- [ ] Failsafes reviewed: RC loss → Return after 0.5 s, return altitude 30 m, battery critical (7 %) → Return, emergency (5 %) → Land, geofence 500 m / 120 m → Hold
- [ ] Rotor geometry checked in QGroundControl (Actuators), motor test passed
- [ ] Arm switch, kill switch (ch 9), Return switch (ch 10) and flight mode switch checked on the ground
- [ ] Telemetry link to QGroundControl stable
- [ ] Logging active (SD card, `SDLOG_MODE = 0`: from arming to disarming)

## Procedure

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
