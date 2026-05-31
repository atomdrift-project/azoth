# `filetype/chrome-manifest`

LightGBM specialist for `chrome-manifest`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `chrome-manifest` slice of the locked test partition: 6 malware / 54 benign (60 rows).

| PR AUC | ROC AUC | F1 | Recall @ L50 | Brier |
|---:|---:|---:|---:|---:|
| 0.691375 | 0.925926 | 0.666667 | 50.00% | 0.0941 |

## Specialist Performance

`filetypes/chrome-manifest` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| PR AUC | ROC AUC | F1 | Recall @ L50 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.691375 | 0.925926 | 0.666667 | 50.00% | 0.0941 | — |

## Routing

Files matching `chrome-manifest` are scored by `general`, `filetypes/chrome-manifest`. The ensemble's per-row score is whatever combiner strategy (`specialist_priority`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 432 (52 mal / 380 ben) |
| Feature spec | 73750 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 50 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
