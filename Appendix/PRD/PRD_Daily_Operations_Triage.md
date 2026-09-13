# PRD-lite — Daily Operations Triage

The AI wedge recommended for pilot. Extracted from Section 3.3 of the final report.

## User problem

The reviewing manager cannot read around 40 free-text campus reports carefully
in the evening window available, so severity is discovered late and
inconsistently.

## Core workflow

1. The Business Operations Associate submits the daily operational report before the 16:00 cut-off, as they do today.
2. On submission, the platform assembles a grounded context package: the report text, the campus's numeric series for the day (fee movement, attendance, open tasks, pending budget approvals), and the last seven days of that campus's history.
3. The model extracts discrete issues from the text, classifies each by type and severity, and produces a two-to-three sentence summary that cites the source sentence for every claim it makes.
4. Deterministic rules run in parallel and can only raise severity, never lower it. A numeric breach always surfaces regardless of what the model concluded.
5. Each report enters the reviewer's queue ranked by severity and confidence, with the evidence attached.
6. The reviewer signs off, sends back, or escalates. Overrides require a one-line reason from a short list plus optional free text.
7. The decision, the model output, the prompt version and the reviewer's reason are written immutably to the audit log.

## Where AI creates the value

AI does exactly three things: it reads unstructured text, it proposes a severity
with cited evidence, and it drafts a summary. It does not compute numbers, does
not decide approvals, does not send anything to anyone, and does not write to
any record other than its own suggestion row.

## Fallback logic

| Failure mode | Fallback behaviour |
|---|---|
| Model API unavailable or times out | Queue falls back to rules-plus-chronological ordering with a visible banner. The workflow never blocks on the model. |
| Model returns low confidence | Item marked "needs full read", summary collapsed by default, raw report shown first. |
| Model output fails schema validation | Output discarded, item treated as unprocessed, failure logged to the evaluation table. |
| Model misses an issue the rules caught | Rule severity wins. The mismatch is flagged into the weekly review sample. |
| Reviewer disagrees with severity | One-click override with reason. Overrides above a weekly threshold trigger a prompt and threshold review. |

## Uncertainty handling in the interface

| Confidence band | System behaviour |
|---|---|
| High | Summary expanded, severity shown, item in the recommended band. Sign-off is one action; the original report stays one click away. |
| Medium | Summary shown with a verify-before-acting marker. Recommended action phrased as a question. Cannot be bulk-signed-off. |
| Low | No summary shown. Item labelled "needs full read", ordered by rules and recency, original report opens first. |
| Failure | Rules-only mode with a visible banner. The reviewer's workflow is unchanged from the pre-AI experience. |

## Human in the loop

- No report changes state without a human action. The model can order the queue; it cannot advance the state machine.
- Escalations and outbound messages are drafts until a human edits and confirms them.
- Overrides capture a structured reason, read weekly as both a quality signal and a check on engagement.
- Auto-sign-off is disabled for any report the layer marked as serious.

## MVP definition

Five campuses, one cluster, one academic month, assist-only.

**In scope:** summary generation with citation, issue extraction, severity
classification, confidence-based ranking, override capture with reasons,
reconciliation with existing numeric rules, the audit trail, and the evaluation
harness with a weekly manually reviewed sample.

**Out of scope:** any automatic approval, any student- or parent-facing message,
any predictive scoring attached to a named student or staff member, exam paper
decisions, and any write access by the model to production operational tables.
