# POC-001 — Gate Authorization & Governance Sign-Off Ledger

| Attribute | Project Record |
| :--- | :--- |
| **Project Identifier** | `POC-001` (Market HFT OS) |
| **Controlling Authority** | Project Owner & Independent Audit Desk |
| **Companion Repositories** | `Shrom-Main/Market-HFT-OS` & `Shrom-Main/ADRs` |
| **Operating Boundary** | Strict DRY_RUN / Paper Simulation; Actuals Execution strictly disabled |

---

## 1. Gate Authorization History

| Milestone Gate | Sign-Off Date (UTC) | Authorizing Authority | Authorized Commit Baseline | Conformance Deliverables & Verified Scope | Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Gate M0** | 2026-10-10 | Project Owner | `Market-HFT-OS: 582637b` | Project Charter v0.2.4; strict quarantine isolation of `_salvage/`; zero-credential environment; root Git initialization. | **APPROVED** |
| **Gate M1** | 2026-10-11 | Project Owner | `ADRs: 77eff71`<br>`Market-HFT-OS: 70121a0` | Frozen Normative Design Specification v1.13; 4-claim promotion state machine; JCS canonicalization; subunit arithmetic. | **APPROVED** |
| **Gate M2** | 2026-10-11 | Project Owner | `Market-HFT-OS: cbafb60`<br>`ADRs: commit cbafb60 companion` | Execution engine; loopback WebSocket transport; simulated gateway; dual-ledger safety isolation; 15 suites (106 tests). | **APPROVED** |
| **Gate M3** | 2026-10-15 | Project Owner & Audit Desk | `Market-HFT-OS: 0ee073e` (Tag: `POC-001-Gate-M3-Verified`)<br>`ADRs: 3daed52` (Tag: `POC-001-Gate-M3-Verified`) | Durable file-backed recovery journal; separate-process crash recovery; native PostgreSQL 16.8 concurrency & commit reconciliation; ActualsGuard dual-ledger verification; Decision OD-02 codification (19 suites, 158 passed). | **APPROVED / CLOSED** |
| **Post-M3 Security Maintenance** | 2026-10-15 | Project Owner (`Decision OD-03`) | `Market-HFT-OS: 80c4bfd`<br>`ADRs: 353edb4` | Dependency security upgrade (`ws@8.22.0`, `vitest@4.1.12`, `vite@6.4.4`, `esbuild@0.25.0`) achieving `0 vulnerabilities` in `npm audit` while strictly preserving exact version pinning and the 158-test baseline. | **MAINTENANCE CLOSED** |
| **Pre-M4 Conformance Baseline** | 2026-10-15 | Project Owner (`Decision OD-04`) | `Market-HFT-OS: cf0faf1`<br>`ADRs: 13071fb` | Implementation and verification of all four Frozen Spec §8.2 normative tests (`PROP-INV-001`, `META-FEE-001`, `HIST-REPLAY-001`, and `FUZZ-CLOCK-001`). Baseline expanded to 161 passed tests across 19 suites (0 skipped, 0 failed). Full evidence separation maintained. | **VERIFIED / SPEC FROZEN** |
| **Gate M4** | 2026-10-15 | Project Owner (`Decision OD-05`) | `Market-HFT-OS: 9bc249a`<br>`ADRs: c5aa59d` | Bounded end-to-end research & capital-allocation vertical slice (DIN 3017 SS304 pack-of-10 clamp); Suite 20 (8/8 passed); 20 suites / 169 tests passed; full provenance envelopes, tax drag, 7-bucket inventory conservation, hurdle gating. | **APPROVED / CLOSED** |
| **Gate M4.1** | 2026-10-16 | Project Owner (`Decision OD-06`) | `Market-HFT-OS: a1053b0`<br>`ADRs: current` | Statutory math remediation (MATH-01–MATH-04: 18% fee GST + ITC, ex-GST TCS/TDS base, non-fungible GST/TDS, supplier credit terms CCC); Governed Formula Registry & Local BM25 RAG Bootstrap (`src/research/formulaRegistry.ts`); Suite 20 expanded to 11 tests; 20 suites / 172 tests passed. | **APPROVED / CLOSED** |

---

## 2. Gate Decision Notes & Operating Boundaries

1. **Gate M0 (Quarantine & Environment Isolation)**:
   - Approved operating under strict read-only salvage inspection.
   - Live broker/exchange APIs prohibited; mock and loopback transports only.

2. **Gate M1 (Design Readiness Specification Freeze)**:
   - Specification frozen as authoritative normative contract.
   - Embedded errata addressed under versioned addendum / Erratum v1.14 (unifying gateway digest binding to full `ClaimSigningPayload` SHA-256 and fail-closed key validation).

3. **Gate M2 (Simulated Execution & Dual-Ledger Isolation)**:
   - Paper execution pipeline operational with monotonic virtual clocks.
   - `ActualsGuard` enforced fail-closed (`E-ERR-020` and `E-ERR-025`).

