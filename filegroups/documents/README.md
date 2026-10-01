# `filegroup/documents`

LightGBM specialist for `doc`, `docx`, `html`, `ole`, `pdf`, `ppt`, `pptx`, `rtf`, `xls`, `xlsx`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `documents`). ROC 0.947908, PR 0.952532, F1 0.8590 on 85,389 rows (42,110 mal / 43,279 ben).

## Routing

Files matching `documents` are scored by none. The ensemble's per-row score is whatever combiner strategy (`—`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 515,144 (213,790 mal / 301,354 ben) |
| Feature spec | 1715 features (`route_specific`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
