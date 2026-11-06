# `filegroup/config`

LightGBM specialist for `ini`, `json`, `package.json`, `packagejson`, `plist`, `toml`, `xml`, `yaml`, `yml`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

Level labels use the [shared pool-adjusted FP allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; L1 allows one; L25 adds an estimated 24 FP/100M beyond the initial FP.

## Performance

Training-time benchmark only (no test-partition rows for `config`). ROC 0.997920, PR 0.987222, F1 0.9668 on 127,406 rows (2,922 mal / 124,484 ben).

## Routing

Files matching `config` are scored by none. The ensemble's decisions apply the saved routing policy, including every level at or below the requested level. Ranking metrics use the signed distance from that policy's decision boundary. See [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 766,628 (20,877 mal / 745,751 ben) |
| Feature spec | 11018 features (`route_specific`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
