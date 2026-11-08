# Logbook

Relevant changes to the aircraft. Details in the linked files.

| Date | Area | Change | Ref |
|---|---|---|---|
| 2026-11-04 | Hardware | Rebuild: MicoAir H743 V2 FC, MicoAir 55 A AM32 ESC, HGLRC M100-5883 GNSS/compass, Holybro Telemetry Radio V3. DJI O3 removed. | [BUILD](BUILD.md) |
| 2026-11-05 | Firmware | PX4 1.17.0, initial configuration. | [01](params/01_pretune.params) |
| 2026-11-06 | Flight | First indoor hover, Stabilized. Arm, kill and mode switches verified. | [BUILD](BUILD.md#first-hover) |
| 2026-11-07 | Motors | DShot600 → DShot300 (better tunability, per Chris Rosser). | [02](params/02_outdoor.params) |
| 2026-11-07 | Geometry | Rotor positions set to measured values. | [02](params/02_outdoor.params) |
| 2026-11-07 | Failsafe | Low battery: Return / Land. Geofence 500 m / 120 m. Return switch on ch 10, kill switch moved to ch 9. | [02](params/02_outdoor.params) |
| 2026-11-07 | GNSS | Constellation config set to receiver default. | [02](params/02_outdoor.params) |
| 2026-11-07 | RC | Dedicated CRSF driver on UART6. | [02](params/02_outdoor.params) |
| 2026-11-07 | Sensors | Gyro, accelerometer, compass and level horizon recalibrated. | [02](params/02_outdoor.params) |
| 2026-11-08 | Filter | ESC RPM notch instead of FFT, static notches at 292 Hz and 370 Hz, gyro LPF 80 → 120 Hz, D-term LPF 20 → 50 Hz. | [FILTER](FILTER.md), [03](params/03_filters.params) |
| 2026-11-08 | Logging | `SDLOG_PROFILE` 273 for filter analysis. | [03](params/03_filters.params) |
| 2026-11-08 | Hover | `MPC_THR_HOVER` 0.5 → 0.2. | [03](params/03_filters.params) |
| 2026-11-08 | RC | CRSF telemetry to transmitter enabled. | [03](params/03_filters.params) |
| 2026-11-08 | Sensors | Level horizon recalibrated. | [03](params/03_filters.params) |
