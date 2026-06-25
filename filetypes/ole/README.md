# `filetype/ole`

LightGBM specialist for `ole`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `ole`). ROC 0.996897, PR 0.996884, F1 0.9769 on 1,698 rows (858 mal / 840 ben).

## Routing

Files matching `ole` are scored by none. The ensemble's per-row score is whatever combiner strategy (`—`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 11,059 (5,179 mal / 5,880 ben) |
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
