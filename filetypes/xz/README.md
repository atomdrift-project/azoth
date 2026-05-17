# `filetype/xz`

LightGBM specialist for `xz`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=2869 (6 malware / 2863 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.7396 [0.4228, 1.0000] | 0.6675 [0.3306, 1.0000] | 0.8000 [0.4946, 1.0000] | - | — |

## Routing

Default-level policy `or_general_primary`. Allowed routes (OR over thresholds): `general`, `filegroups/archive`, `filetypes/xz`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=auto. Feature spec: general-shared, 56209 features, policy `general_shared`. Trained on 20828 rows (48 mal / 20780 ben).
