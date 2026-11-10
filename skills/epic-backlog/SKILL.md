---
name: epic-backlog
description: Grill then draft docs/product/epics.md as user-valued epics traced to outcomes, with rough dependencies. Use after scope/NFR or when product-owner is on step 3 before prioritization.
---

# Epic backlog

Carve **epics**: user-valued capability chunks. Always grill first. No build order here — that is `prioritize-epics`.

## Artifact

Path: `docs/product/epics.md`

```markdown
Status: draft | approved
Approved by: <name or role>   # required when approved
Approved at: <ISO-8601 datetime with offset>
Content language: <agreed at start>
uncovered-outcomes-acknowledged: true | false
```

Optional tracker issue: offer at end; **create only after explicit yes**.

## What counts as an epic

- **Allowed:** capability a user/actor recognizes (create/assign ticket, close visit, see ETA…).
- **Forbidden as epics:** tech-only slices (REST API, Postgres, «интеграция с IdP» as a bare platform task).
- Preparatory work (access, SSO, …) must appear as **functional intent inside epics** (user-facing behaviour in the epic that needs it first) or as a **scope assumption / PO handoff** — not as a standalone tech epic.

## Traceability and coverage

- Read `docs/product/outcomes.md`, `docs/product/scope.md`, and `docs/product/nfr.md` when present (**read-only** — never edit them).
- Every epic **must** reference ≥1 Outcome ID (`O1`…). Several epics may cover one outcome.
- Count: **as many epics as needed to cover outcomes** (no artificial 3–9 cap). Use `## Later epics` for clearly deferred capabilities still worth parking.
- If an outcome has **no** epic: ask the user. On explicit acknowledgment (defer / accept gap), still complete the skill, set `uncovered-outcomes-acknowledged: true`, and list the gap under `Handoff / tensions for PO`. Without acknowledgment — not done.

## Dependencies

Record **rough** epic→epic dependencies here (`E3 blocked by E1`). Fine-grained sequencing and value ranking belong to `prioritize-epics`.

## Steps

### 1. Content language

Ask once. Headings stay English. Record `Content language`.

### 2. Always grill (epic contour only)

Call `grilling` (or `grill-me` / `grill-with-docs`). Cover: epic candidates, outcome links, rough blockers, rejection of tech-only epics.  
Fallback: embedded interview. Do not skip because a parent already interviewed.

Drift into prioritization scores, BRD, ADR → handoff notes only.

### 3. Contradictions with outcomes/scope

Ask the user. They may confirm a deliberate deviation. Write epics as decided; notify PO via `Handoff / tensions for PO`. Never silent-edit upstream files.

### 4. Write `docs/product/epics.md`

Stable IDs `E1…En`. Status starts `draft`.

### 5. Gate

Skill done = file written + every epic traced + coverage rule satisfied (or acknowledged).  
Approve: user explicitly approves + names who; agent sets `approved` / `Approved at`. No `unknown` who.

## Template

```markdown
# Epics

Status: draft
Approved by:
Approved at:
Content language: ...
uncovered-outcomes-acknowledged: false

## Backlog
| ID | Epic | User value | Outcomes | Blocked by | Notes |
|----|------|------------|----------|------------|-------|
| E1 | ... | ... | O1 | — | ... |

## Later epics
| ID | Epic | User value | Outcomes | Notes |
|----|------|------------|----------|-------|
| ... | ... | ... | ... | ... |

## Handoff / tensions for PO
- ...
```

## Out of scope for this skill

Scoring, build order, BRD, tickets, architecture. Do not call `prioritize-epics` from here unless the user explicitly asks to continue.
