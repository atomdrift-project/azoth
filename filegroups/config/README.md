# `filegroup/config`

LightGBM specialist for `ini`, `json`, `package.json`, `plist`, `toml`, `xml`, `yaml`, `yml`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `config`). ROC 0.992781, PR 0.976517, F1 0.9566 on 23,882 rows (2,521 mal / 21,361 ben).

## Routing

Files matching `config` are scored by none. The ensemble's per-row score is whatever combiner strategy (`—`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 166,993 (18,137 mal / 148,856 ben) |
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
