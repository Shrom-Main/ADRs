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
   - **Baseline (Verified Closure Anchor):** `Market-HFT-OS` @ `0ee073eccda1470ece5a05804aabcf311a540a61` (`0ee073e`, Tag: `POC-001-Gate-M3-Verified`) / `ADRs` @ `3daed5299fecee3549c02f7dafbeedb8eddeec60` (`3daed52`, Tag: `POC-001-Gate-M3-Verified`).
   - **Post-M3 Security Maintenance Baseline:** `Market-HFT-OS` @ `80c4bfd95420584ef66dfe5429e5e2fd0b02e10d` (`80c4bfd`) / `ADRs` @ `353edb4`.
   - **Approved Scope:** File-backed recovery journal; separate-process crash worker recovery; native PostgreSQL 16.8 concurrency & commit reconciliation; ActualsGuard dual-ledger cryptographic verification; 19 suites, 158 passed assertions; zero vulnerabilities under npm audit.
   - **Status:** **APPROVED / CLOSED** (Formally authorized under Decision OD-02 and maintained under Decision OD-03 by Project Owner on 2026-10-15).
5. **Gate M4 (End-to-End Research & Capital-Allocation Vertical Slice):**
   - **Baseline:** `Market-HFT-OS` @ `9bc249a1a795af83f838febe5d26bb6a29030158` (`9bc249a`) / `ADRs` @ `c5aa59d`.
   - **Approved Scope:** Bounded research and capital-allocation simulation engine for DIN 3017 W4 SS304 hose clamps (pack of 10); Suite 20 (8 tests); 20 suites, 169 passed tests (0 skipped, 0 failed); five core invariants (provenance envelope & TTL, working-capital tax drag, asymmetric return drag, risk-adjusted hurdle vs T-Bills, deterministic edge-decay detection); zero real-money capital execution.
   - **Status:** **APPROVED / CLOSED** (Formally authorized under Decision OD-05 by Project Owner on 2026-10-15).
6. **Gate M4.1 (Statutory Math Remediation & Governed Formula Registry / RAG Bootstrap):**
   - **Baseline:** `Market-HFT-OS` @ `a1053b086e5025b76db1839b67cfede504c5bce1` (`a1053b0`) / `ADRs` @ current `main`.
   - **Approved Scope:** Remediation of 4 statutory tax and unit-economics flaws (MATH-01 to MATH-04); creation of Governed Formula Registry and Local BM25 RAG Retriever (`src/research/formulaRegistry.ts`); Suite 20 expanded to 11 tests; full test baseline expanded to 172 passed tests across 20 suites (0 skipped, 0 failed).
   - **Status:** **APPROVED / CLOSED** (Formally authorized under Decision OD-06 by Project Owner on 2026-10-16).

### Project Owner Decision OD-02 (Hybrid Scope Resolution for Frozen Spec §8.2)

Formally authorized by Project Owner on 2026-10-15:
1. **Waiver of Legacy Upstream Retail/E-Commerce Fixtures:**
   - `PROP-INV-001` (7-bucket warehouse inventory transitions), `META-FEE-001` (Amazon seller closing fee monotonicity steps), and `HIST-REPLAY-001` (AIStudio March 2026 SS304 clamp landed cost fixture at ₹38.21) are legacy upstream retail/e-commerce artifacts from the AIStudio template that have zero application to the Market-HFT-OS financial trading runtime. They are formally waived and de-scoped from the Market-HFT-OS runtime baseline.
2. **Retention and Verification of Platform Timing Invariants:**
   - `FUZZ-CLOCK-001` (+600s clock skew -> `E-ERR-007: CLOCK_SKEW_EXCEEDED`) is an authentic platform timing invariant and is retained, implemented, and verified in `suite13_market_feed_execution.test.ts`, expanding the verified test suite to **158 passed tests across 19 suites** (0 skipped, 0 failed).
3. **Milestone Disposition:**
   - Gate M3 status is authoritatively confirmed as **APPROVED / CLOSED**.

### Project Owner Decision OD-03 (Post-M3 Dependency Security Advisory Remediation)

