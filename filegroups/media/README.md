# `filegroup/media`

LightGBM specialist for `bmp`, `gif`, `jpeg`, `jpg`, `mp3`, `mp4`, `png`, `svg`, `webp`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `media`). ROC 0.582278, PR 0.136424, F1 0.1434 on 29,362 rows (1,298 mal / 28,064 ben).

## Routing

Files matching `media` are scored by none. The ensemble's per-row score is whatever combiner strategy (`—`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 195,360 (707 mal / 194,653 ben) |
| Feature spec | 9425 features (`general_shared`) |
| n_estimators | 250 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0 / 1 |
| early_stopping_rounds | 25 |
| device | auto |
