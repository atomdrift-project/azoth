# `filetype/markdown`

LightGBM specialist for `markdown`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `markdown` slice of the locked test partition: 41 malware / 6,639 benign (6,680 rows).

| PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Brier |
|---:|---:|---:|---:|---:|
| 0.007195 | 0.541253 | 0.022556 | 0.00% | 0.0090 |

## Specialist Performance

`filetypes/markdown` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.007195 | 0.541253 | 0.022556 | 0.00% | 0.0090 | — |

## Routing

Files matching `markdown` are scored by `general`, `filetypes/markdown`. The ensemble's per-row score is whatever combiner strategy (`specialist_priority`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 46,536 (223 mal / 46,313 ben) |
| Feature spec | 63983 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 50 |
| device | auto |
