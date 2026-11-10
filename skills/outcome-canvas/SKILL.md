---
name: outcome-canvas
description: Grill then draft docs/product/outcomes.md — motto, problems, desired outcomes, non-goals. Use when starting a new system, clarifying product goals, or when product-owner is on step 1.
---

# Outcome canvas

Own **only** the outcomes contour. Always grill first. Do not write scope, epics, BRD, or architecture. Tensions that belong elsewhere go under `Handoff / tensions for PO`.

## Artifact

Path: `docs/product/outcomes.md`

Mandatory metadata in the file:

```markdown
Status: draft | approved
Approved by: <name or role>   # required when Status is approved
Approved at: <ISO-8601 datetime with offset>
weak-metrics: true | false
Content language: <code or label agreed at start>
```

Optional: an issue in the configured tracker — **offer at the end, create only after an explicit yes**.

## Hard limits

| Section | Rule |
|---------|------|
| Motto | ≤ 2 sentences. No tech stack names. |
| Problems | ≤ 5 primary. Overflow → `## Later problems`. |
| Desired outcomes | ≤ 5 rows. |
| Non-goals | Section always present; `None yet` allowed. |

Problem line shape: `<problem> — who hurts — current workaround`.

## Steps

### 1. Content language

Ask once: write body text in the **user's language**, or another they name?  
Section **headings stay English** (template below) for agent traceability.  
Record the choice in `Content language`.

### 2. Always grill (outcomes contour only)

Call the Skill tool with `grilling` (or `grill-me` / `grill-with-docs` if that is what the harness exposes for the interview primitive).

Grill **only**: motto, problems, desired outcomes, signals/metrics, product non-goals.  
If the interview drifts into scope/NFR/epics/architecture — capture as `Handoff / tensions for PO`, do not resolve them here.

**Fallback** (no grilling skill available): run an embedded interview covering the same contour until branches are closed or the user says to draft. Do not skip grilling because a parent agent already interviewed.

### 3. Metrics discipline

- Prefer falsifiable outcomes (metric or observable signal + target).
- Soft wishes → rewrite toward signals when possible.
- If still qualitative: keep the row; set metric fields to `TBD`; for each such row **propose 2–3 proxy metrics** (user may accept, pick later, or leave TBD).
- Choosing a metric is **not** required for skill completion.
- Set `weak-metrics: true` if any outcome lacks metric+target. Else `false`.

### 4. Write the file

Create or overwrite `docs/product/outcomes.md` using the template. Start as `Status: draft`. Leave `Approved by` / `Approved at` empty until approval.

### 5. Completion (skill done ≠ freeze)

Skill is **done** when the file exists, limits are respected, metadata is filled (`weak-metrics`, `Content language`), and Status is `draft` (unless step 6 just ran).

Then:

1. If `weak-metrics: true`, warn the Product Owner / user: approve is allowed, but do not harden BRD/architecture on weak signals.
2. Offer optional tracker issue; create it **only** after explicit yes.
3. Stop for the human **gate**: approve outcomes (or reject / revise).

### 6. Approval (gate)

Agent may set `Status: approved` only when the user explicitly approves in chat **and** names who (`Approved by` = name or role). If who is missing — ask; never write `unknown`.  
Set `Approved at` to now (ISO-8601 with offset).

Approve **is allowed** when `weak-metrics: true`; keep the flag and the warning.

## Template

```markdown
# Outcomes

Status: draft
Approved by:
Approved at:
weak-metrics: true|false
Content language: ...

## Motto
...

## Problems
- ... — ... — ...

## Later problems
- ...

## Desired outcomes
| ID | Outcome | Metric / signal | Baseline | Target | Time horizon | Proxies (if TBD) |
|----|---------|-----------------|----------|--------|--------------|------------------|
| O1 | ... | ... | ... | ... | ... | ... |

## Non-goals
- None yet

## Handoff / tensions for PO
- ...
```

## Out of scope for this skill

Scope in/out, NFR tables, epic lists, prioritization, BRD, ADR, solution design.
