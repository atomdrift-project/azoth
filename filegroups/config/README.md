# `filegroup/config`

LightGBM specialist for `ini`, `json`, `package.json`, `plist`, `toml`, `xml`, `yaml`, `yml`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `config`). ROC 0.9984, PR 0.9916, F1 0.9672 on 23248 rows (2513 mal / 20735 ben).

## Routing

Default-level policy `—`. Allowed routes (OR over thresholds): none. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=300, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 60358 features, policy `general_shared`. Trained on 162484 rows (18106 mal / 144378 ben).
