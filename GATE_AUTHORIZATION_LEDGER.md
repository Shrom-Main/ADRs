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
| **Gate M4.2** | 2026-10-16 | Project Owner (`Decision OD-07`) | `Market-HFT-OS: 3eb11ca`<br>`ADRs: current` | Groq-backed LLM formula discovery and refinement module (`src/research/llmFormulaAdvisor.ts`); sandboxed `CANDIDATE_UI_MODEL` tier; offline fallback; Suite 20 (14/14 passed); 20 suites / 175 tests passed. | **APPROVED / CLOSED** |
| **Gate M5** | 2026-10-16 | Project Owner (`Decision OD-09`) | `Market-HFT-OS: cba9554` (Tag: `POC-001-Gate-M5-Verified`)<br>`ADRs: 5688ed7` (Tag: `POC-001-Gate-M5-Verified`) | 6-Channel Signal Bus & 4D Evidence Architecture (`src/research/m5SignalAndEvidenceEngine.ts`), 9-Stage Deep Research DAG, 6-status return vocabulary, and Silo vs. Simultaneous Group Strategy Simulator (`src/research/m5SiloAndGroupSimulator.ts`); SS304 DIN 3017 matrix (4 sizes x 2 packs), ₹50,000 treasury budget, correlated LME steel shock, T-Bill sweep, Conviction vs Allocation separation firewall, and trading-chart JCS attestation; Suite 21 (7/7 passed); 21 suites / 185 tests passed against live PostgreSQL 16.8. | **APPROVED / CLOSED** |
| **Gate M6** | 2026-10-16 | Project Owner (`Decision OD-10`) | `Market-HFT-OS: 6bafb16` (Tag: `POC-001-Gate-M6-Verified`)<br>`ADRs: commit companion` (Tag: `POC-001-Gate-M6-Verified`) | Governed multi-agent research ecosystem (`src/agents/m6AgentFramework.ts`), TinyFish scoped browser sub-agent, specialist swarm (Media/Chatter, Macro/Lateral, Govt/Tax, RedTeam), 24x7 scheduler and manager orchestrator, and bitemporal decision replay & restatement engine; Suite 22 (7/7 passed); 22 suites / 192 tests passed against live PostgreSQL 16.8. | **APPROVED / CLOSED** |
| **Gate M6.1** | 2026-10-17 | Project Owner (`Decision OD-11`) | `Market-HFT-OS: 95ce444`<br>`ADRs: 75c0190` | Stage 0 Workspace & Charter Reconciliation; Stage 1 Capability-Aware MCP Substrate (`src/mcp/mcpSubstrate.ts`), JSON-RPC 2.0 tool envelopes, forbidden capability firewall, task-scoped immutable CapabilityGrant, McpCapabilityBroker (SSRF/private IP filter, 4-quota enforcement, GET only, redirect blocking), McpRunLedger (RFC 8785 JCS hash chains), conflict-preserving join (`joinSupplementaryClaims`), Bitemporal immutability & duplicate overwrite prevention (`E-ERR-BITEMPORAL-OVERWRITE`), genuine sub-agent scheduler invocations; Suite 23 (8/8 passed); 23 suites / 200 tests passed against live PostgreSQL 16.8. | **APPROVED / CLOSED** |
| **Gate M6.2** | 2026-10-17 | Project Owner (`Decision OD-12`) | `Market-HFT-OS: 8457ddd`<br>`ADRs: 3b5575b` | Stage 1 Surgical Hardening & Stage 2 Implementation: Micro-Agent #1 (`SourceCaptureWorker`), 6-Layer DOM Sanitization Sieve (`sanitizeHtmlDomSieve`), 4-Layer Prompt-Injection & Canary Defense (`InjectionCanaryGuard`), IndiaMART Deterministic Tiered MOQ Bracket Resolver (`resolveTieredMoqPrice`), zero-LLM BigInt subunit numeric extraction (`parseInrToSubunits`), hardcoded status ceiling (`UNVERIFIED`, `ADVERTISED_LISTING`/`SUPPLIER_QUOTE`), deterministic fixture replay & live HTTPS GET; Suite 24 (9/9 passed); 24 suites / 209 tests passed against live PostgreSQL 16.8. | **APPROVED / CLOSED** |
| **Gate M6.3** | 2026-10-18 | Project Owner (`Decision OD-13`) | `Market-HFT-OS: 711fcef`<br>`ADRs: 9b00ac6` | Stage 2 Surgical Polish (`ALLOWED_ATTRIBUTES` expansion, recursive `deepFreeze`), Tiered MOQ Batch Optimizer Integration (`evaluateOptimalBatchSize`), and Stage 3 Implementation: Micro-Agent #2 (`MediaAndChatterWorker`), read-only `mcp://media-corpus/fetch_transcript`, mandatory verbatim citation span verification (`verifyVerbatimCitationSpan`), empirical defect rate math (`observed_defect_rate_bps`), hardcoded 4D evidence ceiling (`UNVERIFIED`, `NOT_APPLICABLE`), prompt-injection defense (`QUARANTINED_INJECTION`), and trigger integration (`evaluateChatterSupplementTrigger`); Suite 25 (8/8 passed); 25 suites / 217 tests passed against live PostgreSQL 16.8. | **APPROVED / CLOSED** |
| **Gate M6.4** | 2026-10-18 | Project Owner (`Decision OD-14`) | `Market-HFT-OS: e0b6697`<br>`ADRs: a3bbb4b` | Stage 3 Surgical Polish (MCW-01 citation span SHA-256 validation, MCW-02 custom `SUBUNITS_INR` trigger support, MCW-03 unused import cleanup); Stage 4 Micro-Agent #3 (`MacroAndLateralMarketWorker`, `worker:macro-lateral:v1`), read-only `mcp://macro-feeds/query_series`, zero-default series ingestion, pure BigInt FX conversion & physical scrap floor derivation (`derivePhysicalScrapFloor`), Formula-RAG dynamic growth driver evaluation via `FormulaRegistry` pure-BigInt rational AST, Sustained Signal vs Fast Opportunity Regime Classifier (`OpportunityTemporalRegime`, Tactical Horizon Gate `E-MLW-EDGE-DECAYS-BEFORE-CASH-RECOVERY`), and empirical factor efficacy ledger (`FactorEfficacyLedger`); Suite 26 (8/8 passed); 26 suites / 225 tests passed against live PostgreSQL 16.8. | **APPROVED / CLOSED** |
| **Gate M6.5** | 2026-10-18 | Project Owner (`Decision OD-15`) | `Market-HFT-OS: 360fd07`<br>`ADRs: 28f5fdf` | Stage 5 Micro-Agent #4 (`GovtAndStatutoryWorker`, `worker:govt-statutory:v1`), read-only `mcp://policy-bulletins/fetch_circular`, immutable statutory citation verification (`verifyStatutoryCitation`), zero fabricated default tax parameters (`E-GSW-STATUTORY-CIRCULAR-REQUIRED`), MSME Section 43B(h) credit ceiling cross-check (`evaluateMsmePaymentTermLimit`, 45d with agreement / 15d without), FormulaRegistry non-mutation firewall (`proposeStatutoryFormulaCandidate`, fails closed with `E-ERR-GOV-002` if attempting to overwrite `PROMOTED_NORMATIVE` cards), prompt injection quarantine (`E-GSW-PROMPT-INJECTION-DETECTED`), and deterministic RFC 8785 JCS canonicalization; Suite 27 (8/8 passed); 27 suites / 233 tests passed against live PostgreSQL 16.8. | **APPROVED / CLOSED** |
| **Gate M6.6** | 2026-10-18 | Project Owner (`Decision OD-16`) | `Market-HFT-OS: 6053f3f`<br>`ADRs: current` | Stage 6 Micro-Agent #5 (`RedTeamAndConflictWorker`, `worker:red-team:v1`), read-only `mcp://audit-corpus/read_joined_claims` with zero network egress (`allowed_hosts: []`), 7 authoritative red-team rules (RT-01 physical scrap floor, RT-02 strict conflict preservation, RT-03 high return illusion, RT-04 metallurgy defect contradiction, RT-05 illegal MSME credit terms, RT-06 zero-cost substitution ban, RT-07 clock skew & TTL expiration), hard disposition ceiling (`HOLD_BLOCKED_BY_RED_TEAM`, `REQUIRES_SUPPLEMENTARY_CORROBORATION`, `ELIGIBLE_FOR_HUMAN_REVIEW` with `E-RTW-DISPOSITION-CEILING-BREACH` on `APPROVED_FOR_EXECUTION`), and Deterministic Context-Routing State Machine (`src/agents/scheduler/contextRoutingStateMachine.ts`) coordinating Pass 1 (Horizontal gap-filling), Pass 2 (Supplementary corroboration & join), and Pass 3 (Red-team audit & deterministic join); Suite 28 (8/8 passed); 28 suites / 241 tests passed against live PostgreSQL 16.8. | **APPROVED / CLOSED** |

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


