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
7. **Gate M4.2 (Groq-Backed LLM Formula Discovery & Refinement Module):**
   - **Baseline:** `Market-HFT-OS` @ `3eb11ca` / `ADRs` @ current `main`.
   - **Approved Scope:** Groq-backed LLM formula discovery and refinement module (`src/research/llmFormulaAdvisor.ts`); sandboxed `CANDIDATE_UI_MODEL` tier; offline fallback; Suite 20 expanded to 14 tests; 20 suites / 175 tests passed.
   - **Status:** **APPROVED / CLOSED** (Formally authorized under Decision OD-07 by Project Owner on 2026-10-16).
8. **Gate M4.3 (RAG-First Sufficiency Gate, Asymptotic LLM Decay & Pure BigInt Rational Evaluator):**
   - **Baseline:** `Market-HFT-OS` @ `1ccf802` / `ADRs` @ `d765720` (Tag: `POC-001-Gate-M4.3-Verified`).
   - **Approved Scope:** RAG-first sufficiency gate; asymptotic LLM decay flywheel; persistent corpus storage; pure BigInt rational AST evaluator; Suite 20 expanded to 17 tests; 20 suites / 178 tests passed.
   - **Status:** **APPROVED / CLOSED** (Formally authorized under Decision OD-08 by Project Owner on 2026-10-16).
9. **Gate M5 (Multi-Opportunity Portfolio Capital Rationing & Sandbox Formula Stress-Testing):**
   - **Baseline:** `Market-HFT-OS` @ `cba9554` / `ADRs` @ `5688ed7` (Tag: `POC-001-Gate-M5-Verified`).
   - **Approved Scope:** Stage 3 Multi-Opportunity Portfolio Capital Rationing Engine (`src/research/m5PortfolioAllocator.ts`); 4-candidate industrial pool under ₹50,000.0000 budget; discrete integer MOQ lot sizing; 50% single-SKU concentration caps; 91-day sovereign T-Bill cash sweep; dual-pass FormulaRegistry bridge with shadow what-if sandbox comparison; bit-for-bit RFC 8785 JCS determinism; Suite 21 (7 passed assertions); full test baseline expanded to 185 passed tests across 21 suites (0 skipped, 0 failed) on live PostgreSQL 16.8 (`localhost:5432`).
   - **Status:** **APPROVED / CLOSED** (Formally authorized under Decision OD-09 by Project Owner on 2026-10-16).
10. **Gate M6 (Governed Multi-Agent Research Swarm & Bitemporal Replay Engine):**
    - **Baseline:** `Market-HFT-OS` @ `6bafb16` / `ADRs` @ commit companion (Tag: `POC-001-Gate-M6-Verified`).
    - **Approved Scope:** Governed multi-agent research ecosystem (`src/agents/m6AgentFramework.ts`), TinyFish scoped browser sub-agent, specialist swarm (Media/Chatter, Macro/Lateral, Govt/Tax, RedTeam), 24x7 scheduler and manager orchestrator, and bitemporal decision replay & restatement engine; Suite 22 (7/7 passed); 22 suites / 192 tests passed against live PostgreSQL 16.8.
    - **Status:** **APPROVED / CLOSED** (Formally authorized under Decision OD-10 by Project Owner on 2026-10-16).
11. **Gate M6.1 (Capability-Aware MCP Substrate & Read-Only Micro-Agent Broker):**
    - **Baseline:** `Market-HFT-OS` @ `95ce444` / `ADRs` @ `75c0190`.
    - **Approved Scope:** Stage 0 Workspace & Charter Reconciliation; Stage 1 Capability-Aware MCP Substrate (`src/mcp/mcpSubstrate.ts`), JSON-RPC 2.0 tool envelopes, forbidden capability firewall, task-scoped immutable CapabilityGrant, McpCapabilityBroker (SSRF/private IP filter, 4-quota enforcement, GET only, redirect blocking), McpRunLedger (RFC 8785 JCS hash chains), conflict-preserving join (`joinSupplementaryClaims`), Bitemporal immutability & duplicate overwrite prevention (`E-ERR-BITEMPORAL-OVERWRITE`), genuine sub-agent scheduler invocations; Suite 23 (8/8 passed); 23 suites / 200 tests passed against live PostgreSQL 16.8.
    - **Status:** **APPROVED / CLOSED** (Formally authorized under Decision OD-11 by Project Owner on 2026-10-17).
