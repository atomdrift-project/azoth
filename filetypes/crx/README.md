# `filetype/crx`

LightGBM specialist for `crx`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `crx` slice of the locked test partition: 281 malware / 288 benign (569 rows).

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier |
|---:|---:|---:|---:|---:|
| 0.956590 | 0.939835 | 0.901408 | 68.33% | 0.0804 |

## Specialist Performance

`filetypes/crx` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.956590 | 0.939835 | 0.901408 | 68.33% | 0.0804 | — |

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="crx: recall by FP level (per 100M benigns)" height="300" />

Each curve plots recall at the per-100M-benign FP target for the route. The vertical dashed line marks the L25 deploy operating point.

## Routing

Files matching `crx` are scored by `general`, `filetypes/crx`. The ensemble's per-row score is whatever combiner strategy (`specialist_priority`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 3,226 (1,116 mal / 2,110 ben) |
| Feature spec | 9309 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 128 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
