# `filetype/plist`

LightGBM specialist for `plist`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=1557 (68 malware / 1489 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.6376 [0.5780, 0.7030] | 0.1172 [0.0703, 0.1804] | 0.1653 [0.1147, 0.2521] | - | — |

## Routing

Default-level policy `or_general_primary`. Allowed routes (OR over thresholds): `general`, `filegroups/config`, `filetypes/plist`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=120, num_leaves=64, max_depth=12, min_child_samples=120, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 11004 rows (538 mal / 10466 ben).
