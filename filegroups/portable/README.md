# `filegroup/portable`

LightGBM specialist for `dex`, `java_class`, `javaclass`, `pyc`, `python-bytecode`, `python_bytecode`, `wasm`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

Level labels use the [shared pool-adjusted FP allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; L1 allows one; L25 adds an estimated 24 FP/100M beyond the initial FP.

## Performance

Training-time benchmark only (no test-partition rows for `portable`). ROC 0.991087, PR 0.922446, F1 0.9080 on 385,099 rows (719 mal / 384,380 ben).

## Routing

Files matching `portable` are scored by none. The ensemble's decisions apply the saved routing policy, including every level at or below the requested level. Ranking metrics use the signed distance from that policy's decision boundary. See [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 2,321,716 (4,316 mal / 2,317,400 ben) |
| Feature spec | 1599 features (`accepted_pinned`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | cpu |
