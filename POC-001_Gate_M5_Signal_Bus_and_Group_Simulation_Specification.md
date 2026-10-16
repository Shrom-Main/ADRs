# POC-001 — Gate M5 Specification: 6-Channel Signal Bus, 4D Evidence State Machine & Silo vs. Simultaneous Group Strategy Simulator

| Document Attribute | Specification Record |
| :--- | :--- |
| **Document Identifier** | `POC-001_Gate_M5_Signal_Bus_and_Group_Simulation_Specification` |
| **Milestone Gate** | **Gate M5** — 6-Channel Signal Bus, 4D Evidence Architecture & Group Strategy Simulator |
| **Document Status** | `FROZEN / AUTHORIZED (OD-09)` |
| **Normative Predecessors** | `POC.docx` (16 October 2026), `POC-001_Gate_M1_Design_Readiness_Specification.md`, `POC-001_Gate_M4_Acceptance_Specification.md`, Decisions `OD-01` through `OD-08` |
| **Authorizing Authority** | Project Owner Decision `OD-09` (16 October 2026) |
| **Operating Boundary** | Strict Dry-Run Simulation; Continuous Signal Plane; Paper Trading Only; Zero Real Capital Execution |
| **Reference Commodity Pool** | SS304 DIN 3017 Clamp Matrix (16–25mm, 20–32mm, 25–40mm, 32–50mm; 10-pack & 20-pack) vs. Lateral Financial Benchmarks (`RBI_91D_TBILL`, `NIFTY_LIQUID_BENCHMARK`) |

---

## 1. Milestone Objective & Scope Definition

Gate M5 establishes the architectural convergence between the **24x7 Continuous Signal & Deep Research Plane** and the **Deterministic Risk & Accounting Core** as specified in `POC.docx`.

In this architecture, autonomous collectors and LLM research workers operate at high frequency on the discovery edge, but their outputs are strictly treated as unverified candidate hypotheses. Capital allocation decisions are governed by a deterministic firewall enforcing:
1. **Four Orthogonal Evidence Dimensions**: Separating the nature of an claim from its verification status, commercial executability, and cryptographic provenance.
2. **Six-Channel Continuous Signal Ingestion**: Normalizing signals across trade news, YouTube video transcripts, social chatter, macroeconomic indicators, lateral financial markets, and government policy schemes into structured candidate parameters.
3. **Nine-Stage "Deep Research Pro" DAG Pipeline Contract**: A typed state machine ensuring external/browser sub-agents and Groq LLM calls remain strictly subordinate to the RAG-First sufficiency gate and 4D evidence promotion rules.
4. **Six-Status Return & Lifecycle Vocabulary**: Explicitly distinguishing incomplete, unrecovered, or unprovable lifecycles rather than collapsing them into a false `0%` return.
5. **Silo vs. Simultaneous Group Simulation Engine**:
   - **Silo Mode**: Evaluates individual SKU/pack-size variants in isolation, generating unit economics, cash-flow J-curve time series, and Arbitrage Greeks ($\Delta, \Theta, \mathcal{V}$).
   - **Simultaneous Group Mode**: Evaluates cohorts of strategies under a shared treasury budget (₹50,000.0000), shared GST Input Tax Credit (ITC) pool, correlated lateral-market shocks (e.g. LME raw material spikes), concentration caps, and passive financial benchmarks.
6. **Conviction vs. Allocation Separation**: Enforcing that conviction (evidence strength) and allocation (capital committed) are orthogonal coordinates: high projected returns backed only by unverified listings receive ₹0 capital.

---

## 2. Four Orthogonal Evidence Dimensions (`POC.docx` §5)

Every input, quote, tariff, and signal ingested by Market HFT OS must be wrapped in a 4-dimensional envelope. These dimensions are strictly orthogonal:

