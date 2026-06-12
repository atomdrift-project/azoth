# `filetype/pe`

LightGBM specialist for `pe`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `pe` slice of the locked test partition: 164,925 malware / 20,260 benign (185,185 rows).

| PR AUC | ROC AUC | F1 | Recall @ L50 | Brier |
|---:|---:|---:|---:|---:|
| 0.999730 | 0.997972 | 0.993953 | 77.41% | 0.0095 |

## Specialist Performance

`filetypes/pe` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| PR AUC | ROC AUC | F1 | Recall @ L50 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.999585 | 0.996756 | 0.992131 | 75.15% | 0.0315 | PR +0.001285 / ROC -0.001444 |

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="pe: recall by FP level (per 100M benigns)" height="300" />

Each curve plots recall at the per-100M-benign FP target for the route. The vertical dashed line marks the L50 deploy operating point.

## Routing

Files matching `pe` are scored by `general`, `filegroups/native`, `filetypes/pe`. The ensemble's per-row score is whatever combiner strategy (`stacked_lr`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 1,309,929 (1,167,724 mal / 142,205 ben) |
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
