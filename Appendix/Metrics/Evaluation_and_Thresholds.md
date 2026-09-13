# Metrics, evaluation and launch thresholds

Extracted from Sections 3.7, 5.3, 5.4, 5.6 and 5.7 of the final report.

## Ground truth, built three ways

1. **Implicit labels** — every reviewer decision (signed off, sent back, escalated) is a label attached to a report, produced by work that would happen anyway.
2. **Explicit labels** — a stratified sample of 30 reports per week, labelled independently by an experienced reviewer against the same written severity rubric given to the model, before seeing the model output. This is the evaluation set of record.
3. **Correction labels** — every override with its reason, where systematic mistakes become visible as patterns rather than anecdotes.

The rubric is versioned in the same repository as the prompt. A disagreement
between two human labellers is treated as a rubric defect to be fixed, not noise
to be averaged away.

## Baselines run in parallel

| Baseline | What it represents | Why it matters |
|---|---|---|
| Chronological queue | Today's behaviour — reports read in arrival order | If AI ordering does not beat arrival order, the feature has no reason to exist |
| Rules-only ordering | Numeric thresholds and keyword flags, buildable in about a week | The honest bar. AI must add value beyond what simple rules catch, specifically on issues expressed only in prose |

## Evaluation framework

| Type | Metric | Why it matters |
|---|---|---|
| Technical | Severity recall on serious (P1) issues | Missing a serious issue is the failure that hurts; recall is prioritised over precision |
| Technical | Severity classification precision overall | Too many false alarms and reviewers stop trusting the ordering |
| Technical | Issue extraction F1 against the weekly labelled sample | Whether the layer sees what a careful human reader sees |
| Technical | Groundedness — share of summary statements traceable to a source sentence | The direct measure of hallucination in this product |
| Technical | Schema validation failure rate and median latency | The queue must be ready when the reviewer opens it |
| Business | Reviewer minutes per campus report | The efficiency claim, measured rather than asserted |
| Business | Time from issue written to issue escalated | The outcome the institution actually cares about |
| Business | Send-back rate for incomplete reports | Upstream quality improvement, not just downstream speed |
| Trust | Override rate, within a two-sided band | Detects both an unhelpful model and a disengaged reviewer |
| Trust | Serious issues surfaced only by rules and missed by the model | The clearest early-warning signal of model drift |
| Trust | Campus-scoping violations detected in output | A single breach is a launch blocker, not a metric to optimise |

## Pilot targets

| Metric | Target |
|---|---|
| Reports where the reviewer accepted the AI severity unchanged | ≥ 70% |
| Median reviewer time per campus report | ≥ 40% below the pre-pilot baseline |
| Time from a serious issue being written to being escalated | Same working day (baseline: one to two days) |
| Reports sent back for missing information | ≥ 30% reduction |

## Go / no-go thresholds, fixed before the pilot

| Condition | Threshold | If not met |
|---|---|---|
| P1 severity recall on the weekly labelled sample | ≥ 0.90 sustained over four weeks | Do not expand. Improve rubric and grounding, re-run. |
| Ungrounded summary statements | ≤ 2% of sampled statements | Tighten grounding constraints; suspend summaries above 5%. |
| Reviewer override rate | Between 10% and 25% | Below 10%: investigate complacency directly. Above 25%: the model is not adding value yet. |
| Campus-scoping or permission violations | Exactly zero | Immediate stop. Absolute launch blocker. |
| Inference cost per campus per month | Within the modelled ceiling | Reduce context size and batch, or restrict to serious items only. |
| Reviewer confidence (structured feedback) | Majority report the queue changed their working order for the better | Treat as workflow-fit failure, not model failure; redesign the surface. |

## Why the override band is two-sided

A very low override rate is not a success signal. It is the most likely early
symptom of automation complacency, which is the specific failure this design is
most afraid of.
