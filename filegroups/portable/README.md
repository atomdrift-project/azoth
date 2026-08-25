# `filegroup/portable`

LightGBM specialist for `dex`, `java_class`, `pyc`, `wasm`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

> Benchmark AUC degenerate on this split. Routed full-corpus calibration governs deployment.

## Performance

Training-time benchmark only (no test-partition rows for `portable`). ROC 0.436741, PR 0.187923, F1 0.3625 on 215,343 rows (292 mal / 215,051 ben).

## Routing

Files matching `portable` are scored by none. The ensemble's per-row score is whatever combiner strategy (`—`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 1,513,785 (1,510 mal / 1,512,275 ben) |
| Feature spec | 1112 features (`route_specific`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
