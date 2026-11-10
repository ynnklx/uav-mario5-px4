# SD logging

MicoAir H743 V2, PX4 1.17.0

## sd_bench

`sd_bench -r 20`, block size 4096 B

| Card | Type | sd_bench on FC |
|---|---|---|
| SanDisk Ultra 16 GB | SDHC, entry level | ~380–430 KB/s |
| SanDisk Extreme 64 GB | SDXC, U3/V30 | ~405–450 KB/s |
| Lexar 64 GB | SDXC, U3 | ~350 KB/s |
| SanDisk Extreme PRO 32 GB | SDHC, U3/V30 | ~424–433 KB/s (avg 428) |

## Logging rates

| Profile | Rate |
|---|---|
| `SDLOG_PROFILE` 17 | ~170 KB/s |
| `SDLOG_PROFILE` 273, `IMU_GYRO_RATEMAX` 800 | ~350 KB/s |
| `SDLOG_PROFILE` 273, `IMU_GYRO_RATEMAX` 1000 | > ~430 KB/s, dropouts |