12. **Gate M6.2 (Stage 1 Surgical Hardening & Stage 2 SourceCaptureWorker):**
    - **Baseline:** `Market-HFT-OS` @ `8457ddd` / `ADRs` @ current `main`.
    - **Approved Scope:** Stage 1 surgical hardening in `src/mcp/mcpSubstrate.ts` (protocol scheme enforcement, IPv6 SSRF expansion, event loop timer cleanup, property type validation); Stage 2 Micro-Agent #1 `SourceCaptureWorker` (`src/agents/workers/sourceCaptureWorker.ts`) with 6-Layer DOM Sanitization Sieve (`sanitizeHtmlDomSieve`), 4-Layer Prompt-Injection & Canary Defense (`InjectionCanaryGuard`), IndiaMART Deterministic Tiered MOQ Bracket Resolver (`resolveTieredMoqPrice` / `expected_type: 'TIERED_SUBUNITS_INR'`), zero-LLM deterministic numeric extraction (`parseInrToSubunits`), hardcoded status ceiling (`UNVERIFIED`, `ADVERTISED_LISTING`/`SUPPLIER_QUOTE`), deterministic fixture replay & live HTTPS GET; Suite 24 (9/9 passed); 24 suites / 209 tests passed against live PostgreSQL 16.8.
    - **Status:** **APPROVED / CLOSED** (Formally authorized under Decision OD-12 by Project Owner on 2026-10-17).

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

### Project Owner Decision OD-08 (Gate M4.3 RAG-First Sufficiency Gate, Asymptotic LLM Decay & Pure BigInt Rational Evaluator)

Formally authorized by Project Owner on 2026-10-16:
1. **Pure BigInt Rational Arithmetic AST Evaluator (`src/research/formulaRegistry.ts`):**
   - Eliminated all IEEE-754 `Number(...)`, `parseFloat(...)`, and `Math.round(...)` floating-point shortcuts from `evaluateSymbolicExpression` per Frozen Specification §1.3 and §6.1 (`AUDIT-45`).
   - Represented all AST nodes as exact rational pairs `{ num: bigint, den: bigint }` with deterministic GCD reduction and zero-division protection (`E-ERR-MATH-001`).
   - At the root of the AST, performed single half-up integer rounding in pure `BigInt`: `(num + den / 2n) / den`, enabling fractional basis point evaluation (e.g. `(Shrinkage_Rate / 10000)`) without premature integer truncation (`50n / 10000n = 0n`) or float precision drift on large subunit values (`> Number.MAX_SAFE_INTEGER`).
   - Upgraded `FIN-CCC-ROWC-005` in `evaluateFormula` to pure `BigInt` evaluation.
2. **Persistent Corpus Storage & Deterministic Appends (`FormulaRegistry`):**
   - Added file-backed persistence via `saveCorpusToFile(filePath)` and `loadCorpusFromFile(filePath)`, verifying RFC 8785 JCS hashes on load to guarantee cross-session cryptographic integrity.
   - Implemented `appendDeterministicFormula(cardInput, options)` allowing programmatic registration of deterministic formula rules with zero LLM involvement, immediately validating test vectors via the pure BigInt rational evaluator and indexing cards into the BM25 corpus.
3. **3-Tier "RAG-First, LLM-Last" Orchestrator & Asymptotic LLM Decay Flywheel (`src/research/llmFormulaAdvisor.ts`):**
   - Implemented `resolveOrSynthesizeFormula(request, registry)` enforcing strict 3-tier routing:
     1. *Tier 1 (`RAG_CACHE_HIT`, `llm_called: false`)*: Queries local BM25 RAG index (`topK: 3`). If top match score meets `min_bm25_score` (default `1.5`) and satisfies all `required_variables`, immediately returns the existing `FormulaCard` without calling Groq.
     2. *Tier 2 (`DETERMINISTIC_APPEND`, `llm_called: false`)*: If deterministic card input is supplied, validates test vector, indexes card into registry, and returns immediately without calling Groq.
     3. *Tier 3 (`LLM_RAG_REFINED_SYNTHESIS`, `llm_called: true`)*: Only on Tier 1 and Tier 2 miss, invokes Groq inference. Injects top-3 closest BM25 neighbor cards into prompt context as structural and domain context, instructing LLM to reuse canonical variable naming/scaling conventions and synthesize only the missing delta. Auto-registers and validates the resulting candidate card in `registry` so subsequent queries hit Tier 1 (`RAG_CACHE_HIT`).
   - Cumulative telemetry tracking in `getTelemetry()`: `{ total_requests, rag_cache_hits, deterministic_appends, llm_calls_invoked, llm_dependency_ratio_bps }`, proving monotonic asymptotic decay of LLM dependency toward zero as the RAG corpus expands.
