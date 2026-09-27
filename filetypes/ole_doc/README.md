# `filetype/ole_doc`

LightGBM specialist for `doc`, `msi`, `ole`, `ppt`, `xls`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `ole_doc` slice of the locked test partition: 11,024 malware / 4,149 benign (15,173 rows).

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier |
|---:|---:|---:|---:|---:|
| 0.994115 | 0.983775 | 0.958553 | 90.53% | 0.0409 |

## Specialist Performance

`filetypes/ole_doc` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.994043 | 0.982690 | 0.958958 | 90.35% | 0.0572 | — |

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="ole_doc: recall by FP level (per 100M benigns)" height="300" />

Each curve plots recall at the per-100M-benign FP target for the route. The vertical dashed line marks the L25 deploy operating point.

## Routing

Files matching `ole_doc` are scored by `general`, `filetypes/ole_doc`. The ensemble's per-row score is whatever combiner strategy (`calibrated_max`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 101,668 (73,782 mal / 27,886 ben) |
| Feature spec | 6388 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 50 |
| device | auto |
