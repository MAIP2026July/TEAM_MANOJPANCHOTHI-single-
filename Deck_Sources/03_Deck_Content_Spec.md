# Presentation deck — full content specification

**Deck:** UniConnect Operations OS — MBA ZG583 capstone product review
**Presenter:** Manoj Kumar Panchothi
**Length:** 12 slides, 12–15 minutes
**Design:** not specified — the assignment brief sets no requirement on colour, typography or layout, so this document contains content only
**Audience framing:** a leadership review group deciding whether to fund a pilot — not a classroom recital

Everything below is final copy. Image filenames refer to the appendix image set
(`appendix/images/` in the A01–A66 archive).

---

## Slide 1 — Title

**Kicker:**
MBA ZG583 · MANAGEMENT OF AI PRODUCTS · CAPSTONE

**Title:**
UniConnect Operations OS

**Subtitle:**
An AI-assisted academic operations platform running across a 40-campus
higher-education network. Product review for a pilot decision.

**Footer:**
Manoj Kumar Panchothi · 11 September 2026

**Speaker notes:**
This is a product review, not a project report. The ask at the end is a pilot
decision on five campuses. The platform already runs the operational day; what
is being decided is the AI layer on top of it.

---

## Slide 2 — The same operational day, forty times over

**Intro paragraph:**
Fees to reconcile, daily reports to write and review, attendance to record,
problems to route — every working day, at every campus. Before the platform it
lived in spreadsheets, email and WhatsApp. The platform fixed the structure.
What remains is a reading problem.

**Three key figures:**

| Number | Label |
|---|---|
| **40** | campuses filing a free-text report every working day |
| **2.5 hrs** | between the 16:00 filing deadline and the 18:30 sign-off |
| **1–2 days** | typical lag before a serious issue is escalated |

**Closing statement:**
The failure is not a missing feature. It is that decision quality falls as the
network grows, because the reading does not scale.

**Speaker notes:**
Operational drag in an education network is paid in student experience —
blocked class access, unresolved facility problems, exam-day failures. Adding
headcount to read reports scales cost linearly with campuses, which is the
economics we are trying to escape.

---

## Slide 3 — Who feels it, and when

**Three profiles:**

**Business Operations Associate**
- Files one campus report before 16:00
- Wants it accepted first time
- Re-sends when it is sent back

**Programme Manager / COS** — the primary user
- Reviews ten to twelve campuses nightly
- Must find the three that need tonight
- Signs off or escalates

**Academic Operations Lead**
- Plans exam cycles per campus
- Portions, papers, seating, invigilation
- Rebuilt in spreadsheets today

**Sub-headline:**
The reviewer's evening is the moment the product is designed around

**Process flow, one line:**
submit → 16:00 deadline → **AI-assisted triage** → **human review** → sign off /
send back / escalate → immutable audit

**Image:** `A30-pm-review-queue.png`
**Caption:** The review surface today: submissions awaiting a decision, in
arrival order, with no ranking applied.

**Speaker notes:**
Named roles, a real cut-off time, a real sign-off deadline. This is not a
generic persona — it is the workflow the platform already enforces.

---

## Slide 4 — Why AI, and why not

**Two contrasting lists:**

**Rules and dashboards already handle this**
- A fee number that drops
- Attendance below target
- A report not filed by 16:00
- Any numeric threshold breach

**They cannot handle this**
- "lab machines down again since Monday"
- Buried in paragraph four of a routine report
- Written by forty different people
- A language problem, not a numbers problem

**Sub-headline: Why now**
- The network reached 40 campuses — the reading load crossed what a small central team can absorb.
- The platform now supplies both things AI needs here: structured context to ground on, and an existing human approval step to catch it when wrong.
- Inference is a per-call cost in fractions of a rupee, so the entry cost is near zero rather than a licence commitment.

**Closing statement:**
**Where AI is deliberately absent:** fee arithmetic, permission enforcement,
approval states and audit records stay deterministic — they must be exactly
correct and defensible to an auditor.

**Speaker notes:**
Two kinds of AI in this platform: language AI that reads and drafts, and
optimisation AI that searches and places — exam seating is constraint
satisfaction, not a language model. They fail in completely different ways and
need different evaluation.

---

## Slide 5 — Platform, plus one narrow wedge

**Band 1 — PLATFORM, live in production**
One database, one permission model, one audit trail. Fees · daily operations
spine · tasks · campaigns · assessments and exam papers · faculty · budgets ·
meetings · academic operations hub

