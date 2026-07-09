# `filetype/vbs`

LightGBM specialist for `vbs`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `vbs` slice of the locked test partition: 1,561 malware / 458 benign (2,019 rows).

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier |
|---:|---:|---:|---:|---:|
| 0.997083 | 0.989767 | 0.975348 | 88.53% | 0.0551 |

## Specialist Performance

`filetypes/vbs` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.997083 | 0.989767 | 0.975348 | 88.53% | 0.0551 | — |

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="vbs: recall by FP level (per 100M benigns)" height="300" />

Each curve plots recall at the per-100M-benign FP target for the route. The vertical dashed line marks the L25 deploy operating point.

## Routing

Files matching `vbs` are scored by `general`, `filetypes/vbs`. The ensemble's per-row score is whatever combiner strategy (`specialist_priority`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 12,903 (9,810 mal / 3,093 ben) |
| Feature spec | 9309 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
