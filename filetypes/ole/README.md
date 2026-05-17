# `filetype/ole`

LightGBM specialist for `ole`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=870 (211 malware / 659 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9949 [0.9878, 0.9998] | 0.9917 [0.9810, 0.9993] | 0.9784 [0.9686, 0.9906] | - | — |

## Routing

Default-level policy `or_general_primary`. Allowed routes (OR over thresholds): `general`, `filegroups/documents`, `filetypes/ole`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=250, num_leaves=128, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=2.0, early_stop=25, device=auto. Feature spec: general-shared, 56209 features, policy `general_shared`. Trained on 6316 rows (1650 mal / 4666 ben).
