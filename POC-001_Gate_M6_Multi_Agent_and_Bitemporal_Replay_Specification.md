# POC-001 — Gate M6 Specification: 24x7 Multi-Agent Research Framework, TinyFish Scoped Browser Sub-Agents & Bitemporal Replay Engine

| Document Attribute | Specification Record |
| :--- | :--- |
| **Document Identifier** | `POC-001_Gate_M6_Multi_Agent_and_Bitemporal_Replay_Specification` |
| **Milestone Gate** | **Gate M6** — Governed Multi-Agent Research Ecosystem, TinyFish Browser Agents & Bitemporal Replay Engine |
| **Document Status** | `FROZEN / AUTHORIZED (OD-10)` |
| **Normative Predecessors** | `POC.docx` (§6.5, §9.2, §11, §15), `POC-001_Gate_M1_Design_Readiness_Specification.md`, `POC-001_Gate_M5_Signal_Bus_and_Group_Simulation_Specification.md`, Decisions `OD-01` through `OD-09` |
| **Authorizing Authority** | Project Owner Decision `OD-10` (16 October 2026) |
| **Operating Boundary** | Strict Dry-Run Simulation; Continuous Signal & Research Edge; Zero Real Capital Execution; Bitemporal Audit Integrity |

---

## 1. Milestone Objective & Scope Definition

Gate M6 codifies the governed multi-agent research ecosystem and bitemporal historical replay engine for Market HFT OS, bridging high-frequency autonomous signal discovery with fail-closed financial and accounting safety.

In accordance with `POC.docx` §6.5, §9.2, §11, and §15, AI agents and continuous signal collectors operate as specialized, sandboxed workers under strict resource quotas and permission boundaries:
1. **Worker Contract, Permissions & Resource Accounting**: Every sub-agent executes under an immutable `AgentWorkerManifest` defining its permission scope, allowed channels, token budget, and timeout limits. Agents have zero authority to write to `PaperLedger` or `ActualsLedger`, cannot promote claims past `UNVERIFIED` without cryptographic attestation or multi-source corroboration, and cannot bypass risk hurdles.
2. **TinyFish Scoped Browser Agent**: A hardened DOM/listing extractor for marketplace (Amazon India ASINs) and supplier (Howrah industrial directories, IndiaMART) pages. Computes a deterministic SHA-256 `dom_snapshot_hash`, extracts structured economic fields, classifies missing attributes as `DATA_REQUIRED` or `DATA_INSUFFICIENT`, and caps commercial status at `ADVERTISED_LISTING` or `SUPPLIER_QUOTE`. Never substitutes `₹0` for missing costs.
3. **Specialist Sub-Agent Swarm**:
   - `MediaAndChatterSubAgent`: Extracts defect rates and seller fee chatter from YouTube transcripts and forum chatter.
   - `MacroAndLateralMarketSubAgent`: Monitors RBI 91-day T-Bill yields, INR/USD, LME Nickel/Steel indices, and freight rates.
   - `GovtSchemeAndTaxSubAgent`: Monitors MSME incentives, customs duty circulars, and Section 43B(h) payment terms.
   - `RedTeamReviewerSubAgent`: Challenges assembled claims against 4D evidence invariants and statutory cost floors before Groq LLM synthesis is invoked.
4. **24x7 Scheduler & Manager Orchestrator**: Event- and TTL-driven orchestrator coordinating the 9-stage research pipeline (`DECOMPOSE` $\to$ `ROUTE` $\to$ `ASSEMBLE_CONTEXT` $\to$ `PROMPT` $\to$ `EXECUTE_SCOPED_WORKER` $\to$ `REVIEW_RED_TEAM` $\to$ `ASSEMBLE_EVIDENCE` $\to$ `POLISH` $\to$ `PRESENT`), supporting graceful degraded mode under network outages or timeouts.
5. **Bitemporal Decision Replay & Restatement Engine**: Preserves the dual-time nature of all allocation decisions: `decision_time_utc` ($t_d$) vs. `knowledge_time_utc` ($t_k$). When new evidence arrives at $t_1$, the engine reconstructs the $t_0$ state bit-for-bit, isolates the exact delta, and determines whether the commercial thesis remains intact or requires an edge-decay halt (`THESIS_INTACT`, `EDGE_DECAY_WARNING`, `THESIS_INVALIDATED_HALT`) without rewriting history.