10. **Project Owner Decision OD-07 (Gate M4.2 Groq-Backed LLM Formula Discovery & Refinement Module)**:
   - **Groq-Backed LLM Formula Advisor (`src/research/llmFormulaAdvisor.ts`)**:
     - Built `GroqFormulaAdvisor` module reading Groq credentials from `Groq_Key.env` or process environment.
     - Implemented `proposeFormulaRefinement(promptContext, existingFormula)` interacting with Groq inference API (`openai/gpt-oss-120b` or configurable models) to synthesize schema-compliant `FormulaCard` definitions (symbolic expression, subunit input variables, deterministic canonical test vectors).
     - Implemented graceful offline fallback simulation mode (`forceSimulated: true` or `GROQ_OFFLINE_MODE=true` or network timeouts) ensuring non-blocking execution across offline and CI test environments.
     - Implemented `evaluateLlmCandidate(cardInput, registry, customEvaluator)` automatically registering candidate formulas under the sandboxed `CANDIDATE_UI_MODEL` tier, deterministically executing test vectors via custom or compiled symbolic evaluators, and returning verifiable execution status.
   - **FormulaRegistry Expansion (`src/research/formulaRegistry.ts`)**:
     - Added `FormulaCardInput` and `FormulaEvaluatorFn` types.
     - Implemented `registerFormulaEvaluator(formulaId, fn)` and `hasEvaluator(formulaId)` allowing dynamic registration of compiled TypeScript BigInt evaluators for candidate formulas.
     - Implemented deterministic `evaluateSymbolicExpression` evaluator for arithmetic expressions with basis point division and floating-point intermediate precision before rounding to BigInt subunits.
     - Reinforced Governance Firewall: `CANDIDATE_UI_MODEL` formulas are strictly prohibited from executing in production mode (`evaluateFormula` throws `E-ERR-GOV-001`) or authorizing capital allocation until formally promoted to `PROMOTED_NORMATIVE` via authorized owner directive (`promoteCandidateFormula`).
   - **Acceptance Tests & Evidence Separation (`Suite 20`)**:
     - Added three normative acceptance assertions in `tests/acceptance/suite20_m4_ss304_vertical_slice.test.ts`:
       1. `M4-GROQ-CREDENTIALS-012`: Verified Groq API credential loading and validation from `Groq_Key.env` with fallback on invalid paths.
       2. `M4-GROQ-ADVISOR-PROPOSAL-013`: Verified candidate formula proposal generation for warehouse inventory shrinkage, customs anti-dumping duty, and normative formula refinement.
       3. `M4-GROQ-ADVISOR-EVAL-ISOLATION-014`: Verified sandboxed registration, test vector execution, BM25 RAG indexing, governance firewall fail-closed enforcement, and post-promotion production execution.
     - Full test baseline expanded to **175 passed tests across 20 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
     - Dedicated Gate M4.2 evidence files generated:
       - `POC-001_Gate_M4_2_Test_Execution_Results.json` (SHA-256: `FEDA66529346B2F0566C9402A19203B36C65B6CAF5588ED0634D680C72E44045`, 175 tests).
       - `POC-001_Gate_M4_2_Typecheck_Execution_Results.txt` (SHA-256: `4596FF7DF1A8F378190D49DBCDBD055A4CB69A39B5C5B32F3E263B81D07AFF96`, 0 errors).
   - Gate M4.2 status is authoritatively confirmed as **APPROVED / CLOSED**.


11. **Project Owner Decision OD-08 (Gate M4.3 RAG-First Sufficiency Gate, Asymptotic LLM Decay, Persistent Corpus & Pure BigInt Rational Evaluator)**:
   - **Pure BigInt Rational Arithmetic AST Evaluator (`src/research/formulaRegistry.ts`)**:
     - Eliminated all IEEE-754 `Number(...)`, `parseFloat(...)`, and `Math.round(...)` floating-point shortcuts from `evaluateSymbolicExpression` per Frozen Specification §1.3 and §6.1 (`AUDIT-45`).
     - Represented all AST nodes as exact rational pairs `{ num: bigint, den: bigint }` with deterministic GCD reduction and zero-division protection (`E-ERR-MATH-001`).
     - At the root of the AST, performed single half-up integer rounding in pure `BigInt`: `(num + den / 2n) / den`, enabling fractional basis point evaluation (e.g. `(Shrinkage_Rate / 10000)`) without premature integer truncation (`50n / 10000n = 0n`) or float precision drift on large subunit values (`> Number.MAX_SAFE_INTEGER`).
     - Upgraded `FIN-CCC-ROWC-005` in `evaluateFormula` to pure `BigInt` evaluation.
   - **Persistent Corpus Storage & Deterministic Appends (`FormulaRegistry`)**:
     - Added file-backed persistence via `saveCorpusToFile(filePath)` and `loadCorpusFromFile(filePath)`, verifying RFC 8785 JCS hashes on load to guarantee cross-session cryptographic integrity.
     - Implemented `appendDeterministicFormula(cardInput, options)` allowing programmatic registration of deterministic formula rules with zero LLM involvement, immediately validating test vectors via the pure BigInt rational evaluator and indexing cards into the BM25 corpus.
   - **3-Tier "RAG-First, LLM-Last" Orchestrator & Asymptotic LLM Decay Flywheel (`src/research/llmFormulaAdvisor.ts`)**:
     - Implemented `resolveOrSynthesizeFormula(request, registry)` enforcing strict 3-tier routing:
       1. *Tier 1 (`RAG_CACHE_HIT`, `llm_called: false`)*: Queries local BM25 RAG index (`topK: 3`). If top match score meets `min_bm25_score` (default `1.5`) and satisfies all `required_variables`, immediately returns the existing `FormulaCard` without calling Groq.
       2. *Tier 2 (`DETERMINISTIC_APPEND`, `llm_called: false`)*: If deterministic card input is supplied, validates test vector, indexes card into registry, and returns immediately without calling Groq.
       3. *Tier 3 (`LLM_RAG_REFINED_SYNTHESIS`, `llm_called: true`)*: Only on Tier 1 and Tier 2 miss, invokes Groq inference. Injects top-3 closest BM25 neighbor cards into prompt context as structural and domain context, instructing LLM to reuse canonical variable naming/scaling conventions and synthesize only the missing delta. Auto-registers and validates the resulting candidate card in `registry` so subsequent queries hit Tier 1 (`RAG_CACHE_HIT`).
     - Cumulative telemetry tracking in `getTelemetry()`: `{ total_requests, rag_cache_hits, deterministic_appends, llm_calls_invoked, llm_dependency_ratio_bps }`, proving monotonic asymptotic decay of LLM dependency toward zero as the RAG corpus expands.
   - **Acceptance Tests & Evidence Separation (`Suite 20`)**:
     - Added three normative acceptance assertions in `tests/acceptance/suite20_m4_ss304_vertical_slice.test.ts`:
       1. `M4-PURE-BIGINT-RATIONAL-AST-015`: Proves pure BigInt rational evaluation of fractional bps on large subunit values (`9007199254740993500n > Number.MAX_SAFE_INTEGER`) without precision loss.
       2. `M4-RAG-FIRST-SUFFICIENCY-GATE-016`: Proves existing concepts (`Section 194-O TDS / Section 52 TCS`, `SS304 landed cost EXW`) resolve via `RAG_CACHE_HIT` (`llm_called: false`) and deterministic rule additions resolve via `DETERMINISTIC_APPEND` (`llm_called: false`).
       3. `M4-ASYMPTOTIC-LLM-DECAY-FLYWHEEL-017`: Multi-step lifecycle proving novel metric LLM synthesis (`Customs anti-dumping duty and port demurrage drag`, `llm_called: true`), RAG neighbor context injection (`FIN-LANDED-COST-001`), subsequent 5-query cache hit sequence dropping LLM dependency ratio from 10,000 bps to 1,667 bps, and persistent corpus file reload.
     - Full test baseline expanded to **178 passed tests across 20 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
     - Dedicated Gate M4.3 evidence files generated:
       - `POC-001_Gate_M4_3_Test_Execution_Results.json` (SHA-256: `1F88EDD3B1DF18D49B4EF7E004E46510871A81A380062559DB9825A77B024EE1`, 178 tests).
       - `POC-001_Gate_M4_3_Typecheck_Execution_Results.txt` (SHA-256: `4596FF7DF1A8F378190D49DBCDBD055A4CB69A39B5C5B32F3E263B81D07AFF96`, 0 errors).
   - Gate M4.3 status is authoritatively confirmed as **APPROVED / CLOSED**.