4. **Acceptance Tests & Evidence Separation (`Suite 20`):**
   - Added three normative acceptance assertions in `tests/acceptance/suite20_m4_ss304_vertical_slice.test.ts`:
     - `M4-PURE-BIGINT-RATIONAL-AST-015`: Proves pure BigInt rational evaluation of fractional bps on large subunit values (`9007199254740993500n > Number.MAX_SAFE_INTEGER`) without precision loss.
     - `M4-RAG-FIRST-SUFFICIENCY-GATE-016`: Proves existing concepts (`Section 194-O TDS / Section 52 TCS`, `SS304 landed cost EXW`) resolve via `RAG_CACHE_HIT` (`llm_called: false`) and deterministic rule additions resolve via `DETERMINISTIC_APPEND` (`llm_called: false`).
     - `M4-ASYMPTOTIC-LLM-DECAY-FLYWHEEL-017`: Multi-step lifecycle proving novel metric LLM synthesis (`Customs anti-dumping duty and port demurrage drag`, `llm_called: true`), RAG neighbor context injection (`FIN-LANDED-COST-001`), subsequent 5-query cache hit sequence dropping LLM dependency ratio from 10,000 bps to 1,667 bps, and persistent corpus file reload.
   - Full test baseline expanded to **178 passed tests across 20 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
   - Dedicated Gate M4.3 evidence files generated:
     - `POC-001_Gate_M4_3_Test_Execution_Results.json` (SHA-256: `1F88EDD3B1DF18D49B4EF7E004E46510871A81A380062559DB9825A77B024EE1`, 178 tests).
     - `POC-001_Gate_M4_3_Typecheck_Execution_Results.txt` (SHA-256: `4596FF7DF1A8F378190D49DBCDBD055A4CB69A39B5C5B32F3E263B81D07AFF96`, 0 errors).
5. **Milestone Disposition:**
   - Gate M4.3 status is authoritatively confirmed as **APPROVED / CLOSED**.

### Project Owner Decision OD-09 (Gate M5 6-Channel Signal Bus, 4D Evidence Architecture & Silo vs. Group Strategy Simulator)

Formally authorized by Project Owner on 2026-10-16:
1. **Stage 3 Specification Freeze:**
   - Drafted and froze `POC-001_Gate_M5_Signal_Bus_and_Group_Simulation_Specification.md` (status: `FROZEN / AUTHORIZED (OD-09)`).
   - Mandated the 4 orthogonal evidence dimensions (`evidence_kind`, `verification_status`, `commercial_status`, `provenance_lineage`), 6-channel continuous signal bus, 9-stage "Deep Research Pro" DAG pipeline contract, 6-status return vocabulary, and Silo vs. Simultaneous Group simulation architecture.
2. **6-Channel Signal Bus & 4D Evidence Engine (`src/research/m5SignalAndEvidenceEngine.ts`):**
   - Implemented 4D evidence dimensions and fail-closed promotion state machine (`EvidencePromotionEngine`), strictly prohibiting `ADVERTISED_LISTING` or `SYNTHETIC_SCENARIO` from auto-promoting to `VERIFIED_EXECUTABLE_OFFER` without cryptographic signature attestation or multi-source corroboration (`E-ERR-EV-001`).
   - Implemented `SignalNormalizer` mapping testable signals across 6 channels (`NEWS_TRADE_PRESS`, `YOUTUBE_VIDEO_TRANSCRIPT`, `SOCIAL_FORUM_CHATTER`, `MACROECONOMIC_INDICATOR`, `LATERAL_FINANCIAL_MARKET`, `GOVERNMENT_SCHEME_POLICY`) into structured economic shocks with RFC 8785 JCS hashes.
   - Implemented 6-status return resolver (`resolveReturnStatus`) distinguishing `CANNOT_CALCULATE_MISSING_INPUTS`, `INSUFFICIENT_UNVERIFIED_EVIDENCE`, `NO_ROOT_FOUND_IN_SEARCH_DOMAIN`, `OPEN_POSITION`, and `NOT_YET_RECOVERED` from `VALID_CALCULATED_RETURN`.
   - Implemented `DeepResearchPipelineOrchestrator` executing the 9-stage DAG contract (`DECOMPOSE` $\to$ `ROUTE` $\to$ `ASSEMBLE_CONTEXT` $\to$ `PROMPT` $\to$ `EXECUTE_SCOPED_WORKER` $\to$ `REVIEW_RED_TEAM` $\to$ `ASSEMBLE_EVIDENCE` $\to$ `POLISH` $\to$ `PRESENT`).
3. **Silo vs. Simultaneous Group Strategy Simulator (`src/research/m5SiloAndGroupSimulator.ts`):**
   - Implemented `M5SiloAndGroupSimulator`:
     * *Silo Mode*: Evaluates SS304 DIN 3017 clamps across the 4-diameter x 2-pack matrix (8 variants), emitting price & breakeven bands, 35-day cash-flow J-curve waterfalls, and Arbitrage Greeks ($\Delta$: price sensitivity, $\Theta$: time decay, $\mathcal{V}$: return drag).
     * *Simultaneous Group Mode*: Evaluates cohorts under ₹50,000 treasury budget, correlated lateral shocks (e.g. $+10\%$ LME stainless steel raw material surge), single-SKU concentration caps ($\le 50\%$), discrete MOQ integer lot-sizing, sovereign 91-Day T-Bill sweeps, and benchmark comparisons (`RBI_91D_TBILL` at 650 bps and `NIFTY_LIQUID_BENCHMARK` at 680 bps).
     * *Conviction vs. Allocation Firewall*: Enforces that unverified listings (`ADVERTISED_LISTING`, `UNVERIFIED`) receive strictly ₹0 capital regardless of theoretical margins, generating bubble chart telemetry coordinates $(X, Y, Z)$.
