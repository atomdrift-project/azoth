# `filetype/elf`

LightGBM specialist for `elf`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=20007 (4500 malware / 15507 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9999 [0.9999, 1.0000] | 0.9998 [0.9997, 0.9999] | 0.9941 [0.9929, 0.9958] | - | ROC +0.0066 / PR +0.0065 |

## Routing

Default-level policy `group_only`. Allowed routes (OR over thresholds): `filegroups/native`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 56209 features, policy `general_shared`. Trained on 139890 rows (32567 mal / 107323 ben).