**Band 2 — INTELLIGENCE LAYER, a feature, not a second product**
Reads the operational text nobody has time to read, states how confident it is,
and routes each item to the right human with the evidence attached. Switch it
off and the platform still runs.

**Sub-headline:**
MVP — five campuses, one cluster, one academic month, assist-only

**Two lists:**

**In scope**
- Summary with cited source sentence
- Severity and confidence ranking
- Override with structured reason
- Weekly labelled evaluation sample

**Out of scope**
- Any automatic approval
- Any student-facing message
- Predictive scoring of a named person
- Model write access to operational tables

**Speaker notes:**
The MVP is intentionally narrow because the binding risk is trust and workflow
fit, not model capability. A wider MVP gives a more impressive demo and a less
trustworthy answer.

---

## Slide 6 — The decisions worth defending

**Table:**

| Layer | Decision | Why |
|---|---|---|
| Model / inference | API — Google Gemini | Quality is adequate, cost is per-call, switching cost stays in our code |
| Workflow, permissions, audit | Build | The differentiation, and the part that must be exactly correct |
| Database, hosting, queues | Buy — Supabase, Railway, Redis | Row-level security at the database layer for a fraction of the cost |
| Identity, mail, calendar | Partner — Google Workspace | The institution already runs on it |

**Two items below:**

**Deferred: predictive student-risk scoring**
The training data reflects recording habits more than student behaviour, and a
wrong prediction attaches to a named student.

**Rejected: AI-scored staff performance**
It turns an operations tool into a surveillance instrument, which destroys the
honest daily reporting the platform depends on.

**Speaker notes:**
The two refusals matter more than the approvals. Cost of error was added as a
scoring dimension alongside value and effort, and it is what moved these two
out.

---

## Slide 7 — Phases end at proof gates, not at dates

**Intro line:**
Phase 2 does not start because Phase 1 finished. It starts because Phase 1 met a
measured threshold.

**Table:**

| Phase | Focus | Gate before proceeding |
|---|---|---|
| 0 — done | Deterministic platform; narrative summaries and meeting intelligence live | Adopted as the daily system of record |
| 1 — MVP pilot | Daily operations triage on five campuses for one month, assist-only, with the evaluation harness | Recall, groundedness, override band and reviewer trust all met |
| 2 — expansion | All 40 campuses; cross-campus patterns; OCR intake; budget completeness checks | Cost per campus-month within ceiling; zero scoping breaches |
| 3 — assisted exams | Paper equivalence assistance and portion inference, faculty approval mandatory | Zero AI-only paper approvals; academic governance sign-off |
| 4 — productisation | Assess offering the platform to peer institutions | Two stable quarters and a defensible support model |

**Closing statement:**
Two AI ideas were cut from this plan rather than sequenced later: predictive
student-risk scoring and AI-scored staff performance. Cost of error, not value,
is what removed them.

**Speaker notes:**
A roadmap with dates invites the question of whether dates slipped. A roadmap
with gates invites the question of whether thresholds were met, which is the
conversation we want.

---

## Slide 8 — The prototype is the production system

**Image 1:** `A46-seating-plan.png`
**Caption:** Seating allocation: 67 of 67 seats filled, interleaving constraint
satisfied, every classroom reporting no violations. An invalid plan is flagged,
never silently emitted.

**Image 2:** `A27-paper-editor-actions.png`
**Caption:** Paper generation ends at Send for Approval — a person approves, and
any question can be swapped.

**Image 3:** `A64-budget-order-tracking.png`
**Caption:** The budget path: no AI anywhere in it, threshold rule printed on the
screen.

**Speaker notes:**
Not a mock-up. Live at uniconnect-app.up.railway.app, public repository, 66
captioned screens in the appendix. The advantage is real workflow fit; the
obligation is precision about what is live and what is designed.

---

## Slide 9 — How we would know it worked

**Intro paragraph:**
Two baselines run alongside the pilot, so the comparison is measured rather than
argued: today's chronological queue, and a rules-only ordering that could be
built in a week.

**Table:**

| Gate | Threshold, fixed before the pilot |
|---|---|
| Serious-issue recall on the weekly labelled sample | ≥ 0.90 sustained over four weeks |
| Summary statements not supported by the source | ≤ 2% of sampled statements |
| Reviewer override rate | Between 10% and 25% — two-sided |
| Campus-scoping or permission violations | Exactly zero — absolute blocker |

**Closing statement:**
The override band is deliberately two-sided. Below 10% is not success — it is the
first symptom of reviewers rubber-stamping, which is the failure this design
fears most.

