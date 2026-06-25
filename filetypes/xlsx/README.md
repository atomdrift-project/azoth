# `filetype/xlsx`

LightGBM specialist for `xlsx`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `xlsx`). ROC 0.608135, PR 0.985908, F1 0.9867 on 8,091 rows (7,879 mal / 212 ben).

## Routing

Files matching `xlsx` are scored by none. The ensemble's per-row score is whatever combiner strategy (`—`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 18,804 (17,054 mal / 1,750 ben) |
| Feature spec | 9330 features (`general_shared`) |
| n_estimators | 250 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0 / 1 |
| early_stopping_rounds | 25 |
| device | auto |
