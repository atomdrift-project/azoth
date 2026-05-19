# `filetype/pdf`

LightGBM specialist for `pdf`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed routed ensemble on the `pdf` slice of the test partition: 21777 malware / 1734 benign (23511 rows). These are the headline numbers from the bundle [README](../../README.md).

| ROC AUC | PR AUC | Recall @ 3FP/M | F1 | Brier |
|---:|---:|---:|---:|---:|
| 0.9813 | 0.9979 | 6.59% | 99.10% | 0.0172 |

## Specialist Performance

`filetypes/pdf` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9438 | 0.9935 | 98.89% | 0.8291 | ROC -0.0474 / PR +0.0002 |

## Routing

Default level `joint_or_at_fp_0` over `general`, `filegroups/documents`, `filetypes/pdf`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 162814 (150685 mal / 12129 ben) |
| Feature spec | 60358 features (`general_shared`) |
| n_estimators | 120 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 40 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
