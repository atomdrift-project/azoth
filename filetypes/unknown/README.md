# `filetype/unknown`

LightGBM specialist for `unknown`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=3118 (1125 malware / 1993 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.8209 [0.8054, 0.8372] | 0.7840 [0.7675, 0.8035] | 0.7574 [0.7384, 0.7827] | - | — |

## Routing

Default-level policy `filetype_only`. Allowed routes (OR over thresholds): `filetypes/unknown`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=120, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 56209 features, policy `general_shared`. Trained on 22657 rows (8921 mal / 13736 ben).
