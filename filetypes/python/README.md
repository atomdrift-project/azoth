# `filetype/python`

LightGBM specialist for `python`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed routed ensemble on the `python` slice of the test partition: 2271 malware / 16286 benign (18557 rows). These are the headline numbers from the bundle [README](../../README.md).

| ROC AUC | PR AUC | Recall @ 3FP/M | F1 | Brier |
|---:|---:|---:|---:|---:|
| 0.9950 | 0.9765 | 53.63% | 0.9324 | 0.0141 |

## Specialist Performance

`filetypes/python` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.9950 | 0.9765 | 0.9324 | 53.63% | 0.0141 | — |

## Routing

Default level `joint_or_at_fp_0` over `general`, `filegroups/scripts`, `filetypes/python`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 128778 (15631 mal / 113147 ben) |
| Feature spec | 60358 features (`general_shared`) |
| n_estimators | 250 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
