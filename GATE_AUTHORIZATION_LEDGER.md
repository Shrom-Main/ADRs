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
| **Gate M6.6** | 2026-10-18 | Project Owner (`Decision OD-16`) | `Market-HFT-OS: 6053f3f`<br>`ADRs: adb139d` | Stage 6 Micro-Agent #5 (`RedTeamAndConflictWorker`, `worker:red-team:v1`), read-only `mcp://audit-corpus/read_joined_claims` with zero network egress (`allowed_hosts: []`), 7 authoritative red-team rules (RT-01 physical scrap floor, RT-02 strict conflict preservation, RT-03 high return illusion, RT-04 metallurgy defect contradiction, RT-05 illegal MSME credit terms, RT-06 zero-cost substitution ban, RT-07 clock skew & TTL expiration), hard disposition ceiling (`HOLD_BLOCKED_BY_RED_TEAM`, `REQUIRES_SUPPLEMENTARY_CORROBORATION`, `ELIGIBLE_FOR_HUMAN_REVIEW` with `E-RTW-DISPOSITION-CEILING-BREACH` on `APPROVED_FOR_EXECUTION`), and Deterministic Context-Routing State Machine (`src/agents/scheduler/contextRoutingStateMachine.ts`) coordinating Pass 1 (Horizontal gap-filling), Pass 2 (Supplementary corroboration & join), and Pass 3 (Red-team audit & deterministic join); Suite 28 (8/8 passed); 28 suites / 241 tests passed against live PostgreSQL 16.8. | **APPROVED / CLOSED** |
| **Gate M6.7** | 2026-10-18 | Project Owner (`Decision OD-17`) | `Market-HFT-OS: 2f918e2`<br>`ADRs: 6ace008` | Stage 7 Typed DAG Scheduler, Bounded Concurrency, Deduplication, Degraded Hold & End-to-End Capital Gate; Suite 29 (8/8 passed); 29 suites / 249 tests passed against live PostgreSQL 16.8. | **APPROVED / CLOSED** |
| **Gate M6.8** | 2026-10-18 | Project Owner (`Decision OD-18` / `Charter DEC-018`) | `Market-HFT-OS: a8b890b`<br>`ADRs: 19a1646` (Tag: `POC-001-Gate-M6.8-Verified`) | Comprehensive MCP Protocol Wire Lifecycle, Constrained HTTPS Egress Connector, First-Class Evidence Origin Firewall, Golden Extraction Certification Bench & Plan-Driven Wave Execution; Suite 30 (10/10 passed); 30 suites / 259 tests passed against live PostgreSQL 16.8. | **APPROVED / CLOSED** |
| **Gate M6.9** | 2026-10-18 | Project Owner (`Decision OD-19` / `Charter DEC-019`) | `Market-HFT-OS: 5f0dbd3`<br>`ADRs: current` (Tag: `POC-001-Gate-M6.9-Hardened-Release`) | Hardened MCP Protocol Substrate (`src/mcp/mcpSubstrate.ts`), Constrained Egress Connector, Golden Extraction Certification Bench (`src/agents/evaluation/goldenExtractionBench.ts`), Plan-Driven Topological Wave Dispatcher, 8-Workspace Read-Only Operator Terminal (`src/mcp/contracts/operatorTerminalContract.ts`, `src/terminal/operatorTerminalController.ts`), 3-Tier Kill Switch, Governed Confirmation Gate, HMAC-SHA256 & DNS-Pinned Egress Telemetry, Two-Level Error Presentation, Self-Contained HTML5/SVG Workstation, Dynamic 7-Bucket Conservation (`OTC-01`), HTML Sanitization (`OTC-02`), and 12-Point Platform Release Gate; Suite 30 (8/8 passed) & Suite 31 (12/12 passed); 31 suites / 269 tests passed against live PostgreSQL 16.8. | **APPROVED / CLOSED** |
| **Gate M7.0** | 2026-10-18 | Project Owner (`Decision OD-20` / `Charter DEC-020`) | `Market-HFT-OS: ce46eac`<br>`ADRs: 8bfa9d8` | Runnable local loopback HTTP and WebSocket workstation server (127.0.0.1:4310 / port 0); browser security firewalls (SRV-01–SRV-04); pure BigInt rational AST; Suite 32 (10/10 passed); 32 suites / 279 tests passed. | **APPROVED / CLOSED** |
| **Gate M7.1** | 2026-10-19 | Project Owner (`Decision OD-21` / `Charter DEC-021`) | `Market-HFT-OS: c0cb3d9`<br>`ADRs: current` | Provenance hardening, 5-worker ingestion pipeline, strict deduplication, TTL expiry, fixture/live badging, 8-variant SS304 matrix, and data-driven SVGs; Suite 33 (10/10 passed); 33 suites / 289 tests passed. | **APPROVED / CLOSED** |
| **Gate M7.2** | 2026-10-19 | Project Owner (`Decision OD-22` / `Charter DEC-022`) | `Market-HFT-OS: d6a070c`<br>`ADRs: current` | Multi-product observation deck (6 archetypes), sell-side dynamics, buyer grievance mining, engineered operational edge, and upstream hub sourcing; Suite 34 (10/10 passed); 34 suites / 294 tests passed. | **APPROVED / CLOSED** |
| **Gate M7.3** | 2026-10-19 | Project Owner (`Decision OD-23` / `Charter DEC-023`) | `Market-HFT-OS: 142e40c`<br>`ADRs: 31f74ec` | Modern React 19 workstation UI (`client/`), Bloomberg split-terminal, grievance mining cockpit, Groq AI strategic advisor, and standalone HTML inlining (>500 KB); Suite 35 (8/8 passed); 35 suites / 302 tests passed. | **APPROVED / CLOSED** |
| **Gate M8.0** | 2026-10-19 | Project Owner (`Decision OD-24` / `Charter DEC-024`) | `Market-HFT-OS: 0111721`<br>`ADRs: current` | Central Research & Allocation Core Loop: Durable Bitemporal Store, Need-Driven Agent Orchestrator, Epistemic Truthfulness, Real Groq Citations & Governed Multi-Scenario Bundle Simulator; Suite 36. | **APPROVED / CLOSED** |
| **Slice 1 (DEC-025)** | 2026-10-22 | Project Owner (`Decision OD-25` / `Charter DEC-025`) | `Market-HFT-OS: current`<br>`ADRs: current` | Truthful Persistence, Provenance & Attribution Baseline: PostgreSQL 16.8 tables (`market_signal_traces`, `market_product_deck_state`, `market_connector_telemetry`), cross-restart hydration, zero caller origin spoofing, exact Subunit BigInt signal economics, truthful idle connector state, and truthful Groq fallback attribution. Verified by Suite 37 (12/12 passed). | **APPROVED / CLOSED (Owner Sign-Off Granted 22 Oct 2026)** |
| **Slice 2 (DEC-026)** | 2026-10-22 | Project Owner (`Decision OD-26` / `Charter DEC-026`) | `Market-HFT-OS: current`<br>`ADRs: current` | Permitted Source Capture, Entity Identity Resolution, Adversarial Verification & 6-Hop Trace: EntityIdentityResolver across 8 canonical catalog items, POST /api/connectors/run through SourceCaptureWorker (6-layer DOM sieve, InjectionCanaryGuard prompt-injection quarantine, 90-day TTL, zero-cost substitution ban, golden fixture replay vs live HTTPS badging), ApiQuotaAndRateGovernor, cross-source conflict preservation without synthetic averaging, and connector telemetry persistence in PostgreSQL. Remediation of 4 Slice 1 catches. Verified by Suite 38 (12/12 passed). | **APPROVED / CLOSED (Owner Sign-Off Granted 22 Oct 2026)** |
| **Slice 3 (DEC-027)** | 2026-10-22 | Project Owner (`Decision OD-27` / `Charter DEC-027`) | `Market-HFT-OS: current`<br>`ADRs: current` | Category-Agnostic Dynamic Agent Planner, 6 Specialist Task Agents & 8 Incumbent-Failure Explanations: Replaces hardcoded SS304 DAG with ProductAwareDynamicResearchPlanner dynamically orchestrating 6 specialist roles (CustomerTaskAgent, SellerTaskAgent, SupplyTaskAgent, LogisticsTaskAgent, UnitEconomicsTaskAgent, AdversarialTaskAgent); evaluates 8 structural incumbent-failure explanations; implements 8-dimension Opportunity Scorecard Engine with unweighted_diagnostic_index_bps and missing_data_penalty_bps; pure BigInt multi-channel comparison across Amazon, Flipkart, Meesho, and B2B (with ESTIMATED_PROXY label); PostgreSQL 16.8 market_hypothesis_ledger persistence; and governed product-tailored DAG execution. Verified by Suite 39 (10/10 passed, 350/350 total tests passed) and Live Server Loopback Probe (6/6 passed). | **⏳ AWAITING_OWNER_SIGN_OFF** |
| **Slice 4 (DEC-028)** | 2026-10-22 | Audit Desk / Antigravity Implementation (`Decision OD-28` / `Charter DEC-028`) | `Market-HFT-OS: current`<br>`ADRs: current` | Local-First Research Query API, Review Span Miner, Single-Lead Opportunity Dossier & Rate-Governed Opt-In Synthesis: Implements ReviewAndGrievanceMiner with exact character-offset verification and denominator tracking; 9-section Opportunity Dossier with RFC 8785 JCS canonicalization, 64-char hex SHA-256 digest, and bitemporal historical cutoff (as_of_utc); LocalFirstResearchQueryEngine answering queries locally from captured evidence with zero external LLM calls by default; contradiction and gap surfacing without synthetic averaging; fail-closed explicit opt-in gate (E-QUERY-EXPLICIT-OPT-IN-REQUIRED); and ApiQuotaAndRateGovernor rate-limited opt-in Gemini/Groq synthesis with NON_AUTHORITATIVE_AI_SYNTHESIS stamping and zero secret leakage. Verified by Suite 40 (10/10 passed, 355/355 total tests passed) and Live Server Loopback Probe (9/9 passed). | **⏳ AWAITING_OWNER_SIGN_OFF** |
| **Slice 5 (DEC-029)** | 2026-10-22 | Audit Desk / Antigravity Implementation (`Decision OD-29` / `Charter DEC-029`) | `Market-HFT-OS: current`<br>`ADRs: current` | Opportunity Bundles, Unprefilled User-Intent Gate, Seasonal/Festival Overlap, Risk-Free Benchmark Comparison & Cited Research Report Exporter: Implements BundleEvaluator portfolio evaluation with mandatory 5-parameter user-intent gate (available_paper_capital_inr, minimum_return_hurdle_bps, holding_period_days, max_drawdown_limit_bps, max_single_supplier_concentration_bps); festive vs industrial calendar windows (DIWALI_FESTIVE, DURGA_PUJA, MONSOON_CORROSION_CYCLE, YEAR_ROUND_INDUSTRIAL_B2B) with suggested order cutoffs and working-capital overlap analysis; supplier and hub concentration limit gating (CONCENTRATION_LIMIT_BREACHED); sovereign benchmark comparison against RBI 91-Day T-Bill (650 bps) and SBI 1-Year Bulk FD (725 bps); 3 deterministic financial scenarios with 90-day cash-flow J-curve in pure BigInt subunits; 9-section AlphaSense/Koyfin-grade Cited Research Report Exporter with authentic [CIT-x] citations and RFC 8785 JCS digests; and governed human confirmation gate (>= 15-char rationale) with PostgreSQL market_committed_bundles persistence. Verified by Suite 41 (10/10 passed, 370/370 total tests passed, 0 skipped) and Live Server Loopback Probe (9/9 passed). | **⏳ AWAITING_OWNER_SIGN_OFF** |

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

