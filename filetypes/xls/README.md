# `filetype/xls`

LightGBM specialist for `xls`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `xls`). ROC 0.991117, PR 0.995896, F1 0.9782 on 7,608 rows (4,956 mal / 2,652 ben).

## Routing

Files matching `xls` are scored by none. The ensemble's per-row score is whatever combiner strategy (`—`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 51,716 (33,606 mal / 18,110 ben) |
| Feature spec | 9330 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
