---
name: adr-lite
description: Grill (tech/architecture focus) then write a pool of lightweight ADRs under docs/adr/ADR-NNNN-title.md. Batch-approve the whole pool. Use for epic-level forks or when product-owner is on step 7; prefer domain-modeling when glossary terms are also shifting.
---

# ADR lite

Record **architecture/technology decisions** as a pool of ADRs. Always grill first with a **technical / architecture** emphasis. One solvable problem → one ADR file. Do not mark the pool accepted until the human batch-approves **all** of it.

## Artifacts

Path pattern: `docs/adr/ADR-NNNN-title.md`  
`NNNN` is zero-padded next free number in `docs/adr/` (scan existing `ADR-*.md`).

Optional tracker issues: offer; create only after explicit yes.

## Relationship to `arch-options`

- Concept-level ADRs from `arch-options` stay as-is.
- If this skill changes/replaces an earlier decision: put a **Supersedes / Refines** link **in the new ADR** naming the old file and whether it is changed or replaced.
- **Do not** edit the old ADR's `Status`.

## Grill → pool → batch approve

1. **Always grill** (`grilling` / `grill-me` / `grill-with-docs`; fallback embedded interview). Contour: technical alternatives, risks, rollback, links to epic work. Skip-not-allowed because a parent already interviewed.
2. From the grill, identify 1..N distinct problems. Each problem → its own ADR file, all written as `Status: proposed` in one run.
3. Present the pool summary. Ask for **approve all** + who.
4. **No partial accept.** If the user rejects or wants changes on any item — revise (re-grill that branch if needed), rewrite affected ADRs, ask again until **every** ADR in the pool is approved together.
5. On batch approve: set each pool ADR to `Status: accepted`, `Approved by`, `Approved at` (who required; never `unknown`).

## Required / optional header fields

| Field | Rule |
|-------|------|
| Epic | **Required** |
| Stories **or** Use cases | **Required** (≥1 id/name) |
| NFR / BR | **Optional** for pure traceability. **Required** when that NFR/BR **justifies** the decision — cite them in Context/Decision, not only as optional tags |
| Supersedes / Refines | When replacing/changing an older ADR |

Concrete technology product names **are allowed** here (unlike concept-only `arch-options`).

## Content language

Ask once if not already fixed for the epic session. Section headings stay English.

## Template — `docs/adr/ADR-NNNN-title.md`

```markdown
# ADR-NNNN — <title>

Date: <ISO-8601 date>
Status: proposed | accepted
Approved by:
Approved at:
Content language: ...
Epic: E?
Stories / use cases: ...
NFR: ...          # if used as justification — required in body too
BR: ...           # if used as justification — required in body too
Supersedes / Refines: docs/adr/ADR-....md (changed | replaced) | none

## Context
## Decision
## Alternatives considered
## Consequences
## Rollback
## Handoff / tensions for PO
```

## Done when

- Grill completed (tech/architecture contour).
- Every problem in scope has its `ADR-NNNN-*.md`.
- Headers satisfy Epic + stories/use cases; justification NFRs/BRs cited when they drive the call.
- Whole pool `accepted` after batch approve + who — or still `proposed` only if the user paused before approve (then Waiting on human; not “half-accepted”).

## Out of scope for this skill

Editing outcomes/scope/nfr/BRD; changing Status on older ADRs; glossary redesign (use `domain-modeling` when terms shift).