19. **Project Owner Decision OD-17 (Gate M6.7 Stage 7 Typed DAG Scheduler, Bounded Concurrency, Deduplication, Degraded Hold & End-to-End Capital Gate)**:
    - **Stage 7 Architectural Upgrades (`src/agents/scheduler/contextRoutingStateMachine.ts`, `src/mcp/mcpSubstrate.ts`, `src/agents/workers/macroLateralWorker.ts`)**:
      - *Typed DAG Nodes & Execution Plan*: Implemented `DagTaskNode`, `DagExecutionPlan`, `DagTaskNodeStatus`, and `DagRunStatus`. Supported nodes across Pass 1 (Horizontal Gap-Filling), Pass 2 (Vertical Corroboration), Pass 3 (Red Team Audit), and Pass 4 (Deterministic Core Gate).
      - *Cycle Detection & Topological Validation*: Implemented `validateDagAcyclicity(nodes)` detecting cycles via Kahn's algorithm / DFS recursion, throwing `E-DAG-CYCLE-DETECTED` fail-closed upon circular task dependencies.
      - *Bounded Parallel Worker Concurrency*: Implemented `runBoundedParallel(tasks, max_parallel_workers)` (default 3 concurrent workers) with deterministic barrier sorting `(pass_number, node_id)` ensuring bit-for-bit identical execution plans and RFC 8785 JCS digests regardless of asynchronous event loop timing or jitter.
      - *Idempotent Task Deduplication*: Implemented canonical task node idempotency keys (`computeTaskNodeIdempotencyKey(run_id, worker_id, request_digest)`). Cache hits return `status: 'DEDUPLICATED_REPLAY'` reusing historical results without consuming additional MCP broker request quotas or invoking sub-agents.
      - *Pass 4 Deterministic Capital Gate*:
        - Connected all 5 micro-agents, Regime Classifier (`SUSTAINED_STRUCTURAL_SIGNAL` vs `FAST_TACTICAL_OPPORTUNITY`), `FactorEfficacyLedger`, and `evaluateOptimalBatchSize` (Pareto bracket selection & concentration constraints).
        - Enforces dry-run simulation mode (`execution_mode: 'PAPER_SIMULATION'`, decision `ALLOCATE_PAPER_SIMULATION`) with bitemporal restatement recording ($t_d$ and $t_k$) in `BitemporalRestatementEngine`. Real capital execution is structurally impossible without human operator ratification.
        - Fail-Closed Degraded Hold: When any provider fails or returns `DATA_REQUIRED` (e.g. macro feed down), marks the node `FAILED_DEGRADED`, assigns run status `PARTIAL_DEGRADED_HOLD`, and emits `DO_NOT_ALLOCATE_CAPITAL` with blocking reason `E-DAG-DEGRADED-PROVIDER-HOLD`.
        - Red-Team Blocking Defense: When Pass 3 Red Team disposition is not `ELIGIBLE_FOR_HUMAN_REVIEW`, capital gate emits `DO_NOT_ALLOCATE_CAPITAL` with blocking reason `E-DAG-RED-TEAM-BLOCKED`.
        - Factor Refutation Defense: When dynamic factor driver is classified `DISCREDITED_REFUTED` or historical win-rate < 50%, capital gate emits `DO_NOT_ALLOCATE_CAPITAL` with blocking reason `E-DAG-REFUTED-GROWTH-DRIVER`.
        - Edge Decay Defense: When tactical opportunity has CCC exceeding half-life ($CCC > \text{half\_life}$), capital gate fails closed with `E-MLW-EDGE-DECAYS-BEFORE-CASH-RECOVERY`.
      - *Surgical Fixes & Broker Hardening*:
        - MLW-01: Pure BigInt half-life math in `calculateHalflifeDecayBps` (`half_life_days * 86400n`).
        - MLW-02: Async LLM integration via `evaluateDynamicGrowthDriverWithAdvisor`.
        - Broker `getUsage(grantId)`: Added method to `McpCapabilityBroker` exposing real-time usage metrics.
    - **Acceptance Tests & Evidence Separation (`Suite 29`)**:
      - Implemented `tests/acceptance/suite29_m6_7_context_dag_and_cooperation.test.ts` (8 normative assertions):
        1. `MCP-DAG-ASYNC-BARRIER-JCS-DETERMINISM-001`: Proves bounded parallel execution with random jitter yields bit-for-bit identical RFC 8785 JCS digests under canonical barrier sorting.
        2. `MCP-DAG-COMPLEMENTARY-AND-SUPPLEMENTARY-COOPERATION-002`: Executes 4-pass DAG coordinating all 5 micro-agents and proves optimal batch sizing.
        3. `MCP-DAG-IDEMPOTENT-DEDUPLICATION-NO-QUOTA-003`: Proves duplicate node execution returns `DEDUPLICATED_REPLAY` without consuming MCP broker quotas.
        4. `MCP-DAG-DEGRADED-PROVIDER-HOLD-004`: Simulates provider timeout/failure, asserting `PARTIAL_DEGRADED_HOLD` and `DO_NOT_ALLOCATE_CAPITAL`.
        5. `MCP-DAG-ACYCLICITY-CYCLE-REJECTION-005`: Proves cyclic dependency graph fails closed with `E-DAG-CYCLE-DETECTED`.
        6. `MCP-DAG-BITEMPORAL-REPLAY-EQUIVALENCE-006`: Validates bitemporal restatement $t_0 \to t_1$ and historical replay invariance.
        7. `MCP-DAG-REFUTED-DRIVER-BLOCKS-CAPITAL-007`: Validates discredited factor driver blocks capital gate with `E-DAG-REFUTED-GROWTH-DRIVER`.
        8. `MCP-DAG-TACTICAL-EDGE-DECAY-REJECTION-008`: Validates $CCC > \text{half\_life}$ triggers `E-MLW-EDGE-DECAYS-BEFORE-CASH-RECOVERY`.
    - **Full Baseline Conformance**:
      - Full test baseline expanded to **249 passed tests across 29 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
      - Dedicated Gate M6.7 evidence files generated:
        - `POC-001_Gate_M6_7_Test_Execution_Results.json` (SHA-256: `3002FE6935AA3ECD8A0B110FD540B2647951A534F754AF813ED38341A0FDFDC7`, 249 tests).
        - `POC-001_Gate_M6_7_Typecheck_Execution_Results.txt` (SHA-256: `34EB2E7BF4A843CF8B8757466FAF65929EFA90339B18470CB3284D23F76A19A7`, 0 errors).
    - Gate M6.7 status is authoritatively confirmed as **APPROVED / CLOSED**.

