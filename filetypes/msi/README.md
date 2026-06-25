# `filetype/msi`

LightGBM specialist for `msi`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `msi`). ROC 0.893123, PR 0.995925, F1 0.9882 on 604 rows (588 mal / 16 ben).

## Routing

Files matching `msi` are scored by none. The ensemble's per-row score is whatever combiner strategy (`—`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 4,441 (4,231 mal / 210 ben) |
| Feature spec | 9330 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 50 |
| device | auto |
