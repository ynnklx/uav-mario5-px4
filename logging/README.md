# SD logging

MicoAir H743 V2, PX4 1.17.0

## sd_bench

`sd_bench`

| Card | Type | sd_bench on FC |
|---|---|---|
| SanDisk Ultra 16 GB | SDHC, entry level | ~380–430 KB/s |
| SanDisk Extreme 64 GB | SDXC, U3/V30 | ~405–450 KB/s |
| Lexar 64 GB | SDXC, U3 | ~350 KB/s |
| SanDisk Extreme PRO 32 GB | SDHC, U3/V30 | ~424–433 KB/s (avg 428) |

## Logging rates

Measured: log file size / log duration

| Profile | Rate | Source |
|---|---|---|
| `SDLOG_PROFILE` 17, `IMU_GYRO_RATEMAX` 800 | ~170 KB/s | measured, 13 logs, no dropouts |
| `SDLOG_PROFILE` 273, `IMU_GYRO_RATEMAX` 800 | ~390 KB/s | measured, 10 logs, dropouts typically < 1 % |
| `SDLOG_PROFILE` 273, `IMU_GYRO_RATEMAX` 1000 | above SD write limit | estimated; 27 % dropouts in test flight |