```
┌─────────────────────────────────────────────────────────────────────────────────────────┐
│                           FOUR ORTHOGONAL EVIDENCE DIMENSIONS                           │
├────────────────────────────────┬────────────────────────────────────────────────────────┤
│ 1. Evidence Kind               │ OBSERVED_FACT | SOURCE_DOCUMENT | ASSUMPTION |         │
│                                │ FORECAST | SYNTHETIC_SCENARIO                          │
├────────────────────────────────┼────────────────────────────────────────────────────────┤
│ 2. Verification Status         │ UNVERIFIED | CRYPTOGRAPHICALLY_ATTESTED |               │
│                                │ CROSS_SOURCE_CORROBORATED | REJECTED                   │
├────────────────────────────────┼────────────────────────────────────────────────────────┤
│ 3. Commercial Status           │ NOT_APPLICABLE | ADVERTISED_LISTING | SUPPLIER_QUOTE |  │
│                                │ VERIFIED_EXECUTABLE_OFFER | ACCEPTED_COMMITMENT |       │
│                                │ COMPLETED_TRANSACTION                                  │
├────────────────────────────────┼────────────────────────────────────────────────────────┤
│ 4. Provenance Lineage          │ source_id, channel, observed_at_utc, ttl_seconds,       │
│                                │ parent_claim_hashes, transformation_rule_id             │
└────────────────────────────────┴────────────────────────────────────────────────────────┘
```

### 2.1. Promotion Firewall Invariant
An `ADVERTISED_LISTING` (e.g., an IndiaMART public directory listing) or a `SYNTHETIC_SCENARIO` can **NEVER** silently auto-promote to a `VERIFIED_EXECUTABLE_OFFER`.
Promotion requires:
1. Valid cryptographic signature attestation against `TrustAnchorRegistry`, OR
2. Cross-source corroboration from at least two independent, verified source IDs within valid TTLs.
Any attempt to allocate capital to an offer lacking verified status triggers immediate fail-closed rejection (`E-M5-UNVERIFIED-PROVENANCE`).

---

## 3. Six-Channel Continuous Signal Taxonomy

The signal bus ingests testable signals from six operational channels and normalizes them into structured evidence items:

| Channel Identifier | Channel Domain | Normalized Payload Attributes | Downstream Economic Mapping |
| :--- | :--- | :--- | :--- |
| `NEWS_TRADE_PRESS` | Trade press, metals bulletins, logistics alerts | `headline, publisher, confidence_bps, sentiment` | Inbound lead-time shock, macro supply risk |
| `YOUTUBE_VIDEO_TRANSCRIPT` | Factory walk-throughs, product teardowns, unboxings | `video_id, channel_name, timestamp_sec, defect_flag` | Customer return rate drag, packaging defect risk |
| `SOCIAL_FORUM_CHATTER` | Seller forums, industrial buyer communities | `platform, thread_id, complaint_category, volume` | Customer return attrition rate spike |
| `MACROECONOMIC_INDICATOR` | RBI policy, MOSPI WPI/CPI, FBIL benchmark rates | `metric_name, value_bps, observation_date` | Risk-free opportunity cost (91-day T-Bill rate) |
| `LATERAL_FINANCIAL_MARKET` | LME Nickel/Steel, Nifty Metal Index, container freight | `symbol, spot_price, change_24h_bps, index_source` | Raw material procurement cost inflation |
| `GOVERNMENT_SCHEME_POLICY` | MSME notifications, CBIC GST circulars, Section 43B(h) | `notification_id, statutory_act, impact_variable` | Statutory payment terms, tax deduction holdbacks |

---

## 4. Nine-Stage "Deep Research Pro" Pipeline Contract (`POC.docx` §15)

The research control plane operates as a Directed Acyclic Graph (DAG) State Machine:

$$\text{DECOMPOSE} \longrightarrow \text{ROUTE} \longrightarrow \text{ASSEMBLE\_CONTEXT} \longrightarrow \text{PROMPT} \longrightarrow \text{EXECUTE\_SCOPED\_WORKER} \longrightarrow \text{REVIEW\_RED\_TEAM} \longrightarrow \text{ASSEMBLE\_EVIDENCE} \longrightarrow \text{POLISH} \longrightarrow \text{PRESENT}$$

