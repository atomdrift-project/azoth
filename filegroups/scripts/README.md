# `filegroup/scripts`

LightGBM specialist for `batch`, `javascript`, `lua`, `perl`, `php`, `powershell`, `python`, `ruby`, `shell`, `typescript`, `vbscript`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `scripts`). ROC 0.999558, PR 0.998915, F1 0.9870 on 161,384 rows (39,524 mal / 121,860 ben).

## Routing

Files matching `scripts` are scored by none. The ensemble's per-row score is whatever combiner strategy (`—`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 1,123,774 (276,210 mal / 847,564 ben) |
| Feature spec | 73750 features (`general_shared`) |
| n_estimators | 300 |
| num_leaves | 128 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0 / 1 |
| early_stopping_rounds | 25 |
| device | auto |