4. **Acceptance Tests & Evidence Separation (`Suite 21`):**
   - Implemented `tests/acceptance/suite21_m5_silo_group_and_signals.test.ts` (7 passed assertions):
     - `M5-4D-EVIDENCE-ORTHOGONALITY-001`: 4D evidence dimensions and fail-closed promotion firewall.
     - `M5-SIX-CHANNEL-SIGNAL-INGEST-002`: 6-channel signal normalization & 9-stage DAG pipeline.
     - `M5-SIX-STATUS-VOCABULARY-003`: 6-status return vocabulary preventing 0% collapse.
     - `M5-SILO-PACK-SIZE-MATRIX-004`: SS304 DIN 3017 matrix (4 sizes x 2 packs), price bands, J-curves, Greeks.
     - `M5-SIMULTANEOUS-GROUP-CORRELATION-005`: Portfolio allocation, LME steel shock, T-Bill sweep, conservation.
     - `M5-CONVICTION-VS-ALLOCATION-SEPARATION-006`: Firewall rejecting unverified listings (₹0 capital).
     - `M5-TRADING-CHART-JCS-DETERMINISM-007`: Bit-for-bit RFC 8785 JCS telemetry attestation.
5. **Full Baseline Conformance:**
   - Full test baseline expanded to **185 passed tests across 21 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
   - Dedicated Gate M5 evidence files generated:
     - `POC-001_Gate_M5_Test_Execution_Results.json` (SHA-256: `2C1FF1854228C4447D9F7BF500A6511727CD60ECF6EC4ACAB976FF151BE1A78B`, 185 tests).
     - `POC-001_Gate_M5_Typecheck_Execution_Results.txt` (SHA-256: `2E4823FBA10769EA72EB0937EF1AF01D144509845F2E4B2BE022E9FC52EDAF2D`, 0 errors).
6. **Milestone Disposition:**
   - Gate M5 status is authoritatively confirmed as **APPROVED / CLOSED**.

### Project Owner Decision OD-10 (Gate M6 Governed Multi-Agent Research Ecosystem, TinyFish Browser Sub-Agents & Bitemporal Replay Engine)

Formally authorized by Project Owner on 2026-10-16:
1. **Stage 3 Specification Freeze:**
   - Drafted and froze `POC-001_Gate_M6_Multi_Agent_and_Bitemporal_Replay_Specification.md` (status: `FROZEN / AUTHORIZED (OD-10)`).
   - Mandated worker contract manifests and permission boundaries (`READ_ONLY_DISCOVERY`, `SANDBOX_MODELING`, `RED_TEAM_AUDIT`), deterministic resource accounting, TinyFish scoped DOM scraping with missing-data classification (`DATA_REQUIRED` vs `DATA_INSUFFICIENT`), zero-cost substitution prohibition, specialist sub-agent swarm (Media/Chatter, Macro/Lateral, Govt/Tax, RedTeam), 24x7 manager orchestrator with degraded-mode resilience, and bitemporal historical decision replay and restatement.
2. **Multi-Agent Research Framework & Bitemporal Engine (`src/agents/m6AgentFramework.ts`):**
   - Implemented `AgentSecurityFirewall` strictly prohibiting agent workers from mutating `PaperLedger` or `ActualsLedger` (`E-M6-PERMISSION-DENIED`) and enforcing deterministic token/request quotas (`E-M6-QUOTA-EXCEEDED`).
   - Implemented `TinyFishScopedBrowserAgent` computing SHA-256 `dom_snapshot_hash`, extracting structured marketplace/supplier fields, classifying missing attributes as `DATA_REQUIRED` (never substituting `₹0`), and capping commercial status at `ADVERTISED_LISTING`.
   - Implemented specialist swarm: `MediaAndChatterSubAgent`, `MacroAndLateralMarketSubAgent`, `GovtSchemeAndTaxSubAgent`, and adversarial `RedTeamReviewerSubAgent` (quarantining offers below raw scrap metal floor cost or with metallurgy defects).
   - Implemented `ResearchSchedulerAndManager` coordinating the 9-stage research workflow (`DECOMPOSE` $\to$ `ROUTE` $\to$ `ASSEMBLE_CONTEXT` $\to$ `PROMPT` $\to$ `EXECUTE_SCOPED_WORKER` $\to$ `REVIEW_RED_TEAM` $\to$ `ASSEMBLE_EVIDENCE` $\to$ `POLISH` $\to$ `PRESENT`) with degraded-mode resilience under external timeouts.
   - Implemented `BitemporalRestatementEngine` capturing $t_0$ decisions (`decision_time_utc` and `knowledge_time_utc`), reconstructing historical baselines bit-for-bit, evaluating $t_1$ restatements against incoming evidence, and issuing `THESIS_INVALIDATED_HALT`, `EDGE_DECAY_WARNING`, or `THESIS_INTACT` without altering historical records.
