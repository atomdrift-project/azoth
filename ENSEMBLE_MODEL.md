# Azoth — Routed Ensemble

## How a file is scored

1. `cleave` identifies the file's format — `elf`, `pe`, `pdf`, `javascript`, and so on.
2. `route_policies.json` answers: given that format and a severity level L0..L20, which routes are allowed, and at what calibrated thresholds?
3. Each allowed route scores the file with its own model and feature spec.
4. If any allowed route's score crosses its threshold, the file is flagged at that severity.

A route is one of: the general model, a filegroup specialist (`filegroups/<name>`), or a filetype specialist (`filetypes/<name>`). Specialists are trained only on files of their domain; the general model is trained on everything.

## Per-filetype combiner selection

The Ensemble Performance row in the bundle README shows the **best combiner per filetype**, picked from a handful of candidates evaluated on the dev partition:

- `specialist_priority` — for each row, use the most specific route's raw score (filetype specialist → filegroup → general). By construction this equals the specialist on filetype-X rows, so `ensemble ≥ specialist` holds always for this strategy.
- `calibrated_max` — per-route isotonic-calibrate (5-fold OOF), then `max` of the calibrated probabilities. Wins when routes score on different distributions and the calibrated max is more comparable than the raw max.
- `stacked_lr` / `stacked_xgb` — a small stacker (logistic regression or XGBoost) over the per-route calibrated probs. Wins when routes carry complementary signal that linear/tree combination can exploit.
- `naive_max` — raw `max` across routes, kept as a sanity check; rejected from the picker because raw scores don't share a probability calibration.

**Selection criterion**: maximize **recall at 3 FP/M** on the dev partition (matching the deployment FP/M target), with **PR AUC** as a secondary tiebreak. The picker is constrained by a floor: no combiner may report worse than `specialist_priority`, on either dev or test. If a combiner would clear the floor on dev but regress below it on test (sampling variance), the report falls back to `specialist_priority`. This guarantees the **ensemble ≥ specialist** invariant in every row of the bundle README.

## Routing policies

Per filetype per level, `azoth_route_policy_search.py` picks one of these policy forms by recall at the FP/M target, with F1 and fp-count tiebreaks. The chosen policy and its calibrated thresholds are written to `route_policies.json` and read by litmus at scan time:

- `joint_or_at_fp_N` — OR-rule across the allowed routes, with per-route thresholds calibrated to a joint FP/M target of N per million. The common case.
- `learned_blend_at_fp_N` — a logit blend `σ(b + Σ wᵢ · logit(pᵢ))` over calibrated route probabilities, thresholded to hit the FP/M target. Wins when route scores are complementary in a way a simple OR misses.
- `filetype_only` / `filetype_only_at_fp_N` — the specialist fires alone.
- `general_only`, `group_only`, `or_general_primary`, `group_primary_with_escape` — the single-route or single-primary variants.
- `calibrate_inherited` — the level inherits its threshold from a stricter level (no fresh calibration was warranted).
- `no_policy` — no configuration meets the FP/M target at this level; the route does not fire at this severity.

## Severity levels (L0..L20)

L0..L20 are observation-derived strictness grades, not optimization targets. For each route, level Lk's threshold is set so that roughly qk benigns per million would be flagged on the dev partition. Strict levels (where `n_benign · qk · 10⁻⁶ < 1` falls below empirical resolution) use a generalized Pareto fit to the benign-score upper tail; looser levels use direct empirical quantiles.

Litmus reads the per-level thresholds from `route_policies.json` and assigns severity per file.

Default deploy level: L3 (litmus loads both hostile and suspicious thresholds at the same level). Per-route L0..L20 thresholds and observed FP/M live in [route_policies.md](route_policies.md) and each `filetypes/<name>/README.md`.
