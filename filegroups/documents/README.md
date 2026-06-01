# `filegroup/documents`

LightGBM specialist for `doc`, `docx`, `html`, `ole`, `pdf`, `ppt`, `pptx`, `rtf`, `xls`, `xlsx`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `documents`). ROC 0.998872, PR 0.999730, F1 0.9937 on 48,151 rows (38,513 mal / 9,638 ben).

## Routing

Files matching `documents` are scored by none. The ensemble's per-row score is whatever combiner strategy (`—`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 337,032 (269,896 mal / 67,136 ben) |
| Feature spec | 76116 features (`general_shared`) |
| n_estimators | 350 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0 / 2 |
| early_stopping_rounds | 25 |
| device | auto |