3. **Acceptance Tests & Evidence Separation (`Suite 22`):**
   - Implemented `tests/acceptance/suite22_m6_agent_swarm_and_bitemporal.test.ts` (7 passed assertions):
     - `M6-TINYFISH-SCOPED-BROWSER-001`: DOM extraction, SHA-256 snapshot, ADVERTISED_LISTING cap, DATA_REQUIRED handling.
     - `M6-SUBAGENT-SWARM-DECOMPOSE-002`: Multi-channel signal decomposition and 9-stage DAG execution.
     - `M6-RED-TEAM-ADVERSARIAL-BLOCK-003`: Red team blocking of below-scrap-cost fraud and metallurgy defect quotes.
     - `M6-AGENT-PERMISSION-AND-QUOTA-FIREWALL-004`: Fail-closed ledger access denial and token/request quota enforcement.
     - `M6-DEGRADED-MODE-RESILIENCE-005`: Control plane degraded mode resilience during external worker timeout.
     - `M6-BITEMPORAL-REPLAY-AND-RESTATEMENT-006`: Bit-for-bit historical t0 reconstruction and t1 restatement halting.
     - `M6-END-TO-END-POLISH-AND-PRESENT-JCS-007`: RFC 8785 JCS determinism of research and restatement payloads.
4. **Full Baseline Conformance:**
   - Full test baseline expanded to **192 passed tests across 22 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
   - Dedicated Gate M6 evidence files generated:
     - `POC-001_Gate_M6_Test_Execution_Results.json` (SHA-256: `A74A2AB274C4E7670A7158CE03584B6692051BC8D7C8314D7E754C67D3BC14DE`, 192 tests).
     - `POC-001_Gate_M6_Typecheck_Execution_Results.txt` (SHA-256: `2E4823FBA10769EA72EB0937EF1AF01D144509845F2E4B2BE022E9FC52EDAF2D`, 0 errors).
5. **Milestone Disposition:**
   - Gate M6 status is authoritatively confirmed as **APPROVED / CLOSED**.

### Project Owner Decision OD-11 (Stage 0 Workspace Reconciliation & Stage 1 Capability-Aware MCP Substrate)

Formally authorized by Project Owner on 2026-10-17:
1. **Stage 0 Charter & Boundary Reconciliation:**
   - Cleared uncommitted scratch files and reset workspace to clean baseline.
   - Extracted and reconciled `ADRXX3.pdf` against frozen specifications, verifying alignment across all 6 engines.
   - Updated `PROJECT_CHARTER.md` to v0.2.5, codifying Gates M6.1–M6.8 MCP Broker & Micro-Agent Framework.
2. **Stage 1 Capability-Aware MCP Substrate (`src/mcp/mcpSubstrate.ts`):**
   - Implemented JSON-RPC 2.0 / MCP tool schema envelopes with strict runtime validation.
   - Implemented `McpServerAdapter` with forbidden capability firewall (shell, SQL, ledger mutation, promotion, order routing, secrets).
   - Implemented task-scoped immutable `CapabilityGrant` (`Object.freeze`) scoping allowed tools, hosts, methods, and redirect blocking.
   - Implemented `McpCapabilityBroker` enforcing strict SSRF and private IP / loopback / metadata egress blocking, GET-only operations, redirect denial, and 4-quota enforcement (`requests_made`, `wall_clock_ms`, `payload_bytes`, `tokens_used`).
   - Implemented `McpRunLedger` with append-only hash chains under RFC 8785 JCS canonicalization.
   - Implemented `joinSupplementaryClaims` preserving multi-source agreement (`CROSS_SOURCE_CORROBORATED`) and disagreement (`CONFLICT`) without averaging, voting, or guessing.
   - Hardened `BitemporalRestatementEngine` to prevent duplicate decision overwrites fail-closed (`E-ERR-BITEMPORAL-OVERWRITE`) and deepFreeze all historical state.
3. **Acceptance Tests & Evidence Separation (`Suite 23`):**
   - Implemented `tests/acceptance/suite23_m6_1_mcp_substrate_and_broker.test.ts` (8 passed assertions).
   - Full test baseline expanded to **200 passed tests across 23 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
   - Dedicated Gate M6.1 evidence files:
     - `POC-001_Gate_M6_1_Test_Execution_Results.json` (SHA-256: `F914CF559382AD74A5910224AE1A035AC90AD30CABB708DE52640EBA00096DBB`, 200 tests).
     - `POC-001_Gate_M6_1_Typecheck_Execution_Results.txt` (SHA-256: `2E4823FBA10769EA72EB0937EF1AF01D144509845F2E4B2BE022E9FC52EDAF2D`, 0 errors).
