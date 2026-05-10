# Azoth Filegroup — `archive`

Specialist classifier for `7z`, `apk`, `cab`, `deb`, `egg`, `gz`, `msi`, `rar`, `rpm`, `tar`, `tar.gz`, `tgz`, `vsix`, `war`, `whl`, `xpi`, `xz`, `zip`, `zst`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

Training-time benchmark (no test-bucket-only metric on file):

- ROC AUC / PR AUC / F1: 0.9579 / 0.9488 / 0.9205
- Benchmark rows: 16636 (6170 malware, 10466 benign).

## Training

- Inputs: shared general `feature_spec.json` (37595 features); feature-spec policy `general_shared`.
- Algorithm: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Feature families:
  - aggregate finding counts
  - ATT&CK/MBC n-grams
  - cleave trait taxonomy
  - element tokens
  - extended file metrics
  - format-group hints
  - hopper score
  - hostile density/escalation
  - packaged capability mode=paths
  - path/criticality bigrams/trigrams
  - repetition penalties
  - severity distribution
  - soft presence
  - structural coverage
- Training rows: 83389 (42971 malware, 40418 benign).
- Internal training-time benchmark rows: 16636 (6170 malware, 10466 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9579 / 0.9488 / 0.9205.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 78.49% | 0.00 | 0.994853 | 8.0 | 81.17% | 95.55 | 0.981812 |
| 1 | 1.0 | 81.17% | 95.55 | 0.981812 | 16.0 | 81.17% | 95.55 | 0.981812 |
| 2 | 2.0 | 81.17% | 95.55 | 0.981812 | 24.0 | 81.17% | 95.55 | 0.981812 |
| 3 | 3.0 | 81.17% | 95.55 | 0.981812 | 32.0 | 81.17% | 95.55 | 0.981812 |
| 4 | 4.0 | 81.17% | 95.55 | 0.981812 | 40.0 | 81.17% | 95.55 | 0.981812 |
| 5 | 5.0 | 81.17% | 95.55 | 0.981812 | 48.0 | 81.17% | 95.55 | 0.981812 |
| 6 | 6.0 | 81.17% | 95.55 | 0.981812 | 56.0 | 81.17% | 95.55 | 0.981812 |
| 7 | 7.0 | 81.17% | 95.55 | 0.981812 | 64.0 | 81.17% | 95.55 | 0.981812 |
| 8 | 8.0 | 81.17% | 95.55 | 0.981812 | 72.0 | 81.17% | 95.55 | 0.981812 |
| 9 | 9.0 | 81.17% | 95.55 | 0.981812 | 80.0 | 81.17% | 95.55 | 0.981812 |
