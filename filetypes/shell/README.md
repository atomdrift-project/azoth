# `filetype/shell`

LightGBM specialist for `shell`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `shell` slice of the locked test partition: 1,158 malware / 6,129 benign (7,287 rows).

| PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Brier |
|---:|---:|---:|---:|---:|
| 0.971603 | 0.991567 | 0.933211 | 81.35% | 0.0427 |

## Specialist Performance

`filetypes/shell` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.986613 | 0.996501 | 0.945958 | 79.79% | 0.0149 | — |

## Routing

Files matching `shell` are scored by `general`, `filegroups/scripts`, `filetypes/shell`. The ensemble's per-row score is whatever combiner strategy (`calibrated_max`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 50,474 (7,355 mal / 43,119 ben) |
| Feature spec | 63983 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 128 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