---

## 2. Worker Contract, Permissions & Resource Accounting (`POC.docx` §15)

Every sub-agent worker must register an immutable manifest:

```typescript
export type AgentPermissionScope =
  | 'READ_ONLY_DISCOVERY'
  | 'SANDBOX_MODELING'
  | 'RED_TEAM_AUDIT';

export interface AgentWorkerManifest {
  agent_id: string;
  role: string;
  permission_scope: AgentPermissionScope;
  allowed_channels: SignalChannel[];
  max_token_budget: number;
  max_latency_ms: number;
}
```

### 2.1. Security & Capital Allocation Invariants
- **No Direct Ledger Access**: Agent workers are strictly prohibited from writing to `PaperLedger` or `ActualsLedger`. Any invocation of ledger mutation methods throws fail-closed error `E-M6-PERMISSION-DENIED`.
- **Promotion Firewall**: Agents cannot promote evidence to `VERIFIED_EXECUTABLE_OFFER` on their own authority. Status remains capped at `ADVERTISED_LISTING` or `SUPPLIER_QUOTE` until verified via cryptographic attestation or multi-source corroboration (`E-ERR-EV-001`).
- **Deterministic Resource Quotas**: Tokens consumed, HTTP/DOM requests made, and execution durations are tracked per execution cycle. If `tokens_consumed > max_token_budget`, the worker is halted immediately with `E-M6-QUOTA-EXCEEDED`.

---

## 3. TinyFish Scoped Browser Agent (`POC.docx` §9.2)

The TinyFish Scoped Browser Agent ingests raw DOM/HTML or structured web listing payloads and extracts verified economic fields:

```typescript
export interface TinyFishExtractionResult {
  source_url: string;
  dom_snapshot_hash: string; // SHA-256 of raw DOM/HTML
  extracted_at_utc: string;
  extracted_fields: Record<string, string | number | bigint>;
  missing_mandatory_fields: string[];
  extraction_status: 'COMPLETE' | 'DATA_REQUIRED' | 'DATA_INSUFFICIENT';
  evidence_envelope: EvidenceEnvelope<any>;
}
```

### 3.1. Missing Data Handling Invariant
In accordance with `POC.docx` §9.2:
- If mandatory pricing, freight, or fee fields are missing from the page, TinyFish **NEVER** inserts default values such as `₹0` or null guesses.
- Missing fields are explicitly categorized:
  - `DATA_REQUIRED`: Essential for unit economics (e.g., product price, shipping fee, referral percentage). The candidate cannot be evaluated and resolves to `CANNOT_CALCULATE_MISSING_INPUTS`.
  - `DATA_INSUFFICIENT`: Ambiguous description or uncorroborated claim.
- The commercial status of scraped listings is strictly set to `ADVERTISED_LISTING`.

---

## 4. Specialist Sub-Agent Swarm

The research ecosystem comprises four specialist workers supervised by an adversarial reviewer:
1. **`TinyFishScopedBrowserAgent`**: Scrapes marketplace ASIN buy-box prices, FBA fee tiers, and supplier directory quotes (Howrah clamp clusters, IndiaMART).
2. **`MediaAndChatterSubAgent`**: Ingests video teardowns, YouTube transcripts, and seller forums to detect defect trends (e.g. rust on claimed SS304 indicating SS202 scrap mix) and marketplace fee hikes.
3. **`MacroAndLateralMarketSubAgent`**: Tracks sovereign 91-day T-Bills, LME Nickel/Stainless Steel spot prices, and logistics freight rates.
4. **`GovtSchemeAndTaxSubAgent`**: Ingests statutory circulars, customs anti-dumping tariffs, MSME SAMADHAAN 45-day credit limits, and Section 43B(h) disallowances.
5. **`RedTeamReviewerSubAgent`**: Validates whether supplier quotes violate fundamental cost bounds. For example, if a supplier quotes ₹12 per 10-pack for SS304 clamps when LME raw stainless steel coil scrap floor is ₹18 per 10-pack, the claim is flagged as fraudulent or mislabeled metallurgy and quarantined (`E-M6-RED-TEAM-REJECTED`).

