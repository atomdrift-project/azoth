# `filetype/elf`

LightGBM specialist for `elf`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=17668 (2793 malware / 14875 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9999 [0.9999, 1.0000] | 0.9996 [0.9994, 0.9998] | 0.9929 [0.9909, 0.9954] | - | ROC +0.0066 / PR +0.0063 |

## Routing

Default-level policy `or_general_primary`. Allowed routes (OR over thresholds): `general`, `filegroups/native`, `filetypes/elf`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=120, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 122544 rows (19468 mal / 103076 ben).
