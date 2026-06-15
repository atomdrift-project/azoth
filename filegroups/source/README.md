# `filegroup/source`

LightGBM specialist for `c`, `cpp`, `csharp`, `go`, `java`, `kotlin`, `makefile`, `rust`, `scala`, `swift`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `source`). ROC 0.926914, PR 0.646051, F1 0.6166 on 180,970 rows (8,819 mal / 172,151 ben).

## Routing

Files matching `source` are scored by none. The ensemble's per-row score is whatever combiner strategy (`—`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 1,222,489 (22,954 mal / 1,199,535 ben) |
| Feature spec | 9425 features (`general_shared`) |
| n_estimators | 300 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0 / 1 |
| early_stopping_rounds | 25 |
| device | auto |