---

## 5. 24x7 Scheduler & Manager Orchestrator

The `ResearchSchedulerAndManager` operates continuously to manage research tasks and maintain data freshness:
- **Quote TTL & Expiration Tracking**: Monitors time-to-live (`ttl_seconds`) on supplier quotes and marketplace fee schedules. When an asset's quote expires or market shock occurs, the manager automatically triggers a targeted research run.
- **Nine-Stage Pipeline Execution**:
  1. `DECOMPOSE`: Dissects thesis into atomic sub-queries.
  2. `ROUTE`: Checks local BM25 RAG index (`llm_called: false`). Only novel claims route to external workers.
  3. `ASSEMBLE_CONTEXT`: Retrieves FormulaCards and verified baselines.
  4. `PROMPT`: Compiles schema-locked instructions.
  5. `EXECUTE_SCOPED_WORKER`: Dispatches tasks to TinyFish and specialist sub-agents within budget quotas.
  6. `REVIEW_RED_TEAM`: Adversarial check for below-cost anomalies or contradictory reviews.
  7. `ASSEMBLE_EVIDENCE`: Bundles normalized outputs into RFC 8785 JCS 4D evidence envelopes.
  8. `POLISH`: Synthesizes concise operator briefing and risk metrics.
  9. `PRESENT`: Emits canonical trading telemetry with SHA-256 digest.
- **Degraded Mode Resilience**: If an external data source or LLM service experiences network latency or failure, the system falls back to cached verified values, logs `degraded_mode_triggered: true`, and never substitutes false `0` values.

---

## 6. Bitemporal Decision Replay & Restatement Engine (`POC.docx` §11)

Every simulation and capital allocation decision is bitemporal:
- **Decision Time ($t_d$)**: When the decision occurred in virtual simulation time.
- **Knowledge Time ($t_k$)**: When the evidence was recorded and ingested into the system knowledge base.

```typescript
export interface BitemporalDecisionRecord {
  decision_id: string;
  decision_time_utc: string;
  knowledge_time_utc: string;
  evidence_snapshot_hashes: string[];
  allocation_decision: any;
  jcs_digest_sha256: string;
}

export type RestatementStatus =
  | 'THESIS_INTACT'
  | 'EDGE_DECAY_WARNING'
  | 'THESIS_INVALIDATED_HALT';

export interface BitemporalRestatementReport {
  original_decision_id: string;
  t0_decision_time_utc: string;
  t1_restatement_time_utc: string;
  input_deltas: Record<string, { t0_value: string; t1_value: string }>;
  restatement_status: RestatementStatus;
  original_annualized_rowc_bps: string;
  restated_annualized_rowc_bps: string;
  rowc_delta_bps: string;
  explanation: string;
  restatement_digest_sha256: string;
}
```

### 6.1. Replay Invariant
- Re-running an evaluation at $t_0$ with historical knowledge state $t_k \le t_0$ must reproduce the exact decision and SHA-256 digest bit-for-bit.
- Restating an evaluation at $t_1$ with newly arrived evidence (e.g. Amazon price reduction or LME steel price surge) generates a new restatement record without altering or deleting the historical $t_0$ record.
- If restated RoWC drops below the sovereign T-Bill hurdle rate, the engine issues `THESIS_INVALIDATED_HALT`.

---

## 7. Deterministic JCS Canonicalization

All agent manifests, extraction results, manager research records, and bitemporal restatement reports must serialize deterministically via `canonicalizeJCS` (`json-canonicalize@3.0.1`), ensuring crash recovery reproducibility and auditable provenance.
