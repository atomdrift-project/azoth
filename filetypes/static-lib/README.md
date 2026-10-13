# `filetype/static-lib`

LightGBM specialist for `static-lib`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `static-lib` slice of the locked test partition: 101 malware / 1,604 benign (1,705 rows).

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier |
|---:|---:|---:|---:|---:|
| 0.738621 | 0.956165 | 0.714286 | 35.64% | 0.0288 |

## Specialist Performance

`filetypes/static-lib` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.480415 | 0.857050 | 0.514706 | 34.65% | 0.0401 | — |

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="static-lib: recall by FP level (per 100M benigns)" height="300" />

Each curve plots recall at the per-100M-benign FP target for the route. The vertical dashed line marks the L25 deploy operating point.

## Routing

Files matching `static-lib` are scored by `general`, `filetypes/static-lib`. The ensemble's per-row score is whatever combiner strategy (`stacked_xgb`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 11,376 (156 mal / 11,220 ben) |
| Feature spec | 1015 features (`route_specific`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 50 |
| device | auto |
