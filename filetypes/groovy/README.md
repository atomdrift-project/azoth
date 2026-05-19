# `filetype/groovy`

LightGBM specialist for `groovy`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=663 (15 malware / 648 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.4101 [0.2457, 0.5783] | 0.0232 [0.0196, 0.0354] | 0.0593 [0.0452, 0.0986] | - | — |

## Routing

Default-level policy `joint_or_at_fp_0`. Allowed routes (OR over thresholds): `general`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=120, num_leaves=96, max_depth=12, min_child_samples=30, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 60358 features, policy `general_shared`. Trained on 4500 rows (108 mal / 4392 ben).