12. **Project Owner Decision OD-09 (Gate M5 6-Channel Signal Bus, 4D Evidence Architecture & Silo vs. Group Strategy Simulator)**:
    - **Stage 3 Specification Freeze**:
      - Drafted and froze `POC-001_Gate_M5_Signal_Bus_and_Group_Simulation_Specification.md` (status: `FROZEN / AUTHORIZED (OD-09)`).
      - Mandated the 4 orthogonal evidence dimensions (`evidence_kind`, `verification_status`, `commercial_status`, `provenance_lineage`), 6-channel continuous signal bus, 9-stage "Deep Research Pro" DAG pipeline contract, 6-status return vocabulary, and Silo vs. Simultaneous Group simulation architecture.
    - **6-Channel Signal Bus & 4D Evidence Engine (`src/research/m5SignalAndEvidenceEngine.ts`)**:
      - Implemented 4D evidence dimensions and fail-closed promotion state machine (`EvidencePromotionEngine`), strictly prohibiting `ADVERTISED_LISTING` or `SYNTHETIC_SCENARIO` from auto-promoting to `VERIFIED_EXECUTABLE_OFFER` without cryptographic signature attestation or multi-source corroboration (`E-ERR-EV-001`).
      - Implemented `SignalNormalizer` mapping testable signals across 6 channels (`NEWS_TRADE_PRESS`, `YOUTUBE_VIDEO_TRANSCRIPT`, `SOCIAL_FORUM_CHATTER`, `MACROECONOMIC_INDICATOR`, `LATERAL_FINANCIAL_MARKET`, `GOVERNMENT_SCHEME_POLICY`) into structured economic shocks with RFC 8785 JCS hashes.
      - Implemented 6-status return resolver (`resolveReturnStatus`) distinguishing `CANNOT_CALCULATE_MISSING_INPUTS`, `INSUFFICIENT_UNVERIFIED_EVIDENCE`, `NO_ROOT_FOUND_IN_SEARCH_DOMAIN`, `OPEN_POSITION`, and `NOT_YET_RECOVERED` from `VALID_CALCULATED_RETURN`.
      - Implemented `DeepResearchPipelineOrchestrator` executing the 9-stage DAG contract (`DECOMPOSE` $\to$ `ROUTE` $\to$ `ASSEMBLE_CONTEXT` $\to$ `PROMPT` $\to$ `EXECUTE_SCOPED_WORKER` $\to$ `REVIEW_RED_TEAM` $\to$ `ASSEMBLE_EVIDENCE` $\to$ `POLISH` $\to$ `PRESENT`).
    - **Silo vs. Simultaneous Group Strategy Simulator (`src/research/m5SiloAndGroupSimulator.ts`)**:
      - Implemented `M5SiloAndGroupSimulator`:
        * *Silo Mode*: Evaluates SS304 DIN 3017 clamps across the 4-diameter x 2-pack matrix (8 variants), emitting price & breakeven bands, 35-day cash-flow J-curve waterfalls, and Arbitrage Greeks ($\Delta$: price sensitivity, $\Theta$: time decay, $\mathcal{V}$: return drag).
        * *Simultaneous Group Mode*: Evaluates cohorts under ₹50,000 treasury budget, correlated lateral shocks (e.g. $+10\%$ LME stainless steel raw material surge), single-SKU concentration caps ($\le 50\%$), discrete MOQ integer lot-sizing, sovereign 91-Day T-Bill sweeps, and benchmark comparisons (`RBI_91D_TBILL` at 650 bps and `NIFTY_LIQUID_BENCHMARK` at 680 bps).
        * *Conviction vs. Allocation Firewall*: Enforces that unverified listings (`ADVERTISED_LISTING`, `UNVERIFIED`) receive strictly ₹0 capital regardless of theoretical margins, generating bubble chart telemetry coordinates $(X, Y, Z)$.
    - **Acceptance Tests & Evidence Separation (`Suite 21`)**:
      - Implemented `tests/acceptance/suite21_m5_silo_group_and_signals.test.ts` (7 passed assertions):
        1. `M5-4D-EVIDENCE-ORTHOGONALITY-001`: 4D evidence dimensions and fail-closed promotion firewall.
        2. `M5-SIX-CHANNEL-SIGNAL-INGEST-002`: 6-channel signal normalization & 9-stage DAG pipeline.
        3. `M5-SIX-STATUS-VOCABULARY-003`: 6-status return vocabulary preventing 0% collapse.
        4. `M5-SILO-PACK-SIZE-MATRIX-004`: SS304 DIN 3017 matrix (4 sizes x 2 packs), price bands, J-curves, Greeks.
        5. `M5-SIMULTANEOUS-GROUP-CORRELATION-005`: Portfolio allocation, LME steel shock, T-Bill sweep, conservation.
        6. `M5-CONVICTION-VS-ALLOCATION-SEPARATION-006`: Firewall rejecting unverified listings (₹0 capital).
        7. `M5-TRADING-CHART-JCS-DETERMINISM-007`: Bit-for-bit RFC 8785 JCS telemetry attestation.
    - **Full Baseline Conformance**:
      - Full test baseline expanded to **185 passed tests across 21 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
      - Dedicated Gate M5 evidence files generated:
        - `POC-001_Gate_M5_Test_Execution_Results.json` (SHA-256: `2C1FF1854228C4447D9F7BF500A6511727CD60ECF6EC4ACAB976FF151BE1A78B`, 185 tests).
        - `POC-001_Gate_M5_Typecheck_Execution_Results.txt` (SHA-256: `2E4823FBA10769EA72EB0937EF1AF01D144509845F2E4B2BE022E9FC52EDAF2D`, 0 errors).
    - Gate M5 status is authoritatively confirmed as **APPROVED / CLOSED**.

