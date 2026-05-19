# `filetype/xml`

LightGBM specialist for `xml`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed routed ensemble on the `xml` slice of the test partition: 288 malware / 17921 benign (18209 rows). These are the headline numbers from the bundle [README](../../README.md).

| ROC AUC | PR AUC | Recall @ 3FP/M | F1 | Brier |
|---:|---:|---:|---:|---:|
| 0.7434 | 0.1440 | 0.00% | 0.3299 | 0.0155 |

## Specialist Performance

`filetypes/xml` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.7451 | 0.1445 | 0.3306 | 0.00% | 0.0155 | — |

## Routing

Default level `joint_or_at_fp_0` over `general`, `filegroups/config`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 125937 (1948 mal / 123989 ben) |
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
