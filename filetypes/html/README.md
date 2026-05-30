# `filetype/html`

LightGBM specialist for `html`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `html` slice of the locked test partition: 20 malware / 3,224 benign (3,244 rows).

| PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Brier |
|---:|---:|---:|---:|---:|
| 0.802315 | 0.974116 | 0.756757 | 60.00% | 0.0023 |

## Specialist Performance

`filetypes/html` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.802315 | 0.974116 | 0.756757 | 60.00% | 0.0023 | — |

## Routing

Files matching `html` are scored by `filegroups/documents`, `filetypes/html`. The ensemble's per-row score is whatever combiner strategy (`specialist_priority`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 22,524 (137 mal / 22,387 ben) |
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