20. **Project Owner Decision OD-18 (Gate M6.8 Comprehensive MCP Protocol Hardening, Constrained Egress Connector, First-Class Evidence Origin Firewall, Provider Certification & Plan-Driven DAG Execution Closure)**:
    - **Stage 8 Implementation & Architecture (`src/mcp/mcpSubstrate.ts`, `src/agents/evaluation/goldenExtractionBench.ts`, `src/research/llmFormulaAdvisor.ts`, `src/agents/scheduler/contextRoutingStateMachine.ts`, `src/research/m5SignalAndEvidenceEngine.ts`, `src/mcp/contracts/redTeamContract.ts`, `src/agents/workers/redTeamWorker.ts`)**:
      - *MCP Wire Lifecycle & Transport Protocol*: Implemented `handleRpcMessage` supporting full JSON-RPC 2.0 / MCP 2025-11-25 wire lifecycle: `initialize` (negotiating server protocol version `2025-11-25`, server capabilities, and server info), `notifications/initialized`, `ping`, `tools/list`, `resources/list`, `resources/read`, `notifications/cancelled`, and `tools/call`.
      - *Positive Tool Manifest Registry & Code Attestation*: Replaced ad-hoc regex blacklists with strict positive JSON schemas enforcing `additionalProperties: false` (throwing `E-MCP-UNKNOWN-ARGUMENT-REJECTED`) and cryptographic handler attestation (verifying handler SHA-256 against registered manifest hash, throwing `E-MCP-HANDLER-TAMPERED`).
      - *HMAC-SHA256 Signed Capability Grants & Wall-Clock Budget*: Added cryptographic HMAC-SHA256 signatures (`grant_signature_hmac`) to `CapabilityGrant` generated via `signCapabilityGrant` and validated fail-closed via `verifyCapabilityGrantSignature`. Enforced calling worker and task identity validation (`E-MCP-WORKER-IDENTITY-MISMATCH`) and cumulative task wall-clock budget (`E-MCP-TASK-WALL-CLOCK-EXCEEDED`).
      - *Constrained HTTPS Egress Connector*: Hardened network egress to port 443 only (`E-MCP-PORT-DENIED`), DNS pre-resolution checking private/loopback/metadata IPs (`E-MCP-DNS-REBINDING-OR-PRIVATE-IP-DENIED`), streaming byte cutoff via `ReadableStream` reader immediately aborting the underlying socket (`E-MCP-STREAM-PAYLOAD-TOO-LARGE`), and abort signal timeout.
      - *Append-Only McpRunLedger File Persistence*: Implemented durable disk persistence via `saveLedgerToFile` and `loadLedgerFromFile`, validating RFC 8785 JCS monotonic hash chains and throwing `E-MCP-LEDGER-TAMPERED` upon post-hoc mutation.
      - *First-Class Evidence Origin Firewall*: Formally introduced `EvidenceOriginClass = 'LIVE_VERIFIED_CAPTURE' | 'RECORDED_GOLDEN_FIXTURE' | 'CALLER_SUPPLIED_PAYLOAD' | 'SYNTHETIC_SIMULATION' | 'LLM_MODEL_PROPOSAL'`. Preserved distinct `requested_url` (canonical supplier catalog URI) and `resolved_source_identity` (e.g. `caller://raw_html_payload` or `fixture://...`). Enforced origin promotion firewall in `EvidencePromotionEngine` and red-team rule `RT-08-NON-LIVE-EVIDENCE-ORIGIN`, strictly prohibiting non-live origins from promoting to `VERIFIED_EXECUTABLE_OFFER` (`E-EV-NON-LIVE-ORIGIN-PROMOTION-FORBIDDEN`).
      - *Look-Ahead Bias Elimination*: Macro and statutory workers enforce that observation timestamps and circular effective dates do not exceed task `reference_time_utc`, failing closed with `E-MLW-LOOKAHEAD-BIAS-REJECTED`.
      - *Groq LLM Egress Boundary & Secret Redaction*: In `src/research/llmFormulaAdvisor.ts`, network egress is locked strictly to `APPROVED_GROQ_ENDPOINT = 'https://api.groq.com/openai/v1/chat/completions'` (`E-GROQ-UNAPPROVED-ENDPOINT`), input secrets are scrubbed via `redactPromptSecrets`, and generated formula proposals are tagged with origin `LLM_MODEL_PROPOSAL`.
      - *Adala-Inspired Golden Extraction Bench*: Implemented `GoldenExtractionBench` evaluating precision, recall, and exact match rates in pure BigInt basis points (`10000n` bps required for `certified_pass = true`).
      - *Plan-Driven Topological Wave Dispatcher*: Implemented `executeCompiledDagPlan` in `ContextRoutingStateMachine` evaluating node `activation_predicate`, bounded parallel wave batches, cumulative wall-clock budget checking (`E-DAG-BUDGET-OVERFLOW`), and durable JCS checkpointing (`DagCheckpointStore.saveCheckpointToFile` / `resumeFromCheckpoint`).
    - **Acceptance Tests & Evidence Separation (`Suite 30`)**:
      - Implemented `tests/acceptance/suite30_m6_8_mcp_hardening_and_worker_certification.test.ts` (10 normative acceptance tests).
      - Full test baseline expanded to **259 passed tests across 30 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
      - Dedicated Gate M6.8 evidence files generated:
        - `POC-001_Gate_M6_8_Test_Execution_Results.json` (SHA-256: `D51FB20D6570B7B8B0260C6560D655B0639CCF4DFBE7F4107D04D38DB3A42A78`, 259 tests).
        - `POC-001_Gate_M6_8_Typecheck_Execution_Results.txt` (SHA-256: `957B9839BF6E3D6165A6B902132DAAAB9CE8E65C5ACF3AC7867D6406123ADE57`, 0 errors).
    - Gate M6.8 status is authoritatively confirmed as **APPROVED / CLOSED**.

