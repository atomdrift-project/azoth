# `filegroup/scripts`

LightGBM specialist for `batch`, `javascript`, `lua`, `perl`, `php`, `powershell`, `python`, `ruby`, `shell`, `typescript`, `vbscript`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `scripts`). ROC 0.9997, PR 0.9992, F1 0.9891 on 137,715 rows (35,696 mal / 102,019 ben).

## Routing

Files matching `scripts` are scored by none. The ensemble's per-row score is whatever combiner strategy (`—`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 957,406 (248,710 mal / 708,696 ben) |
| Feature spec | 60790 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 50 |
| device | auto |
