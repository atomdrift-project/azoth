# `filetype/python`

LightGBM specialist for `python`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=16448 (1843 malware / 14605 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9949 [0.9938, 0.9959] | 0.9711 [0.9655, 0.9760] | 0.9195 [0.9109, 0.9322] | - | — |

## Routing

Default-level policy `or_general_primary`. Allowed routes (OR over thresholds): `general`, `filegroups/scripts`, `filetypes/python`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=130, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 115381 rows (12782 mal / 102599 ben).
