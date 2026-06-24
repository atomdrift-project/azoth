# `filetype/pdf`

LightGBM specialist for `pdf`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `pdf` slice of the locked test partition: 22,516 malware / 3,091 benign (25,607 rows).

| PR AUC | ROC AUC | F1 | Recall @ L50 | Brier |
|---:|---:|---:|---:|---:|
| 0.989491 | 0.926535 | 0.966748 | 74.82% | 0.2221 |

## Specialist Performance

`filetypes/pdf` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| PR AUC | ROC AUC | F1 | Recall @ L50 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.989491 | 0.926535 | 0.966748 | 74.82% | 0.2221 | PR -0.003809 / ROC -0.064665 |

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="pdf: recall by FP level (per 100M benigns)" height="300" />

Each curve plots recall at the per-100M-benign FP target for the route. The vertical dashed line marks the L50 deploy operating point.

## Routing

Files matching `pdf` are scored by `general`, `filegroups/documents`, `filetypes/pdf`. The ensemble's per-row score is whatever combiner strategy (`specialist_priority`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 138,955 (117,367 mal / 21,588 ben) |
| Feature spec | 9338 features (`general_shared`) |
| n_estimators | 300 |
| num_leaves | 128 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0 / 1 |
| early_stopping_rounds | 25 |
| device | auto |