21. **Project Owner Decision OD-19 (Gate M6.9 Stage 9 Read-Only Operator Terminal, Safety Controls, Egress Telemetry & 12-Point Release Gate Closure)**:
    - **Stage 9 Implementation & Architecture (`src/mcp/contracts/operatorTerminalContract.ts`, `src/terminal/operatorTerminalController.ts`)**:
      - *8-Workspace Read-Only Projection Layer*: Implemented strictly read-only terminal projections for all 8 workspaces (`POC.docx` §10):
        1. Command Center: Live Origin Breakdown (% of research backed by `LIVE_VERIFIED_CAPTURE` vs `RECORDED_GOLDEN_FIXTURE`), Kill-Switch Halt Scope banner, and Cumulative Task Wall-Clock Budget utilization. Anti-vanity profit firewall (`E-M9-VANITY-PROFIT-FORBIDDEN`) strictly prevents combining forecasts, paper results, and actuals into a single vanity number (`POC.docx` §10.1).
        2. Opportunity Radar: Explicitly distinguishes `MEASURED_DEADLINE` from `MODELLED_ESTIMATE` timers and badges each candidate with temporal regime (`SUSTAINED_STRUCTURAL_SIGNAL` vs `FAST_TACTICAL_OPPORTUNITY`) and `evidence_origin_class`.
        3. Evidence Workbench: Exposes `requested_url` vs `resolved_source_identity` side-by-side, origin promotion firewall blocks (`E-EV-NON-LIVE-ORIGIN-PROMOTION-FORBIDDEN`), and look-ahead bias checks (`published_at_utc <= as_of_utc`).
        4. Economic & Simulation Sandbox: Side-by-side comparison of baseline vs shock, formula AST expression lineage, unit-level cost breakdown, and full sensitivity ladder.
        5. Capital Allocation & Review Queue: Displays all 10 required comparison dimensions (`POC.docx` §8) without collapsing into a single score; strictly enforces Conviction vs Allocation separation (capping allocation at ₹0.00 for non-live fixtures/unverified listings); provides full drill-down lineage to source SHA-256 (`POC.docx` §10.2).
        6. Strategy & Factor Lifecycle: Exposes active factors, empirical efficacy scores, regime classifications, decay status, and half-life monitoring.
        7. Risk & Exposure Monitor: Tracks portfolio-wide gross exposure, unrecovered cash, single-supplier concentration, MSME 43B(h) payment aging, and real-time 7-bucket inventory conservation (`E-M9-RECONCILIATION-EXCEPTION`).
        8. Statutory & Audit Ledger: Complete immutable audit log of verified circular citations, prompt-injection defense logs, HMAC-SHA256 capability grants, DNS-pinned egress calls, and Golden Extraction certification bench results.
      - *3-Tier Kill Switch Controller (`KillSwitchController`)*: Implements all 3 halt tiers from `POC.docx` §8: `HALT_NEW_ALLOCATIONS`, `HALT_ALL_SIMULATION_PROCESSING`, and `ENTER_RECOVERY_ONLY_MODE`. Emits structured audit events and preserves 100% of historical records.
      - *Governed Confirmation Gate (`executeGovernedOperatorAction`)*: Requires confirmation token matching the action and an operator rationale string $\ge 15$ characters (`E-M9-CONFIRMATION-AND-RATIONALE-REQUIRED`).
      - *Two-Level Error Presentation & Secret Scrubbing (`formatTwoLevelError`)*: Scrubs sensitive secrets (`Groq_Key.env`, `gsk_...`, DB passwords) with `[E-M9-SECRET-REDACTED]`, providing high-level business explanations for operators while preserving technical diagnostics and distinguishing `DEFINITE_FAILURE` from `OUTCOME_UNKNOWN_RECONCILIATION_REQUIRED` on write timeouts.
      - *Self-Contained HTML5/SVG Workstation Renderer (`renderOperatorTerminalHtml`)*: Produces dark-mode terminal UI with tabbed workspace navigation, dynamic SVG data visualizations (origin distribution bar, portfolio risk pie, capital deployment curve), status badges, and telemetry tables.
      - *12-Point Platform Release Gate (`evaluateTwelvePointPlatformReadiness`)*: Evaluates all 12 platform release criteria from `POC.docx` §13, producing an RFC 8785 JCS canonical SHA-256 readiness certificate.
    - **Acceptance Tests & Evidence Separation (`Suite 30` & `Suite 31`)**:
      - Maintained `tests/acceptance/suite30_m6_8_operator_terminal_and_release_gate.test.ts` (8 normative acceptance tests for Stage 8 Operator Terminal & 12-Point Release Gate).
      - Implemented `tests/acceptance/suite31_m6_9_mcp_hardening_and_terminal_certification.test.ts` (12 normative acceptance tests covering MCP wire protocol lifecycle, positive manifests, HMAC capability grants, constrained HTTPS egress, DNS pre-resolution, streaming byte cutoff, honest evidence origin firewall, look-ahead bias checks, brokered Groq LLM egress, Adala-style GoldenExtractionBench certification at 10000n bps, plan-driven topological wave DAG dispatcher, durable ledger/checkpoint persistence, operator terminal origin/HMAC/bench telemetry badges, dynamic 7-bucket check OTC-01, and HTML sanitization OTC-02).
      - Full test baseline expanded to **269 passed tests across 31 suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`).
      - Dedicated Gate M6.9 evidence files generated:
        - `POC-001_Gate_M6_9_Test_Execution_Results.json` (SHA-256: `FA0699204A5A2A66822ED2032B3EF78F95AFD0CB5F3589C880FD08CFC2C95B72`, 269 tests).
        - `POC-001_Gate_M6_9_Typecheck_Execution_Results.txt` (SHA-256: `A5A992297C6739D45A6C4B9347C5F84DB162FC660C39605928F7EEBEE660C9F7`, 0 errors).
    - Gate M6.9 status is authoritatively confirmed as **APPROVED / CLOSED**.

22. **Project Owner Decision OD-20 (Gate M7.0 Runnable Local Loopback Workstation Server, Authoritative State Manager, Interactive 8-Workspace Client & Zero-Trust Security Acceptance Gate Closure)**:
    - **Gate M7.0 Implementation & Architecture (`src/server/workstationServer.ts`, `src/server/workstationStateManager.ts`, `src/cli/workstationCli.ts`, `src/terminal/operatorTerminalController.ts`)**:
      - *Runnable Local Loopback Workstation Server (`WorkstationServer`)*: Implemented HTTP/WebSocket server strictly confined to loopback interface (`127.0.0.1` / `localhost`) per `POC.docx` §10.5, throwing `E-SRV-NON-LOOPBACK-BIND-FORBIDDEN` if any external or wildcard interface is requested. Default port `4310`, with support for ephemeral OS port assignment (`port: 0`) for collision-free test runs (`SRV-04`).
      - *Browser DNS-Rebinding & CSWSH Firewall (`SRV-01`)*: Inspects `Host` header on every request, rejecting non-loopback hosts with HTTP 403 Forbidden and `E-SRV-INVALID-HOST-HEADER`. Validates `Origin` header on all `POST` requests and WebSocket `/ws` upgrades, rejecting cross-origin attackers with HTTP 403 Forbidden and `E-SRV-CROSS-ORIGIN-BLOCKED`. Enforces hard 64 KB (65,536 bytes) request body cap, rejecting oversized payloads with HTTP 413 and `E-SRV-REQUEST-BODY-TOO-LARGE`.
      - *Strict Security Headers (`SRV-01`)*: Enforces `Content-Security-Policy: default-src 'self' 'unsafe-inline'; frame-ancestors 'none'`, `X-Frame-Options: DENY`, `X-Content-Type-Options: nosniff`, and `Cache-Control: no-store` on all responses.
      - *Zero Client-Side Float Math / Zero Optimistic UI (`SRV-02`)*: UI is strictly a read-only projection (`POC.docx` §10.5). What-If evaluations execute purely on the backend via `stateManager.evaluateWhatIfFormula` evaluating symbolic expressions in pure `BigInt` rational AST arithmetic (`CANDIDATE_UI_MODEL` tier), completely eliminating JavaScript IEEE 754 floating-point drift and client-side optimistic state mutations.
      - *Live Kill-Switch Fail-Closed Enforcement (`SRV-03`)*: When kill switch is `HALT_ALL_SIMULATION_PROCESSING` or `ENTER_RECOVERY_ONLY_MODE`, `POST /api/actions/run-dag` fails closed with HTTP 409 Conflict and `TwoLevelErrorEnvelope` (`E-M8-KILLSWITCH-ALL-SIMULATION-HALTED` / `E-M8-KILLSWITCH-RECOVERY-ONLY`), while read-only inspection endpoints (`GET /`, `GET /api/snapshot`, `GET /api/health`, `GET /api/certificate`) remain 100% available and responsive.
      - *Live WebSocket Snapshot Broadcast*: WebSocket clients connecting to `ws://127.0.0.1:<port>/ws` receive initial snapshot immediately (`SNAPSHOT_INITIAL`), followed by live real-time broadcast of all authoritative state transitions (`TERMINAL_SNAPSHOT_BROADCAST`).
      - *CLI Workstation Runner (`src/cli/workstationCli.ts`)*: Added `"workstation": "tsx src/cli/workstationCli.ts"` script to `package.json`, printing structured terminal banner with loopback URLs and security status on startup.
    - **Acceptance Tests & Evidence Separation (`Suite 32`)**:
      - Implemented `tests/acceptance/suite32_m7_0_workstation_server.test.ts` (10 normative acceptance tests):
        1. `MCP-WRK-NON-LOOPBACK-BIND-REJECT-001`: Strict loopback confinement (127.0.0.1 / localhost only).
        2. `MCP-WRK-DNS-REBINDING-HOST-FIREWALL-002`: Host header DNS-rebinding rejection (HTTP 403 / `E-SRV-INVALID-HOST-HEADER`).
        3. `MCP-WRK-CSWSH-ORIGIN-FIREWALL-003`: Cross-site POST & WebSocket upgrade rejection (HTTP 403 / `E-SRV-CROSS-ORIGIN-BLOCKED`).
        4. `MCP-WRK-REQUEST-BODY-CAP-004`: 64 KB request envelope cap rejection (HTTP 413 / `E-SRV-REQUEST-BODY-TOO-LARGE`).
        5. `MCP-WRK-SECURITY-HEADERS-ENFORCED-005`: Strict security headers on all HTTP responses (CSP, XFO, nosniff, no-store).
        6. `MCP-WRK-READ-ONLY-PROJECTION-ROOT-006`: Self-contained HTML5/SVG terminal rendering with all 8 workspaces.
        7. `MCP-WRK-READ-ONLY-API-ENDPOINTS-007`: Frozen snapshot, health, and 12-point platform readiness certificate APIs.
        8. `MCP-WRK-KILL-SWITCH-GOVERNED-ACTION-008`: 3-tier kill-switch transition requiring $\ge 15$-character rationale.
        9. `MCP-WRK-KILL-SWITCH-DAG-HALT-ENFORCEMENT-009`: DAG execution fail-closed (HTTP 409) under halt scopes (`SRV-03`).
        10. `MCP-WRK-WEBSOCKET-LIVE-BROADCAST-010`: Live WebSocket broadcast of snapshot transitions (`TERMINAL_SNAPSHOT_BROADCAST`).
    - **Full Baseline Conformance**:
      - Full test baseline expanded to **279 passed tests across 32 contiguous suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`) and 0 TypeScript compilation errors.
      - Dedicated Gate M7.0 evidence files generated:
        - `POC-001_Gate_M7_0_Test_Execution_Results.json` (SHA-256: `8A4E3D35960B94E545352E1231FF55D3C6A2A237461FF6E83211B57FC913BEE1`, 279 tests).
        - `POC-001_Gate_M7_0_Typecheck_Execution_Results.txt` (SHA-256: `7C70531016D2170F58C0AA0159CBA4B6B90949D6E57707CB71232ECA3011B323`, 0 errors).
    - Gate M7.0 status is authoritatively confirmed as **APPROVED / CLOSED**.

23. **Project Owner Decision OD-21 (Gate M7.1 Multi-Channel Signal Ingestion Pipeline, Provenance Hardening, 8-Variant SS304 Matrix & 3-Pane Research Cockpit UI Closure)**:
    - **Gate M7.1 Implementation & Architecture (`src/research/m5SignalAndEvidenceEngine.ts`, `src/mcp/contracts/signalIngestionContract.ts`, `src/server/workstationStateManager.ts`, `src/server/workstationServer.ts`, `src/terminal/operatorTerminalController.ts`, `src/cli/exportStandaloneHtml.ts`)**:
      - *Provenance Hardening & Fallback Elimination*: Completely eliminated hardcoded fallback signal magnitudes and simulated assumptions from `src/research/m5SignalAndEvidenceEngine.ts`. Mandatory supplier quote components (`unit_price_subunits`, `inbound_freight_subunits`, `packaging_kitting_subunits`) must be present or extraction fails closed with `DATA_REQUIRED` (`E-SIG-MANDATORY-FIELD-MISSING`). Seed state boots badged `RECORDED_GOLDEN_FIXTURE` (`[FIXTURE]`); promotion to `LIVE_VERIFIED_CAPTURE` (`[LIVE]`) requires genuine live capture tool calls recorded in `McpRunLedger`.
      - *Genuine 5-Worker DAG Execution*: Replaced stubbed DAG closure in `WorkstationStateManager.triggerGovernedDagRun` with genuine execution of all 5 certified MCP specialist workers (`SourceCaptureWorker`, `MacroAndLateralMarketWorker`, `GovtAndStatutoryWorker`, `MediaAndChatterWorker`, `RedTeamAndConflictWorker`) via `ContextRoutingStateMachine`, logging verifiable `TOOL_CALL_INVOKED` events to the append-only `mcpRunLedger`.
      - *Multi-Channel Signal Ingestion Pipeline*: Implemented `ingestSignalEnvelope` across 6 distinct signal channels (`RAW_MATERIAL_BENCHMARK_FEED`, `TRADE_POLICY_STATUTORY_RECORD`, `FREIGHT_RATE_SURCHARGE_INDEX`, `MARKETPLACE_OR_SUPPLIER_HTML`, `COMMUNITY_SOCIAL_MEDIA_STREAM`, `SYNTHETIC_SIMULATION_SCENARIO`). Enforces 3-tier kill switch state, payload size limit, look-ahead bias validation (`timestamp_utc <= as_of_utc`), 90-day stale TTL rejection (`E-SIG-EVENT-EXPIRED`), idempotency deduplication (`E-SIG-DUPLICATE-ENVELOPE`), canary scanning (`InjectionCanaryGuard` / `E-SIG-INJECTION-ATTEMPT-QUARANTINED`), connector routing, and 6-stage lineage tracing (`SignalProcessingTraceRecord`).
      - *REST API Endpoints*: Exposed `POST /api/signals/ingest`, `GET /api/signals/inbox`, `GET /api/signals/trace`, and `GET /api/variants/ss304` on `WorkstationServer`, protected by the loopback interface, Host header firewall, and CSWSH origin verification.
      - *8-Variant SS304 DIN 3017 Matrix*: Integrated the complete 8-variant SS304 commodity hose clamp catalog (W1 through W5 material specs, 8-12mm to 50-70mm diameter ranges, pack sizes 10 to 100) with deterministic bitemporal 36-point J-curves, landed cost breakdowns, and capital allocation recommendations.
      - *3-Pane Institutional Research Cockpit UI & Data-Driven SVGs*:
        - Designed institutional 3-pane layout: Top Telemetry Header (Kill Switch, Live/Fixture Origin Breakdown, Conserved Capital, Memory/Host Telemetry), Left Navigation Tabs (Workspaces 0–8), Center Cockpit Workspace, and Right Slide-Over Lineage Drawer (`#lineage-drawer`).
        - Integrated Workspace 0: 5 Source Connectors status table, Signal Intake form with 7 preset buttons, real-time Signal Surveillance inbox table, and the 8-Variant SS304 DIN 3017 matrix table.
        - Replaced mock SVG charts with 100% data-driven SVG generators (`renderDataDrivenJCurveSvg`, `renderDataDrivenSpreadBandsSvg`, `renderDataDrivenGreeksSvg`, `renderDataDrivenConvictionMatrixSvg`) based on authoritative BigInt backend state.
        - Standalone HTML export updated in `src/cli/exportStandaloneHtml.ts` generating self-contained file `dist/POC-001_Standalone_Workstation.html`.
    - **Acceptance Tests & Evidence Separation (`Suite 33`)**:
      - Implemented `tests/acceptance/suite33_m7_1_signal_ingestion_and_cockpit_ui.test.ts` (10 normative acceptance tests):
        1. `M71-SIG-CHANNEL-INGESTION-001`: Multi-channel ingestion across 6 channels.
        2. `M71-SIG-QUARANTINE-INJECTION-002`: Prompt injection detection and quarantine (`E-SIG-INJECTION-ATTEMPT-QUARANTINED`).
        3. `M71-SIG-DEDUPLICATION-003`: Duplicate envelope rejection (`E-SIG-DUPLICATE-ENVELOPE`).
        4. `M71-SIG-LOOKAHEAD-BIAS-004`: Future timestamp rejection (`E-SIG-LOOKAHEAD-BIAS-DETECTED`).
        5. `M71-SIG-STALE-TTL-005`: Stale event rejection (>90 days, `E-SIG-EVENT-EXPIRED`).
        6. `M71-SIG-MANDATORY-COSTS-006`: Missing mandatory supplier quote rejection (`E-SIG-MANDATORY-FIELD-MISSING`).
        7. `M71-SIG-PROVENANCE-HONESTY-007`: Initial fixture badging (`[FIXTURE]`) and live promotion (`[LIVE]`) after DAG tool invocation.
        8. `M71-SIG-SS304-CATALOG-008`: 8-variant SS304 DIN 3017 matrix completeness and 36-point J-curves.
        9. `M71-SIG-UI-COCKPIT-PANE-009`: Workspace 0 cockpit, connectors table, preset buttons, and lineage drawer in HTML projection.
        10. `M71-SIG-DATA-DRIVEN-SVG-010`: Real data-driven SVG rendering in Economics and Capital Allocator workspaces.
    - **Full Baseline Conformance**:
      - Full test baseline expanded to **289 passed tests across 33 contiguous suites (0 skipped, 0 failed)** with live PostgreSQL 16.8 (`localhost:5432`) and 0 TypeScript compilation errors.
      - Dedicated Gate M7.1 evidence files generated:
        - `POC-001_Gate_M7_1_Test_Execution_Results.json` (SHA-256: `21623F9A6F1A23C99A0A15C00D647B395CF14AC437DDC3A991141DC0AE1BCC52`, 289 tests).
        - `POC-001_Gate_M7_1_Typecheck_Execution_Results.txt` (SHA-256: `174101613E05AFFB47F166F4C0E244508D25007496395CECA4123C36425003F7`, 0 errors).
    - Gate M7.1 status is authoritatively confirmed as **APPROVED / CLOSED**.

