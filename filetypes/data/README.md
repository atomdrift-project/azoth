# `filetype/data`

LightGBM specialist for `data`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=1207 (57 malware / 1150 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9697 [0.9454, 0.9883] | 0.8871 [0.8180, 0.9428] | 0.8713 [0.7997, 0.9346] | - | — |

## Routing

Default-level policy `or_general_primary`. Allowed routes (OR over thresholds): `general`, `filetypes/data`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=120, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 8124 rows (346 mal / 7778 ben).