4. **Gate M3 (Persistence, Crash Recovery & Native PostgreSQL Concurrency)**:
   - Separate-process crash worker restarts validated against WAL and snapshot storage.
   - Real PostgreSQL 16.8 server verification completed on `localhost:5432` with zero skips across all 6 test cases in Suite 17.
   - WAL boundary normalization, fail-closed torn-tail truncation, and single-pass fill recovery integrated and verified.

5. **Project Owner Decision OD-02 (Hybrid Scope Resolution for Frozen Spec §8.2)**:
   - `PROP-INV-001` (7-bucket warehouse inventory transitions), `META-FEE-001` (Amazon closing fee monotonicity), and `HIST-REPLAY-001` (AIStudio March 2026 SS304 clamp landed cost fixture at ₹38.21) were initially waived under OD-02. (Note: This waiver is superseded by Decision OD-04 below).
   - `FUZZ-CLOCK-001` (+600s clock skew -> `E-ERR-007: CLOCK_SKEW_EXCEEDED`) is retained, implemented, and verified in `suite13_market_feed_execution.test.ts`, expanding the verified baseline to 158 passed tests across 19 suites (0 skipped, 0 failed).
   - Gate M3 status is authoritatively confirmed as **APPROVED / CLOSED**.

6. **Project Owner Decision OD-03 (Post-M3 Dependency Security Upgrade)**:
   - Upgraded `ws` to exact `"8.22.0"` and `vitest` to exact `"4.1.12"` (with pinned overrides for `vite@6.4.4` and `esbuild@0.25.0`), eliminating all advisories (`GHSA-58qx-3vcg-4xpx`, `GHSA-96hv-2xvq-fx4p`, `GHSA-5gmw-xhrv-c9v3`, `GHSA-85c8-ppgw-ccpr`, `GHSA-67mh-4wv8-2f99`, `GHSA-5xrq-8626-4rwp`) and achieving `found 0 vulnerabilities` in `npm audit`.
   - The verified Gate M3 closure baseline was permanently anchored with annotated Git tag `POC-001-Gate-M3-Verified` at commit `0ee073e` in `Market-HFT-OS` and commit `3daed52` in `ADRs`.
   - The post-M3 security maintenance commit advances `Market-HFT-OS` to `80c4bfd` while strictly maintaining the 158-test baseline (19 suites passed, 0 skipped, 0 failed) and zero-caret pinning policy (`ADR-0004`).

7. **Project Owner Decision OD-04 (Pre-M4 Conformance Closure, Evidence Separation & Full §8.2 Implementation)**:
   - **Supersession of OD-02 Waiver**: Recognizing that `PROP-INV-001` (7-bucket inventory conservation), `META-FEE-001` (fee monotonicity), and `HIST-REPLAY-001` (canonical SS304 pack-of-10 clamp fixture landed cost ₹38.21) represent essential invariants for the commercial arbitrage vertical slice, all three tests were fully implemented and verified in `Market-HFT-OS` (`tests/acceptance/suite07_financial_engine.test.ts`), expanding the verified baseline to **161 passed tests across 19 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8.
   - **Tripartite Evidence Separation**: Strictly preserves evidence files across 3 lifecyle baselines:
     1. *Gate M3 Closure Baseline*: Anchored at `0ee073eccda1470ece5a05804aabcf311a540a61` (`0ee073e`) in `Market-HFT-OS` and `3daed5299fecee3549c02f7dafbeedb8eddeec60` (`3daed52`) in `ADRs` via tag `POC-001-Gate-M3-Verified`. Evidence file `POC-001_Gate_M3_Test_Execution_Results.json` (SHA-256: `2A67460967C339D290C925396F321B59753A9A6AD73034162962D439BC2E1434`, 158 tests) and `POC-001_Gate_M3_Typecheck_Execution_Results.txt` remain permanently intact.
     2. *Post-M3 Maintenance Baseline*: Codified under Decision OD-03 at commit `80c4bfd95420584ef66dfe5429e5e2fd0b02e10d` (`80c4bfd`) in `Market-HFT-OS`, achieving `0 vulnerabilities` in `npm audit` with exact pins.
     3. *Pre-M4 Conformance Baseline*: Established under Decision OD-04 at commit `cf0faf19024d40236fec372bbdfb105beebd9441` (`cf0faf1`) in `Market-HFT-OS`, accompanied by dedicated evidence files `POC-001_Pre_M4_Conformance_Test_Execution_Results.json` (SHA-256: `2BD75AE3EB2A8E9F2A2629315499896B314F2BB307790BA9FAC436A7BB9B7FEC`, 161 tests) and `POC-001_Pre_M4_Typecheck_Execution_Results.txt`.
   - **Zero Outstanding Waivers**: 100% of the 111 normative tests across Frozen Spec §8.1 and §8.2 are implemented and verified. Gate M4 acceptance specification is formally proposed and frozen for owner review.

