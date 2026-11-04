# Azoth — Routed Ensemble

## How a file is scored

1. `cleave` identifies the file's format — `elf`, `pe`, `pdf`, `javascript`, and so on.
2. `route_policies.json` answers: given that format and a severity level L0..L20, which routes are allowed, and at what calibrated thresholds?
3. Each allowed route scores the file with its own model and feature spec.
4. If any allowed route's score crosses its threshold, the file is flagged at that severity.

A route is one of: the general model, a filegroup specialist (`filegroups/<name>`), or a filetype specialist (`filetypes/<name>`). Specialists are trained only on files of their domain; the general model is trained on everything.

## Selection and reporting

Policy search selects route combinations and thresholds on dev raw scores from the exact exported ensembles. The locked test partition is used only to report saved decisions, without fitting a new calibrator, threshold, or combiner. Models, feature specs and policies stay fixed during publication.

## Routing policies

Per filetype per level, `azoth_route_policy_search.py` picks one of these policy forms by recall at the shared FP allowance, with F1 and fp-count tiebreaks. The chosen policy and its calibrated thresholds are written to `route_policies.json` and read by Scan at scan time:

- `joint_or_at_fp_N` — OR-rule across the allowed routes, with per-route thresholds sharing a total allowance of N observed false positives in the decision pool. The common case.
- `learned_blend_at_fp_N` — a logit blend `σ(b + Σ wᵢ · logit(pᵢ))` over raw route probabilities, thresholded to hit the shared FP allowance. Wins when route scores are complementary in a way a simple OR misses.
- `filetype_only` / `filetype_only_at_fp_N` — the specialist fires alone.
- `general_only`, `group_only`, `or_general_primary`, `group_primary_with_escape` — the single-route or single-primary variants.
- `calibrate_inherited` — the level inherits its threshold from a stricter level (no fresh calibration was warranted).
- `no_policy` — no configuration meets the shared FP allowance at this level; the route does not fire at this severity.

## Severity levels (L0..L25000)

L0 allows zero observed calibration FPs. For N benign files, positive L has continuous allowance `1 + (L - 1) * N / 100_000_000`, rounded down for a count budget. L1 allows one FP; L25 adds an estimated 24 FP/100M. General, group, and specialist models share the final decision allowance. Interpolation or extrapolation does not guarantee live-traffic rates. See the [shared level definition](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md).

Litmus reads the per-level thresholds from `route_policies.json` and assigns severity per file.

Default deploy level: L25 (one FP plus an estimated additional 24 FP/100M) (Scan loads the hostile threshold at that level; any suspicious band is derived consumer-side). Per-route thresholds and observed FP/100M live in [route_policies.md](route_policies.md) and each `filetypes/<name>/README.md`.
