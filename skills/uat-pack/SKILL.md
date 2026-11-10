---
name: uat-pack
description: Grill then draft docs/product/uat/E<id>.md — few comprehensive human UAT scenarios, pack approve, then record Verdict with who and open follow-up tickets after the summary. No technical load metrics in UAT. Use at product-owner step 10.
---

# UAT pack

Prepare and close **human** acceptance for one epic. You never invent a `pass` Verdict yourself.

## Artifact

Path: `docs/product/uat/E<epic-id>.md` (e.g. `docs/product/uat/E1.md`).  
No extra follow-up markdown files — follow-ups become **tracker issues** only.

```markdown
Status: draft | approved          # pack (scenarios) approve — before the run
Approved by:
Approved at:
Verdict: pending | pass | pass-with-followups | fail
Verdict by:
Verdict at:
```

## When the human run happens

```text
Build ready (step 9)
  → grill + draft UAT pack
  → explicit pack approve (Status + who)   # scenarios agreed
  → human executes scenarios on Build under test
  → record Results + Verdict (+ who)
  → if Verdict ≠ pass: after summary, create tracker tickets for follow-ups
```

## Always grill (UAT contour)

Call `grilling` (or `grill-me` / `grill-with-docs`; fallback embedded). Focus: what a non-dev can exercise end-to-end, test data, out-of-scope, which must-NFR are human-checkable. Do not skip because a parent already interviewed.

Read (read-only): epic stories/AC, build claims, `nfr.md` must-haves, contracts catalog as needed.

## Scenario design

- Prefer **few large comprehensive** scenarios (happy path + critical failures in one walkthrough) so the human makes **fewer passes**.
- Do **not** explode to one scenario per AC by default; cover stories/AC inside those journeys (traceability column still cites Story/AC).
- If scenario count would exceed **5**: warn the user; proceed only if they explicitly agree.
- Steps must be executable by a non-developer when possible (UI path, sample data, expected screens/messages).

## NFR in UAT

- Include **must-have** NFR spot checks relevant to the epic **only** when a human can meaningfully observe them (e.g. audit entry visible, permission denied UX, required field).
- **Exclude** technical load/perf metrics (RPS, p95 latency benches, throughput, soak) — those belong in automated tests (`ac-to-tests` / CI), not UAT.

## Steps

### 1. Content language

Ask once if needed. Headings English.

### 2. Draft pack

Write/overwrite `docs/product/uat/E<id>.md`. Leave scenario `Result` and `Verdict` as `pending`.

### 3. Pack approve (before run)

Explicit approve of the **scenario pack** + who → `Status: approved`. No `unknown` who.

### 4. Human run

Point the human at Build under test. Do not mark scenario results without their report.

### 5. Record outcome

When the human reports results: fill Result columns; set `Verdict` + **`Verdict by` / `Verdict at`** (who required — ask if missing).

### 6. After summary — auto tickets

When Verdict is `fail` or `pass-with-followups` (after the summary is written in Follow-ups):

1. Create issues in the configured **issue tracker** (Matt setup / project tracker) — one ticket per follow-up item (or a tight cluster the user accepts).
2. No parallel markdown follow-up file.
3. If tracker unavailable: stop with the exact list + ask how to file; do not silently skip.
4. On Verdict `pass`: no tickets unless the user still wants chores.

Link ticket ids back into the Follow-ups section of `E<id>.md`.

## Template — `docs/product/uat/E1.md`

```markdown
# UAT — E1 — <epic title>

Status: draft
Approved by:
Approved at:
Verdict: pending
Verdict by:
Verdict at:
Content language: ...

## Build under test
- Branch / version / env:
- Out of scope for this UAT:

## Scenarios
| ID | Covers (stories/AC) | Steps | Expected | Result | Notes |
|----|---------------------|-------|----------|--------|-------|
| U-01 | ... | ... | ... | pending | |

## NFR spot checks (human-observable must-haves only)
| NFR | How to check | Result |
|-----|--------------|--------|
| ... | ... | pending |

## Follow-ups
- ... → ticket: <id or TBD>

## Handoff / tensions for PO
- ...
```

## Done when

- Pack grilled, drafted, **explicitly approved** with who.
- After the run: Verdict + Verdict by set; tickets filed when Verdict ≠ pass (post-summary).
- Technical perf metrics were not smuggled into UAT.

## Out of scope

Automating the UAT clicks as a substitute for the human verdict; implementing fixes; editing `nfr.md`; load-test authorship.
