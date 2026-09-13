# AI Collaboration Log

**MBA ZG583 — Management of AI Products, capstone**
UniConnect Operations OS · Manoj Kumar Panchothi

This log discloses how AI tools were used to produce this submission and the
product artifacts behind it. It is written to be honest rather than flattering,
because a collaboration log that reports no failures is not a log.

## Tools used

| Tool | Used for |
|---|---|
| Claude | Structuring the report, drafting and rewriting PM artifacts, generating edge cases, stress-testing the risk register and metric design, reviewing prototype code |
| Google Gemini | Inside the product itself — daily and weekly narrative summaries, meeting summarisation, document analysis |
| AI coding assistance | Scaffolding components, migrations and repetitive interface code during platform development |
| Google Vision | Inside the product — OCR for document intake |

## Where AI helped

- **Discovery** — turning scattered field notes from campus visits into a structured problem list, which made repeated patterns visible faster than re-reading the notes would have.
- **Drafting** — first versions of PRD sections and the report structure, which removed the blank-page cost and let effort go into judgement.
- **Edge cases** — generating long candidate lists of failure scenarios across scheduling, seating, invigilation and paper generation. This was the single highest-value use: the model reliably proposes cases a tired human forgets.
- **Coding** — scaffolding repetitive parts of a large application quickly.
- **Metrics** — proposing alternative metric formulations, including the two-sided override band, which came out of pushing back on a first draft that had only a lower bound.
- **Risk review** — challenging the risk register and surfacing the function-creep scenario that became R7.

## Example prompts and workflows

**1.** *"Given this daily operations workflow and this database schema, list every way an AI triage layer could fail in a way the reviewer would not notice."*
A long list, roughly two-thirds useful. It produced the automation-complacency framing that became R2 and reshaped the override metric. Generic entries about "model bias" were discarded as unactionable.

**2.** *"Argue against building this feature. Assume a competent manager who thinks a rules engine would be enough."*
The strongest single prompt used. It forced the rules-only baseline into the evaluation design, which is now a running comparison in the pilot rather than a rhetorical claim.

**3.** *"Draft severity classification rubric options for operational campus reports, with worked examples per level."*
Three rubric drafts. All were too abstract initially; usable only after real report examples were supplied, and then rewritten by hand.

**4.** *"Review this PRD section and identify claims that are asserted without evidence."*
Accurately caught several unsupported efficiency claims, which were either removed or moved into the assumptions section.

**5.** *"Propose an exam timetable generation approach for cohorts with shared subjects across sections."*
Suggested graph-colouring with a conflict graph, a genuinely useful starting point, but the initial version ignored the requirement to maximise the gap between a student's consecutive exams — added by hand afterwards.

## Where AI was weak or wrong

- **A live grounding failure in the product itself.** On the day the appendix screens were captured, the shipped narrative summary stated that there was a complete absence of operational activity and zero values across all indicators, on the same screen that reported 355 of 369 sessions completed and 30.6 per cent attendance. This is the clearest evidence in the submission for risk R1, and the reason the layer is assist-only.
- **Generic personas and workflows.** Every unprompted persona was a stock "operations manager" with no resemblance to how a Business Operations Associate actually spends an afternoon. Only field notes fixed this.
- **Unrealistic automation ambition.** Default suggestions consistently pushed towards full automation and end-to-end agents, with no weight given to the cost of a wrong decision in an academic setting.
- **Invented numbers.** When asked for efficiency estimates, plausible-looking percentages were produced with no basis. These were deleted; unmeasured figures in the report are labelled as assumptions rather than replaced with confident-sounding ones.
- **Weak prioritisation.** Ranking suggestions were sensitive to the order in which features were listed and did not weigh the cost of error until that dimension was explicitly added.
- **Shallow governance framing.** Risk sections came back as compliance boilerplate. The specific harm scenarios in the risk note came from knowing the people who write these reports, not from a model.
- **Over-confident architecture.** Suggested designs occasionally ignored constraints already stated, such as the requirement that permission scoping be enforced at the database layer rather than in application code.

## Human corrections applied

| AI proposal | Correction | Reasoning |
|---|---|---|
| Fully automated report approval for high-confidence items | Assist-only; no automatic state advancement of any kind | The error cost is concentrated on a named campus, and the oversight step is the entire safety argument |
| Predictive student dropout scoring in the MVP | Deferred out of the MVP entirely | Training data reflects recording habits more than student behaviour, and a wrong prediction attaches to a real student |
| Override rate with a lower bound only | Two-sided band, 10% to 25% | A very low override rate warns of rubber-stamping, not success |
| Broad multi-module AI rollout | One wedge, five campuses, one month | Only a narrow scope produces an evaluation anyone should believe |
| Estimated efficiency gains stated as facts | Rewritten as pilot targets and assumptions | Fabricated evidence would invalidate the entire argument |
| Model-generated numeric analysis | All numbers stay deterministic; the model never computes | Arithmetic must be exactly correct and is trivially handled in code |

## Final reflection

AI accelerated the parts of product management that are production work:
structuring documents, drafting, enumerating edge cases, generating alternatives
and scaffolding code. On edge-case generation in particular it was better than
working alone, and the exam-operations design is more complete because of it.

It could not do the parts that are actually the job. It did not know which
problem was worth solving, because that came from standing in campuses and
watching people work. It did not know what error cost the institution could
tolerate. It could not decide that automated staff scoring should be rejected
outright rather than deferred, and when asked, it produced a balanced discussion
instead of a decision. It could not tell the difference between a number that
was measured and a number that sounded right — which is, in the end, the
difference between a product recommendation and a pitch.

**The practical lesson:** the most useful pattern was adversarial rather than
generative — asking the model to argue against the product, to find unsupported
claims, and to list ways the system could fail invisibly. Used that way it is a
demanding reviewer. Used as an author, it produces confident, generic,
unfalsifiable work.