Formally authorized by Project Owner on 2026-10-15:
1. **Dependency Pin Upgrades & Supply Chain Hardening:**
   - Upgraded `ws` to exact `"8.22.0"` and `vitest` to exact `"4.1.12"`, accompanied by exact-pinned overrides for `"vite": "6.4.4"` and `"esbuild": "0.25.0"` to eliminate all advisories (`GHSA-58qx-3vcg-4xpx`, `GHSA-96hv-2xvq-fx4p`, `GHSA-5gmw-xhrv-c9v3`, `GHSA-85c8-ppgw-ccpr`, `GHSA-67mh-4wv8-2f99`, `GHSA-5xrq-8626-4rwp`), achieving **`0 vulnerabilities`** in `npm audit`.
2. **Baseline Preservation:**
   - The verified Gate M3 closure state was permanently anchored via annotated tag `POC-001-Gate-M3-Verified` on both repositories (`0ee073e` in `Market-HFT-OS` and `3daed52` in `ADRs`).
   - The post-M3 security maintenance commit advances `Market-HFT-OS` to `80c4bfd` while strictly maintaining the 158-test baseline (19 suites passed, 0 skipped, 0 failed) and zero-caret pinning policy (`ADR-0004`).

### Project Owner Decision OD-04 (Pre-M4 Conformance Closure, Evidence Separation & Full §8.2 Implementation)

Formally authorized by Project Owner on 2026-10-15:
1. **Supersession of OD-02 Waiver & Full Implementation of Section 8.2 Invariants:**
   - The waiver portion of Decision OD-02 regarding `PROP-INV-001`, `META-FEE-001`, and `HIST-REPLAY-001` is formally superseded. These three tests represent essential invariants for the initial commercial arbitrage vertical slice (DIN 3017 SS304 hose clamp pack of 10, landed cost ₹38.21, 7-bucket inventory conservation, and Amazon fee monotonicity).
   - All three tests have been implemented and verified in `Market-HFT-OS` (`tests/acceptance/suite07_financial_engine.test.ts`), expanding the verified baseline to **161 passed tests across 19 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8.
   - Zero normative requirements in Frozen Spec §8.2 remain waived or unverified.
2. **Strict Evidence Separation Across Distinct Baselines:**
   - **Gate M3 Closure Baseline**: Permanently anchored at `0ee073eccda1470ece5a05804aabcf311a540a61` (`0ee073e`) in `Market-HFT-OS` and `3daed5299fecee3549c02f7dafbeedb8eddeec60` (`3daed52`) in `ADRs` via tag `POC-001-Gate-M3-Verified`. The canonical Gate M3 test evidence file `POC-001_Gate_M3_Test_Execution_Results.json` has exact SHA-256 `2A67460967C339D290C925396F321B59753A9A6AD73034162962D439BC2E1434` (158 tests) and is accompanied by `POC-001_Gate_M3_Typecheck_Execution_Results.txt`.
   - **Post-M3 Security Maintenance Baseline**: Pinned at commit `80c4bfd95420584ef66dfe5429e5e2fd0b02e10d` (`80c4bfd`) under Decision OD-03 (`0 vulnerabilities` in `npm audit`, 158 tests).
   - **Pre-M4 Conformance Baseline**: Pinned at commit `cf0faf19024d40236fec372bbdfb105beebd9441` (`cf0faf1`) in `Market-HFT-OS` under Decision OD-04, with dedicated evidence files `POC-001_Pre_M4_Conformance_Test_Execution_Results.json` (SHA-256: `2BD75AE3EB2A8E9F2A2629315499896B314F2BB307790BA9FAC436A7BB9B7FEC`, 161 tests) and `POC-001_Pre_M4_Typecheck_Execution_Results.txt`.
3. **Gate M4 Scoping & Specification Freeze:**
   - Gate M4 is formally bounded as a research and capital-allocation simulation gate, excluding live physical fulfillment, production payment APIs, and ERP integrations.

### Project Owner Decision OD-05 (Gate M4 Specification Freeze & Bounded Vertical Slice Authorization)

Formally authorized by Project Owner on 2026-10-15:
1. **Specification Freeze & Authorization:**
   - Formally froze `POC-001_Gate_M4_Acceptance_Specification.md` and `POC-001_Gate_M4_SS304_Vertical_Slice_Test_Scenario.md` as `FROZEN / AUTHORIZED (OD-05)`.
   - Enforces five core invariants: (1) cryptographic provenance envelopes & TTL enforcement, (2) full working-capital cash-conversion cycle & tax drag (GST, TCS, TDS), (3) asymmetric return & quarantine attrition modeling across 7 buckets, (4) risk-adjusted hurdle rate vs 91-day T-Bill opportunity cost, and (5) deterministic decision outcomes & edge-decay transitions.
