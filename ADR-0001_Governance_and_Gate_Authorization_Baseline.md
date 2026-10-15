# ADR-0001: Governance and Gate Authorization Baseline

* **Status:** Accepted
* **Date:** 2026-10-14
* **Deciders:** Project Owner, System Architect, Independent Audit Desk
* **Technical Domain:** Project Governance, Lifecycle Gates, Authorization Hierarchy

---

## Context and Problem Statement

`PROJECT_CHARTER.md` v0.2.4 was drafted at commit `582637b` establishing a strict `PROPOSED — awaiting project-owner approval` state and a `Strict Read-Only prior to Gate M0 authorization` operating rule (§10.1). As the project progressed across Gates M1, M2, and M3 (advancing from baseline `582637b` to `abfaa04`, `70121a0`, `cbafb60`, `7415c61`, and `a1bd359`), implementation proceeded based on interactive owner authorizations and audit verifications, but the in-tree charter header was not retroactively mutated in Git.

This created an authority ambiguity (`F-03`): a literal reading of `PROJECT_CHARTER.md` v0.2.4 would classify all subsequent implementation commits as unauthorized, even though Gate M1 design freeze (`77eff71`), Gate M1 conformance matrix (`70121a0`), Gate M2 integration (`cbafb60`), and Gate M3 persistence (`a1bd359`) were formally authorized and documented in gate conformance reports.

## Decision Drivers

1. Maintain historical immutability of `PROJECT_CHARTER.md` v0.2.4 at baseline commit `582637b`.
2. Establish an authoritative, versioned gate authorization ledger documenting the retroactive and forward approvals of Gates M0, M1, M2, and M3.
3. Formally delineate the operational boundary: strict `DRY_RUN` / paper simulation isolation with actuals ledger execution permanently blocked.
4. Harmonize the documentary authority hierarchy between `Shrom-Main/ADRs` and `Shrom-Main/Market-HFT-OS`.

## Considered Options

* **Option 1:** Retroactively edit `PROJECT_CHARTER.md` in `Market-HFT-OS` and change the header from `PROPOSED` to `APPROVED`.
* **Option 2:** Adopt this Architecture Decision Record (`ADR-0001`) alongside `GATE_AUTHORIZATION_LEDGER.md` in `ADRs`, establishing the formal gate lineage without mutating the historical charter text at `582637b`.

## Decision Outcome

Chosen option: **Ratified Dual Approach (Owner Ratified October 15, 2026)**.
1. The Human Project Owner explicitly ratified the status header update in `PROJECT_CHARTER.md` (transitioning Line 4 to `APPROVED / IN-FLIGHT` and Line 9 to `DRY_RUN / Paper Simulation only`).
2. Historical gate lineage, normative errata, and ongoing gate transitions are authoritatively maintained through this ADR and `GATE_AUTHORIZATION_LEDGER.md`.

### Gate Authorization Lineage

1. **Gate M0 (Quarantine & Environment Isolation):**
   - **Baseline:** `Market-HFT-OS` @ `582637b`.
   - **Approved Scope:** Acceptance of Charter v0.2.4; strict quarantine isolation of legacy `_salvage/`; zero-credential environment; root Git initialization.
2. **Gate M1 (Design Readiness Specification Freeze):**
   - **Baseline:** `ADRs` @ `77eff71` / `Market-HFT-OS` @ `70121a0`.
   - **Approved Scope:** Frozen Normative Design Specification v1.13; 4-claim promotion state machine; JCS canonicalization (RFC 8785); integer subunit money; AUDIT-01 through AUDIT-52 compliance. (Amended under versioned Erratum v1.14 ratified by Owner).
3. **Gate M2 (Simulated Execution & Dual-Ledger Isolation):**
   - **Baseline:** `Market-HFT-OS` @ `cbafb60`.
   - **Approved Scope:** Paper execution pipeline; monotonic virtual clock; simulated gateway; loopback WebSocket feed; dual-ledger safety isolation (15 suites, 106 tests).
4. **Gate M3 (Persistence, Crash Recovery, Dual-Ledger Verification & Native PostgreSQL Concurrency):**
   - **Baseline:** `Market-HFT-OS` @ `0ee073eccda1470ece5a05804aabcf311a540a61` (`0ee073e`) / `ADRs` @ current `main`.
   - **Approved Scope:** File-backed recovery journal; separate-process crash worker recovery; native PostgreSQL 16.8 concurrency & commit reconciliation; ActualsGuard dual-ledger cryptographic verification; 19 suites, 158 passed assertions.
   - **Status:** **APPROVED / CLOSED** (Formally authorized under Decision OD-02 by Project Owner on 2026-10-15).

### Project Owner Decision OD-02 (Hybrid Scope Resolution for Frozen Spec §8.2)

Formally authorized by Project Owner on 2026-10-15:
1. **Waiver of Legacy Upstream Retail/E-Commerce Fixtures:**
   - `PROP-INV-001` (7-bucket warehouse inventory transitions), `META-FEE-001` (Amazon seller closing fee monotonicity steps), and `HIST-REPLAY-001` (AIStudio March 2026 SS304 clamp landed cost fixture at ₹38.21) are legacy upstream retail/e-commerce artifacts from the AIStudio template that have zero application to the Market-HFT-OS financial trading runtime. They are formally waived and de-scoped from the Market-HFT-OS runtime baseline.
2. **Retention and Verification of Platform Timing Invariants:**
   - `FUZZ-CLOCK-001` (+600s clock skew -> `E-ERR-007: CLOCK_SKEW_EXCEEDED`) is an authentic platform timing invariant and is retained, implemented, and verified in `suite13_market_feed_execution.test.ts`, expanding the verified test suite to **158 passed tests across 19 suites** (0 skipped, 0 failed).
3. **Milestone Disposition:**
   - Gate M3 status is authoritatively confirmed as **APPROVED / CLOSED**.

### Safety Invariants

- **Zero Real Capital / Simulation Isolation:** No live exchange, broker, bank, or payment gateway API connections are permitted. All order routing is confined to `SimulatedExecutionGateway`.
- **Dual-Ledger Enforcement:** Writes to actuals ledger from simulation contexts are blocked fail-closed with error `E-ERR-020` / `E-ERR-040`. Writes to simulation ledger from actuals contexts are blocked with `E-ERR-025`.
- **Authority Scope:** Decisions affecting design specifications, gate progression, or system contracts require formal ADR entry and Owner concurrence.

## Traceability

- Charter: `Market-HFT-OS/PROJECT_CHARTER.md` (§10.1, §10.2).
- Ledger: `ADRs/GATE_AUTHORIZATION_LEDGER.md`.
- Conformance Reports:
  - `POC-001_Gate_M1_Comprehensive_Conformance_Matrix_Report.md`
  - `POC-001_Gate_M2_Execution_and_Integration_Conformance_Report.md`
  - `POC-001_Gate_M3_Persistence_and_Crash_Recovery_Conformance_Report.md`
