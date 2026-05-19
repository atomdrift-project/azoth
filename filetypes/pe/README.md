# `filetype/pe`

LightGBM specialist for `pe`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=128908 (109970 malware / 18938 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9983 [0.9982, 0.9985] | 0.9997 [0.9997, 0.9997] | 0.9942 [0.9940, 0.9946] | - | ROC +0.0001 / PR +0.0014 |

## Routing

Default-level policy `learned_blend_at_fp_3`. Allowed routes (OR over thresholds): `general`, `filegroups/native`, `filetypes/pe`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 60358 features, policy `general_shared`. Trained on 919254 rows (786579 mal / 132675 ben).
