# `filetype/tar`

LightGBM specialist for `tar`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `tar` slice of the locked test partition: 129 malware / 57 benign (186 rows).

| PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Brier |
|---:|---:|---:|---:|---:|
| 0.993503 | 0.983068 | 0.984252 | 96.90% | 0.0234 |

## Specialist Performance

`filetypes/tar` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.994412 | 0.986672 | 0.984252 | 92.25% | 0.0504 | — |

## Routing

Files matching `tar` are scored by `filetypes/tar`. The ensemble's per-row score is whatever combiner strategy (`calibrated_max`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 1,458 (1,037 mal / 421 ben) |
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
