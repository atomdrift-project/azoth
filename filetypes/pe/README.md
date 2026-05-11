# `filetype/pe`

LightGBM specialist for `pe`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=74705 (56704 malware / 18001 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9986 [0.9985, 0.9988] | 0.9996 [0.9995, 0.9996] | 0.9906 [0.9901, 0.9911] | - | ROC +0.0004 / PR +0.0013 |

## Routing

Default-level policy `or_general_primary`. Allowed routes (OR over thresholds): `general`, `filegroups/native`, `filetypes/pe`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 540091 rows (413888 mal / 126203 ben).
