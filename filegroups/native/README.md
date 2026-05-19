# `filegroup/native`

LightGBM specialist for `elf`, `macho`, `pe`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `native`). ROC 0.9999, PR 1.0000, F1 0.9987 on 156,723 rows (119,341 mal / 37,382 ben).

## Routing

At the L3 deploy level the policy is `—` over none. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 1,116,880 (856,135 mal / 260,745 ben) |
| Feature spec | 48518 features (`route_specific`) |
| n_estimators | 350 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 40 |
| device | auto |
