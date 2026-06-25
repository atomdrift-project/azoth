# `filetype/pkg-info`

LightGBM specialist for `pkg-info`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `pkg-info`). ROC 0.985514, PR 0.992849, F1 0.9831 on 1,742 rows (1,264 mal / 478 ben).

## Routing

Files matching `pkg-info` are scored by none. The ensemble's per-row score is whatever combiner strategy (`—`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 12,295 (9,007 mal / 3,288 ben) |
| Feature spec | 9330 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 128 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