4. **Milestone Disposition:**
   - Gate M6.1 status is authoritatively confirmed as **APPROVED / CLOSED**.

### Project Owner Decision OD-12 (Gate M6.2 Stage 1 Surgical Hardening & Stage 2 SourceCaptureWorker Closure)

Formally authorized by Project Owner on 2026-10-17:
1. **Stage 1 Surgical Hardening (`src/mcp/mcpSubstrate.ts`):**
   - Enforced protocol scheme allowlisting (`https:` and `mcp:` only, rejecting all others with `E-MCP-SCHEME-DENIED`).
   - Expanded SSRF IP filter to block IPv4-mapped IPv6 (`::ffff:`), IPv6 ULA (`f[cd]..:`), IPv6 link-local (`fe80:`), and unwhitelisted raw IP literals (`E-MCP-HOST-OR-SSRF-DENIED`).
   - Eliminated event loop dangling timers via `try { ... } finally { if (timerHandle) clearTimeout(timerHandle); }`.
   - Added runtime property type validation in `validateArguments` throwing `E-MCP-INVALID-ARGUMENTS` on schema mismatch.
   - Guaranteed deterministic sorting and deep freezing of `sources` and `conflicting_values` in `joinSupplementaryClaims`.
2. **Stage 2: Micro-Agent #1 SourceCaptureWorker (`src/agents/workers/sourceCaptureWorker.ts`):**
   - Implemented `SourceCaptureWorker` (`worker:source-capture:v1`) routing read-only requests exclusively through `McpCapabilityBroker.invokeTool` under task-scoped `CapabilityGrant`.
   - Registered `mcp://source-capture/http_get_snapshot` on `McpServerAdapter` supporting deterministic `RECORDED_FIXTURE_REPLAY` and live `APPROVED_LIVE_HTTPS_GET` with `redirect: 'error'`.
   - Implemented 6-Layer DOM Sanitization Sieve (`sanitizeHtmlDomSieve`):
     * *Layer 1*: 512KB cap (`E-MCP-PAYLOAD-TOO-LARGE`), null-byte rejection (`E-SCW-NULL-BYTE-DETECTED`), and raw SHA-256 calculation.
     * *Layer 2*: Purges executable & active tag subtrees (`<script>`, `<style>`, `<iframe>`, `<form>`, `<input>`, etc.), event handlers (`on*`), and `javascript:`/`data:`/`vbscript:` URIs.
     * *Layer 3*: Purges HTML comments (`<!-- ... -->`) and cloaked/hidden nodes (`hidden`, `aria-hidden="true"`, `display:none`, `visibility:hidden`, `opacity:0`, `font-size:0`, `width:0`, `height:0`, `left:-9999px`, `top:-9999px`, `color:transparent`) using depth-tracked iterative parsing.
     * *Layer 4*: Retains structural selector attributes only (`id`, `class`, `data-asin`, `data-sku`, `data-price`, `data-moq`, `itemprop`, `href`), stripping free-text and LLM prompt smuggling attributes.
     * *Layer 5*: Normalizes text to Unicode NFC, strips zero-width and BiDi control characters (`\u200B-\u200F`, `\uFEFF`), and rejects fullwidth/Cyrillic homographs in price contexts (`E-SCW-HOMOGRAPH-DETECTED`).
     * *Layer 6*: Collapses redundant whitespace and computes canonical `sanitized_dom_sha256`.
   - Implemented 4-Layer Prompt-Injection & Canary Defense (`InjectionCanaryGuard`):
     * *Zero-LLM Numeric Extraction*: Deterministic BigInt subunit parser (`parseInrToSubunits`) strictly banning zero/0n substitution on missing or non-numeric costs (`status: 'DATA_REQUIRED'`, `E-SCW-MANDATORY-COST-MISSING`).
     * *Lexical & Domain Canary Scanner*: Scans for instruction overrides, role/ChatML delimiters, domain enum spoofing literals (`VERIFIED_EXECUTABLE_OFFER`, `ALLOCATE_CAPITAL`, `CROSS_SOURCE_CORROBORATED`, `ACTUALS_LEDGER`, `PROMOTED_NORMATIVE`), and internal URI smuggling, quarantining captures with `E-SCW-PROMPT-INJECTION-DETECTED`.
     * *Hardcoded Status Ceiling*: Enforces strict output ceilings (`verification_status: 'UNVERIFIED'`, `commercial_status: 'ADVERTISED_LISTING' | 'SUPPLIER_QUOTE'`), throwing `E-SCW-STATUS-ESCALATION-FORBIDDEN` on elevation attempts.
     * *Cryptographic Spotlighting*: Encloses extracted text in nonce-delimited tags (`<untrusted_dom_field_${nonce}>...`).
