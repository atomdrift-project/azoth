# `filetype/xlsx`

LightGBM specialist for `xlsx`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

> Benchmark AUC degenerate on this split. Routed full-corpus calibration governs deployment.

## Performance

Test partition, n=2244 (2232 malware / 12 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.5000 [0.5000, 0.5000] | 0.9947 [0.9947, 0.9947] | 0.9973 [0.9973, 0.9973] | - | — |

## Routing

Default-level policy `learned_blend_at_fp_0`. Allowed routes (OR over thresholds): `general`, `filegroups/documents`, `filetypes/xlsx`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=100, num_leaves=48, max_depth=12, min_child_samples=20, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 60358 features, policy `general_shared`. Trained on 15655 rows (15523 mal / 132 ben).
