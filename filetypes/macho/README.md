# `filetype/macho`

LightGBM specialist for `macho`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=949 (152 malware / 797 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9990 [0.9979, 0.9996] | 0.9949 [0.9902, 0.9981] | 0.9589 [0.9481, 0.9803] | - | — |

## Routing

Default-level policy `filetype_only`. Allowed routes (OR over thresholds): `filetypes/macho`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=120, num_leaves=160, max_depth=12, min_child_samples=60, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 6584 rows (1202 mal / 5382 ben).
