# `filegroup/config`

LightGBM specialist for `ini`, `json`, `package.json`, `plist`, `toml`, `xml`, `yaml`, `yml`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `config`). ROC 0.880572, PR 0.767957, F1 0.8413 on 118,140 rows (3,695 mal / 114,445 ben).

## Routing

Files matching `config` are scored by none. The ensemble's per-row score is whatever combiner strategy (`—`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 822,218 (19,528 mal / 802,690 ben) |
| Feature spec | 1037 features (`route_specific`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
