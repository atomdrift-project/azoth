# `filetype/elf`

LightGBM specialist for `elf`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=25753 (8826 malware / 16927 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9999 [0.9999, 0.9999] | 0.9999 [0.9998, 0.9999] | 0.9947 [0.9935, 0.9957] | - | ROC +0.0066 / PR +0.0066 |

## Routing

Default-level policy `learned_blend_at_fp_0`. Allowed routes (OR over thresholds): `general`, `filegroups/native`, `filetypes/elf`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 60358 features, policy `general_shared`. Trained on 178232 rows (61224 mal / 117008 ben).
