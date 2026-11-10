# Handoff — <cut-id>

Copy to `docs/agents/handoff-<cut-id>.md` (e.g. `handoff-after-epics.md`).  
Fresh agents load **this file + process-state + linked artifacts** — not the previous chat.

## Meta

| Field | Value |
|-------|--------|
| Cut id | `after-epics` \| `after-architecture` \| `epic-E?` |
| Written at | <ISO-8601 with offset> |
| Written by session | <short label> |
| Run profile | through-stories \| frame-only \| full |
| Next agent role | Frame-B (BRD+arch) \| Epic agent \| PO dispatcher |

## Approved so far

- Step / artifact / Status / Approved by

## Artifact pointers (read these)

- `docs/agents/process-state.md`
- …

## Open tensions for PO

- …

## Explicitly out of scope for next agent

- …

## Next command

```text
/product-owner resume handoff-<cut-id>
```

Or for an epic:

```text
/product-owner spawn epic E1
```

## Do not

- Re-grill settled approved artifacts unless the user reopens a gate
- Reload or summarize the previous chat transcript into context
- Continue past the next mandatory cut without a new handoff
