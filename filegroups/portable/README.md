# `filegroup/portable`

LightGBM specialist for `dex`, `java_class`, `javaclass`, `pyc`, `python-bytecode`, `python_bytecode`, `wasm`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `portable`). ROC 0.890019, PR 0.727668, F1 0.8156 on 385,100 rows (726 mal / 384,374 ben).

## Routing

Files matching `portable` are scored by none. The ensemble's decisions apply the saved routing policy, including every level at or below the requested level. Ranking metrics use the signed distance from that policy's decision boundary. See [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 2,320,448 (3,078 mal / 2,317,370 ben) |
| Feature spec | 8075 features (`route_specific`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