13. **Project Owner Decision OD-10 (Gate M6 Governed Multi-Agent Research Ecosystem, TinyFish Browser Sub-Agents & Bitemporal Replay Engine)**:
    - **Stage 3 Specification Freeze**:
      - Drafted and froze `POC-001_Gate_M6_Multi_Agent_and_Bitemporal_Replay_Specification.md` (status: `FROZEN / AUTHORIZED (OD-10)`).
      - Mandated worker contract manifests and permission boundaries (`READ_ONLY_DISCOVERY`, `SANDBOX_MODELING`, `RED_TEAM_AUDIT`), deterministic resource accounting, TinyFish scoped DOM scraping with missing-data classification (`DATA_REQUIRED` vs `DATA_INSUFFICIENT`), zero-cost substitution prohibition, specialist sub-agent swarm (Media/Chatter, Macro/Lateral, Govt/Tax, RedTeam), 24x7 manager orchestrator with degraded-mode resilience, and bitemporal historical decision replay and restatement.
    - **Multi-Agent Research Framework & Bitemporal Engine (`src/agents/m6AgentFramework.ts`)**:
      - Implemented `AgentSecurityFirewall` strictly prohibiting agent workers from mutating `PaperLedger` or `ActualsLedger` (`E-M6-PERMISSION-DENIED`) and enforcing deterministic token/request quotas (`E-M6-QUOTA-EXCEEDED`).
      - Implemented `TinyFishScopedBrowserAgent` computing SHA-256 `dom_snapshot_hash`, extracting structured marketplace/supplier fields, classifying missing attributes as `DATA_REQUIRED` (never substituting `₹0`), and capping commercial status at `ADVERTISED_LISTING`.
      - Implemented specialist swarm: `MediaAndChatterSubAgent`, `MacroAndLateralMarketSubAgent`, `GovtSchemeAndTaxSubAgent`, and adversarial `RedTeamReviewerSubAgent` (quarantining offers below raw scrap metal floor cost or with metallurgy defects).
      - Implemented `ResearchSchedulerAndManager` coordinating the 9-stage research workflow (`DECOMPOSE` $\to$ `ROUTE` $\to$ `ASSEMBLE_CONTEXT` $\to$ `PROMPT` $\to$ `EXECUTE_SCOPED_WORKER` $\to$ `REVIEW_RED_TEAM` $\to$ `ASSEMBLE_EVIDENCE` $\to$ `POLISH` $\to$ `PRESENT`) with degraded-mode resilience under external timeouts.
      - Implemented `BitemporalRestatementEngine` capturing $t_0$ decisions (`decision_time_utc` and `knowledge_time_utc`), reconstructing historical baselines bit-for-bit, evaluating $t_1$ restatements against incoming evidence, and issuing `THESIS_INVALIDATED_HALT`, `EDGE_DECAY_WARNING`, or `THESIS_INTACT` without altering historical records.
    - **Acceptance Tests & Evidence Separation (`Suite 22`)**:
      - Implemented `tests/acceptance/suite22_m6_agent_swarm_and_bitemporal.test.ts` (7 passed assertions):
        1. `M6-TINYFISH-SCOPED-BROWSER-001`: DOM extraction, SHA-256 snapshot, ADVERTISED_LISTING cap, DATA_REQUIRED handling.
        2. `M6-SUBAGENT-SWARM-DECOMPOSE-002`: Multi-channel signal decomposition and 9-stage DAG execution.
        3. `M6-RED-TEAM-ADVERSARIAL-BLOCK-003`: Red team blocking of below-scrap-cost fraud and metallurgy defect quotes.
        4. `M6-AGENT-PERMISSION-AND-QUOTA-FIREWALL-004`: Fail-closed ledger access denial and token/request quota enforcement.
        5. `M6-DEGRADED-MODE-RESILIENCE-005`: Control plane degraded mode resilience during external worker timeout.
        6. `M6-BITEMPORAL-REPLAY-AND-RESTATEMENT-006`: Bit-for-bit historical t0 reconstruction and t1 restatement halting.
        7. `M6-END-TO-END-POLISH-AND-PRESENT-JCS-007`: RFC 8785 JCS determinism of research and restatement payloads.
    - **Full Baseline Conformance**:
      - Full test baseline expanded to **192 passed tests across 22 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
      - Dedicated Gate M6 evidence files generated:
        - `POC-001_Gate_M6_Test_Execution_Results.json` (SHA-256: `A74A2AB274C4E7670A7158CE03584B6692051BC8D7C8314D7E754C67D3BC14DE`, 192 tests).
        - `POC-001_Gate_M6_Typecheck_Execution_Results.txt` (SHA-256: `2E4823FBA10769EA72EB0937EF1AF01D144509845F2E4B2BE022E9FC52EDAF2D`, 0 errors).
    - Gate M6 status is authoritatively confirmed as **APPROVED / CLOSED**.
 
14. **Project Owner Decision OD-11 (Stage 0: Reconciliation & Stage 1: Gate M6.1 Capability-Aware MCP Substrate & Read-Only Micro-Agent Broker)**:
    - **Stage 0: Workspace Cleanup & Governance Reconciliation**:
      - Restored clean baseline across `Market-HFT-OS` and `ADRs`, eliminating uncommitted drift.
      - Extracted `D:\ADRs\ADRXX3.pdf` (46 pages, 201,353 characters), confirming it as the rendered archive of `POC-001 — Gate M1 Design-Readiness Specification v1.13 Final` with closure evidence for AUDIT-01 through AUDIT-52.
      - Updated `PROJECT_CHARTER.md` to v0.2.5, establishing Gates M6.1–M6.8 MCP Broker & Micro-Agent Framework with strict read-only and human-authorized capital boundaries.
    - **Stage 1: Capability-Aware MCP Substrate (`src/mcp/mcpSubstrate.ts`)**:
      - Implemented typed JSON-RPC 2.0 / MCP tool schema envelopes (`McpToolDescriptor`, `McpToolCallRequest`, `McpToolCallResponse`).
      - Implemented `McpServerAdapter` with runtime schema validation and hard firewall blocking forbidden capabilities: shell, SQL, ledger mutation, evidence promotion, order routing, and secrets (`E-MCP-FORBIDDEN-CAPABILITY`).
      - Implemented `CapabilityGrant` with deep freeze (`Object.freeze`), scoping allowed tools, hosts, allowed methods (`GET` only), and redirect blocking (`E-MCP-REDIRECT-DENIED`).
      - Implemented `McpCapabilityBroker` with deterministic SSRF and private/loopback/metadata IP blocking (`127.0.0.0/8`, `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`, `169.254.169.254`, `localhost`, `0.0.0.0`, `::1`), and 4-quota enforcement on every call (`requests_made`, `wall_clock_ms`, `payload_bytes`, `tokens_used`).
      - Implemented `McpRunLedger` with append-only hash chains under RFC 8785 JCS canonicalization.
      - Implemented `joinSupplementaryClaims` preserving multi-source agreement (`CROSS_SOURCE_CORROBORATED`) and disagreement (`CONFLICT`) without averaging, voting, or guessing.
    - **Stage 1: M6 Engine Hardening & Sub-Agent Wiring (`src/agents/m6AgentFramework.ts`)**:
      - Hardened `BitemporalRestatementEngine` to deep-clone and `deepFreeze` all records and inputs, reject duplicate decision overwrites fail-closed (`E-ERR-BITEMPORAL-OVERWRITE`), and support distinct decision time ($t_d$) and knowledge time ($t_k$).
      - Connected `GovtSchemeAndTaxSubAgent` and `RedTeamReviewerSubAgent` genuinely into `ResearchSchedulerAndManager` execution ticks, and provided `executeResearchTickAsync` integrating `GroqFormulaAdvisor.resolveOrSynthesizeFormula`.
    - **Acceptance Tests & Evidence Separation (`Suite 23`)**:
      - Implemented `tests/acceptance/suite23_m6_1_mcp_substrate_and_broker.test.ts` (8 passed assertions):
        1. `MCP-SUBSTRATE-SCHEMA-AND-FORBIDDEN-TOOLS-001`: JSON-RPC 2.0 envelopes & forbidden capability rejection.
        2. `MCP-BROKER-CAPABILITY-AND-HOST-POLICY-002`: Frozen CapabilityGrant & host/method/redirect policy enforcement.
        3. `MCP-BROKER-SSRF-PRIVATE-IP-BLOCK-003`: Hard SSRF & private IP / loopback / metadata egress blocking.
        4. `MCP-BROKER-MULTI-QUOTA-ENFORCEMENT-004`: Deterministic enforcement of all 4 resource quotas.
        5. `MCP-RUN-LEDGER-HASH-CHAIN-005`: RFC 8785 JCS hash-chained execution run ledger.
        6. `MCP-SUPPLEMENTARY-CONFLICT-JOIN-006`: Conflict-preserving supplementary claims join.
        7. `MCP-BITEMPORAL-IMMUTABILITY-PROOF-007`: Bitemporal deepFreeze immutability & duplicate overwrite prevention.
        8. `MCP-SCHEDULER-FULL-WORKER-INVOCATION-008`: Genuine subagent execution & RFC 8785 JCS telemetry.
    - **Full Baseline Conformance**:
      - Full test baseline expanded to **200 passed tests across 23 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
      - Dedicated Gate M6.1 evidence files generated:
        - `POC-001_Gate_M6_1_Test_Execution_Results.json` (SHA-256: `F914CF559382AD74A5910224AE1A035AC90AD30CABB708DE52640EBA00096DBB`, 200 tests).
        - `POC-001_Gate_M6_1_Typecheck_Execution_Results.txt` (SHA-256: `2E4823FBA10769EA72EB0937EF1AF01D144509845F2E4B2BE022E9FC52EDAF2D`, 0 errors).
    - Gate M6.1 status is authoritatively confirmed as **APPROVED / CLOSED**.

