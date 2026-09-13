# UniConnect Operations OS

**An operations platform for a multi-campus higher-education network.**
One database, one permission model, one audit trail — replacing the
spreadsheets, email threads and side files that campus operations used to run
on.

🔗 **Live:** https://uniconnect-app.up.railway.app

`SvelteKit` · `TypeScript` · `Supabase / PostgreSQL` · `Redis + BullMQ` ·
`Google Workspace` · `Gemini` · `Railway`

> **On the repository name:** this began as a mail-automation tool and grew into
> the operations platform described below. The name hasn't caught up.

---

## What it does

### Daily operations

- **Daily report spine** — one report per campus by a 16:00 cut-off, sign-off by
  18:30, on a strict state machine: draft → submitted → in review → signed off,
  with send-back, reminders, auto-sign-off and immutability once locked.
- **Task centre** — assignable tasks with multiple assignees, checklists and a
  view log, so it's clear who saw what and when.
- **Operations dashboard** — sessions, attendance, instructors and at-risk views
  across the network, with daily, weekly and monthly reporting.

### Academic operations

- **Examinations** — question bank, per-university paper templates, and
  generation of multiple distinct-but-equivalent paper sets.
- **Exam plans** — classroom seating allocation under an interleaving
  constraint, invigilation assignment with a conflict-of-interest ladder, and
  marks entry.
- **Faculty and success coaches** — profiles and subject mappings that drive
  scheduling eligibility, daily attendance, and coach call targets.

### Money

- **Budget proposals** — a multi-stage approval workflow with a two-level path,
  a value threshold requiring administrative approval, post-event reporting, and
  a webhook into the facilities system on final approval.
- **Petty cash** — the same approval spine, tracking requests, disbursement and
  bill settlement.
- **Fee collection** — semester-window tracking synchronised from institutional
  sheets, twice-daily snapshots, per-batch and per-coach rollups, dropout
  tracking.

### Communication

- **Campaigns and mailboxes** — per-university mailboxes, mail-merge templates,
  bulk send with per-recipient open and acknowledgement tracking, and a full
  mail audit log.
- **Meeting intelligence** — discovers scheduled meetings, pulls the transcript,
  and produces a summary, action items and attendance.

---

## AI in the platform

Two different kinds, with different failure modes — and one place it's kept out
on purpose.

| | Where | What it does |
|---|---|---|
| **Language AI** | Narrative reports, meeting summaries, document analysis | Reads, ranks and drafts. Assist-only: it never advances a state, sends a message, or writes to an operational table. |
| **Optimisation AI** | Examination classroom allocation | Constraint satisfaction with a repair pass, not a language model. A plan that can't satisfy the interleaving invariant is flagged, never silently emitted. |
| **No AI, by design** | Fees, permissions, approvals, thresholds, audit | Deterministic code. These have to be exactly correct and defensible to an auditor. |

---

## Architecture

| Layer | Implementation |
|---|---|
| Application | SvelteKit · TypeScript · Tailwind, on Railway |
| Data | Supabase PostgreSQL, event-sourced, row-level security |
| Worker | Node/TypeScript — scheduled loops and BullMQ queues |
| Cache and queues | Redis |
| AI services | Google Gemini · Google Vision (OCR) |
| Integrations | Google OAuth, Gmail, Calendar, Sheets, Drive; push notifications |

**The core model:** the university is the scoping key on nearly every table, and
a role-to-permission matrix gates every page and endpoint. Adding a university
makes it a filter everywhere; changing a role changes what exists for that user.

---

## Repository layout

```
apps/                  application and worker
packages/shared        shared types, database access, migrations
extensions/            meet-tracker browser extension
scripts/               operational and migration scripts
docs/                  design and product documentation
PRD.md                 product requirements
OPS_OS_FEATURES.md     feature inventory
```

---

## Getting started

```bash
pnpm install
cp .env.example .env
pnpm --filter shared migrate
```

Then, in two terminals:

```bash
pnpm --filter app dev        # application
pnpm --filter worker start   # background worker
```

**Environment values required:**

| Variable | Purpose |
|---|---|
| `DATABASE_URL` | Supabase Postgres connection |
| `REDIS_URL` | Queues and cache |
| `GOOGLE_CLIENT_ID` / `GOOGLE_CLIENT_SECRET` | OAuth, Gmail, Calendar, Sheets |
| `ADMIN_EMAIL` | Bootstrap admin account |
| `ENCRYPTION_KEY_BASE64` | 32-byte key for field encryption |

No credentials are committed to this repository.

**Deployment**

```bash
pnpm --filter app build && node build/index.js
```

---

## Roles

| Role | Access |
|---|---|
| Super Admin / Admin | Full access; university and user management |
| Programme Manager / Chief of Staff | Review, sign-off and escalation |
| Business Operations Associate | The daily operator, scoped to one campus |
| Programme Management Associate | Shares the daily operational load |
| University Operator | Restricted to an assigned university |

---

## Security and privacy

- **Scoping at the database.** Row-level security filters every query by
  university and role, rather than relying on application code.
- **Encrypted student fields.** Sensitive identifiers are stored with
  AES-256-GCM, masked by default, and every reveal is logged.
- **A second factor for sensitive records.** A per-user PIN gates access, with
  verification cached for five minutes only.
- **An immutable audit log.** Approvals, state transitions and reveals are all
  recorded and cannot be edited after the fact.
