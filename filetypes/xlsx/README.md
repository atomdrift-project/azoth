# `filetype/xlsx`

LightGBM specialist for `xlsx`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `xlsx` slice of the locked test partition: 7,425 malware / 198 benign (7,623 rows).

| PR AUC | ROC AUC | F1 | Recall @ L50 | Brier |
|---:|---:|---:|---:|---:|
| 0.997488 | 0.940077 | 0.996242 | 47.03% | 0.0075 |

## Specialist Performance

`filetypes/xlsx` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| PR AUC | ROC AUC | F1 | Recall @ L50 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.987033 | 0.705207 | 0.986842 | 31.80% | 0.6667 | — |

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="xlsx: recall by FP level (per 100M benigns)" height="300" />

Each curve plots recall at the per-100M-benign FP target for the route. The vertical dashed line marks the L50 deploy operating point.

## Routing

Files matching `xlsx` are scored by `general`, `filegroups/documents`, `filetypes/xlsx`. The ensemble's per-row score is whatever combiner strategy (`stacked_xgb`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 17,733 (16,092 mal / 1,641 ben) |
| Feature spec | 80203 features (`general_shared`) |
| n_estimators | 300 |
| num_leaves | 128 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0 / 1 |
| early_stopping_rounds | 25 |
| device | auto |
