# Roadmap — phases end at proof gates

Extracted from Section 3.6 of the final report. Phase 2 does not start because
Phase 1 finished; it starts because Phase 1 met a measured threshold.

| Phase | Focus | Proof gate before proceeding |
|---|---|---|
| **0 — done** | Deterministic platform: submission spine, fees, tasks, approvals, campaigns, exams, audit. Gemini narrative summaries and meeting intelligence live. | Platform adopted as the daily system of record; daily submission compliance stable. |
| **1 — MVP pilot** (1 month, 5 campuses) | Daily operations triage in assist-only mode with the full evaluation harness. | Severity recall, summary error rate, override rate and reviewer trust thresholds all met. |
| **2 — controlled expansion** (1 quarter) | All 40 campuses; cross-campus weekly pattern detection; OCR document intake; budget-proposal completeness checking; scoped natural-language query. | Cost per campus per month within the modelled ceiling; no campus-scoping breach; sustained reviewer agreement rate. |
| **3 — assisted exam operations** | Paper equivalence assistance and portion-completion inference feeding the examinations flow, with mandatory faculty approval. | Zero AI-only paper approvals; faculty acceptance measured; academic governance sign-off obtained. |
| **4 — evaluate productisation** | Assess whether the platform is offered to peer institutions as a product. | Two consecutive quarters of stable internal operation and a defensible support model. |

## Cut rather than sequenced

Two high-value ideas were removed from the plan entirely rather than deferred to
a later phase, because cost of error — not value — decided them:

- **Predictive fee-default and dropout risk scoring.** The training data
  available today reflects operational recording habits more than student
  behaviour, and a wrong prediction attaches to a named student.
- **Automated staff performance scoring from operational logs.** It converts an
  operations tool into a surveillance instrument, which would destroy the trust
  the platform depends on for honest daily reporting.

## Prerequisites for Phase 2, independent of model quality

- Documentation, a written runbook and a second engineer. One builder is not an
  operating model, and this is the most serious operational risk in the
  submission.
- Data minimisation in place before any text reaches the model API.
- A working single-flag rollback to rules-only ordering.
