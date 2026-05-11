# `filetype/jar`

LightGBM specialist for `jar`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=307 (108 malware / 199 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9930 [0.9855, 0.9978] | 0.9868 [0.9724, 0.9962] | 0.9533 [0.9245, 0.9771] | - | — |

## Routing

Default-level policy `no_policy`. Allowed routes (OR over thresholds): none. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=120, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 2017 rows (504 mal / 1513 ben).
