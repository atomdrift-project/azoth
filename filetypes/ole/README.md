# `filetype/ole`

LightGBM specialist for `ole`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=885 (221 malware / 664 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9863 [0.9727, 0.9976] | 0.9858 [0.9717, 0.9963] | 0.9775 [0.9661, 0.9910] | - | — |

## Routing

Default-level policy `joint_or_at_fp_0`. Allowed routes (OR over thresholds): `general`, `filetypes/ole`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=250, num_leaves=128, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=2.0, early_stop=25, device=auto. Feature spec: general-shared, 60358 features, policy `general_shared`. Trained on 6395 rows (1702 mal / 4693 ben).
