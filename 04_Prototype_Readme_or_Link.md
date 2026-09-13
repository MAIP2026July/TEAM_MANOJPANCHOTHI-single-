# Prototype — access, scope and what it demonstrates

**Project:** UniConnect Operations OS — an AI-assisted academic operations platform
**Submission:** MBA ZG583, Management of AI Products — capstone
**Submitted by:** Manoj Kumar Panchothi

---

## Links

| Item | Location |
|---|---|
| Live application | https://uniconnect-app.up.railway.app |
| Repository | https://github.com/programopscentral-art/Uniconnect-mail-automation- |
| Screens and captions | Appendix — Prototype Evidence (66 captioned figures, separate document) |

## Access

Sign-in is Google OAuth against the institution's Workspace, and every page is
scoped by role and by university, so an anonymous visitor cannot see
operational data. An evaluator account limited to a demonstration university is
provisioned on request.

The application carries live institutional data for a working campus network,
which is why open credentials are not published here. The appendix document
covers the same ground without requiring access: every screen referenced in the
report appears there with a caption and a pointer to the section it supports.

## What this prototype is

Not a mock-up and not a staged demonstration. It is the production system the
campus network uses to run its operational day, built and owned by the
submitter. The report is written about a system already in use, which is
unusual for a capstone and carries an obligation to be precise about what is
live and what is designed.

## Technology

| Layer | Implementation |
|---|---|
| Application | SvelteKit, TypeScript, deployed on Railway |
| Data | Supabase PostgreSQL, row-level security enforcing university and role scoping |
| Background processing | Node worker with scheduled loops and BullMQ job queues |
| Cache and queues | Redis |
| AI services | Google Gemini for summarisation and narrative reporting; Google Vision for OCR |
| Integrations | Google OAuth, Gmail, Calendar, Sheets and Drive; push notifications |

## What it demonstrates

- The full daily decision loop: submission, deadline, AI-assisted triage, human review, sign-off or escalation, and an immutable audit record.
- Confidence-based routing, where a low-confidence item behaves differently rather than merely displaying a different label.
- A visible separation between deterministic facts and generated text.
- The override path with reason capture, and the weekly evaluation view built from those overrides.
- Examination operations: paper generation with four equivalent sets, seating allocation under an interleaving constraint, and invigilation assignment.
- A budget approval path that contains no AI at all, by design.
- Safe degradation: with AI switched off, the product is still the platform the network already runs on.

## What it does not yet prove

- Sustained severity accuracy. Four weeks of labelled samples supports a go/no-go decision, not a claim about the year.
- That reviewers keep reading. Automation complacency develops over months and one month of pilot cannot rule it out.
- That the inference cost ceiling holds at 40 campuses, since the pilot measures five.
- Absence of bias across campuses and writing styles. The measurement that would detect it exists; the result does not yet.
- Supportability. One builder is not an operating model.

## Running it locally

```bash
pnpm install
cp .env.example .env          # then fill in the values below
pnpm --filter shared migrate

# terminal 1 — application
pnpm --filter app dev

# terminal 2 — background worker
pnpm --filter worker start
```

Required environment values: `DATABASE_URL` (Supabase Postgres), `REDIS_URL`,
`GOOGLE_CLIENT_ID` and `GOOGLE_CLIENT_SECRET`, `ADMIN_EMAIL`, and
`ENCRYPTION_KEY_BASE64` (a 32-byte key). No credentials are committed to the
repository.
