# hk_bus-data

Hosted data feed for [HK Bus — Next Arrival](https://github.com/NEvolution-zz/hk_bus). This repo holds a single generated file, `stops-data.json`, which is the merged CityBus (CTB) + KMB stop/route index consumed by the iOS app at runtime.

It exists so the app doesn't have to make thousands of live CTB/KMB API calls on-device to build this index — instead it downloads this one static file via a conditional GET (ETag).

## Consumer

The iOS app's `DataIndexRefresher` polls `stops-data.json` from this repo's `main` branch once a day (via `BGAppRefreshTask`, plus a foreground stale-check fallback), decodes it into `StopsDataIndex`, and caches it on-device.

## Updating

This repo is written to only by the `hk_bus` repo's CI workflow. Manual edits or pushes to `main` will be overwritten by the next scheduled run (daily, 02:00 HKT).
