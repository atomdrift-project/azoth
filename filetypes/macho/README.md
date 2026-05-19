# `filetype/macho`

LightGBM specialist for `macho`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=1640 (258 malware / 1382 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9988 [0.9981, 0.9994] | 0.9936 [0.9899, 0.9966] | 0.9594 [0.9459, 0.9753] | - | — |

## Routing

Default-level policy `learned_blend_at_fp_0`. Allowed routes (OR over thresholds): `general`, `filegroups/native`, `filetypes/macho`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=250, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 60358 features, policy `general_shared`. Trained on 11059 rows (1783 mal / 9276 ben).