24. **Project Owner Decision OD-22 (Gate M7.2 Multi-Product Universe Observation Deck, Sell-Side Analytics, Buyer Grievance Mining, Engineered Operational Edge & Governed Research Dispatch Closure)**:
    - **Gate M7.2 Implementation & Architecture (`src/mcp/contracts/productObservationContract.ts`, `src/research/productObservationDeckRegistry.ts`, `src/server/workstationStateManager.ts`, `src/server/workstationServer.ts`, `src/terminal/operatorTerminalController.ts`, `src/cli/exportStandaloneHtml.ts`)**:
      - *Multi-Product Universe Expansion*: Expanded catalog from single-product SS304 vertical slice to an extensible, category-agnostic multi-product observation deck across 6 commercial archetypes (`CLUSTER_MRO_STANDARDIZED`, `TECHNICAL_COMPLIANCE`, `SEASONAL_D2C_VISUAL`, `D2C_CONSUMABLE`, `MRO_INDUSTRIAL`, `REPLACEMENT_PARTS`) and 7 industrial/consumer categories. Preserves SS304 DIN 3017 (`prod:din3017:ss304:16-25mm:pack-10`) as the immutable `is_guiding_reference: true` anchor.
      - *Sell-Side Marketplace Dynamics ("What Others Are Selling")*: Captures primary marketplace, product listing URLs, BSR (Best Seller Rank), monthly sales volume estimates, monthly gross revenue in INR, prevailing retail ASP, active competitor count, top competitor brand names, and dominant pack formats for each product.
      - *Buyer Review Grievance Mining ("What Buyers Are Noting as Feedback")*: Analyzes negative review frequency and categorizes structured customer grievances (`QUALITY_DEFECT`, `DURABILITY_FAILURE`, `SAFETY_HAZARD`, `PACKAGING_DAMAGE`, `REGULATORY_NON_COMPLIANCE`, `SPEC_MISMATCH`), capturing failure modes and verbatim representative buyer feedback quotes.
      - *Engineered Operational Edge (Quality Fix Formulation)*: Directly formulates exact physical, metallurgical, chemical, and operational remediations (e.g. Geomet 500 coating, optical thread sorting, platinum-cured VMQ silicone, BIS certification) to systematically eliminate negative reviews and capture the marketplace Buy Box.
      - *Upstream Sourcing Hub Cluster & Financial Spread Analysis*: Models geographic manufacturing hubs (Jamnagar, Ludhiana, Jalandhar, Khurja, Vasai/Pune, Moradabad), factory-gate unit quotes, MOQs, lead times, raw material bases, landed costs, gross spreads, contribution margin bps, and annualized RoWC bps with conservative working capital and CCC calculations.
      - *Governed Strategic Arbitrage & Research Dispatch*: Defines explicit strategic decisions (`PURSUE`, `INVESTIGATING`, `MONITOR_ONLY`, `REJECT`), bull-case rationale, and bear-case downside risk. Dispatches research tasks to specialist workers via `ContextRoutingStateMachine` with full `McpRunLedger` audit logging.
      - *Interactive Observation Deck Table & Slide-Over Teardown Drawer*: Integrated into Workspace 0 with category/archetype filter pills, expandable "+ Push Product to Deck" operator form, dual-mode slide-over drawer (`#lineage-drawer`) presenting comprehensive product teardowns, and full cross-workspace reflection into Opportunity Radar (Workspace 2) and Evidence Workbench (Workspace 3).
      - *Offline Standalone HTML Bundle*: Exported self-contained bundle `dist/POC-001_Standalone_Workstation.html` with all 8 products and offline drawer interactivity.
    - **Acceptance Tests & Evidence Separation (`Suite 34`)**:
      - Implemented `tests/acceptance/suite34_m7_2_multi_product_observation_deck.test.ts` (10 normative acceptance tests):
        1. `M72-PROD-CATALOG-ARCHETYPES-001`: Multi-product catalog completeness across 6 archetypes.
        2. `M72-PROD-SELLSIDE-DYNAMICS-002`: Marketplace sell-side dynamics and revenue estimates.
        3. `M72-PROD-GRIEVANCE-MINING-003`: Buyer review grievance clustering and verbatim quotes.
        4. `M72-PROD-OPERATIONAL-EDGE-004`: Engineered quality remediation formulations.
        5. `M72-PROD-UPSTREAM-SPREADS-005`: Upstream hub sourcing, landed costs, and financial spreads.
        6. `M72-PROD-PUSH-OBSERVATION-006`: Fail-closed ingestion of new product observations.
        7. `M72-PROD-RESEARCH-DISPATCH-007`: Governed research dispatch and ledger recording.
        8. `M72-PROD-REST-ENDPOINTS-008`: Workstation server REST API verification (`/api/products/*`).
        9. `M72-PROD-UI-DRAWER-INTERACTION-009`: HTML markup, drawer interactivity, and archetype filters.
        10. `M72-PROD-CROSS-WORKSPACE-010`: Cross-workspace projection into Opportunity Radar and Evidence Workbench.
    - **Full Baseline Conformance**:
      - Full test baseline expanded to **294 passed tests across 34 contiguous suites (0 failed, 6 skipped conditional postgres)** with 0 TypeScript compilation errors.
      - Dedicated Gate M7.2 evidence files generated:
        - `POC-001_Gate_M7_2_Test_Execution_Results.json` (SHA-256: `E74CAFD0509178F5A3F11C55F0079FC212D3DCC8866006B14D209AEFF7B7CD37`, 294 tests).
        - `POC-001_Gate_M7_2_Typecheck_Execution_Results.txt` (SHA-256: `E3B0C44298FC1C149AFBF4C8996FB92427AE41E4649B934CA495991B7852B855`, 0 errors).
    - Gate M7.2 status is authoritatively confirmed as **APPROVED / CLOSED**.