15. **Project Owner Decision OD-12 (Gate M6.2 Stage 1 Surgical Hardening & Stage 2 SourceCaptureWorker Closure)**:
    - **Stage 1 Surgical Hardening (`src/mcp/mcpSubstrate.ts`)**:
      1. *Protocol Scheme & IPv6 SSRF Hardening (`validateHostAndSsrf`)*: Permits exclusively `https:` and `mcp:` schemes, rejecting `http:`, `file:`, `ftp:`, `data:`, `ws:`, and all others with `E-MCP-SCHEME-DENIED`. Expanded SSRF IP filter to block IPv4-mapped IPv6 (`::ffff:`), IPv6 ULA (`f[cd]..:`), IPv6 link-local (`fe80:`), and unwhitelisted raw IP literals (`E-MCP-HOST-OR-SSRF-DENIED`).
      2. *Timer Cleanup (`invokeTool`)*: Captured `setTimeout` handle and enclosed `Promise.race([execPromise, timeoutPromise])` in `try { ... } finally { if (timerHandle) clearTimeout(timerHandle); }`, eliminating dangling event loop timer handles.
      3. *Argument Type Validation (`validateArguments`)*: Validates runtime argument property types (`string`, `number`, `boolean`, `object`, `array`) against declared JSON Schema types, throwing `E-MCP-INVALID-ARGUMENTS` on mismatch.
      4. *Deterministic Ordering & Immutability (`joinSupplementaryClaims`)*: Deterministically sorts `sources` and `conflicting_values` and deeply freezes all returned claim structures with `Object.freeze`.
    - **Stage 2: Micro-Agent #1 SourceCaptureWorker (`src/agents/workers/sourceCaptureWorker.ts`)**:
      - Implemented `SourceCaptureWorker` (`worker:source-capture:v1`) routing read-only requests exclusively through `McpCapabilityBroker.invokeTool` under task-scoped `CapabilityGrant`.
      - Registered `mcp://source-capture/http_get_snapshot` on `McpServerAdapter` supporting deterministic `RECORDED_FIXTURE_REPLAY` and live `APPROVED_LIVE_HTTPS_GET` with `redirect: 'error'`.
      - Implemented 6-Layer DOM Sanitization Sieve (`sanitizeHtmlDomSieve`):
        * *Layer 1*: 512KB cap (`E-MCP-PAYLOAD-TOO-LARGE`), null-byte rejection (`E-SCW-NULL-BYTE-DETECTED`), and raw SHA-256 calculation.
        * *Layer 2*: Purges executable & active tag subtrees (`<script>`, `<style>`, `<iframe>`, `<form>`, `<input>`, etc.), event handlers (`on*`), and `javascript:`/`data:`/`vbscript:` URIs.
        * *Layer 3*: Purges HTML comments (`<!-- ... -->`) and cloaked/hidden nodes (`hidden`, `aria-hidden="true"`, `display:none`, `visibility:hidden`, `opacity:0`, `font-size:0`, `width:0`, `height:0`, `left:-9999px`, `top:-9999px`, `color:transparent`) using depth-tracked iterative parsing.
        * *Layer 4*: Retains structural selector attributes only (`id`, `class`, `data-asin`, `data-sku`, `data-price`, `data-moq`, `data-min-qty`, `data-max-qty`, `itemprop`, `href`), stripping free-text and LLM prompt smuggling attributes.
        * *Layer 5*: Normalizes text to Unicode NFC, strips zero-width and BiDi control characters (`\u200B-\u200F`, `\uFEFF`), and rejects fullwidth/Cyrillic homographs in price contexts (`E-SCW-HOMOGRAPH-DETECTED`).
        * *Layer 6*: Collapses redundant whitespace and computes canonical `sanitized_dom_sha256`.
      - Implemented 4-Layer Prompt-Injection & Canary Defense (`InjectionCanaryGuard`):
        * *Zero-LLM Numeric Extraction*: Deterministic BigInt subunit parser (`parseInrToSubunits`) strictly banning zero/0n substitution on missing or non-numeric costs (`status: 'DATA_REQUIRED'`, `E-SCW-MANDATORY-COST-MISSING`).
        * *IndiaMART Deterministic Tiered MOQ Bracket Resolver (`resolveTieredMoqPrice`)*: Parses quantity-slab rows into `PriceBracketTier` arrays and selects exact unit-price bracket for `target_batch_quantity` (`expected_type: 'TIERED_SUBUNITS_INR'`). Fails closed with `DATA_REQUIRED` (`E-SCW-BELOW-MINIMUM-TIER-MOQ`) when below minimum supplier tier, and with `PARSE_REJECTED` (`E-SCW-AMBIGUOUS-TIER-BRACKET`) on overlapping/ambiguous slabs.
        * *Lexical & Domain Canary Scanner*: Scans for instruction overrides, role/ChatML delimiters, domain enum spoofing literals (`VERIFIED_EXECUTABLE_OFFER`, `ALLOCATE_CAPITAL`, `CROSS_SOURCE_CORROBORATED`, `ACTUALS_LEDGER`, `PROMOTED_NORMATIVE`), and internal URI smuggling, quarantining captures with `E-SCW-PROMPT-INJECTION-DETECTED`.
        * *Hardcoded Status Ceiling*: Enforces strict output ceilings (`verification_status: 'UNVERIFIED'`, `commercial_status: 'ADVERTISED_LISTING' | 'SUPPLIER_QUOTE'`), throwing `E-SCW-STATUS-ESCALATION-FORBIDDEN` on elevation attempts.
        * *Cryptographic Spotlighting*: Encloses extracted text in nonce-delimited tags (`<untrusted_dom_field_${nonce}>...`).
    - **Acceptance Tests & Evidence Separation (`Suite 24`)**:
      - Implemented `tests/acceptance/suite24_m6_2_source_capture_worker.test.ts` (9 passed assertions):
        1. `MCP-SCW-CLEAN-EXTRACT-001`: Clean extraction on Amazon India (`1050000`) and Howrah Supplier (`250000`) with distinct raw vs sanitized DOM hashes and status ceiling.
        2. `MCP-SCW-MISSING-FIELD-NO-ZERO-002`: Missing freight or non-numeric string returns `DATA_REQUIRED` with `E-SCW-MANDATORY-COST-MISSING` and never substitutes 0 or 0n.
        3. `MCP-SCW-HIDDEN-DOM-CLOAKING-003`: Layer 3 strips cloaked hidden nodes and HTML comments, extracting exact visible ₹38.21 (`382100`).
        4. `MCP-SCW-PROMPT-INJECTION-CANARY-004`: Canary scanner triggers `E-SCW-PROMPT-INJECTION-DETECTED` on adversarial overrides and domain spoofing.
        5. `MCP-SCW-HOST-METHOD-REDIRECT-SCHEME-005`: Broker blocks `file://`, `http://`, `POST`, unapproved hosts, and redirects (`E-MCP-SCHEME-DENIED`, `E-MCP-METHOD-DENIED`, `E-MCP-HOST-OR-SSRF-DENIED`, `E-MCP-REDIRECT-DENIED`).
        6. `MCP-SCW-SSRF-IPV6-AND-OVERSIZE-006`: Broker blocks `127.0.0.1`, IPv4-mapped IPv6, IPv6 ULA, and payloads $> 524,288$ bytes (`E-MCP-PAYLOAD-TOO-LARGE`).
        7. `MCP-SCW-UNICODE-HOMOGRAPH-007`: Layer 5 strips zero-width chars (`₹3\u200B8.21` -> `382100`) and rejects fullwidth/Cyrillic homographs (`E-SCW-HOMOGRAPH-DETECTED`).
        8. `MCP-SCW-INDIAMART-TIERED-MOQ-008`: Tests IndiaMART B2B tiered quantity-slab pricing (100-249 @ ₹31.00, 250-499 @ ₹28.50, 500+ @ ₹25.00), selecting '250000' at 500, '285000' at 300, failing closed with DATA_REQUIRED (`E-SCW-BELOW-MINIMUM-TIER-MOQ`) at 50, and PARSE_REJECTED (`E-SCW-AMBIGUOUS-TIER-BRACKET`) on overlapping brackets.
        9. `MCP-SCW-REPRODUCIBLE-JCS-009`: Bit-for-bit reproducible JCS response and SHA-256 digest with monotonic hash-chained `McpRunLedger`.
    - **Full Baseline Conformance**:
      - Full test baseline expanded to **209 passed tests across 24 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
      - Dedicated Gate M6.2 evidence files generated:
        - `POC-001_Gate_M6_2_Test_Execution_Results.json` (SHA-256: `F63A2E0EA984ADB6915B7DE6405F8E34A2512D2C4023FA7BF1BE6A97173B8EDD`, 209 tests).
        - `POC-001_Gate_M6_2_Typecheck_Execution_Results.txt` (SHA-256: `6267F8C0BFB93AA18DB8139A5B057D2D04539B3E1966835187870369E796C495`, 0 errors).
    - Gate M6.2 status is authoritatively confirmed as **APPROVED / CLOSED**.

