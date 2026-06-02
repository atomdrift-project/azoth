# `filetype/tar.gz`

LightGBM specialist for `tar.gz`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `tar.gz`). ROC 0.998298, PR 0.998746, F1 0.9829 on 4,486 rows (2,599 mal / 1,887 ben).

## Routing

Files matching `tar.gz` are scored by none. The ensemble's per-row score is whatever combiner strategy (`—`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 40,438 (27,194 mal / 13,244 ben) |
| Feature spec | 76116 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 64 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.02 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.5 |
| early_stopping_rounds | 25 |
| device | auto |
