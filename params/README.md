# Parameter history

Every parameter set flown is exported from QGroundControl and stored here.

**Naming:** `YYYY-MM-DD_NN_short-description.params`, e.g. `2026-11-05_01_baseline-pre-tune.params`

**Compare two states:**

```
git diff --no-index params/<old>.params params/<new>.params
```

## Index

| File | Firmware | Description | Flown in |
|---|---|---|---|
| [`2026-11-05_01_baseline-pre-tune.params`](2026-11-05_01_baseline-pre-tune.params) | PX4 1.17.0 | State after migration, first indoor hover | first hover |

### Legacy (before PX4)

| File | Firmware | Description |
|---|---|---|
| [`legacy/2026-11-01_betaflight_speedybeef405v4_cli-dump.txt`](legacy/2026-11-01_betaflight_speedybeef405v4_cli-dump.txt) | Betaflight 2026.6.1 | Full CLI dump of the original configuration |
| [`legacy/2026-11-01_ardupilot-4.7.2_f405_stock.params`](legacy/2026-11-01_ardupilot-4.7.2_f405_stock.params) | ArduCopter 4.7.2 | After first flash, before setup |
| [`legacy/2026-11-01_ardupilot-4.7.2_f405_pretune.params`](legacy/2026-11-01_ardupilot-4.7.2_f405_pretune.params) | ArduCopter 4.7.2 | 5" starting values used for flight 2 |

## Baseline: notable settings

Settings in the baseline that are relevant for the upcoming tuning work.

| Area | Parameter | Value | Note |
|---|---|---|---|
| Airframe | `SYS_AUTOSTART` | 4001 | Generic quadcopter |
| Board | `SENS_BOARD_ROT` | 4 | FC mounted yaw 180° |
| Rate loop | `IMU_GYRO_RATEMAX` | 800 | Hz |
| Rate PID roll | `MC_ROLLRATE_K / P / I / D` | 0.35 / 0.15 / 0.2 / 0.003 | |
| Rate PID pitch | `MC_PITCHRATE_K / P / I / D` | 0.4 / 0.15 / 0.2 / 0.003 | |
| Rate PID yaw | `MC_YAWRATE_K / P / I / D` | 1.2 / 0.2 / 0.1 / 0 | |
| Gyro filter | `IMU_GYRO_CUTOFF` | 80 | Hz, low-pass |
| D-term filter | `IMU_DGYRO_CUTOFF` | 20 | Hz |
| Dynamic notch | `IMU_GYRO_DNF_EN` | 0 | off; ESC RPM telemetry is available via BiDi DShot |
| Motor output | `DSHOT_BIDIR_EN`, `MOT_POLE_COUNT` | 1, 14 | |
| Airmode | `MC_AIRMODE` | 0 | off |
| Autotune | `MC_AT_EN` | 1 | enabled |
| Hover thrust | `MPC_THR_HOVER`, `MPC_USE_HTE` | 0.5, 1 | default value, estimator active |
| Battery | `BAT1_N_CELLS`, `BAT1_CAPACITY` | 6, 1300 mAh | |
| Battery | `BAT1_V_EMPTY`, `BAT1_V_CHARGED` | 3.2 V, 4.2 V | must be revised for Li-Ion |
| Failsafe | `COM_LOW_BAT_ACT` | 0 | warning only |
| Failsafe | `NAV_RCL_ACT`, `COM_RC_LOSS_T` | 2 (Return), 0.5 s | |
| Geofence | `GF_MAX_HOR_DIST`, `GF_MAX_VER_DIST` | 0, 0 | not set |
| Flight modes | `COM_FLTMODE1 / 4 / 6` | Stabilized / Altitude / Position | |
