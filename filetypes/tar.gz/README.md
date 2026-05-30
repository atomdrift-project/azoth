# `filetype/tar.gz`

LightGBM specialist for `tar.gz`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `tar.gz` slice of the locked test partition: 2,589 malware / 1,786 benign (4,375 rows).

| PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Brier |
|---:|---:|---:|---:|---:|
| 0.995217 | 0.993069 | 0.971046 | 74.47% | 0.0493 |

## Specialist Performance

`filetypes/tar.gz` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.998018 | 0.997292 | 0.980862 | 73.77% | 0.0191 | — |

## Routing

Files matching `tar.gz` are scored by `general`, `filetypes/tar.gz`. The ensemble's per-row score is whatever combiner strategy (`calibrated_max`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 39,639 (27,138 mal / 12,501 ben) |
| Feature spec | 63983 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 64 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.02 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.5 |
| early_stopping_rounds | 25 |
| device | auto |
