# `filetype/7z`

LightGBM specialist for `7z`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

> Benchmark AUC degenerate on this split. Routed full-corpus calibration governs deployment.

## Performance

Test partition, n=540 (528 malware / 12 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.5000 [0.5000, 0.5000] | 0.9778 [0.9778, 0.9778] | 0.9888 [0.9888, 0.9888] | - | — |

## Routing

Default-level policy `no_policy`. Allowed routes (OR over thresholds): none. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=auto. Feature spec: general-shared, 56209 features, policy `general_shared`. Trained on 3567 rows (3507 mal / 60 ben).
