# `filegroup/png_retained_hnm_recovery`

LightGBM specialist for `png`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

Level labels use the [shared pool-adjusted FP allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; L1 allows one; L25 adds an estimated 24 FP/100M beyond the initial FP.

## Performance

Training-time benchmark only (no test-partition rows for `png_retained_hnm_recovery`). ROC -, PR -, F1 - on 0 rows (0 mal / 0 ben).

## Routing

Files matching `png_retained_hnm_recovery` are scored by none. The ensemble's decisions apply the saved routing policy, including every level at or below the requested level. Ranking metrics use the signed distance from that policy's decision boundary. See [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 413,838 (5,869 mal / 407,969 ben) |
| Feature spec | 303 features (`route_specific`) |
| n_estimators | 400 |
| num_leaves | 31 |
| max_depth | 8 |
| min_child_samples | 20 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0 / 5 |
| early_stopping_rounds | 0 |
| device | cpu |