2. **Implementation Verification:**
   - Implemented `M4ResearchAllocationEngine` (`src/research/m4VerticalSlice.ts`) and acceptance test suite `suite20_m4_ss304_vertical_slice.test.ts` (8 passed assertions).
   - Verified 100% passing across **20 suites / 169 tests (0 skipped, 0 failed)** on live PostgreSQL 16.8 (`localhost:5432`).
3. **Dedicated Evidence Partitioning:**
   - Generated dedicated Gate M4 evidence files: `POC-001_Gate_M4_Test_Execution_Results.json` (SHA-256: `04A7BAA3497DD138BCD3CF901D9EBB35515EFA4A05A7B8BC5BC1AC4C6DF2A0C7`), `POC-001_Gate_M4_Typecheck_Execution_Results.txt`, and `POC-001_Gate_M4_Vertical_Slice_Conformance_Report.md`.
4. **Milestone Disposition:**
   - Gate M4 status is authoritatively confirmed as **APPROVED / CLOSED**.

### Project Owner Decision OD-06 (Gate M4.1 Statutory Math Remediation & Governed Formula Registry / RAG Bootstrap)

Formally authorized by Project Owner on 2026-10-16:
1. **Statutory Tax & Unit Economics Remediation (MATH-01 to MATH-04):**
   - Corrected four real-world Indian statutory tax and unit-economics approximations in `src/research/m4VerticalSlice.ts`:
     - **MATH-01 (18% Marketplace Fee GST & ITC)**: Marketplace fees incur 18% GST ($₹39.75 \times 18\% = ₹7.1550$) withheld from disbursements and added to eligible Input Tax Credit (ITC) under CGST Act Sec 16.
     - **MATH-02 (Ex-GST Tax Base for Sec 52 TCS & Sec 194-O TDS)**: TCS (1%) and TDS (1%) are levied strictly on the ex-GST net taxable base (₹88.9830), yielding ₹0.8898 each, rather than the GST-inclusive gross price.
     - **MATH-03 (Non-Fungible Tax Ledger Separation)**: Section 52 GST TCS in the GST Electronic Cash Ledger offsets GSTR-3B Output GST liability (reducing cash liability from ₹3.0333 to ₹2.1435), while Section 194-O Income Tax TDS is non-fungible with GST and is tracked separately as an income-tax holdback.
     - **MATH-04 (Supplier Trade Credit Terms in CCC)**: Supplier payment terms are explicitly incorporated into the cash-conversion cycle: $\text{CCC} = \max(1, \text{Lead} + \text{Dwell} + \text{DisbursementDelay} - \text{PaymentTerms})$. Set to 0 for advance EXW MOQ procurement (35 days), and verified that 15-day supplier credit compresses CCC to 20 days and expands RoWC to 698.97%.
2. **Governed Formula Registry & Local BM25 RAG Architecture:**
   - Implemented `src/research/formulaRegistry.ts` exporting `FormulaRegistry` and pre-loading 5 canonical formulas (`FIN-LANDED-COST-001`, `FIN-MKT-FEES-GST-002`, `FIN-STATUTORY-TCS-TDS-003`, `FIN-RETURN-ATTRITION-004`, `FIN-CCC-ROWC-005`) sealed with RFC 8785 JCS digests.
   - Built deterministic Okapi BM25 keyword/semantic search over statutory citations and invariants (`retrieveFormulas("Section 194-O TDS GST offset")` returns `FIN-STATUTORY-TCS-TDS-003`).
   - Enforced strict dual-tier isolation: candidate formulas reside in `CANDIDATE_UI_MODEL` and fail closed (`E-ERR-GOV-001`) if executed in production without explicit owner promotion (`promoteCandidateFormula`).
