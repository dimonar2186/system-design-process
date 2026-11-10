# Phase recipes

Each recipe lists skills in call order. Prefer installed Matt skills by name. Skills with no Matt equivalent live in this pack.

## Skill readiness

| Skill | Ready for live use |
|-------|--------------------|
| `outcome-canvas`, `scope-nfr`, `epic-backlog`, `prioritize-epics`, `to-brd`, `arch-options`, `adr-lite`, `contracts-from-stories`, `ac-to-tests`, `uat-pack`, `outcome-check` | Yes |
| `to-spec`, `to-tickets`, `tdd`, `implement`, `implement-spec`, `code-review`, `grilling`, … | Yes if Matt pack installed; else slash-handoff |

### Not-ready protocol

If a recipe would call a skill marked **No** (none in pack currently), or the active **Run profile** excludes the step:

1. Do **not** call the skill.
2. Set `Waiting on human` / Notes: `blocked: step N — <skill> not ready` or `out of profile`.
3. Tell the user what is blocked and how to continue later (change profile or wait for skill grill).
4. Stay stable — no invented artifacts for that step.

---

## Step 1 — Outcomes

1. Call `outcome-canvas` only. Grilling lives **inside** that skill (step isolation). Do not call `grill-with-docs` / `grill-me` here — that would double-interview.
2. If `outcome-canvas` surfaces async stakeholder gaps, call `to-questionnaire`, then pause until answers return; re-enter `outcome-canvas` if the canvas must be updated.
3. Gate: **Approve outcomes**. Respect `weak-metrics` warnings from the canvas; do not pretend metrics are strong.

## Step 2 — Scope + NFR

1. Call `scope-nfr` only (grilling inside that skill).
2. Optional: `research` for external standards/APIs that bind NFR — after or during scope-nfr if it requests it via handoff.
3. Gate: **Approve scope + must-have NFR** (per-file approve, any order). Resolve tensions vs outcomes if `Handoff / tensions for PO` conflicts with the canvas.

## Step 3 — Epics + priority

1. Call `epic-backlog` (grilling inside; no build order yet). Gate: **Approve epic backlog**.
2. Call `prioritize-epics` (grilling inside). Gate: **Approve epic order**. Write ordered backlog into process-state.
3. Only if the route is still foggy across many sessions: tell human to run `/wayfinder` (decision map), then return — do not treat wayfinder as value prioritization.
4. Resolve `Handoff / tensions for PO` from either skill before freezing order.
5. **Mandatory context cut `after-epics`:** after build-order approve, write `docs/agents/handoff-after-epics.md`, set state Waiting to `/product-owner resume handoff-after-epics`, **stop this chat**. Do **not** start step 4 here.

## Step 4 — BRD

*Enter only after `resume handoff-after-epics` in a fresh session.*

1. Call `to-brd` only (grilling inside; default high-level). Do not edit `nfr.md` here — absorb `Proposed NFR` from the BRD via a later `scope-nfr` pass or explicit PO decision if needed.
2. Optional later (not a substitute for BRD): `to-spec` as technical synthesis when entering an epic.
3. Gate: **BRD freeze** (business requirements enough to argue architecture next). Soft-freeze if `has-tbd-sections: true`.

## Step 5 — Architecture concept + early ADR

*Enter only from `/product-owner resume handoff-after-epics` (or equivalent fresh session that loaded that handoff).*

1. Optional: if a design question needs a runnable answer before concepts settle, call `prototype` (or human `/prototype`).
2. Optional: `domain-modeling` when glossary terms for the contour are shifting.
3. Call `arch-options` only (grilling inside). One sound concept option is enough; skill offers more; extras on request. No brand-tech lock-in.
4. Gate: **Choose option** (Chosen + who). `arch-options` then writes `proposed` ADR(s) (one file if ≤3 decision questions, else split).
5. If codebase already exists and seams are the topic after choice: call `codebase-design`.
6. Resolve Assumptions / Proposed-NFR tensions before treating the concept as hard.
7. **Mandatory context cut `after-architecture`:** write `docs/agents/handoff-after-architecture.md`.  
   - `frame-only` → mode `done`; stop.  
   - `through-stories` / `full` → Waiting lists spawn commands for each epic in build order (at least the first): `/product-owner spawn epic E1`. **Stop this chat**; epic work runs in **new** agent chats (one epic per chat preferred).

---

## Step 6 — Stories, contracts, tickets (active epic)

### 6a — Stories (**in `through-stories` and `full`**)

*Enter via `/product-owner spawn epic E<id>` in a **fresh** chat after `handoff-after-architecture`.*

1. Call `to-spec` for the active epic (Matt). If unavailable — ask human to run `/to-spec`, set waiting, resume on `continue`.
2. Gate: **Approve epic spec / stories**.
3. If Run profile is `through-stories`: mark epic `stories-done`; optionally write `docs/agents/handoff-epic-E<id>.md`; clear active epic; tell human to `spawn epic` for the next id (do **not** chain all epics in one context by default). Mode `done` when no epics left. **Stop** — do not enter 6b/6c/7–11.

### 6b — Contracts (**`full` only**)

1. Call `contracts-from-stories` (grilling inside).
2. Gate: **Approve contracts for epic**.

### 6c — Tickets (**`full` only**)

1. Call `to-tickets` (Matt or slash-handoff).
2. Gate: **Approve AC / ticket breakdown**. Reject horizontal slices.

## Step 7 — Detailed ADR (**`full` only**)

1. Prefer `adr-lite` for epic tech/architecture forks (grilling inside; writes a **pool**, batch-approve all). Use `domain-modeling` when ubiquitous language / glossary must move too.
2. Gate: **Batch-approve the ADR pool** (no partial accept). Waive only for pure presentation changes with no new coupling.

## Step 8 — Tests first (**`full` only**)

1. Call `ac-to-tests` (grilling inside; failing tests + maps + `test_results.md`; **batch-approve** maps with who).
2. Then `tdd` / later `implement` owns going green — not this step's job to implement features.

## Step 9 — Build (**`full` only**)

Choose one:

- **Controlled:** call `implement` per ready ticket (drives `tdd`, then `code-review`).
- **Parallel frontier:** call `implement-spec` for the whole epic task graph, then `code-review`.

Then call `pr` when opening a pull request. Slash-handoff if Matt missing.

Stay inside the active epic.

## Step 10 — Verify + UAT (**`full` only**)

1. Ensure `code-review` ran on the epic diff if applicable; `diagnosing-bugs` if red.
2. Call `uat-pack` (grilling inside; `docs/product/uat/E<id>.md`; pack approve → human run → Verdict+who → auto tickets if ≠ pass).
3. Gate: **Accept Verdict** (and that follow-up tickets exist when required).

`triage` is only for *incoming* external bugs/requests after demo — never for tickets produced by `to-tickets` / UAT follow-ups already filed.

## Step 11 — Ship + outcomes (**`full` only**)

1. `wizard` / handoff if human-only ops.
2. Call `outcome-check` (**no grill**; append `outcome-log.md`; explicit section approve + who; PO handoff only — no auto tickets).
3. Optional: `retro` (Matt) for agent-environment improvements — separate from product outcomes.
4. Gate: **Next epic / stop**.
