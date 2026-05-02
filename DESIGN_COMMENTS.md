# Design Comments: Path to Top-Performing

DESIGN.md gets the routing algebra right. The honest path to "top-performing
malware analysis model in the world" has less to do with the ensemble structure
and more to do with five things outside that doc.

## 1. Time-split evaluation, not random-split

Calibration today uses a deterministic content-hash partition. That measures
fit on a fixed corpus, not generalization forward. The world-record path is:

- Train on samples ingested before timestamp `T_train`.
- Calibrate thresholds on `[T_train, T_calibrate]`.
- Report FP rate and hostile recall on held-out windows `[T_calibrate, now]`.
- Track the curve as the held-out window slides.

Then "is azoth top-performing?" has a defensible answer ("FP rate stays under
budget for X weeks past calibration") and you have a measured cadence for
re-calibration. EMBER 2024 spends a chapter on this for a reason; it is the
difference between a benchmark-winning model and a deployable one.

This is evaluation methodology, not v1 architecture, but it should appear in
DESIGN.md's Research Questions section.

## 2. Family-grouped evaluation

Random hash-split leaks family identity. 800 Emotet variants in train and 200
in test produces flattering numbers that do not survive contact with novel
families. Build a family or cluster grouping — cheap version: behavioral hash,
AV-label clustering, or VirusTotal family tags — and report recall at the
family level.

A model that averages 95% sample-recall but only 60% family-recall is fragile
in a way that does not show up on leaderboards. The score-table schema should
carry the grouping:

```text
family_id    (or cluster_id, when family unknown)
```

Threshold search and promotion can stay sample-level. The measurement is what
matters.

## 3. Closed-loop FP/FN mining

The collimator Makefile already has `false-positives`, `false-positives-triage`,
`near-false-positives`, and the matching false-negative targets. The artifacts
exist. What is not yet documented is the cadence.

Top systems treat production FPs as the highest-priority training signal:

- litmus deployments emit a structured FP/FN log (sha + score + features
  + classification).
- A regular ingest job pulls those into hopper tagged as production false
  positives or false negatives.
- Each training run upweights or oversamples production-fp benigns.
- The promotion gate explicitly checks that production FPs from the previous
  deployment are caught, or shown to be irreducible at the configured budget.

This is the flywheel that separates "good model" from "compounding lead".
DESIGN.md could state the cadence explicitly: weekly retrain, monthly,
triggered by FP threshold breach, etc.

## 4. The model is bounded by cleave

The ML side has now had multiple iterations of design attention. The feature
extractor probably has not. The honest question is not "is the LightGBM
hyperparameter tuned" — it is "is there a signal cleave is missing that would
let any model classify the hard 5%."

Candidate signals worth auditing for:

- Reachable-string analysis, not just string presence.
- API-call sequence n-grams from the import table plus indirect-call resolution.
- Control-flow shape: basic-block count distribution, indegree, loop nesting.
- Section-entropy curves, not just averages.
- Authenticode chain validation as a numeric feature, not just a signed flag.
- Embedded-payload signals beyond base64: steganography in PNG IDAT, polyglots,
  MZ-in-PDF, archive-in-archive recursion depth.
- Cross-archive-member relationships: parent-archive context features for
  embedded files.

This investment pays more than anything in the routing layer. Cleave is the
ceiling.

## 5. Adversarial slices in evaluation, not just averages

Aggregate metrics hide the cases that matter. Build named evaluation slices
and report them every release:

- Packed binaries (UPX, custom packers).
- Obfuscated scripts (PowerShell, JS).
- Living-off-the-land binaries: `certutil`, `mshta`, `regsvr32`, etc.
- Recent-family malware: last 90 days, by first-seen.
- Low-popularity benigns: long-tail open-source software, internal tools,
  niche utilities.
- Source-code malware, not compiled.
- Multi-stage and dropper chains.

If azoth is 99% on EMBER but 70% on packed-fileless, that is a real story you
want to know before users do. The score table makes this almost free — add a
`slice_tag` column populated from rule labels and aggregate per-slice on demand.

## Priority

Of these, (1) and (3) are the highest leverage. They make every subsequent
improvement measurable and create a feedback loop that compounds. (4) is where
the next 2-3 percentage points of recall actually live. (2) and (5) are cheap
insurance against declaring victory prematurely.

## Open question

What is hopper's current ingest cadence, and what fraction of the benign
corpus comes from the long tail — not popular OSS, not Windows desktop apps?
That is the data dimension that is not visible from outside collimator, and
it caps everything else. A world-class detection model trained on a corpus
biased toward popular software will be a world-class detector of popular
software, and unremarkable on the rest.
