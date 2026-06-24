# `filegroup/native`

LightGBM specialist for `elf`, `macho`, `pe`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `native`). ROC 0.998718, PR 0.999672, F1 0.9940 on 245,015 rows (192,844 mal / 52,171 ben).

## Routing

Files matching `native` are scored by none. The ensemble's per-row score is whatever combiner strategy (`—`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 1,722,707 (1,359,194 mal / 363,513 ben) |
| Feature spec | 8531 features (`route_specific`) |
| n_estimators | 250 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0 / 1 |
| early_stopping_rounds | 25 |
| device | auto |
