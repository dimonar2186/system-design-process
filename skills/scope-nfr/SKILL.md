---
name: scope-nfr
description: Grill then draft docs/product/scope.md and docs/product/nfr.md. Use for system boundaries and non-functional requirements, or when product-owner is on step 2.
---

# Scope + NFR

One skill, **two artifacts**. Always grill first (this contour only). Never edit `docs/product/outcomes.md`. Do not write epics, BRD, or architecture.

## Artifacts

| File | Owns |
|------|------|
| `docs/product/scope.md` | Stakeholders, in/out scope, assumptions |
| `docs/product/nfr.md` | Must / nice-to-have NFR |

Each file has its own approval metadata:

```markdown
Status: draft | approved
Approved by: <name or role>   # required when approved
Approved at: <ISO-8601 datetime with offset>
Content language: <agreed at start>
```

`nfr.md` additionally:

```markdown
to-be-determined: true | false   # true if any NFR measure/constraint is TBD
```

Optional tracker issues: **offer at end, create only after explicit yes** (one issue per file, or one combined — ask the user).

## Hard limits

| Rule | Limit |
|------|--------|
| In scope | ≤ 10 primary bullets. Overflow → `## Later scope`. |
| Out of scope | Section always present; `None yet` allowed. |
| Must-have NFR | ≤ 3. |
| Nice-to-have NFR | Unbounded but keep short; label as nice-to-have («хорошо бы»). |

## NFR quality bar

- **No abstract NFR.** Reject «must be fast / secure / convenient» without a defined axis (what is measured or constrained).
- The **value** of a measure may be set later: write a concrete NFR row with `Measure / constraint: TBD` and set file flag `to-be-determined: true`.
- Propose 2–3 candidate measures when TBD; user is not required to pick one for skill completion.
- Approve of `nfr.md` is allowed while `to-be-determined: true`; warn PO not to treat TBD measures as locked SLOs.

## Outcomes awareness (read-only)

1. Read `docs/product/outcomes.md` if it exists.
2. Grill **with that knowledge** (align questions to motto/problems/outcomes).
3. **Never modify** outcomes.
4. On contradiction with outcomes: **ask the user**. They may confirm a deliberate deviation. If they confirm, write scope/NFR as decided and record the conflict under `Handoff / tensions for PO` in **both** files (or the file where it shows up) so the Product Owner can resolve at controller level.

## Steps

### 1. Content language

Ask once for body language. Section headings stay English. Record in both files' `Content language`.

### 2. Always grill (scope + NFR contour)

Call `grilling` (or `grill-me` / `grill-with-docs`). Cover stakeholders, in/out, assumptions, must/nice NFR.  
Fallback: embedded interview on the same contour if grilling is unavailable. Do not skip because a parent already interviewed.

Drift into epics/BRD/architecture → `Handoff / tensions for PO` only.

### 3. Write both files

Create/overwrite both templates below. Status starts as `draft`. Skill **done** when both files exist and limits/quality bars hold — even if neither is approved yet.

### 4. Gates (independent, any order)

- User may approve **scope** and **nfr** separately, in any order.
- Agent sets `Status: approved` on a file only when the user explicitly approves **that** file and names `Approved by`; if who is missing — ask. Set `Approved at` to now.

### 5. Optional tracker

Offer issues after drafts exist; create only on explicit yes.

## Template — `docs/product/scope.md`

```markdown
# Scope

Status: draft
Approved by:
Approved at:
Content language: ...

## Stakeholders
| Role | Interest | Decision power |
|------|----------|----------------|
| ... | ... | ... |

## In scope
- ...

## Later scope
- ...

## Out of scope
- None yet

## Assumptions
- None yet

## Handoff / tensions for PO
- ...
```

## Template — `docs/product/nfr.md`

```markdown
# NFR

Status: draft
Approved by:
Approved at:
Content language: ...
to-be-determined: true|false

## Must-have
| ID | NFR | Class | Measure / constraint | Proxies (if TBD) |
|----|-----|-------|----------------------|------------------|
| N1 | ... | performance\|security\|audit\|... | ... or TBD | ... |

## Nice-to-have
| ID | NFR | Class | Measure / constraint | Proxies (if TBD) |
|----|-----|-------|----------------------|------------------|
| N4 | ... | ... | ... | ... |

## Handoff / tensions for PO
- ...
```

## Out of scope for this skill

Editing outcomes, epics, prioritization, BRD, ADR, solution design.
