---
name: to-brd
description: Grill then draft docs/product/BRD.md — business requirements per epic with stable BR IDs. Default high-level; detailed only on request. May propose NFR candidates without editing nfr.md. No architecture.
---

# To BRD

Synthesize a **system** Business Requirements Document. Always grill first. Depth defaults to **high-level**; go **detailed** only when the user explicitly asks. Do not choose architecture, modules, schemas, or stacks.

## Artifact

Path: `docs/product/BRD.md` (single file; epics as sections).

```markdown
Status: draft | approved
Approved by: <name or role>
Approved at: <ISO-8601 datetime with offset>
Content language: ...
Depth: high-level | detailed
has-tbd-sections: true | false
```

Optional tracker issue: offer; **create only after explicit yes**.

## Prerequisites

- **Required:** `docs/product/epics.md` with a backlog. If missing — stop; tell user to run `epic-backlog` (and ideally `prioritize-epics`).
- **Read-only when present:** `outcomes.md`, `scope.md`, `nfr.md`. Never edit them from this skill.
- Epic list for sections: prefer **Build order** (then Deferred as TBD stubs if needed); else all backlog epics.

## Traceability

- Stable requirement IDs: `BR-E<epic-number>-<nn>` (e.g. `BR-E1-01`).
- Each BR traces to **its epic** (`Epic: E1`). Tracing further to outcomes is **not** required here (outcomes↔epics already live in `epics.md`).
- Every epic in scope for this BRD **must** have a section. Section body may be `TBD` if the user cannot detail it yet → set `has-tbd-sections: true` and list under Handoff for PO. Ask before leaving TBD; on explicit acknowledgment, skill may complete.

## NFR relationship

- BRD is **not** an NFR document and must not rewrite `nfr.md`.
- A BR **may spawn** NFR candidates (e.g. “action must complete within N seconds”). Put them only in `## Proposed NFR` inside the BRD + `Handoff / tensions for PO` so the Product Owner / `scope-nfr` can absorb them later.
- Do not invent architecture to satisfy those constraints.

## Depth

- Default: `Depth: high-level` — capabilities, top scenarios, key business rules, open questions.
- `detailed` only on explicit user request — richer scenarios, edge cases, rule tables; still no architecture.

## Steps

### 1. Content language + depth

Ask content language (headings English). Confirm depth: default high-level unless user asked for detailed.

### 2. Always grill (BR contour)

Call `grilling` (or `grill-me` / `grill-with-docs`). Cover: per-epic business needs, rules, actors, failures worth stating, TBD sections, NFR-spawning constraints.  
Fallback: embedded interview. Do not skip because a parent already interviewed.  
Architecture talk → deflect to Handoff, do not write design decisions.

### 3. Contradictions with outcomes/scope/epics

Ask the user. On confirmed deviation — write BRD as decided + PO handoff. Never silent-edit upstream files.

### 4. Write `docs/product/BRD.md`

Status starts `draft`. Include Proposed NFR if any.

### 5. Gate

Skill done = file exists, every required epic has a section (content or acknowledged TBD), BR IDs stable, no architecture section.  
If `has-tbd-sections: true`, warn PO that freeze is soft.  
Approve: explicit approve + named who.

## Template

```markdown
# BRD — <system name>

Status: draft
Approved by:
Approved at:
Content language: ...
Depth: high-level
has-tbd-sections: false

## Context
### Motto (from outcomes, quoted)
### Problems (summary)
### Scope pointers
- In/out: see docs/product/scope.md

## Stakeholders and users
(short; detail lives in scope.md)

## Requirements by epic

### E1 — <epic title>
Status: drafted | TBD

| ID | Statement | Epic | Business rule / scenario notes |
|----|-----------|------|--------------------------------|
| BR-E1-01 | ... | E1 | ... |

#### Top scenarios
- Happy: ...
- Key failure: ...

### E2 — ...
...

## Proposed NFR
| Source BR | Candidate NFR | Suggested measure | Notes |
|-----------|---------------|-------------------|-------|
| BR-E1-03 | ... | ... | for PO / scope-nfr |

## Open questions
- ...

## Handoff / tensions for PO
- ...
```

## Out of scope for this skill

Editing nfr/outcomes/scope/epics (except reading), ADR, architecture options, `to-spec`, implementation.