1. **DECOMPOSE**: Planner breaks complex commercial theses (e.g., "SS304 4-size matrix Howrah vs. Amazon India") into atomic sub-queries: supplier EXW quote, LME coil trend, Amazon FBA fee schedule, MSME payment limits.
2. **ROUTE**: Checks Tier 1 Local BM25 RAG index (`llm_called: false`). Only missing or stale claims route to external workers.
3. **ASSEMBLE_CONTEXT**: Hydrates FormulaCards, verified supplier history, and 4D schemas from local DB.
4. **PROMPT**: Compiles schema-locked instructions with zero authority to hallucinate missing data. Missing fields emit `DATA_REQUIRED`.
5. **EXECUTE_SCOPED_WORKER**: Executes sandboxed worker adapters (TinyFish DOM scraper, transcript analyzer, macro feeds).
6. **REVIEW_RED_TEAM**: Challenges every collected claim: validates TTL, checks for listing vs. verified inventory confusion, audits contradiction against customer review complaints.
7. **ASSEMBLE_EVIDENCE**: Wraps outputs into RFC 8785 JCS-hashed 4D Evidence Envelopes.
8. **POLISH**: Synthesizes structured metric cards and risk assessments.
9. **PRESENT**: Generates trading-terminal telemetry with bidirectional traceability to source documents and FormulaCards.

---

## 5. Six-Status Return & Lifecycle Vocabulary (`POC.docx` §5)

To prevent deceptive financial engineering, the system strictly prohibits collapsing incomplete or unrecovered lifecycle states into a naive `0%` or `NaN`:

1. `VALID_CALCULATED_RETURN`: Complete lifecycle with verified procurement, inbound, sale, and cash settlement. Exact BigInt RoWC/XIRR computed.
2. `CANNOT_CALCULATE_MISSING_INPUTS`: Mandatory economic fields (e.g., freight tariff or referral fee) missing.
3. `INSUFFICIENT_UNVERIFIED_EVIDENCE`: Inputs present but unverified or uncorroborated.
4. `NO_ROOT_FOUND_IN_SEARCH_DOMAIN`: Polynomial solver cannot converge on unique real XIRR within search bounds.
5. `NOT_YET_RECOVERED`: Capital deployed in an active batch where cumulative net cash has not crossed the breakeven threshold ($< 0$).
6. `OPEN_POSITION`: Inventory held in warehouse or in-transit; position is active and cash flows are incomplete.

---

## 6. Silo vs. Simultaneous Group Simulation Architecture

### 6.1. Silo Simulation Mode (Single-Variant Isolation)
Evaluates an individual SKU/pack-size variant in complete isolation:
- Matrix: DIN 3017 W4 SS304 across 4 diameters (`16-25mm`, `20-32mm`, `25-40mm`, `32-50mm`) and 2 pack hypotheses (`10-pack` vs. `20-pack`).
- Generates:
  1. **Price and Breakeven Bands**: Gross price, landed cost, and breakeven floor.
  2. **Cash-Flow J-Curve Waterfall**: Cumulative cash from Day 0 (outflow) through Day 35 (disbursement).
  3. **Arbitrage Greeks**:
     - $\Delta$ (Price/Cost Delta): $\frac{\partial \text{RoWC}}{\partial \text{Price}}$ (basis points return per ₹1 price change).
     - $\Theta$ (Time / Edge Decay): Daily loss of annualized RoWC as warehouse dwell stretches or quote TTL expires.
     - $\mathcal{V}$ (Return/Defect Vega): RoWC sensitivity to customer return rate increases ($\Delta \text{RoWC}$ per 100 bps return rate).

### 6.2. Simultaneous Group Mode (Cohort & Portfolio Interaction)
Evaluates a cohort of opportunities simultaneously against:
- **Finite Treasury Budget**: ₹50,000.0000 (`500000000n` subunits) hard cap; discrete MOQ integer lot-sizing.
- **Single-SKU Concentration Limit**: Default 50.00% (`250000000n` subunits).
- **Correlated Lateral-Market Shocks**: A $+10\%$ surge in LME stainless steel raw material prices detected from lateral markets simultaneously inflates landed costs across all SS304 sizes.
- **Passive Financial Benchmarks**: Compares survivor allocations against `RBI_91D_TBILL` (6.50% p.a.) and `NIFTY_LIQUID_BENCHMARK` (6.80% p.a.).
- **Conviction vs. Allocation Bubble Coordinates**:
  - X: Evidence Conviction Score ($0$ to $100\%$, percentage of claims verified).
  - Y: Risk-Adjusted Annualized Return over T-Bill hurdle.
  - Z (Radius): Capital committed (`allocated_capital_subunits`).

---

## 7. Deterministic RFC 8785 JCS Attestation

All generated trading-chart series, evidence envelopes, and group allocation decisions must serialize identically via `json-canonicalize@3.0.1` and emit a verifiable SHA-256 digest (`telemetry_digest_sha256`), guaranteeing crash recovery reproducibility.
