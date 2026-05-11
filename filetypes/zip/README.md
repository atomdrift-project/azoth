# `filetype/zip`

LightGBM specialist for `zip`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=4733 (4042 malware / 691 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9709 [0.9670, 0.9746] | 0.9948 [0.9941, 0.9954] | 0.9716 [0.9688, 0.9745] | - | — |

## Routing

Default-level policy `group_only`. Allowed routes (OR over thresholds): `filegroups/archive`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=250, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 34767 rows (29644 mal / 5123 ben).
