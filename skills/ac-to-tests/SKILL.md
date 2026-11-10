---
name: ac-to-tests
description: Grill AC/seams, write failing acceptance and ours-contract tests, map them in docs/product/tests/test-<Epic>-<US>.md, log the red run in test_results.md, then batch-approve. No production code. Use for ATDD setup or product-owner step 8.
---

# AC → tests

Write **failing** tests from acceptance criteria. Do **not** implement production code. Going green is `tdd` / `implement`.

## Artifacts

| Path | Role |
|------|------|
| `docs/product/tests/test-<Epic_id>-<US_id>.md` | Durable map: AC → test id/path; Status + approve |
| `docs/product/tests/test_results.md` | **Overwrite** each run: current red/green evidence (helper only) |

Example map names: `test-E1-US03.md`, `test-E2-US01.md`.

Optional tracker comments: offer; create only after explicit yes.

## Always grill (tests contour)

Call `grilling` (or `grill-me` / `grill-with-docs`; fallback embedded interview). Focus: AC clarity, seams, ours contracts in slice, what “fail for the right reason” means. Do not skip because a parent already interviewed.

## AC sources

1. Approved epic spec / tickets / stories (read-only upstream).
2. User supplements in chat.
3. Agent **may invent and propose** any number of candidate AC for consideration — never treat them as in-scope until the user **accepts** them.

If nothing accepted remains — stop; do not invent silently into tests.

## Seams

- Prefer seams already recorded in `to-spec` / Testing Decisions.
- If missing — agree with the user before the first test.
- Prefer the highest meaningful seam. No tests against unconfirmed seams.

## What to write (code)

In the project's normal test layout:

1. **Acceptance / behavior tests** for each accepted AC (or tight AC cluster) on the story.
2. **Contract tests** for **every `ours`** contract of this epic in the current slice (`docs/architecture/contracts/` + `catalog.md`). Mandatory — not only when a story mentions them.
3. **UI-only / no-contract stories:** behavior tests only from accepted AC.
4. **External** contracts: do **not** author tests against foreign IDL as if we owned it. At most a **consumer** check if an accepted AC requires verifying our call against the mirrored/registered contract.

Run tests. They must **fail for the right reason** (missing behaviour), not harness/import noise. Fix harness only until the failure message names the gap.

## Maps and results

### `test-<Epic_id>-<US_id>.md` (one file per user story; multiple AC inside OK)

```markdown
# Tests — <Epic_id> / <US_id>

Status: draft | approved
Approved by:
Approved at:
Content language: ...
Epic: E?
Story / US: ...
Seams: ...

## AC → tests
| AC id | Statement (accepted) | Test id / path | Expected fail signal |
|-------|----------------------|----------------|----------------------|
| ... | ... | ... | ... |

## Ours contracts covered
| Contract id | Test path |
|-------------|-----------|

## Notes
```

### `test_results.md` (overwrite every run)

```markdown
# Test results (current run)

Epic: E?
At: <ISO-8601 with offset>
Command(s): ...

| Test | Map file | Result | Why red (or noise?) |
|------|----------|--------|---------------------|
| ... | test-E?-US?.md | RED | ... |

## Summary
- Maps ready for batch approve: yes/no
- Blockers: ...
```

One shared `test_results.md` is enough while epics run **one chat at a time**. If epic agents run in parallel later, switch to `test_results-E<id>.md`.

## Explicit approve (batch)

After maps exist and `test_results` shows the intended **RED** set:

1. Ask for **batch approve** of all `test-<Epic>-US*.md` for this epic + **who** (name/role).
2. **No partial accept** by default — revise until the whole epic test pack is approved together (same spirit as `adr-lite`).
3. On approve: set each map `Status: approved`, `Approved by`, `Approved at`. Never `unknown` who.
4. Do not put lasting Status on `test_results.md` — it is scratch evidence.

## Done when

- Grill done; accepted AC set clear (incl. accepted proposals).
- Seams known; every accepted AC for in-scope stories has a failing test; every **ours** contract in the slice has a contract test.
- Maps written; `test_results.md` overwritten with the red run.
- Whole epic map pack **explicitly approved** with who.

## Out of scope

Production implementation, flipping tests to green, editing BRD/contracts/ADR Status, treating proposed AC as accepted without user OK.