25. **Project Owner Decision OD-23 (Gate M7.3 Modern React Workstation UI, Bloomberg Split-Terminal Temporal Dynamics, Multi-Product Grievance Mining Cockpit & Groq AI Strategic Advisor Certification Closure)**:
    - **Gate M7.3 Implementation & Architecture (`client/`, `src/server/workstationServer.ts`, `src/terminal/operatorTerminalController.ts`, `src/cli/exportStandaloneHtml.ts`)**:
      - *Modern React 19 + Tailwind CSS + Lucide Workstation UI (`client/`)*: Completely redesigned the user interface into a modern, responsive single-page application built on React 19, Tailwind CSS v4, Lucide icons, and Vite. Decoupled from backend dependencies to maintain strict zero-runtime-npm compliance in `Market HFT OS` core (`ADR-0004`).
      - *Primary Product Opportunity & Grievance Mining Cockpit (`CockpitHome.tsx`)*: Elevated as the primary home view, showcasing all 8 products across 6 commercial archetypes, with top KPI ribbons (aggregate volume, gross capture revenue, active investigations), archetype filter pills, live search, and collapsible "+ Push Product to Deck" observation form.
      - *Rich Grievance Teardowns & Operational Edge Formulations*: Highlights verbatim customer feedback quotes, failure severity badges (`CRITICAL`, `HIGH`), and exact physical/operational fixes directly on product cards and in the comprehensive 4-tab slide-over inspection drawer (`ProductTeardownDrawer.tsx`).
      - *Bloomberg-Style Split-Screen Temporal & Market Dynamics Terminal (`BloombergSplitTerminal.tsx`)*:
        - *Left Screen (Fundamentals)*: Interactive Landed Cost Waterfall SVG chart (Factory Gate $\to$ Inbound Freight $\to$ Packaging/Kitting $\to$ Buffer $\to$ Net Landed $\to$ Target ASP), volume margin sensitivity ladder, Cash Conversion Cycle (CCC) metrics, and live What-If sandbox evaluating symbolic expressions via pure BigInt rational AST on the backend (`POST /api/actions/what-if-formula`).
        - *Right Screen (Market Forces)*: 36-point bitemporal raw material benchmark wave vs capture spread, competitor seller concentration, return rate reduction metrics, and Buy Box capture probability surface.
        - *Split-Screen Controls*: Dynamic timeframe selection (`1D`, `7D`, `30D`, `90D`, `1Y`), macro regime toggle (`BASE`, `SHOCK`, `OPTIMISTIC`), and split layout toggles (50/50, left-heavy, right-heavy, maximized).
      - *Autonomous Micro-Agent Research Desk (`AgentResearchDesk.tsx`)*: Visualizes the 5 certified specialist workers (`SourceCapture`, `MacroMarket`, `GovtStatutory`, `MediaChatter`, `RedTeamConflict`), 7-stage governed topological wave execution, live append-only execution log stream, and governed DAG action dispatch with rationale validation.
      - *Groq AI Strategic Advisor (`GroqAiIntelligenceModal.tsx` & `/api/ai/analyze`)*: Integrated LLM opportunity synthesizer powered by Groq (`llama-3.3-70b-versatile`), extracting unserved customer pain points, suggesting engineered operational edges, and commenting on commodity price sensitivities.
      - *WorkstationServer Static Asset Delivery & Root Injection*: `WorkstationServer` delivers compiled Vite client bundles (`/assets/*`) with strict security headers (CSP, nosniff, cache control). `renderOperatorTerminalHtml` automatically discovers client bundles, mounting `<div id="root"></div>` in the browser while preserving all semantic DOM hooks and test assertions for headless runners.
      - *100% Inlined Offline Standalone HTML*: `src/cli/exportStandaloneHtml.ts` generates `dist/POC-001_Standalone_Workstation.html` (583,782 bytes) with the entire compiled React bundle and styles inlined for completely offline inspection.
    - **Acceptance Tests & Evidence Separation (`Suite 35`)**:
      - Implemented `tests/acceptance/suite35_m7_3_modern_react_workstation_ui.test.ts` (8 normative acceptance tests):
        1. `M73-UI-CLIENT-BUNDLE-INTEGRITY-001`: Vite production build bundle integrity in `dist/client/assets`.
        2. `M73-UI-SERVER-STATIC-ASSETS-002`: WorkstationServer delivery of static JS/CSS bundles with security headers.
        3. `M73-UI-HTML-MOUNT-INJECTION-003`: Root HTML mount injection and backward-compatible test hooks.
        4. `M73-UI-BLOOMBERG-SPLIT-TERMINAL-004`: Bloomberg split-terminal What-If formula simulation integration.
        5. `M73-UI-GROQ-AI-ANALYZE-API-005`: `/api/ai/analyze` endpoint validation and structured AI recommendations.
        6. `M73-UI-STANDALONE-INLINED-HTML-006`: Standalone HTML snapshot inlined self-contained bundling (>500 KB).
        7. `M73-UI-AGENT-RESEARCH-DESK-007`: 5-Worker DAG dispatcher contract and ledger telemetry verification.
        8. `M73-UI-GRIEVANCE-MINING-COCKPIT-008`: Multi-product grievance clustering and operational edge formulation.
    - **Full Baseline Conformance**:
      - Full test baseline expanded to **302 passed tests across 35 contiguous suites (0 failed, 6 skipped conditional postgres)** with 0 TypeScript compilation errors.
      - Dedicated Gate M7.3 evidence files generated:
        - `POC-001_Gate_M7_3_Test_Execution_Results.json` (SHA-256: `391A7BF111D8C98EF6DF19101BD6B2D43965F102895539DE27E92ADC84B8187A`, 302 tests).
        - `POC-001_Gate_M7_3_Typecheck_Execution_Results.txt` (SHA-256: `E3B0C44298FC1C149AFBF4C8996FB92427AE41E4649B934CA495991B7852B855`, 0 errors).
    - Gate M7.3 status is authoritatively confirmed as **APPROVED / CLOSED**.

