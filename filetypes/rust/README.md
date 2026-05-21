# `filetype/rust`

LightGBM specialist for `rust`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `rust` slice of the locked test partition: 164 malware / 9,604 benign (9,768 rows).

| PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Brier |
|---:|---:|---:|---:|---:|
| 0.1102 | 0.7258 | 0.1660 | 1.83% | 0.0164 |

## Specialist Performance

`filetypes/rust` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.1102 | 0.7258 | 0.1660 | 1.83% | 0.0164 | — |

## Routing

Files matching `rust` are scored by `general`, `filegroups/source`, `filetypes/rust`. The ensemble's per-row score is whatever combiner strategy (`specialist_priority`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 68,451 (1,117 mal / 67,334 ben) |
| Feature spec | 60778 features (`general_shared`) |
| n_estimators | 200 |
| num_leaves | 128 |
| max_depth | 14 |
| min_child_samples | 50 |
| learning_rate | 0.04 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
