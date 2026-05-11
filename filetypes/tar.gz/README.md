# `filetype/tar.gz`

LightGBM specialist for `tar.gz`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=3005 (1497 malware / 1508 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9986 [0.9980, 0.9993] | 0.9987 [0.9980, 0.9993] | 0.9844 [0.9815, 0.9886] | - | — |

## Routing

Default-level policy `group_only`. Allowed routes (OR over thresholds): `filegroups/archive`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=120, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 28529 rows (17975 mal / 10554 ben).
