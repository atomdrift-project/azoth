# `filetype/deb`

LightGBM specialist for `deb`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `deb` slice of the locked test partition: 28 malware / 784 benign (812 rows).

| PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Brier |
|---:|---:|---:|---:|---:|
| 0.321129 | 0.952920 | 0.529412 | 78.57% | 0.0292 |

## Specialist Performance

`filetypes/deb` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.321129 | 0.952920 | 0.529412 | 78.57% | 0.0292 | — |

## Routing

Files matching `deb` are scored by `general`. The ensemble's per-row score is whatever combiner strategy (`specialist_priority`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 5,506 (184 mal / 5,322 ben) |
| Feature spec | 63983 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