3. **Acceptance Tests & Evidence Separation (`Suite 24`):**
   - Implemented `tests/acceptance/suite24_m6_2_source_capture_worker.test.ts` (8 passed assertions).
   - Full test baseline expanded to **208 passed tests across 24 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
   - Dedicated Gate M6.2 evidence files:
     - `POC-001_Gate_M6_2_Test_Execution_Results.json` (SHA-256: `0B661002CB336F894C2D6B18329F9FDFB88E7088B0654DE55F3B730388393536`, 208 tests).
     - `POC-001_Gate_M6_2_Typecheck_Execution_Results.txt` (SHA-256: `0C8CBFA6266109AE38761BEA2F38FC147DF50211ADB28505373F8E752540AE60`, 0 errors).
4. **Milestone Disposition:**
   - Gate M6.2 status is authoritatively confirmed as **APPROVED / CLOSED**.

### Project Owner Decision OD-13 (Stage 2 Surgical Polish, Tiered Batch Optimizer Integration & Stage 3 Micro-Agent #2 MediaAndChatterWorker Closure)

Formally authorized by Project Owner on 2026-10-18:
1. **Stage 2 Surgical Polish & Tiered Batch Optimizer Integration:**
   - Custom attribute allowlist in `src/agents/workers/sourceCaptureWorker.ts` expanded with `'data-pack'`, `'data-freight'`, `'data-material'`, `'data-size'`, and `'data-hsn'`, enabling direct selector matches without relying solely on class fallbacks.
   - Deep immutability enforced in `SourceCaptureWorker.captureAndExtract` via recursive `deepFreeze(parsed)`.
   - Tiered MOQ batch optimizer `evaluateOptimalBatchSize` implemented in `src/research/m5SiloAndGroupSimulator.ts` enforcing treasury budget (`E-M5-BUDGET-EXHAUSTED`) and concentration caps (`E-M5-CONCENTRATION-CAP-EXCEEDED`) with statutory subunit arithmetic (18% fee GST, ex-GST TCS/TDS, GSTR-3B net settlement, return drag, and CCC).
2. **Stage 3: Micro-Agent #2 MediaAndChatterWorker Implementation (`src/agents/workers/mediaChatterWorker.ts`):**
   - Implemented `MediaAndChatterWorker` (`worker:media-chatter:v1`) routing read-only requests exclusively through `McpCapabilityBroker.invokeTool` under task-scoped `CapabilityGrant`.
   - Registered `mcp://media-corpus/fetch_transcript` on `McpServerAdapter` with strict tool policy (GET only, 256 KB cap, hosts: `'transcripts.approved-corpus.local'`, `'www.youtube.com'`, `'sellercentral.amazon.in'`, `'www.amazon.in'`).
   - Mandatory Verbatim Citation Span Verification (`verifyVerbatimCitationSpan`): Enforces exact character offset substring match (`sanitizedTranscript.slice(start, end) === verbatim_quote`), 10–280 character quote length bounds, SHA-256 integrity, fail-closed rejection on uncited claims (`E-MCW-UNCITED-CLAIM-REJECTED`), and offset mismatches (`E-MCW-INVALID-CITATION-SPAN`).
   - Structured Signal Taxonomy & Empirical Defect Math: Supports `METALLURGY_GRADE_DEFECT`, `DIMENSIONAL_OR_TORQUE_FAILURE`, `PACKAGING_COUNT_SHORTFALL`, and `SELLER_FEE_OR_RETURN_SPIKE`, computing deterministic `observed_defect_rate_bps = Math.floor((observed_defect_mention_count * 10000) / total_sampled)`.
   - Hardcoded 4D Evidence Ceiling: Hard-binds `verification_status: 'UNVERIFIED'` and `commercial_status: 'NOT_APPLICABLE'`. Zero commercial pricing authority (elevation throws `E-MCW-COMMERCIAL-STATUS-FORBIDDEN`).
   - Complementary & Supplementary Trigger Helper (`evaluateChatterSupplementTrigger`): Dispatches `COMPLEMENTARY_GAP_FILL` when empirical return data is missing, `SUPPLEMENTARY_ANOMALY_CHECK` when supplier quote is within 15% of physical scrap floor, and `NONE` when verified quote has fresh return observations.
3. **Acceptance Tests & Evidence Separation (`Suite 25`):**
   - Implemented `tests/acceptance/suite25_m6_3_media_chatter_worker.test.ts` (8 passed assertions).
   - Full test baseline expanded to **217 passed tests across 25 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
   - Dedicated Gate M6.3 evidence files:
     - `POC-001_Gate_M6_3_Test_Execution_Results.json` (SHA-256: `4A28BB44EC556F129C5DEEA0AFADB88D1AB4DB93D31B72B6A9E8D990CE0691CF`, 217 tests).
     - `POC-001_Gate_M6_3_Typecheck_Execution_Results.txt` (SHA-256: `860A1C910A4A7960518DEBF6D82A52CA8102AC617BBFA2D655E93881DC5BC5CB`, 0 errors).
