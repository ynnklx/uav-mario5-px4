# Logbook

Relevant changes to the aircraft. Details in the linked files.

| Date | Area | Change | Ref |
|---|---|---|---|
| 2026-11-04 | Hardware | Rebuild: MicoAir H743 V2 FC, MicoAir 55 A AM32 ESC, HGLRC M100-5883 GNSS/compass, Holybro Telemetry Radio V3. DJI O3 removed. | [build/01](docs/build/01-betaflight-to-px4.md) |
| 2026-11-05 | Firmware | PX4 1.17.0, initial configuration. | [params 01](params/2026-11-05_01_baseline-pre-tune.params) |
| 2026-11-06 | Flight | First indoor hover, Stabilized. Arm, kill and mode switches verified. | [build/01](docs/build/01-betaflight-to-px4.md#first-hover) |
| 2026-11-07 | Motors | DShot600 → DShot300 (better tunability, per Chris Rosser). | [params 02](params/2026-11-07_02_outdoor-failsafe-dshot300.params) |
| 2026-11-07 | Geometry | Rotor positions set to measured values. | [params 02](params/2026-11-07_02_outdoor-failsafe-dshot300.params) |
| 2026-11-07 | Failsafe | Low battery: Return / Land. Geofence 500 m / 120 m. Return switch on ch 10, kill switch moved to ch 9. | [params 02](params/2026-11-07_02_outdoor-failsafe-dshot300.params) |
| 2026-11-07 | GNSS | Constellation config set to receiver default. | [params 02](params/2026-11-07_02_outdoor-failsafe-dshot300.params) |
| 2026-11-07 | RC | Dedicated CRSF driver on UART6. | [params 02](params/2026-11-07_02_outdoor-failsafe-dshot300.params) |
| 2026-11-07 | Sensors | Gyro, accelerometer, compass and level horizon recalibrated. | [params 02](params/2026-11-07_02_outdoor-failsafe-dshot300.params) |
