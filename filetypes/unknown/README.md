# `filetype/unknown`

LightGBM specialist for `unknown`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=3362 (1342 malware / 2020 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.8312 [0.8195, 0.8450] | 0.8045 [0.7914, 0.8199] | 0.7651 [0.7458, 0.7857] | - | — |

## Routing

Default-level policy `filetype_only_at_fp_3`. Allowed routes (OR over thresholds): `filetypes/unknown`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=120, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 60358 features, policy `general_shared`. Trained on 23626 rows (9702 mal / 13924 ben).