15. **Project Owner Decision OD-13 (Stage 2 Surgical Polish, Tiered Batch Optimizer Integration & Stage 3 Micro-Agent #2 `MediaAndChatterWorker` Closure)**:
    - **Stage 2 Surgical Polish**:
      1. *Custom Attributes Allowlist*: Added `'data-pack'`, `'data-freight'`, `'data-material'`, `'data-size'`, and `'data-hsn'` to `ALLOWED_ATTRIBUTES` in `src/agents/workers/sourceCaptureWorker.ts` so attribute selectors in `getDefaultExtractionRules` match directly.
      2. *Deep-Freeze Parsed Response*: Replaced shallow `Object.freeze` with recursive `deepFreeze(parsed)` in `SourceCaptureWorker.captureAndExtract`, guaranteeing deep immutability on all extracted fields, telemetry, and evidence envelopes.
    - **Tiered MOQ Batch Optimizer Integration (`src/research/m5SiloAndGroupSimulator.ts`)**:
      - Implemented `evaluateOptimalBatchSize` using exact statutory subunit math (18% fee GST, ex-GST TCS/TDS, GSTR-3B net settlement, return drag, and CCC).
      - Enforces treasury budget (`E-M5-BUDGET-EXHAUSTED`) and single-SKU concentration cap (`E-M5-CONCENTRATION-CAP-EXCEEDED`) feasibility checks across price brackets, selecting the optimal bracket maximizing `annualized_rowc_bps` (or throwing `E-M5-NO-FEASIBLE-BRACKET`).
    - **Stage 3: Micro-Agent #2 MediaAndChatterWorker (`src/agents/workers/mediaChatterWorker.ts`)**:
      - Implemented `MediaAndChatterWorker` (`worker:media-chatter:v1`) routing read-only requests exclusively through `McpCapabilityBroker.invokeTool` under task-scoped `CapabilityGrant`.
      - Registered `mcp://media-corpus/fetch_transcript` on `McpServerAdapter` with strict tool policy (GET only, 256 KB cap, hosts: `'transcripts.approved-corpus.local'`, `'www.youtube.com'`, `'sellercentral.amazon.in'`, `'www.amazon.in'`).
      - Mandatory Verbatim Citation Span Verification (`verifyVerbatimCitationSpan`): Enforces exact character offset substring match (`sanitizedTranscript.slice(start, end) === verbatim_quote`), 10–280 character quote length bounds, SHA-256 integrity, fail-closed rejection on uncited claims (`E-MCW-UNCITED-CLAIM-REJECTED`), and offset mismatches (`E-MCW-INVALID-CITATION-SPAN`).
      - Structured Signal Taxonomy & Defect Math: Supports `METALLURGY_GRADE_DEFECT`, `DIMENSIONAL_OR_TORQUE_FAILURE`, `PACKAGING_COUNT_SHORTFALL`, and `SELLER_FEE_OR_RETURN_SPIKE`, computing deterministic `observed_defect_rate_bps = Math.floor((observed_defect_mention_count * 10000) / total_sampled)`.
      - Hardcoded 4D Evidence Ceiling: Hard-binds `verification_status: 'UNVERIFIED'` and `commercial_status: 'NOT_APPLICABLE'`. Zero commercial pricing authority (elevation throws `E-MCW-COMMERCIAL-STATUS-FORBIDDEN`).
      - Complementary & Supplementary Trigger Helper (`evaluateChatterSupplementTrigger`): Dispatches `COMPLEMENTARY_GAP_FILL` when empirical return data is missing, `SUPPLEMENTARY_ANOMALY_CHECK` when supplier quote is within 15% of physical scrap floor, and `NONE` when verified quote has fresh return observations.
    - **Acceptance Tests & Evidence Separation (`Suite 25`)**:
      - Implemented `tests/acceptance/suite25_m6_3_media_chatter_worker.test.ts` (8 passed assertions):
        1. `MCP-MCW-VERBATIM-CITATION-EXTRACT-001`: Extracts metallurgy defect and torque failure claims with exact verbatim citation spans and defect rates.
        2. `MCP-MCW-UNCITED-AND-OFFSET-MISMATCH-REJECT-002`: Fails closed on uncited claims (`E-MCW-UNCITED-CLAIM-REJECTED`) and mismatched offsets (`E-MCW-INVALID-CITATION-SPAN`).
        3. `MCP-MCW-PROMPT-INJECTION-QUARANTINE-003`: Quarantines adversarial instructions with `QUARANTINED_INJECTION` and returns zero claims.
        4. `MCP-MCW-COMMERCIAL-STATUS-AND-AUTHORITY-CEILING-004`: Proves hardcoded `UNVERIFIED` / `NOT_APPLICABLE` ceiling and throws on commercial elevation.
        5. `MCP-MCW-BROKER-POLICY-AND-QUOTA-005`: Enforces allowed hosts, GET method, 256KB payload limit, and request quota.
        6. `MCP-MCW-COMPLEMENTARY-VS-SUPPLEMENTARY-TRIGGER-006`: Dispatches `COMPLEMENTARY_GAP_FILL` and `SUPPLEMENTARY_ANOMALY_CHECK` correctly.
        7. `MCP-SCW-M5-TIERED-BATCH-OPTIMIZATION-007`: Feeds IndiaMART price tiers into `evaluateOptimalBatchSize`, proving 500 packs selected under ₹50k budget (399.41% RoWC) and 250 packs under ₹15k budget (`E-M5-BUDGET-EXHAUSTED` on 500+).
        8. `MCP-MCW-REPRODUCIBLE-JCS-008`: Bit-for-bit identical RFC 8785 JCS SHA-256 digests and deep immutability (`deepFreeze`).
    - **Full Baseline Conformance**:
      - Full test baseline expanded to **217 passed tests across 25 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
      - Dedicated Gate M6.3 evidence files generated:
        - `POC-001_Gate_M6_3_Test_Execution_Results.json` (SHA-256: `4A28BB44EC556F129C5DEEA0AFADB88D1AB4DB93D31B72B6A9E8D990CE0691CF`, 217 tests).
        - `POC-001_Gate_M6_3_Typecheck_Execution_Results.txt` (SHA-256: `860A1C910A4A7960518DEBF6D82A52CA8102AC617BBFA2D655E93881DC5BC5CB`, 0 errors).
    - Gate M6.3 status is authoritatively confirmed as **APPROVED / CLOSED**.

16. **Project Owner Decision OD-14 (Stage 3 Surgical Polish, Stage 4 Micro-Agent #3 `MacroAndLateralMarketWorker`, Formula-RAG Dynamic Growth Driver Engine & Dynamic Regime Classifier Closure)**:
    - **Stage 3 Surgical Polish**:
      1. *MCW-01 (Citation Span SHA-256 Validation)*: Passed `sanitizedSha256` as 3rd parameter to `verifyVerbatimCitationSpan(sanitizedText, citation, sanitizedSha256)` in `registerMediaChatterTool`, enforcing that citation spans carrying forged or mismatched `source_artifact_sha256` fail closed with `E-MCW-INVALID-CITATION-SPAN`.
      2. *MCW-02 (Custom SUBUNITS_INR Trigger Support)*: Updated `evaluateChatterSupplementTrigger` to inspect all extracted fields for `status === 'EXTRACTED' && unit === 'SUBUNITS_INR'` if default keys are absent, ensuring tiered B2B captures trigger the 15% scrap floor anomaly check.
      3. *MCW-03 (Unused Import Cleanup)*: Removed unused `randomBytes` import from `src/agents/workers/mediaChatterWorker.ts`.
    - **Stage 4: Micro-Agent #3 MacroAndLateralMarketWorker (`src/agents/workers/macroLateralWorker.ts`)**:
      - Implemented `MacroAndLateralMarketWorker` (`worker:macro-lateral:v1`) and registered read-only MCP tool `mcp://macro-feeds/query_series` on `McpServerAdapter` with policy `MACRO_LATERAL_TOOL_POLICY` (GET only, 128 KB payload cap, max 4 requests per task, hosts: `www.rbi.org.in`, `www.fbil.org.in`, `www.lme.com`, `www.nseindia.com`, `mospi.gov.in`).
      - Zero-Default Policy: Refuses to fabricate default T-Bill yields or commodity prices; returns `DATA_REQUIRED` (`E-MLW-SERIES-DATA-REQUIRED`) for missing/non-positive series, and `STALE_OBSERVATION_REJECTED` (`E-MLW-STALE-SERIES`) for observations exceeding `max_staleness_seconds`.
      - FX Firewall & Scrap Floor: Enforces fresh `FBIL_USD_INR_REFERENCE_RATE` for converting USD/tonne to scale-4 INR/kg (`convertUsdPerTonneToInrPerKg`), and computes physical scrap floor + minimum viable EXW manufacturing floor via `derivePhysicalScrapFloor` in pure `BigInt`.
      - Formula-RAG Dynamic Growth Driver Evaluator (`evaluateDynamicGrowthDriver`): Evaluates economic factors via `FormulaRegistry` pure-BigInt rational AST arithmetic without hardcoding static function calls, computing `net_change_bps`, `persistence_consistency_bps`, and `estimated_half_life_days`.
      - Sustained Signal vs Fast Opportunity Regime Classifier: Classifies drivers into `SUSTAINED_STRUCTURAL_SIGNAL`, `FAST_TACTICAL_OPPORTUNITY`, or `SPURIOUS_OR_UNPROVEN_NOISE`. Enforces the **Tactical Horizon Gate** (`E-MLW-EDGE-DECAYS-BEFORE-CASH-RECOVERY`) when cash conversion cycle (CCC) exceeds signal half-life.
      - Empirical Factor Efficacy Ledger (`FactorEfficacyLedger`): Records historical forecast vs. realized outcomes across cycles, computing `hit_rate_bps` and `mean_absolute_error_bps` to classify drivers into `UNPROVEN_HYPOTHESIS`, `EMPIRICALLY_VALIDATED_DRIVER`, and `EMPIRICALLY_REFUTED_NOISE`.
    - **Acceptance Tests & Evidence Separation (`Suite 26`)**:
      - Implemented `tests/acceptance/suite26_m6_4_macro_lateral_and_regime_worker.test.ts` (8 passed assertions):
        1. `MCP-MLW-CORE-SERIES-AND-SCRAP-FLOOR-001`: Ingests RBI T-Bill (650 bps), FBIL USD/INR (₹84.0500), and LME SS304 coil, deriving exact BigInt physical scrap floor for 140g clamp pack (₹25.8874 raw metal, ₹29.7705 with 15% stamping).
        2. `MCP-MLW-STALE-AND-MISSING-NO-DEFAULT-002`: Proves expired timestamps fail closed and missing series require data with zero fabricated fallbacks.
        3. `MCP-MLW-UNIT-AND-FX-FIREWALL-003`: Proves querying USD/tonne without fresh FBIL USD/INR rate fails closed with `UNIT_MISMATCH_REJECTED` (`E-MLW-MISSING-FX-REFERENCE`).
        4. `MCP-MLW-DYNAMIC-FORMULA-RAG-DRIVER-004`: Evaluates dynamic growth driver by resolving formula from `FormulaRegistry` with pure BigInt rational arithmetic.
        5. `MCP-MLW-SUSTAINED-VS-FAST-REGIME-CLASSIFIER-005`: Contrasts 60-day sustained structural signal vs 10-day fast opportunity with Tactical Horizon Gate.
        6. `MCP-MLW-EMPIRICAL-EFFICACY-LEARNING-006`: Tracks forecast vs realized cycles, promoting capex signal and refuting noisy social hype.
        7. `MCP-MLW-BROKER-SECURITY-AND-INJECTION-007`: Verifies broker policy, prompt injection quarantine (`E-MLW-PROMPT-INJECTION-DETECTED`), status ceiling (`E-MLW-COMMERCIAL-STATUS-FORBIDDEN`), and Stage 3 MCW-01 citation span SHA-256 rejection.
        8. `MCP-MLW-REPRODUCIBLE-JCS-008`: Bit-for-bit identical RFC 8785 JCS SHA-256 digests and deep immutability (`deepFreeze`).
    - **Full Baseline Conformance**:
      - Full test baseline expanded to **225 passed tests across 26 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
      - Dedicated Gate M6.4 evidence files generated:
        - `POC-001_Gate_M6_4_Test_Execution_Results.json` (SHA-256: `CB5B643D855F0E9B2C61531F0E0898D71E6F41E607091AE51C31BB83A9FD9717`, 225 tests).
        - `POC-001_Gate_M6_4_Typecheck_Execution_Results.txt` (SHA-256: `C844D31403B9BC823C1F62DE8AAA77AE2B4F63F4C8325B506055CADB02960E24`, 0 errors).
    - Gate M6.4 status is authoritatively confirmed as **APPROVED / CLOSED**.

17. **Project Owner Decision OD-15 (Stage 5 Micro-Agent #4 `GovtAndStatutoryWorker`, Statutory Citations, MSME Sec 43B(h) & Tax Formula Non-Mutation Firewall)**:
    - **Stage 5: Micro-Agent #4 GovtAndStatutoryWorker (`src/agents/workers/govtStatutoryWorker.ts`) & Contract (`src/mcp/contracts/govtStatutoryContract.ts`)**:
      - Implemented `GovtAndStatutoryWorker` (`worker:govt-statutory:v1`) and registered read-only MCP tool `mcp://policy-bulletins/fetch_circular` on `McpServerAdapter` with policy `GOVT_STATUTORY_TOOL_POLICY` (GET only, 256 KB payload cap, max 2 requests per task, hosts: `cbic-gst.gov.in`, `incometaxindia.gov.in`, `dgft.gov.in`, `msme.gov.in`).
      - Authoritative Circular Registry (`StatutoryCircularRegistry`): Preloaded with CBIC HSN 73269099 GST rate (1800 bps = 18.00%), CBIC Section 52 TCS (100 bps = 1.00%), CBDT Section 194-O TDS (100 bps = 1.00%), DGFT Customs Tariff BCD on HSN 73269099 (750 bps = 7.50%), and DGFT Anti-Dumping Duty baseline on SS304.
      - Immutable Statutory Citation Sieve (`verifyStatutoryCitation`): Enforces that every rule claim binds to an approved authority (`CBIC`, `CBDT`, `DGFT`, `MINISTRY_OF_MSME`), notification/section ID, ISO effective date (`YYYY-MM-DD`), and 64-char hex document SHA-256 (`E-GSW-INVALID-CITATION`).
      - Zero-Default Policy: Missing circular or unknown HSN code fails closed with `DATA_REQUIRED` (`E-GSW-STATUTORY-CIRCULAR-REQUIRED`) with zero fabricated tax rate fallbacks.
      - MSME Section 43B(h) Payment Term Cross-Check: Evaluates statutory credit ceiling under Finance Act 2023 / MSMED Act 2006 (`evaluateMsmePaymentTermLimit`): 45 days with written agreement, 15 days without, and 0 days for non-MSME. Emits structured `msme_cross_check` envelope enabling downstream Red-Team detection of illegal 60–90 day DPO credit assumptions.
      - FormulaRegistry Non-Mutation Firewall: Proves that attempting to overwrite or mutate `PROMOTED_NORMATIVE` tax formula cards (e.g. `FIN-STATUTORY-TCS-TDS-003`) fails closed with `E-ERR-GOV-002: CANNOT_OVERWRITE_NORMATIVE_FORMULA`. Worker can only emit `UNVERIFIED` claims or register sandboxed `CANDIDATE_UI_MODEL` formulas. Unauthorized promotion without human authorization token (`GOVERNED_RATIFICATION_*`) fails closed with `E-ERR-GOV-003`.
      - Prompt-Injection Canary Quarantine: Quarantines adversarial circular payloads via `InjectionCanaryGuard`, returning `status: 'QUARANTINED_INJECTION'`, `error_code: 'E-GSW-PROMPT-INJECTION-DETECTED'`.
    - **Acceptance Tests & Evidence Separation (`Suite 27`)**:
      - Implemented `tests/acceptance/suite27_m6_5_govt_statutory_worker.test.ts` (8 passed assertions):
        1. `MCP-GSW-CORE-HSN-AND-TCS-TDS-EXTRACTION-001`: Ingests CBIC HSN 73269099 (18%), CBIC TCS (1%), CBDT TDS (1%), and DGFT BCD (7.5%), verifying unverified ceiling.
        2. `MCP-GSW-ZERO-DEFAULT-POLICY-002`: Proves unknown HSN fails closed with `DATA_REQUIRED` and zero fabricated defaults.
        3. `MCP-GSW-CITATION-COMPLETENESS-AND-TAMPER-DEFENSE-003`: Rejects unverified authorities or tampered citations with `E-GSW-INVALID-CITATION`.
        4. `MCP-GSW-NO-AUTONOMOUS-TAX-FORMULA-MUTATION-004`: Strictly prohibits overwriting normative formulas (`E-ERR-GOV-002`) and confines candidate proposals to sandboxed tier.
        5. `MCP-GSW-MSME-SEC43BH-PAYMENT-TERM-CROSS-CHECK-005`: Evaluates 45d/15d payment term limits and emits cross-check envelope.
        6. `MCP-GSW-PROMPT-INJECTION-QUARANTINE-006`: Quarantines prompt injection payload via `InjectionCanaryGuard`.
        7. `MCP-GSW-BROKER-SECURITY-AND-AUTHORITY-CEILING-007`: Enforces host allowlisting, commercial status ceiling (`E-GSW-COMMERCIAL-STATUS-FORBIDDEN`), and task grant boundaries.
        8. `MCP-GSW-DETERMINISTIC-JCS-AND-IMMUTABILITY-008`: Bit-for-bit identical RFC 8785 JCS SHA-256 digests and deep immutability (`deepFreeze`).
    - **Full Baseline Conformance**:
      - Full test baseline expanded to **233 passed tests across 27 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
      - Dedicated Gate M6.5 evidence files generated:
        - `POC-001_Gate_M6_5_Test_Execution_Results.json` (SHA-256: `90FF1A25470BC812590971145C6402A2C5863FDBA69BC4E50D184611D77FBFF0`, 233 tests).
        - `POC-001_Gate_M6_5_Typecheck_Execution_Results.txt` (SHA-256: `D3799E8B201645F3813E47DE5A9B31946EFC9C4743B2C7760DB96198E24DE251`, 0 errors).
    - Gate M6.5 status is authoritatively confirmed as **APPROVED / CLOSED**.

18. **Project Owner Decision OD-16 (Stage 6 Micro-Agent #5 `RedTeamAndConflictWorker`, 7 Red-Team Rules, Hard Disposition Ceiling & Deterministic Context-Routing State Machine)**:
    - **Stage 6: Micro-Agent #5 RedTeamAndConflictWorker (`src/agents/workers/redTeamWorker.ts`) & Contract (`src/mcp/contracts/redTeamContract.ts`)**:
      - Implemented `RedTeamAndConflictWorker` (`worker:red-team:v1`) and registered read-only MCP tool `mcp://audit-corpus/read_joined_claims` on `McpServerAdapter` with policy `RED_TEAM_TOOL_POLICY` (GET only, 256 KB payload cap, max 4 requests per task, zero network egress `allowed_hosts: []`).
      - 7 Authoritative Red-Team Adversarial & Conflict Rules:
        1. `RT-01-BELOW-PHYSICAL-SCRAP-FLOOR`: Blocks candidate quotes priced below LME SS304 raw metal scrap floor (`raw_material_scrap_floor_subunits`) or minimum viable EXW manufacturing floor (`min_viable_exw_floor_subunits`). Quarantines sub-scrap quotes with `BLOCK_ALLOCATION_GATE` and disposition `HOLD_BLOCKED_BY_RED_TEAM`.
        2. `RT-02-UNRESOLVED-CROSS-SOURCE-CONFLICT`: Strictly preserves cross-source conflicts without voting, averaging, or guessing. When independent sources disagree (e.g. ₹28 vs ₹35), flags `BLOCK_ALLOCATION_GATE` and disposition `HOLD_BLOCKED_BY_RED_TEAM`.
        3. `RT-03-UNVERIFIED-HIGH-RETURN-ILLUSION`: Flags RoWC > 10,000 bps (100.00%) resting solely on unverified `ADVERTISED_LISTING` evidence with `WARNING_REQUIRES_CORROBORATION` and disposition `REQUIRES_SUPPLEMENTARY_CORROBORATION`. Resolves cleanly upon verified purchase invoice.
        4. `RT-04-METALLURGY-CHATTER-CONTRADICTION`: Rejects candidate quotes where supplier advertises SS304 but customer reviews, teardowns, or forum chatter identify SS202 adulteration or defect rates > 1,000 bps (10.00%). Flags `BLOCK_ALLOCATION_GATE` and disposition `HOLD_BLOCKED_BY_RED_TEAM`.
        5. `RT-05-ILLEGAL-MSME-CREDIT-TERM-ASSUMPTION`: Enforces statutory MSME Section 43B(h) credit ceilings. Flags assumed supplier DPO payment terms > 45 days (or > 15 days without written contract) with `BLOCK_ALLOCATION_GATE` and disposition `HOLD_BLOCKED_BY_RED_TEAM`.
        6. `RT-06-MANDATORY-COST-DATA-REQUIRED`: Enforces zero-cost substitution ban under Frozen Spec §2.3. Flags missing or non-positive freight, packaging, or statutory tax rates with `BLOCK_ALLOCATION_GATE` and disposition `HOLD_BLOCKED_BY_RED_TEAM`.
        7. `RT-07-EXPIRED-OR-CLOCK-SKEWED-EVIDENCE`: Enforces evidence freshness and clock skew firewalls. Flags evidence envelopes observed in the future (>60s clock skew) or exceeding their TTL with `BLOCK_ALLOCATION_GATE` and disposition `HOLD_BLOCKED_BY_RED_TEAM`.
      - Hard Disposition Ceiling:
        - Worker output is strictly restricted to `HOLD_BLOCKED_BY_RED_TEAM`, `REQUIRES_SUPPLEMENTARY_CORROBORATION`, or `ELIGIBLE_FOR_HUMAN_REVIEW`.
        - Attempting to pass or request `APPROVED_FOR_EXECUTION` fails closed with `E-RTW-DISPOSITION-CEILING-BREACH: RedTeam worker is structurally prohibited from approving real capital execution.` Promotion to real execution rests solely with the Human Project Owner.
    - **Deterministic Context-Routing State Machine (`src/agents/scheduler/contextRoutingStateMachine.ts`)**:
      - Pass 1: Complementary Dispatch (Horizontal Gap-Filling across Stages 2, 4, 5) — queries primary supplier catalog, macro benchmarks (T-Bill, FBIL USD/INR, LME SS304), and CBIC/MSME statutory circulars.
      - Pass 2: Context Evaluation & Supplementary Dispatch (Vertical Corroboration & Stress-Testing) — evaluates scrap floor proximity trigger S-1 (dispatching YouTube chatter analysis for defect rates), secondary catalog trigger S-2 (dispatching secondary supplier capture), and executes deterministic `joinSupplementaryClaims` strictly preserving conflicts.
      - Pass 3: Stage 6 Red-Team Audit & Deterministic Join — dispatches `RedTeamAndConflictWorker` to audit joined claims, assign hard disposition, and format the multi-pass execution trace into bit-for-bit reproducible RFC 8785 JCS canonical attestation with SHA-256 telemetry digest.
    - **Acceptance Tests & Evidence Separation (`Suite 28`)**:
      - Implemented `tests/acceptance/suite28_m6_6_red_team_conflict_worker.test.ts` (8 passed assertions):
        1. `MCP-RTW-SCRAP-FLOOR-AND-METALLURGY-DEFENSE-001`: Blocks sub-scrap quotes below LME SS304 physical floor and passes valid quotes.
        2. `MCP-RTW-UNRESOLVED-CROSS-SOURCE-CONFLICT-002`: Strictly preserves cross-source conflict without voting or averaging.
        3. `MCP-RTW-HIGH-RETURN-ILLUSION-ON-ADVERTISED-003`: Flags RoWC > 100% resting solely on advertised listing.
        4. `MCP-RTW-METALLURGY-CHATTER-CONTRADICTION-004`: Quarantines quotes contradicted by chatter defect and adulteration reports.
        5. `MCP-RTW-ILLEGAL-MSME-CREDIT-TERM-DEFENSE-005`: Blocks credit term assumptions violating statutory MSME Sec 43B(h).
        6. `MCP-RTW-MANDATORY-COST-DATA-AND-CLOCK-SKEW-006`: Enforces zero-cost substitution ban and clock skew defense.
        7. `MCP-RTW-DISPOSITION-CEILING-AND-ZERO-NETWORK-EGRESS-007`: Enforces zero network egress and hard disposition ceiling (`E-RTW-DISPOSITION-CEILING-BREACH`).
        8. `MCP-RTW-3PASS-SCHEDULER-STATE-MACHINE-008`: Executes 3-pass `ContextRoutingStateMachine` with RFC 8785 JCS attestation.
    - **Full Baseline Conformance**:
      - Full test baseline expanded to **241 passed tests across 28 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
      - Dedicated Gate M6.6 evidence files generated:
        - `POC-001_Gate_M6_6_Test_Execution_Results.json` (SHA-256: `81A20C41204E0D776FB7A9FD68317F52DEA712D07A5E02A9FA350E0D3423460B`, 241 tests).
        - `POC-001_Gate_M6_6_Typecheck_Execution_Results.txt` (SHA-256: `7808FD347CB9B2BAB4A5A91EEF5F976584C3D319641274B1EFAB6572DE48DC6E`, 0 errors).
    - Gate M6.6 status is authoritatively confirmed as **APPROVED / CLOSED**.

