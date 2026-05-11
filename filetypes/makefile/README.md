# `filetype/makefile`

LightGBM specialist for `makefile`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=2524 (17 malware / 2507 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.7847 [0.7144, 0.8559] | 0.0775 [0.0151, 0.2504] | 0.1111 [0.0372, 0.3810] | - | — |

## Routing

Default-level policy `or_general_primary`. Allowed routes (OR over thresholds): `general`, `filegroups/source`, `filetypes/makefile`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=120, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 17314 rows (147 mal / 17167 ben).
