# Ethics, governance and risk note

Extracted from Section 7 of the final report.

## Risk register

| # | Risk | Severity |
|---|---|---|
| R1 | Hallucinated or unsupported statements in a summary lead a reviewer to act on something never reported | High |
| R2 | Automation complacency — reviewers stop reading the original reports and oversight becomes ceremonial | High |
| R3 | A serious issue is ranked low, signed off routinely, and surfaces days later as an escalation | High |
| R4 | Campus or role scoping failure exposes one campus's operational data to another | Critical |
| R5 | Personal data of students or staff is sent to a third-party model API without a clear basis | High |
| R6 | Systematic bias against particular campuses, associates or writing styles | High |
| R7 | Function creep — the layer is quietly repurposed for staff performance evaluation | High |
| R8 | Over-claiming in internal communication creates expectations the system cannot meet | Medium |
| R9 | Key-person dependency on a single builder and owner | High |

## Harm scenarios

- A Business Operations Associate honestly reports a genuine problem in plain, non-fluent English. The model rates it low because it lacks urgent phrasing. The problem persists for a week, students are affected, and the associate learns that reporting honestly achieved nothing.
- A summary states that a fee issue was "resolved" when the report said it was "being resolved". The reviewer signs off, and a student is blocked from class the next day.
- Operational text including a named student's personal circumstances is sent to an external API without a considered basis, and the institution has no answer when asked where that data went.
- A manager begins using severity distributions as an informal ranking of associates. Associates learn to write reports that score well rather than reports that are true.

## Controls

| Control | Addresses | Status |
|---|---|---|
| No autonomy — AI cannot advance any state or send any message | R1, R2, R3 | Enforced by the existing state machine |
| Mandatory source citation for every generated claim, shown in the interface | R1 | Designed for the pilot |
| Rules can raise severity but never lower it | R3 | Designed for the pilot |
| Auto-sign-off disabled for any item marked serious | R2, R3 | Configuration change to existing behaviour |
| Two-sided override band monitored weekly, reasons read by a human | R2 | Part of the evaluation harness |
| Row-level security enforcing campus scoping at the database, not only in application code | R4 | Live in production |
| Data minimisation — identifiers redacted before the API call wherever the task does not need them | R5 | Designed; a launch prerequisite |
| Bias audit on the weekly sample, comparing severity across campuses and authors | R6 | Part of the evaluation harness |
| Written policy that AI outputs are never used in staff performance assessment | R7 | Governance commitment, signed off before the pilot |
| Immutable audit log capturing model output, prompt version and human decision together | R1–R7 | Live in production |
| Documentation, runbook and a second engineer before Phase 2 | R9 | Open — a gate on expansion |

## Privacy position

Operational text can incidentally contain personal information. The position is
data minimisation before capability: identifiers are stripped from text sent to
the model wherever the task does not require them, because severity
classification almost never depends on knowing which named student was
involved. Where an identifier is genuinely needed, the reference stays inside
the platform and the model receives a placeholder. Retention follows the
platform's existing policy, and the audit log records what was sent for every
call. Alignment with the institution's obligations, including India's Digital
Personal Data Protection Act, is treated as a prerequisite for the pilot.

## Launch blockers

Any one of these stops the launch. They are absolutes: a blocker that can be
negotiated under delivery pressure is not a blocker.

- Any cross-campus or cross-role data exposure, even once, even in a test.
- Ungrounded statements above five per cent of sampled summary statements.
- P1 severity recall below 0.90 on the labelled weekly sample.
- No data-minimisation step in place before text is sent to the model API.
- Absence of a working single-flag rollback to rules-only ordering.
- Any proposal to use the layer for staff performance evaluation.
