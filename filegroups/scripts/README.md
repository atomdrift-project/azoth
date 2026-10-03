# `filegroup/scripts`

LightGBM specialist for `batch`, `javascript`, `lua`, `perl`, `php`, `powershell`, `python`, `ruby`, `shell`, `typescript`, `vbscript`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `scripts`). ROC 0.881169, PR 0.650348, F1 0.6762 on 495,831 rows (47,508 mal / 448,323 ben).

## Routing

Files matching `scripts` are scored by none. The ensemble's per-row score is whatever combiner strategy (`—`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 3,323,367 (186,452 mal / 3,136,915 ben) |
| Feature spec | 2284 features (`route_specific`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
