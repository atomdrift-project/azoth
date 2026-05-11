# `filetype/javascript`

LightGBM specialist for `javascript`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=57574 (7439 malware / 50135 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9959 [0.9956, 0.9963] | 0.9816 [0.9801, 0.9831] | 0.9507 [0.9479, 0.9546] | - | — |

## Routing

Default-level policy `filetype_only`. Allowed routes (OR over thresholds): `filetypes/javascript`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=300, num_leaves=128, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 398014 rows (51191 mal / 346823 ben).
