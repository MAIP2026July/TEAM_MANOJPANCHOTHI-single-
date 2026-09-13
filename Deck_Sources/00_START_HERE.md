# Sources for building the presentation deck

Twelve slides. The deck is a product review for a leadership group deciding
whether to fund a pilot — not a classroom presentation.

## Use these as sources, in this order of authority

**1. `03_Deck_Content_Spec.md` — the primary source.**
Final copy for all twelve slides: headlines, every bullet, the table contents,
the callout statements, the speaker notes, and which image belongs on which
slide. Do not shorten or rewrite this copy. Build the slides from it directly.

**2. `02_Final_Report.pdf` — the full argument behind the deck.**
42 pages. Use it for background and to resolve any question the spec leaves
open. It is not slide copy; the deck should not grow beyond twelve slides.

**3. `01_Executive_Summary.pdf` — the two-page version of the argument.**
Useful if a slide needs tightening: this is the same case at its shortest.

**4. `Appendix_Prototype_Evidence_All66.pdf` — the screen evidence.**
Captions for all 66 screens from the live system, each mapped to the report
section it supports. Reference only; the five screens the deck needs are
supplied separately as image files.

**5. `04_Prototype_Readme.md` and `05_AI_Collaboration_Log.pdf` — supporting context.**
What the prototype is and is not, and how AI tools were used to produce the
submission. Background only.

## Images — insert these manually

`deck-images/` holds the five screenshots the deck uses, at full resolution:

| Slide | File | Caption to place beneath it |
|---|---|---|
| 3 | `A30-pm-review-queue.png` | The review surface today: submissions awaiting a decision, in arrival order, with no ranking applied. |
| 8 | `A46-seating-plan.png` | Seating allocation: 67 of 67 seats filled, interleaving constraint satisfied, every classroom reporting no violations. An invalid plan is flagged, never silently emitted. |
| 8 | `A27-paper-editor-actions.png` | Paper generation ends at Send for Approval — a person approves, and any question can be swapped. |
| 8 | `A64-budget-order-tracking.png` | The budget path: no AI anywhere in it, threshold rule printed on the screen. |
| 11 | `A35-ops-copilot.png` | Risk R1, demonstrated rather than asserted: on this day the generated summary reported a complete absence of activity, on a screen showing 355 of 369 sessions completed. |

## Copy that must survive intact

These three carry the marks. If something has to be cut, cut elsewhere.

- Slide 4 — "Where AI is deliberately absent: fee arithmetic, permission
  enforcement, approval states and audit records stay deterministic."
- Slide 9 — the override band is two-sided; below 10% is a warning sign, not a
  success.
- Slide 12 — the "We stop when" list, stated as confidently as "We expand when".

## Two things to avoid

- Ending on the prototype. The deck closes on the recommendation.
- Dropping the speaker notes. They carry the argument the slides only anchor.
