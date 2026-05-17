# `filegroup/archive`

LightGBM specialist for `7z`, `apk`, `cab`, `deb`, `egg`, `gz`, `msi`, `rar`, `rpm`, `tar`, `tar.gz`, `tgz`, `vsix`, `war`, `whl`, `xpi`, `xz`, `zip`, `zst`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `archive`). ROC 0.9993, PR 0.9993, F1 0.9889 on 25478 rows (11843 mal / 13635 ben).

## Routing

Default-level policy `—`. Allowed routes (OR over thresholds): none. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=250, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 56209 features, policy `general_shared`. Trained on 190756 rows (94311 mal / 96445 ben).
