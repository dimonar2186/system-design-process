---
name: outcome-check
description: Append an approved section to docs/product/outcome-log.md comparing epic-traced outcomes to observed signals. No grilling. Propose measurement methods when needed; handoff PO on rethink/flat/regressing — no auto tickets. Use after UAT/release or product-owner step 11.
---

# Outcome check

Close the loop to step-1 **outcomes** for the active epic/release. Product measurement — not coding `retro`.

**Do not grill.** Synthesize from disk + what the user supplies this turn. Ask short factual questions only if a required input is missing (e.g. Observed number).

## Artifact

Path: `docs/product/outcome-log.md` — **append** a dated section per run (do not wipe history).

Each section carries its own approve metadata:

```markdown
## <ISO-8601 date> — <epic or release id>

Status: draft | approved
Approved by:
Approved at:
Epic / release: E? / …
Sources: outcomes.md, UAT E?.md, …
```

## Scope of outcomes

Include **only** outcomes traced to **this** epic (via `epics.md` Outcomes column / BRD links).  
Do not re-score the whole canvas unless the user explicitly asks for a system-wide check.

## Reading inputs (read-only)

- `docs/product/outcomes.md` (respect `weak-metrics`)
- `docs/product/epics.md` (trace)
- Epic UAT pack / Verdict if present (`docs/product/uat/E*.md`)
- Any metrics or notes the user pastes

## Measurement

- Prefer stated Metric / signal + Target from the canvas.
- Agent **may propose** how to measure (proxy, query, dashboard) when Metric is TBD or Observed is missing — wait for user data or acknowledgment before inventing “Observed” numbers.
- If `weak-metrics: true` or no data: still add a row with Status **`unknown`**, note the gap, and recommend the **smallest instrumentation** slice.

Row statuses: `moved` | `flat` | `unknown` | `regressing`.

## Handoff (no auto tickets)

If Recommended next is rethink / gather data / address regressing / similar — write clear items under **Handoff / tensions for PO** in the log section (and process-state Notes if called from PO).  
**Do not** create tracker tickets from this skill.

## Steps

1. Identify epic/release and traced outcomes.
2. Build the table (Expected move vs Observed vs Status).
3. Write Interpretation + Recommended next (`continue epic backlog` | `new epic` | `rethink outcome` | `gather data` | …).
4. Append section with `Status: draft`.
5. **Explicit approve** of this section + who → `approved` / `Approved by` / `Approved at`. No `unknown` who.
6. Done when every traced outcome has a row, Recommended next is explicit, and the section is approved.

## Template section

```markdown
## 2026-11-10T18:00:00+03:00 — E1

Status: draft
Approved by:
Approved at:
Epic / release: E1
Sources: docs/product/outcomes.md; docs/product/uat/E1.md; …

| Outcome ID | Metric / signal | Expected move | Observed | Status |
|------------|-----------------|---------------|----------|--------|
| O1 | ... | ... | ... | moved\|flat\|unknown\|regressing |

### Measurement proposals (if any)
- O?: …

### Interpretation
- ...

### Recommended next
- ...

### Handoff / tensions for PO
- ...
```

## Out of scope

Grilling sessions, coding retro, filing tickets, editing `outcomes.md` targets silently, scoring unrelated outcomes.