26. **Project Owner Decision OD-24 (Gate M8.0 Central Research & Allocation Core Loop, Epistemic Truthfulness, Need-Driven Agent Orchestration, Passage Citations & Governed Multi-Scenario Bundle Simulator Authorization)**:
    - **Architectural Scope & Invariants**:
      1. *Central Research System as Local System of Record (`src/research/centralResearchCore.ts`)*: Owns durable evidence records with SHA-256 digests, DNS pre-resolution logs, bitemporal timestamps (`observed_at_utc` vs `as_of_utc`), backed by PostgreSQL 16.8 with in-memory fallback.
      2. *Epistemic Truthfulness & Evidence Provenance*: Rejects caller-supplied `origin_class` attempting to self-attest `LIVE_VERIFIED_CAPTURE`. Requires cryptographic tool run proof from authenticated MCP execution. Distinguishes observed facts from estimated sales proxies (documenting formula $V = \alpha \cdot \text{BSR}^{-\beta}$). Reports live PostgreSQL pool connectivity.
      3. *Need-Driven Research Planner*: Inspects evidence gaps per product and dynamically dispatches only relevant specialist micro-agents (`SourceCapture`, `ReviewMining`, `DemandSalesProxy`, `StatutoryCompliance`, `Seasonality`, `AdversarialReviewer`), replacing static SS304 DAG execution.
      4. *Real Groq Review Mining & Passage Citations (`src/research/groqResearchSynthesizer.ts`)*: Connects Groq API (`llama-3.3-70b-versatile`) to extract grievance clusters with verbatim passage-level quotes and character spans, strictly isolated by BigInt calculation firewall.
      5. *User Intent Capture & Governed Bundle Allocator (`src/research/bundleEvaluator.ts`)*: Interactive capital parameters (capital budget, hurdle rate, holding period, risk tolerance), multi-scenario deterministic simulation (Base, Upside, Downside) in pure BigInt rational math, and governed human confirmation gate.
      6. *Institutional 3-Pane Research Terminal*: Dynamic Lead Watchlist (Left), Linked Bitemporal Superchart with event overlays & historical replay (Center), Scoped Research, Groq Citations & Intent Allocation (Right).
    - **Status**: **APPROVED / CLOSED** (Verified by Acceptance Suite 36).

27. **Project Owner Decision OD-25 (POC-001 Governed 6-Slice Remediation & Hardening Plan: Slice 1 Truthful Persistence, Provenance & Attribution Baseline Authorization)**:
    - **Remediation Context**: Following the read-only audit of Gate M8.0, the Project Owner authorized a strict 6-slice remediation roadmap. Slice 1 is authorized immediately with 5 mandatory tightening rules:
      1. *Truthful Groq Fallback Attribution*: In `workstationServer.ts` and `groqResearchSynthesizer.ts`, non-Groq fallback returns `llm_called: false`, `generation_mode: 'DETERMINISTIC_TEMPLATE_FALLBACK'`, and `llm_model: null`. Local string templates are never labeled `(via Groq)`.
      2. *Truthful Connector Idle State at Boot*: In `workstationStateManager.ts`, `initSourceConnectors()` initializes all connectors with `status: 'IDLE_NEVER_RUN'`, `ingested_count: 0`, `last_successful_fetch_utc: null`, and `freshness_age_seconds: null`. Only transition to `'ACTIVE'` upon verified signal ingestion.
      3. *Exact Subunit BigInt Economics (Zero Hardcoded Magic Literals)*: Resolves target `product_id` from the persisted deck. Computes baseline before-economics in pure `BigInt`. If signal provides validated numeric deltas, computes after-economics deterministically in `BigInt`. If required numeric inputs are missing or unmapped, sets `economic_impact_status: 'DATA_REQUIRED'`, `landed_cost_after_inr: null`, `rowc_after_bps: null`, and `allocation_gate_status: 'HOLD_DATA_REQUIRED'`. Eliminates hardcoded `38.21 -> 37.85` and `3994 -> 4120`.
      4. *Real PostgreSQL 16.8 Persistence & Cross-Restart Hydration*: Maintains tables `market_signal_traces`, `market_product_deck_state`, and `market_connector_telemetry` alongside `market_bitemporal_evidence` and `market_event_overlays` on `market_hft_test` (`localhost:5432`). Both `/api/health` and `/api/health/db` execute live `SELECT 1` + table row-count queries + measure query latency in ms. On boot, `WorkstationStateManager` hydrates state from PostgreSQL so products, traces, and connector states survive process restarts.
      5. *Caller Origin Spoofing Blocked*: Refuses caller self-attestation of `LIVE_VERIFIED_CAPTURE`. Without a verified `McpToolProof` in `McpRunLedger`, demotes caller inputs to `'UNATTESTED_USER_INTAKE'` with `verification_status: 'UNVERIFIED'`. Eliminates synthetic tool-call injection.
    - **Status**: **APPROVED / CLOSED (Owner Sign-Off Granted 22 Oct 2026)** (Verified by Acceptance Suite 37, 12/12 tests passed).

28. **Project Owner Decision OD-26 (Slice 2 Permitted Source Capture, Entity Identity Resolution, Adversarial Verification & 6-Hop Trace Authorization & Closure)**:
    - **Architecture & Implementation Scope**:
      1. *EntityIdentityResolver (`src/research/entityIdentityResolver.ts`)*: Deterministic matching across 8 canonical products via ASIN, supplier SKU, HSN, and title spec. Places ambiguous captures on `UNRESOLVED_ENTITY_HOLD` without inventing phantom entities.
      2. *Permitted Source Capture & 6-Layer DOM Sieve (`src/agents/workers/sourceCaptureWorker.ts`)*: Connected `POST /api/connectors/run` through `SourceCaptureWorker`, applying CSS cloaking sanitization, `InjectionCanaryGuard` prompt-injection quarantine, 90-day TTL expiration, and zero-cost substitution ban (`E-SCW-MANDATORY-COST-MISSING`).
      3. *Cross-Source Conflict Preservation*: Preserves divergent quotes under `CONFLICT_DETECTED` with explicit side-by-side attribution without synthetic averaging.
      4. *ApiQuotaAndRateGovernor (`src/mcp/apiQuotaAndRateGovernor.ts`)*: Enforces sliding-window RPM/RPD/RPW rate limiting across Google Maps Places, Routes, Gemini, and Groq APIs; enforces minimal field masks (`X-Goog-FieldMask`); badges route estimates as `'MAPPED_ROUTE_ESTIMATE'`.
      5. *Canonical Market Graph Contract (`src/mcp/contracts/canonicalMarketGraphContract.ts`)*: 10 core entities and 8 incumbent-failure hypotheses evaluator.
      6. *Remediation of 4 Slice 1 Catches*: Eliminates 1,054,532 bps double-scaling bug in `BundleEvaluator`; enforces pure BigInt subunit arithmetic; demotes unverified caller claims to `UNATTESTED_USER_INTAKE`; caps fixture-backed bundles at `READY_FOR_PAPER_TEST`; eliminates synthetic landed-cost corridor; isolates test table cleanups.
    - **Status**: **APPROVED / CLOSED (Owner Sign-Off Granted 22 Oct 2026)** (Verified by Acceptance Suite 38, 12/12 tests passed; full test baseline 340 passed across 38 suites, 0 failed, 0 skipped; live loopback probe `probeSlice2Live.ts` 12/12 assertions passed).

29. **Project Owner Decision OD-27 (Slice 3 Category-Agnostic Dynamic Agent Planner, 6 Specialist Task Agents & 8 Incumbent-Failure Explanations Closure & Surgical Audit Remediation)**:
    - **Remediation Context & Audit Resolutions**:
      Following the independent audit of Slice 3, four surgical probe catches (`SLICE3-FIX-01` through `SLICE3-FIX-04`) and five codebase audit catches were resolved prior to sign-off:
      1. *SLICE3-FIX-01 (Hypothesis Ledger Persistence on Dispatch)*: In `src/research/centralResearchCore.ts` and `src/research/productAwareDynamicResearchPlanner.ts`, executing research dispatch for any catalog lead persists all 8 structural incumbent-failure hypotheses (`HYP-${product_id}-${explanation_type}`) to PostgreSQL 16.8 (`market_hypothesis_ledger`) with deterministic ascending timestamps (+10ms per record) so `GET /api/hypothesis/list?product_id=...` accurately returns all 8 evaluated hypotheses.
      2. *SLICE3-FIX-02 (5 Canonical Connectors Telemetry Seeding)*: In `src/research/centralResearchCore.ts` (`DurableEvidenceStore.initializeTables()`), all 5 canonical connectors (`conn:marketplace:amazon-in`, `conn:supplier:indiamart`, `conn:media:youtube-reviews`, `conn:macro:rbi-fbil-lme`, `conn:statutory:cbic-msme`) are seeded via `INSERT ... ON CONFLICT (connector_id) DO NOTHING` in `market_connector_telemetry`, preventing telemetry count regression.
      3. *SLICE3-FIX-03 (Unweighted Diagnostic Index & Hard Per-Dimension Thresholds)*: In `src/research/opportunityScorecardEngine.ts`, renamed `overall_score_bps` to `unweighted_diagnostic_index_bps` and flagged `is_authoritative_gate_score: false`. Decision outcomes gate strictly on per-dimension minimum score thresholds and explicit missing-data penalties (`missing_data_penalty_bps`), completely eliminating composite average masking.
      4. *SLICE3-FIX-04 (B2B Price Epistemic Class & Assumptions)*: In `src/research/opportunityScorecardEngine.ts`, added `price_epistemic_class: 'OBSERVED_QUOTE' | 'ESTIMATED_PROXY' | 'DATA_REQUIRED'` and `explicit_assumptions: readonly string[]` to `DistributionChannelAnalysis`. Labeled the 35% B2B wholesale discount truthfully as `ESTIMATED_PROXY`.
      5. *Truthful Task Dispatched Logging & Immutability*: Removed synthetic 15ms simulated tool calls from `ProductAwareDynamicResearchPlanner.ts`, logging truthful `TASK_DISPATCHED` events. Enforced append-only immutability in `storeEvidence` (`ON CONFLICT (evidence_id) DO NOTHING`). Converted all fee and margin calculations to pure BigInt subunit integer arithmetic.
    - **Status**: **⏳ AWAITING_OWNER_SIGN_OFF** (Remediated and staged for formal Owner Sign-Off).

