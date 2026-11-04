# `filegroup/nightly_filetypes_json_frozen`

LightGBM specialist for `json`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

Level labels use the [shared pool-adjusted FP allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; L1 allows one; L25 adds an estimated 24 FP/100M beyond the initial FP.

## Performance

Training-time benchmark only (no test-partition rows for `nightly_filetypes_json_frozen`). ROC 0.996700, PR 0.298613, F1 0.4238 on 39,111 rows (37 mal / 39,074 ben).

## Routing

Files matching `nightly_filetypes_json_frozen` are scored by none. The ensemble's decisions apply the saved routing policy, including every level at or below the requested level. Ranking metrics use the signed distance from that policy's decision boundary. See [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 235,272 (1,006 mal / 234,266 ben) |
| Feature spec | 3008 features (`route_specific`) |
| n_estimators | 320 |
| num_leaves | 128 |
| max_depth | 12 |
| min_child_samples | 150 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 2.0 |
| early_stopping_rounds | 25 |
| device | cpu |
