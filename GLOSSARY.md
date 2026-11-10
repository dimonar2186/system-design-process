# Glossary

Shared language for this process pack.

**Frame**:
Steps 1–5 of the greenfield flow: outcomes through early architecture. Done once per system (then only revised deliberately).
_Avoid_: phase A as a spoken synonym in tickets — say **Frame**.

**Epic loop**:
Steps 6–11 repeated per prioritized epic after the **Frame** is done.

**Outcome**:
A desired result of the system, preferably falsifiable (metric or observable signal), not a feature request.
_Avoid_: goal (too vague), KPI (use when the metric is already institutionalized).

**weak-metrics**:
Flag on `docs/product/outcomes.md` when any outcome lacks metric+target. Approve is still allowed; BRD/architecture must not pretend the signals are strong.

**to-be-determined** (NFR):
Flag on `docs/product/nfr.md` when a concrete NFR has measure/constraint still TBD. Abstract NFRs are forbidden; delayed numeric/SLO values are allowed with this flag.

**Architecture concept**:
C4 L1/L2 contour and style choices (`arch-options`), not detailed design or brand technology picks. Recorded in `docs/architecture/options.md`; chosen concept yields `proposed` ADR(s) refinable per epic.

**ADR lite**:
Epic-level tech/architecture decision files `docs/adr/ADR-NNNN-title.md` (`adr-lite`). One problem per file; grill then write a pool; batch-approve all. May name concrete technologies. Links to older ADRs on change/replace without editing the old Status.

**Contract catalog**:
`docs/architecture/contracts/catalog.md` — registry of ours/external contracts per epic, with links to IDL files or external git paths (`contracts-from-stories`).

**Test map**:
`docs/product/tests/test-<Epic_id>-<US_id>.md` — AC→test registry with explicit Status approve (`ac-to-tests`). Companion `test_results.md` is an overwrite-only run log.

**UAT pack**:
`docs/product/uat/E<id>.md` — few comprehensive human scenarios (`uat-pack`). Pack Status approve before the run; Verdict + who after; technical load metrics stay in automated tests; follow-ups become tracker tickets.

**Outcome log**:
`docs/product/outcome-log.md` — append-only checks of epic-traced outcomes (`outcome-check`). No grilling; section Status approve; propose measurement methods; PO handoff only (no auto tickets).

**Epic**:
A user-valued capability chunk that can be delivered as vertical slices. Not a technical layer. Tech-only enablers are not epics; they appear as functional intent inside epics or as scope assumptions.
_Avoid_: theme (looser), milestone (time-boxed delivery, not capability).

**Tracer bullet**:
A narrow end-to-end vertical slice that is demoable or verifiable alone.

**Gate**:
A human decision point the Product Owner must not skip (outcomes, scope, priority, architecture, AC, critical ADR, UAT, next/stop).

**Process state**:
The file `docs/agents/process-state.md` owned by `product-owner`, recording mode, step, and waits.

**BRD**:
Business requirements document (`docs/product/BRD.md`) with stable `BR-E#-##` IDs traced to epics (`to-brd`). Not an NFR doc; may list **Proposed NFR** for PO. Distinct from a technical **spec** (`to-spec`). No architecture inside the BRD.

**NFR**:
Non-functional requirement. Not NFT.
