# `filetype/pdf`

LightGBM specialist for `pdf`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `pdf` slice of the locked test partition: 21,801 malware / 1,734 benign (23,535 rows).

| PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Brier |
|---:|---:|---:|---:|---:|
| 0.9989 | 0.9925 | 0.9959 | 17.59% | 0.0085 |

## Specialist Performance

`filetypes/pdf` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.9969 | 0.9745 | 0.9935 | 6.26% | 0.8190 | PR +0.0036 / ROC -0.0167 |

## Routing

Files matching `pdf` are scored by `general`, `filegroups/documents`, `filetypes/pdf`. The ensemble's per-row score is whatever combiner strategy (`stacked_xgb`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 163,541 (151,412 mal / 12,129 ben) |
| Feature spec | 60778 features (`general_shared`) |
| n_estimators | 120 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 40 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