30. **Project Owner Decision OD-28 (Slice 4 Local-First Research Query API, Review Span Miner, Single-Lead Opportunity Dossier & Rate-Governed Opt-In Synthesis — Staged for Owner Sign-Off)**:
    - **Architecture & Implementation Scope**:
      1. *ReviewAndGrievanceMiner (`src/research/reviewAndGrievanceMiner.ts`)*:
         - Extracts verified customer problems and incumbent strengths from reviews and forum transcripts.
         - Enforces mandatory verbatim citation span verification (`verifyCitationSpan`): character offsets `[start, end]` must substring-match the raw source artifact, bounded to 10–280 chars, with SHA-256 integrity check.
         - Records sample size denominators (`sample_size_denominator`), grievance frequency percentage, willingness-to-pay impact delta (basis points), and reviewer bias flags (`AFFILIATE_LINK`, `SPONSORED_FREE_SAMPLE`, `UNVERIFIED_PURCHASE`, `COMPETITOR_ASTROTURF`).
      2. *OpportunityDossierService (`src/research/opportunityDossierService.ts`)*:
         - Aggregates single-lead data into 9 canonical frozen sections: `lead_header`, `demand_and_seasonality`, `customer_pain_and_strengths`, `seller_and_competition`, `supply_and_logistics`, `unit_economics_waterfall`, `incumbent_failure_matrix`, `scorecard`, `evidence_and_citations`.
         - Deterministic RFC 8785 JCS canonicalization and 64-character hex SHA-256 digest (`dossier.jcs_sha256`).
         - Bitemporal historical cutoff (`as_of_utc` parameter): excludes future event overlays, proving zero look-ahead bias.
         - Human-readable provenance badge (`"Supplier quote"`, `"Verified capture"`, `"Fixture data"`, `"Modelled Est"`).
         - Marketplace sales evidence truthfulness: sets `observed_transaction_evidence: 'UNKNOWN'` when marketplaces do not disclose volume.
      3. *LocalFirstResearchQueryEngine (`src/research/localFirstResearchQueryEngine.ts`)*:
         - Answers user queries locally by default (`execution_mode: 'LOCAL_DETERMINISTIC_FIRST'`, `external_llm_called: false`, `provider_used: 'LOCAL_DETERMINISTIC_INDEX'`) from bitemporal evidence, review citations, and scorecard data.
         - Surfaces active contradictions (`active_contradictions`) and knowledge gaps (`unknowns_and_gaps`) explicitly without synthetic averaging or hallucination.
         - Includes verbatim inline citations with character offsets and human-readable origin labels.
         - Governed Opt-In External Provider Synthesis: External LLM synthesis (`GEMINI_OPT_IN`, `GROQ_OPT_IN`) strictly requires `user_explicit_provider_opt_in: true`; fails closed with `400 Bad Request` (`E-QUERY-EXPLICIT-OPT-IN-REQUIRED`) if omitted or false.
         - Strictly governed by `ApiQuotaAndRateGovernor` sliding-window quotas; all outputs stamped `epistemic_class: 'NON_AUTHORITATIVE_AI_SYNTHESIS'`.
         - Absolute Secret Protection: API keys are never read from disk, logged, or serialized into responses (0 occurrences of key prefixes).
      4. *HTTP REST Routes (`src/server/workstationServer.ts`)*:
         - `GET /api/research/dossier?product_id=...&as_of_utc=...`
         - `POST /api/research/query`
      5. *Database Quarantine Note*: Historical test-generated rows in `market_hft_test` remain isolated and append-only immutability is preserved; no production table-wide truncations occur.
    - **Acceptance Tests & Verification**:
      - `tests/acceptance/suite40_slice4_local_query_and_dossier.test.ts` (10 normative tests, 10/10 passed).
      - Total test baseline: **40 contiguous suites, 355 passed tests (0 failed, 0 skipped)**.
      - Compilation health: 0 TypeScript diagnostics (`npx.cmd tsc --noEmit`).
      - Live Server Loopback Probe (`src/cli/probeSlice4Live.ts`): All 9 probes passed against port 4310.
    - **Status**: **⏳ AWAITING_OWNER_SIGN_OFF** (Staged for formal Project Owner sign-off before proceeding to Slice 5 / Slice 6).

31. **Project Owner Decision OD-29 (Slice 5 Multi-Lead Opportunity Bundles, Unprefilled User-Intent Gate, Seasonal/Festival Overlap, Risk-Free Benchmark Comparison & Cited Research Report Exporter — Staged for Owner Sign-Off)**:
    - **Architecture & Implementation Scope**:
      1. *BundleEvaluator & Unprefilled User-Intent Gate (`src/research/bundleEvaluator.ts`)*:
         - Enforces explicit user intent validation (`validateExplicitUserIntent`) across 5 mandatory numeric parameters: `available_paper_capital_inr`, `minimum_return_hurdle_bps`, `holding_period_days`, `max_drawdown_limit_bps`, and `max_single_supplier_concentration_bps`. Omission or non-positive value fails closed with `400 Bad Request` (`status: 'USER_INTENT_REQUIRED'`, `error_code: 'E-BUNDLE-INTENT-REQUIRED'`) and lists the exact missing fields.
         - Rejects synthetic ASP corridors and unverified pricing inputs (`E-BUNDLE-INSUFFICIENT-COST-DATA`).
         - Supplier & Hub Concentration Analysis (`ConcentrationAnalysis`): Aggregates capital outlay by sourcing hub. If any single hub exceeds `max_single_supplier_concentration_bps`, flags `concentration_limit_breached: true`, demotes bundle disposition to `CONCENTRATION_LIMIT_BREACHED`, and blocks paper commitment (`E-BUNDLE-UNQUALIFIED-COMMIT-BLOCKED`).
         - Seasonal & Festival Overlap Engine (`SeasonalWindowAnalysis`): Maps products to operational calendar windows (`DIWALI_FESTIVE`, `DURGA_PUJA`, `KALI_LAKSHMI_PUJA`, `CHRISTMAS_YEAR_END`, `MONSOON_CORROSION_CYCLE`, `YEAR_ROUND_INDUSTRIAL_B2B`), computes suggested order cutoffs (e.g. 15 Sept for Diwali), and calculates peak working-capital overlap intensity.
         - Risk-Free Opportunity-Cost Benchmark Spread (`BenchmarkComparison`): Benchmarks annualized Base RoWC against the RBI 91-Day T-Bill (650 bps) and SBI 1-Year Bulk FD (725 bps). Bundles failing to beat risk-free sovereign returns are flagged `ECONOMICS_FAIL_BELOW_BENCHMARK`.
         - Pure BigInt 90-Day Cash-Flow J-Curve (`JCurveDataPoint`): Simulates day-by-day cash outlay, locked working capital, inventory liquidation, and cumulative net cash position in integer subunits.
      2. *Cited Research Report Exporter (`src/research/citedReportExporter.ts`)*:
         - Generates 9-section AlphaSense/Koyfin-grade research reports and investment memos for single leads and multi-lead bundles.
         - Inline Citations (`[CIT-x]`): Verbatim evidence quotes bound to exact character offsets with source origins, epistemic badges, and SHA-256 hashes.
         - Transparent Assumptions Table: Lists parameter names, assumed values, explicit epistemic classes (`OBSERVED_QUOTE`, `FIXTURE_QUOTE`, `ESTIMATED_PROXY`, `PUBLISHED_SCHEDULE`, `MODELLED_ESTIMATE`), and source rationales.
         - Contrary Evidence & Structural Incumbent Failures: Surfaced explicitly alongside unresolved conflicts and unknowns.
         - RFC 8785 JCS Canonicalization: Bit-for-bit reproducible SHA-256 digest (`report_jcs_sha256`) independent of key ordering or whitespace.
         - Bitemporal Cutoff: `as_of_utc` filter guarantees zero look-ahead bias and reproducible historical auditing.
      3. *Governed Commitment Gate & PostgreSQL Persistence (`src/server/workstationStateManager.ts` & `src/research/centralResearchCore.ts`)*:
         - Enforces human confirmation gate with explicit rationale ($\ge 15$ characters) via `executeGovernedOperatorAction`.
         - Persists committed bundles into PostgreSQL 16.8 table `market_committed_bundles` (`allocation_id`, `bundle_name`, `committed_at_utc`, `total_allocated_capital_inr`, `blended_target_rowc_bps`, `status`, `bundle_json`, `jcs_sha256`).
         - Rehydrates committed bundles across state manager restarts.
      4. *HTTP REST Routes (`src/server/workstationServer.ts`)*:
         - `POST /api/bundle/evaluate`
         - `POST /api/bundle/commit`
         - `GET /api/reports/export?target_type=...&target_id=...&as_of_utc=...`
    - **Acceptance Tests & Verification**:
      - `tests/acceptance/suite41_slice5_bundles_intent_and_reports.test.ts` (10 normative tests, 10/10 passed).
      - Total test baseline: **41 contiguous suites, 370 passed tests (0 failed, 0 skipped)**.
      - Compilation health: 0 TypeScript diagnostics (`npx.cmd tsc --noEmit`).
      - Live Server Loopback Probe (`src/cli/probeSlice5Live.ts`): All 9 probes passed against port 4310.
    - **Status**: **⏳ AWAITING_OWNER_SIGN_OFF** (Staged for formal Project Owner sign-off before proceeding to Slice 6).
