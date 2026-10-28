# `filetype/ole_doc`

LightGBM specialist for `doc`, `msg`, `msi`, `ole`, `ole_doc`, `oledoc`, `ppt`, `xls`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `ole_doc` slice of the locked test partition: 11,041 malware / 4,150 benign (15,191 rows).

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier |
|---:|---:|---:|---:|---:|
| 0.994489 | 0.984096 | 0.946625 | 89.87% | - |

## Specialist Performance

`filetypes/ole_doc` specialist scored alone on the same held-out slice, using its saved thresholds.

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.995360 | 0.986953 | 0.869619 | 76.93% | 0.0616 | — |

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="ole_doc: recall by FP level (per 100M benigns)" height="300" />

Each curve plots recall at the per-100M-benign FP target for the route. The vertical dashed line marks the L25 deploy operating point.

## Routing

Files matching `ole_doc` are scored by `filegroups/documents`, `filetypes/ole_doc`, `general`. The ensemble's decisions apply the saved routing policy, including every level at or below the requested level. Ranking metrics use the signed distance from that policy's decision boundary. See [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 86,924 (62,968 mal / 23,956 ben) |
| Feature spec | 25488 features (`route_specific`) |
| n_estimators | 300 |
| num_leaves | 128 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 2.0 |
| early_stopping_rounds | 25 |
| device | auto |