**Speaker notes:**
Ground truth is built three ways: implicit labels from every reviewer decision,
a stratified sample of thirty reports labelled independently each week, and
correction labels from overrides. The rubric is versioned alongside the prompt.

---

## Slide 10 — Economics: one campus, one month

**Opening statement:**
Inference and infrastructure per campus, plus amortised maintenance, must stay
materially below the loaded cost of the reviewer and associate hours removed —
at every campus count between five and forty.

**Two lists:**

**Why it should hold**
- A daily report is a small amount of text
- ~22 working days bounds call volume
- The hours displaced are managerial

**What could break it**
- Context size growing beyond seven days
- Extending to high-volume, low-value items
- Both controlled by pinned configuration

**Italic line:**
Rupee figures are computed from measured pilot volumes and current API pricing
rather than presented as an estimate. A fabricated cost table would be the
fastest way to lose the argument.

**Final line:**
Scaling risks: latency at the 16:00 burst · linear cost growth · per-campus
exception creep · governance overhead · single-builder dependency

**Speaker notes:**
The platform is internal, so the test is an internal value case — stricter than
an external product, because there is no revenue line to hide behind.
Key-person dependency on one builder is the most serious operational risk in
the submission.

---

## Slide 11 — The risk that actually worries us

**Opening statement:**
Automation complacency: reviewers stop reading the source reports, oversight
becomes ceremonial, and the platform has made the institution less informed
while appearing more informed.

**Image:** `A35-ops-copilot.png`
**Caption:** Risk R1, demonstrated rather than asserted: on this day the
generated summary reported a complete absence of activity, on a screen showing
355 of 369 sessions completed.

**Controls that follow from it:**
- AI cannot advance a state or send a message
- Every generated claim cites its source sentence
- Rules can raise severity, never lower it
- Auto-sign-off disabled on serious items
- Override reasons read by a human weekly
- Row-level security at the database, not the app
- Identifiers stripped before the API call

**Speaker notes:**
Launch blockers are absolute: any cross-campus exposure, ungrounded statements
above five per cent, recall below 0.90, no data-minimisation step, no one-flag
rollback, or any proposal to use this for staff assessment.

---

## Slide 12 — Recommendation

**Kicker:** RECOMMENDATION

**Headline:**
Pilot. Five campuses, one academic month, assist-only.

**Sub-paragraph:**
Scale the deterministic platform across all 40 campuses in parallel. Do not
extend AI into exam approval, student-facing communication or staff evaluation
until the gates are met.

**Two lists, side by side:**

**We expand when**
- Recall holds at 0.90 for four weeks
- Ungrounded statements stay under 2%
- Override rate sits inside 10–25%
- Reviewers say the queue changed their order

**We stop when**
- Any cross-campus data exposure, even once
- Ungrounded statements above 5%
- Override rate below 10% — rubber-stamping
- Anyone proposes using it to rate staff

**Closing line:**
A team that can say precisely what would make them stop is a team worth funding.

**Speaker notes:**
Close on the recommendation, not the demo. State the stopping conditions as
confidently as the reasons to proceed.

---

## Images used, in order

| Slide | File | What it shows |
|---|---|---|
| 3 | `A30-pm-review-queue.png` | Submissions awaiting decision, in arrival order |
| 8 | `A46-seating-plan.png` | Generated seat map, 67/67 filled, no violations |
| 8 | `A27-paper-editor-actions.png` | Set switching, Send for Approval, no repeated questions |
| 8 | `A64-budget-order-tracking.png` | Approval trail held at the admin threshold |
| 11 | `A35-ops-copilot.png` | The AI summary contradicting the figures beside it |

**Optional substitutes**, if a slide needs a different visual:
`A29-daily-report-form.png` (the BOA's submission form),
`A57-feature-management-admin.png` and `A58-feature-management-boa.png` (the role
matrix, 24 features versus 11), `A61-encrypted-pii.png` (encrypted fields with
logged reveal), `A52-fee-student-wise-sync-error.png` (a sync failure reported
rather than hidden).

---

## Three things the deck must land

1. **AI is the right lever here, and we know where it isn't.** Rules already
   catch the numbers; the remaining problem is language. Money and approvals
   stay deterministic.
2. **The prototype is real, and its limits are stated.** A live production
   system, with an honest list of what it does not yet prove.
3. **The recommendation is decisive in both directions.** Pilot, with the exact
   conditions for scaling and the exact conditions for stopping.
