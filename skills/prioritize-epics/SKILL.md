---
name: prioritize-epics
description: Grill then write Build order into docs/product/epics.md (value/risk/dependency sequencing). May reformulate epics when order requires it. Use after epic-backlog or when product-owner needs an approved epic sequence.
---

# Prioritize epics

Produce an ordered **build sequence** in the same `docs/product/epics.md`. Always grill first. This is value/risk/dependency judgment — not a wayfinder decision map and not ticket blocking.

## Artifact

Path: `docs/product/epics.md` (same file as `epic-backlog`).

Shared file metadata (one Status for the whole file):

```markdown
Status: draft | approved
Approved by: ...
Approved at: ...
Content language: ...
uncovered-outcomes-acknowledged: ...
```

Add or replace:

```markdown
## Build order
1. E? — <one-line reason>
2. E? — <one-line reason>
...

## Deferred
- E? — why later / out of first release
```

No mandatory score table — **ordered list + reason** only. Optional scoring notes may appear in the grill transcript or under Handoff, not required in the file.

Optional tracker update: offer; create/update only after explicit yes.

## Inputs (read; may update epic rows)

- Require an existing epic backlog table in `docs/product/epics.md`. If missing, stop and tell the user to run `epic-backlog` first.
- Read outcomes / scope / nfr when present (read-only for those files).
- **May edit** backlog rows in `epics.md` (titles, user value, outcomes links, `Blocked by`, splits/merges) when reordering needs reformulation — git history is the audit trail.
- Do not edit `outcomes.md`, `scope.md`, or `nfr.md`.

## Dependency rule

Rough `Blocked by` from the backlog is the default constraint.  
You **may** propose an order that breaks it **only after** grilling the user into clearer epic formulations (e.g. move capabilities between epics so the new order is coherent). Update backlog rows + `Blocked by` to match. Record the change under `Handoff / tensions for PO` if anything remains contested.

## Status reset

If this skill changes epic **composition or wording** (not merely appending Build order under an unchanged backlog), set `Status: draft`, clear `Approved by` / `Approved at`, and require a fresh approve gate — even if the file was previously approved.

If only Build order / Deferred are added and backlog rows are untouched, still leave or set `Status: draft` until the user approves the order (shared Status covers order too).

## Steps

### 1. Content language

If `Content language` already set in the file, keep it unless the user asks to change. Else ask once (headings English).

### 2. Always grill (priority contour)

Call `grilling` (or `grill-me` / `grill-with-docs`). Cover: what must ship first for outcomes, risks to burn early, dependency honesty, deferred items, any epic splits needed for a sane order.  
Fallback: embedded interview. Do not skip because a parent already interviewed.

### 3. Write Build order (+ edit backlog if needed)

- Total order for non-deferred epics.
- Each line: epic ID + one-line reason (value, risk, leverage, or dependency).
- Update `docs/agents/process-state.md` epic backlog checkboxes **when called from `product-owner`** (ordered list). If called alone, offer to sync process-state; do it only if the user says yes or process-state is clearly in use.

### 4. Gate

Skill done = Build order present for every non-deferred epic + reasons + backlog consistent with dependencies after any reformulation.  
Approve: explicit user approve + named who → `Status: approved`.

## Out of scope for this skill

BRD, tickets, architecture, wayfinder maps, inventing new outcomes.
