# `filetype/csharp`

LightGBM specialist for `csharp`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=7687 (227 malware / 7460 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.8131 [0.7810, 0.8525] | 0.5420 [0.4893, 0.5976] | 0.5509 [0.4949, 0.6056] | - | — |

## Routing

Default-level policy `or_general_primary`. Allowed routes (OR over thresholds): `general`, `filegroups/source`, `filetypes/csharp`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=120, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 53194 rows (1501 mal / 51693 ben).
