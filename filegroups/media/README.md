# `filegroup/media`

LightGBM specialist for `bmp`, `gif`, `jpeg`, `jpg`, `mp3`, `mp4`, `png`, `svg`, `webp`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

> Benchmark AUC degenerate on this split. Routed full-corpus calibration governs deployment.

## Performance

Training-time benchmark only (no test-partition rows for `media`). ROC 0.411864, PR 0.085538, F1 0.1363 on 114,151 rows (1,270 mal / 112,881 ben).

## Routing

Files matching `media` are scored by none. The ensemble's per-row score is whatever combiner strategy (`—`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 787,705 (707 mal / 786,998 ben) |
| Feature spec | 305 features (`route_specific`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
