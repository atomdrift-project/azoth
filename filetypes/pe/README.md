# `filetype/pe`

LightGBM specialist for `pe`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed routed ensemble on the `pe` slice of the test partition: 109970 malware / 18938 benign (128908 rows). These are the headline numbers from the bundle [README](../../README.md).

| ROC AUC | PR AUC | Recall @ 3FP/M | F1 | Brier |
|---:|---:|---:|---:|---:|
| 0.9991 | 0.9998 | 73.42% | 99.55% | 0.0240 |

## Specialist Performance

`filetypes/pe` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9983 | 0.9997 | 99.42% | 0.0163 | ROC +0.0001 / PR +0.0014 |

## Routing

Default level `learned_blend_at_fp_3` over `general`, `filegroups/native`, `filetypes/pe`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 919254 (786579 mal / 132675 ben) |
| Feature spec | 60358 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
