# `filetype/tar.gz`

LightGBM specialist for `tar.gz`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `tar.gz` slice of the locked test partition: 2,597 malware / 1,866 benign (4,463 rows).

| PR AUC | ROC AUC | F1 | Recall @ L50 | Brier |
|---:|---:|---:|---:|---:|
| 0.993947 | 0.990787 | 0.971082 | 75.93% | 0.0622 |

## Specialist Performance

`filetypes/tar.gz` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| PR AUC | ROC AUC | F1 | Recall @ L50 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.997891 | 0.997188 | 0.979545 | 75.16% | 0.0196 | — |

## Routing

Files matching `tar.gz` are scored by `general`, `filetypes/tar.gz`. The ensemble's per-row score is whatever combiner strategy (`calibrated_max`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 40,381 (27,189 mal / 13,192 ben) |
| Feature spec | 73750 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 64 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.02 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.5 |
| early_stopping_rounds | 25 |
| device | auto |
