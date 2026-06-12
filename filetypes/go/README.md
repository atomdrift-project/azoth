# `filetype/go`

LightGBM specialist for `go`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `go` slice of the locked test partition: 1,396 malware / 16,015 benign (17,411 rows).

| PR AUC | ROC AUC | F1 | Recall @ L50 | Brier |
|---:|---:|---:|---:|---:|
| 0.330400 | 0.727444 | 0.329919 | 7.02% | 0.0643 |

## Specialist Performance

`filetypes/go` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| PR AUC | ROC AUC | F1 | Recall @ L50 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.193946 | 0.512599 | 0.213013 | 5.95% | 0.0749 | — |

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="go: recall by FP level (per 100M benigns)" height="300" />

Each curve plots recall at the per-100M-benign FP target for the route. The vertical dashed line marks the L50 deploy operating point.

## Routing

Files matching `go` are scored by `general`, `filegroups/source`, `filetypes/go`. The ensemble's per-row score is whatever combiner strategy (`stacked_xgb`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 112,174 (1,202 mal / 110,972 ben) |
| Feature spec | 9519 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
