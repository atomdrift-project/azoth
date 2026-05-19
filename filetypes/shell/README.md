# `filetype/shell`

LightGBM specialist for `shell`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=6602 (920 malware / 5682 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9969 [0.9960, 0.9978] | 0.9855 [0.9820, 0.9890] | 0.9470 [0.9366, 0.9577] | - | — |

## Routing

Default-level policy `filetype_only`. Allowed routes (OR over thresholds): `filetypes/shell`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=150, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 60358 features, policy `general_shared`. Trained on 44922 rows (5513 mal / 39409 ben).
