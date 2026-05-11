# `filetype/shell`

LightGBM specialist for `shell`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=5720 (417 malware / 5303 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9971 [0.9960, 0.9979] | 0.9702 [0.9600, 0.9786] | 0.9063 [0.8850, 0.9294] | - | — |

## Routing

Default-level policy `group_only`. Allowed routes (OR over thresholds): `filegroups/scripts`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=150, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 39033 rows (2010 mal / 37023 ben).
