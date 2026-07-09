# `filetype/github_actions`

LightGBM specialist for `github_actions`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `github_actions` slice of the locked test partition: 8 malware / 2,041 benign (2,049 rows).

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier |
|---:|---:|---:|---:|---:|
| 0.483554 | 0.938266 | 0.666667 | 62.50% | 0.0034 |

## Specialist Performance

`filetypes/github_actions` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.533061 | 0.791778 | 0.714286 | 71.43% | 0.0081 | — |

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="github_actions: recall by FP level (per 100M benigns)" height="300" />

Each curve plots recall at the per-100M-benign FP target for the route. The vertical dashed line marks the L25 deploy operating point.

## Routing

Files matching `github_actions` are scored by `general`, `filetypes/github_actions`. The ensemble's per-row score is whatever combiner strategy (`specialist_priority`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 3,721 (27 mal / 3,694 ben) |
| Feature spec | 9309 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 50 |
| device | auto |