8. **Project Owner Decision OD-05 (Gate M4 Specification Freeze & Bounded Vertical Slice Authorization)**:
   - **Specification Freeze**: Formally froze `POC-001_Gate_M4_Acceptance_Specification.md` and `POC-001_Gate_M4_SS304_Vertical_Slice_Test_Scenario.md` as `FROZEN / AUTHORIZED (OD-05)`, mandating the five core financial and operational invariants.
   - **Bounded Implementation**: Implemented `M4ResearchAllocationEngine` (`src/research/m4VerticalSlice.ts`) and acceptance test suite `suite20_m4_ss304_vertical_slice.test.ts` (8 passed tests), expanding the verified baseline to **169 passed tests across 20 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8.
   - **Dedicated Evidence Partitioning**: Generated dedicated Gate M4 evidence files: `POC-001_Gate_M4_Test_Execution_Results.json` (SHA-256: `04A7BAA3497DD138BCD3CF901D9EBB35515EFA4A05A7B8BC5BC1AC4C6DF2A0C7`), `POC-001_Gate_M4_Typecheck_Execution_Results.txt`, and `POC-001_Gate_M4_Vertical_Slice_Conformance_Report.md`.
   - **Out-of-Scope Integrity**: Strictly preserves all boundaries: zero real-money capital execution, zero autonomous agent capital authority, zero LLMs in financial calculations, zero cloud sprawl, and zero multi-strategy expansion.
   - Gate M4 is authoritatively confirmed as **APPROVED / CLOSED**.

9. **Project Owner Decision OD-06 (Gate M4.1 Statutory Math Remediation & Governed Formula Registry / RAG Bootstrap)**:
   - **Statutory Math Remediation (MATH-01–MATH-04)**:
     1. *MATH-01 (18% GST on Marketplace Fees)*: Computed `marketplaceFeeGstSubunits = (totalMarketplaceFeesSubunits * ops.gst_rate_bps) / 10000n` (₹7.1550 in Scenario A), deducted from `netMarketplaceDisbursementSubunits` and added to `itcSubunits` in the GST Electronic Credit Ledger.
     2. *MATH-02 (Ex-GST Base for Sec 52 TCS & Sec 194-O TDS)*: Restructured statutory withholding to compute TCS (1%) and TDS (1%) on the net taxable ex-GST revenue base (`889830n` = ₹88.9830), yielding exactly ₹0.8898 (`8898n`) each.
     3. *MATH-03 (Non-Fungible Separation of GST and Income Tax)*: Enforced strict non-fungibility between GST and Income Tax. Only Section 52 CGST TCS offsets Output GST liability in the GST Electronic Cash Ledger (`netGstSettlementSubunits = netGstCashLiability - tcsSubunits = 21435n` = ₹2.1435). Section 194-O TDS remains an explicit income-tax withholding holdback until annual filing.
     4. *MATH-04 (Supplier Trade Credit Terms in CCC)*: Incorporated `payment_terms_days` into `cccDays = Math.max(1, lead + dwell + disbDelay - paymentTerms)`. Set `payment_terms_days: 0` for Scenario A (advance EXW payment on MOQ) to earn 35-day CCC, and verified that positive supplier credit (`payment_terms_days = 15`) shortens CCC to 20 days and expands RoWC to 698.97%.
   - **Governed Formula Registry & Local BM25 RAG Retriever (`src/research/formulaRegistry.ts`)**:
     - Bootstrapped Formula Knowledge Base indexing 5 canonical Gate M4 formulas (`FIN-LANDED-COST-001`, `FIN-MKT-FEES-GST-002`, `FIN-STATUTORY-TCS-TDS-003`, `FIN-RETURN-ATTRITION-004`, `FIN-CCC-ROWC-005`) under RFC 8785 JCS cryptographic integrity digests.
     - Implemented deterministic Okapi BM25 keyword/semantic search over statutory citations, symbolic ASTs, and invariant rationales (`retrieveFormulas("Section 194-O TDS GST offset")` returns `FIN-STATUTORY-TCS-TDS-003` as top result).
     - Enforced dual-tier promotion architecture: UI/LLM-proposed formulas reside in `CANDIDATE_UI_MODEL` and fail closed (`E-ERR-GOV-001`) if executed in production without explicit owner promotion (`promoteCandidateFormula`).
   - **Evidence Separation & Test Baseline**:
     - Expanded Suite 20 to 11 tests (adding `M4-STATUTORY-MATH-009`, `M4-FORMULA-REGISTRY-RAG-010`, `M4-FORMULA-GOVERNANCE-ISOLATION-011`).
     - Full test baseline expanded to **172 passed tests across 20 suites (0 skipped, 0 failed)** on live PostgreSQL 16.8 (`localhost:5432`).
     - Dedicated Gate M4.1 evidence files generated: `POC-001_Gate_M4_1_Test_Execution_Results.json` (SHA-256: `0BA7C517DE32287309599DE54017E8E0FF4918514A4DBC0B5F37D48BF34863D1`) and `POC-001_Gate_M4_1_Typecheck_Execution_Results.txt` (SHA-256: `AEBAE79954369EA1B651A8917EAF32B981FAF5AE6387EA4A3F21B15B551DF58E`).
   - Gate M4.1 status is authoritatively confirmed as **APPROVED / CLOSED**.
