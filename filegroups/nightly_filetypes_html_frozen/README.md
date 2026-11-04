# `filegroup/nightly_filetypes_html_frozen`

LightGBM specialist for `hta`, `html`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

Level labels use the [shared pool-adjusted FP allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; L1 allows one; L25 adds an estimated 24 FP/100M beyond the initial FP.

## Performance

Training-time benchmark only (no test-partition rows for `nightly_filetypes_html_frozen`). ROC 0.993218, PR 0.982009, F1 0.9734 on 65,784 rows (11,513 mal / 54,271 ben).

## Routing

Files matching `nightly_filetypes_html_frozen` are scored by none. The ensemble's decisions apply the saved routing policy, including every level at or below the requested level. Ranking metrics use the signed distance from that policy's decision boundary. See [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 390,564 (65,762 mal / 324,802 ben) |
| Feature spec | 19224 features (`route_specific`) |
| n_estimators | 250 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0 / 1 |
| early_stopping_rounds | 25 |
| device | auto |
