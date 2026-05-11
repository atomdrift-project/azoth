# `filetype/ole`

LightGBM specialist for `ole`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=688 (30 malware / 658 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9995 [0.9983, 1.0000] | 0.9897 [0.9703, 1.0000] | 0.9655 [0.9091, 1.0000] | - | — |

## Routing

Default-level policy `or_general_primary`. Allowed routes (OR over thresholds): `general`, `filegroups/documents`, `filetypes/ole`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=250, num_leaves=128, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=2.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 4891 rows (229 mal / 4662 ben).
