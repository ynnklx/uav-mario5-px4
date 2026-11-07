# uav-mario5-px4

5" quadcopter migrated from Betaflight to PX4. This repository documents the build, bring-up, flight testing and tuning of the aircraft, including flight logs, parameter history and analysis.

The goal is a well-tuned, GNSS-capable 5" platform that flies autonomous missions under PX4, with every change traceable to a test and a measurement.

## Status

| Phase | State |
|---|---|
| Hardware migration to H743 and PX4 | done, 2026-11-05 |
| Sensor calibration, RC, telemetry, actuator setup | done |
| First indoor hover | done, 2026-11-06 |
| Rate controller tuning (PID) | next |
| Position / altitude controller tuning | planned |
| Short autonomous mission | planned |
| Propeller comparison | planned |
| Li-Ion pack, endurance optimisation | planned |

## Aircraft

| Component | Part |
|---|---|
| Frame | 5" FPV quadcopter frame |
| Motors | iFlight XING2 2306, 1855 KV |
| Flight controller | MicoAir H743 V2 |
| ESC | MicoAir 55 A, AM32 firmware |
| Motor protocol | DShot300, bidirectional (eRPM telemetry) |
| GNSS / compass | HGLRC M100-5883 |
| Telemetry | Holybro Telemetry Radio V3 (433 MHz, TX power being reduced to EU limit), MAVLink |
| RC link | ExpressLRS (CRSF) |
| Autopilot | PX4 v1.17.0 |
| Ground control | QGroundControl (macOS) |
| Battery | 6S 1300 mAh LiPo |
| Not installed currently | DJI O3 Air Unit |

![Mario5 assembled](hardware/photos/2026-11-04_06_assembled.jpg)

Details and photos: [`hardware/`](hardware/) · Build log: [`docs/build/01-betaflight-to-px4.md`](docs/build/01-betaflight-to-px4.md)

## Repository layout

```
hardware/            bill of materials, wiring, build photos
docs/build/          migration from Betaflight, bring-up notes
docs/test-plans/     test cards written before each flight test
docs/test-reports/   results, plots and conclusions after each test
params/              versioned PX4 parameter sets
analysis/            Python scripts for ULog analysis and plots
logs/                selected flight logs (large logs attached to releases)
```

## Method

Each optimisation step follows the same cycle:

1. **Test plan**: objective, configuration, procedure, abort criteria, expected result
2. **Flight test**: flown according to the plan, ULog recorded
3. **Parameter snapshot**: exported from QGroundControl into `params/`
4. **Report**: data, plots, findings, decision on the next step

Because every parameter set is versioned, `git diff` between two snapshots shows exactly what changed between two tests.

## Licence

- Code, scripts and parameter files: [MIT](LICENSE)
- Documentation, photos and plots: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)