4. **Milestone Disposition:**
   - Gate M6.3 status is authoritatively confirmed as **APPROVED / CLOSED**.

### Project Owner Decision OD-14 (Stage 3 Surgical Polish, Stage 4 Micro-Agent #3 MacroAndLateralMarketWorker, Formula-RAG Dynamic Growth Driver Engine & Dynamic Regime Classifier Closure)

Formally authorized by Project Owner on 2026-10-18:
1. **Stage 3 Surgical Polish:**
   - Passed `sanitizedSha256` as 3rd parameter to `verifyVerbatimCitationSpan(sanitizedText, citation, sanitizedSha256)` in `registerMediaChatterTool`, enforcing that citation spans carrying forged or mismatched `source_artifact_sha256` fail closed with `E-MCW-INVALID-CITATION-SPAN`.
   - Updated `evaluateChatterSupplementTrigger` to inspect all extracted fields for `status === 'EXTRACTED' && unit === 'SUBUNITS_INR'` if default keys are absent, ensuring tiered B2B captures trigger the 15% scrap floor anomaly check.
   - Removed unused `randomBytes` import from `src/agents/workers/mediaChatterWorker.ts`.
2. **Stage 4: Micro-Agent #3 MacroAndLateralMarketWorker Implementation (`src/agents/workers/macroLateralWorker.ts`):**
   - Implemented `MacroAndLateralMarketWorker` (`worker:macro-lateral:v1`) and registered read-only MCP tool `mcp://macro-feeds/query_series` on `McpServerAdapter` with policy `MACRO_LATERAL_TOOL_POLICY` (GET only, 128 KB payload cap, max 4 requests per task, hosts: `www.rbi.org.in`, `www.fbil.org.in`, `www.lme.com`, `www.nseindia.com`, `mospi.gov.in`).
   - Zero-Default Policy: Refuses to fabricate default T-Bill yields or commodity prices; returns `DATA_REQUIRED` (`E-MLW-SERIES-DATA-REQUIRED`) for missing/non-positive series, and `STALE_OBSERVATION_REJECTED` (`E-MLW-STALE-SERIES`) for observations exceeding `max_staleness_seconds`.
   - FX Firewall & Scrap Floor: Enforces fresh `FBIL_USD_INR_REFERENCE_RATE` for converting USD/tonne to scale-4 INR/kg (`convertUsdPerTonneToInrPerKg`), and computes physical scrap floor + minimum viable EXW manufacturing floor via `derivePhysicalScrapFloor` in pure `BigInt`.
   - Formula-RAG Dynamic Growth Driver Evaluator (`evaluateDynamicGrowthDriver`): Evaluates economic factors via `FormulaRegistry` pure-BigInt rational AST arithmetic without hardcoding static function calls, computing `net_change_bps`, `persistence_consistency_bps`, and `estimated_half_life_days`.
   - Sustained Signal vs Fast Opportunity Regime Classifier: Classifies drivers into `SUSTAINED_STRUCTURAL_SIGNAL`, `FAST_TACTICAL_OPPORTUNITY`, or `SPURIOUS_OR_UNPROVEN_NOISE`. Enforces the **Tactical Horizon Gate** (`E-MLW-EDGE-DECAYS-BEFORE-CASH-RECOVERY`) when cash conversion cycle (CCC) exceeds signal half-life.
   - Empirical Factor Efficacy Ledger (`FactorEfficacyLedger`): Records historical forecast vs. realized outcomes across cycles, computing `hit_rate_bps` and `mean_absolute_error_bps` to classify drivers into `UNPROVEN_HYPOTHESIS`, `EMPIRICALLY_VALIDATED_DRIVER`, and `EMPIRICALLY_REFUTED_NOISE`.
3. **Acceptance Tests & Evidence Separation (`Suite 26`):**
   - Implemented `tests/acceptance/suite26_m6_4_macro_lateral_and_regime_worker.test.ts` (8 passed assertions).
   - Full test baseline expanded to **225 passed tests across 26 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
   - Dedicated Gate M6.4 evidence files:
     - `POC-001_Gate_M6_4_Test_Execution_Results.json` (SHA-256: `CB5B643D855F0E9B2C61531F0E0898D71E6F41E607091AE51C31BB83A9FD9717`, 225 tests).
     - `POC-001_Gate_M6_4_Typecheck_Execution_Results.txt` (SHA-256: `C844D31403B9BC823C1F62DE8AAA77AE2B4F63F4C8325B506055CADB02960E24`, 0 errors).
4. **Milestone Disposition:**
   - Gate M6.4 status is authoritatively confirmed as **APPROVED / CLOSED**.

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