3. **Evidence Separation & Test Baseline:**
   - Suite 20 expanded to 11 tests (adding `M4-STATUTORY-MATH-009`, `M4-FORMULA-REGISTRY-RAG-010`, and `M4-FORMULA-GOVERNANCE-ISOLATION-011`).
   - Full test suite passes 100% across **20 suites / 172 tests (0 skipped, 0 failed)** on live PostgreSQL 16.8.
   - Dedicated Gate M4.1 evidence files generated: `POC-001_Gate_M4_1_Test_Execution_Results.json` (SHA-256: `0BA7C517DE32287309599DE54017E8E0FF4918514A4DBC0B5F37D48BF34863D1`) and `POC-001_Gate_M4_1_Typecheck_Execution_Results.txt` (SHA-256: `AEBAE79954369EA1B651A8917EAF32B981FAF5AE6387EA4A3F21B15B551DF58E`).
4. **Milestone Disposition:**
   - Gate M4.1 status is authoritatively confirmed as **APPROVED / CLOSED**.

### Project Owner Decision OD-07 (Gate M4.2 Groq-Backed LLM Formula Discovery & Refinement Module)

Formally authorized by Project Owner on 2026-10-16:
1. **Groq-Backed LLM Formula Advisor (`src/research/llmFormulaAdvisor.ts`):**
   - Implemented `GroqFormulaAdvisor` module reading Groq credentials from `Groq_Key.env` or process environment.
   - Built `proposeFormulaRefinement(promptContext, existingFormula)` interacting with Groq inference API (`openai/gpt-oss-120b` or configurable models) to synthesize schema-compliant `FormulaCard` definitions (symbolic expression, subunit input variables, deterministic canonical test vectors).
   - Implemented graceful offline fallback simulation mode (`forceSimulated: true` or `GROQ_OFFLINE_MODE=true` or network timeouts) ensuring non-blocking execution across offline and CI test environments.
   - Implemented `evaluateLlmCandidate(cardInput, registry, customEvaluator)` automatically registering candidate formulas under the sandboxed `CANDIDATE_UI_MODEL` tier, deterministically executing test vectors via custom or compiled symbolic evaluators, and returning verifiable execution status.
2. **FormulaRegistry Expansion (`src/research/formulaRegistry.ts`):**
   - Added `FormulaCardInput` and `FormulaEvaluatorFn` types.
   - Implemented `registerFormulaEvaluator(formulaId, fn)` and `hasEvaluator(formulaId)` allowing dynamic registration of compiled TypeScript BigInt evaluators for candidate formulas.
   - Implemented deterministic `evaluateSymbolicExpression` evaluator for arithmetic expressions with basis point division and floating-point intermediate precision before rounding to BigInt subunits.
   - Reinforced Governance Firewall: `CANDIDATE_UI_MODEL` formulas are strictly prohibited from executing in production mode (`evaluateFormula` throws `E-ERR-GOV-001`) or authorizing capital allocation until formally promoted to `PROMOTED_NORMATIVE` via authorized owner directive (`promoteCandidateFormula`).
3. **Acceptance Tests & Evidence Separation (`Suite 20`):**
   - Added three normative acceptance assertions in `tests/acceptance/suite20_m4_ss304_vertical_slice.test.ts`:
     - `M4-GROQ-CREDENTIALS-012`: Verified Groq API credential loading and validation from `Groq_Key.env` with fallback on invalid paths.
     - `M4-GROQ-ADVISOR-PROPOSAL-013`: Verified candidate formula proposal generation for warehouse inventory shrinkage, customs anti-dumping duty, and normative formula refinement.
     - `M4-GROQ-ADVISOR-EVAL-ISOLATION-014`: Verified sandboxed registration, test vector execution, BM25 RAG indexing, governance firewall fail-closed enforcement, and post-promotion production execution.
   - Full test baseline expanded to **175 passed tests across 20 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
   - Dedicated Gate M4.2 evidence files generated:
     - `POC-001_Gate_M4_2_Test_Execution_Results.json` (SHA-256: `FEDA66529346B2F0566C9402A19203B36C65B6CAF5588ED0634D680C72E44045`, 175 tests).
     - `POC-001_Gate_M4_2_Typecheck_Execution_Results.txt` (SHA-256: `4596FF7DF1A8F378190D49DBCDBD055A4CB69A39B5C5B32F3E263B81D07AFF96`, 0 errors).
4. **Milestone Disposition:**
   - Gate M4.2 status is authoritatively confirmed as **APPROVED / CLOSED**.

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
