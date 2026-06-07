# `filegroup/source`

LightGBM specialist for `c`, `cpp`, `csharp`, `go`, `java`, `kotlin`, `makefile`, `rust`, `scala`, `swift`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `source`). ROC 0.925223, PR 0.651832, F1 0.5990 on 151,998 rows (7,857 mal / 144,141 ben).

## Routing

Files matching `source` are scored by none. The ensemble's per-row score is whatever combiner strategy (`—`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 1,026,989 (22,182 mal / 1,004,807 ben) |
| Feature spec | 80203 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 128 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
