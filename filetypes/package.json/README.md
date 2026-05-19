# `filetype/package.json`

LightGBM specialist for `package.json`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=3523 (2162 malware / 1361 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9992 [0.9983, 0.9998] | 0.9996 [0.9992, 0.9999] | 0.9972 [0.9956, 0.9986] | - | — |

## Routing

Default-level policy `joint_or_at_fp_0`. Allowed routes (OR over thresholds): `general`, `filegroups/config`, `filetypes/package.json`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=150, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 60358 features, policy `general_shared`. Trained on 25259 rows (15617 mal / 9642 ben).
