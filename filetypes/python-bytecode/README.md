# `filetype/python-bytecode`

LightGBM specialist for `python-bytecode`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `python-bytecode`). ROC 0.921131, PR 0.781843, F1 0.8582 on 55,928 rows (445 mal / 55,483 ben).

## Routing

Files matching `python-bytecode` are scored by none. The ensemble's per-row score is whatever combiner strategy (`—`) the metrics step selected for this route. The per-level operating thresholds litmus applies on top live in [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 393,038 (2,270 mal / 390,768 ben) |
| Feature spec | 9330 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 50 |
| device | auto |
