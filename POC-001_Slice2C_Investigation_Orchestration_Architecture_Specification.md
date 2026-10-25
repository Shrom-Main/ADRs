# POC-001: Slice 2C Architecture Specification & Contract Proposal (Normative Revision 010)
**Document ID:** `POC-001-ARCH-SPEC-SLICE-2C-010`  
**Governance Anchor:** Decision `DEC-030` (*Proposed by Specification Author — Pending Owner Formal Recording in Authoritative Ledger*)  
**Authoritative Ledger Location:** [`D:\ADRs\GATE_AUTHORIZATION_LEDGER.md`](file:///d:/ADRs/GATE_AUTHORIZATION_LEDGER.md)  
**Revision Date:** 25 October 2026  
**Document Status:** **PROPOSED — OWNER APPROVAL PENDING (IMPLEMENTATION STRICTLY NOT AUTHORIZED)**  
**Companion Commit Baseline:** [`4ba8191`](https://github.com/Shrom-Main/Market-HFT-OS/commit/4ba8191)  
**Operating Boundary:** Strictly Offline / Recorded Historical Fixtures / Synthetic Scenarios / Zero Real Capital / Zero Live Connectors  

---

> [!IMPORTANT]
> **GOVERNANCE STATUS & IMPLEMENTATION BOUNDARY:**  
> This specification defines normative contracts, database schemas, financial algorithms, and interface proposals for **Slice 2C (Controlled Investigation Orchestration)**. It **does not confer implementation authorization**.  
> - `DEC-030`: Status is **`PROPOSED — OWNER APPROVAL PENDING`**. Approval occurs solely upon formal owner recording in [`GATE_AUTHORIZATION_LEDGER.md`](file:///d:/ADRs/GATE_AUTHORIZATION_LEDGER.md). A specification cannot approve itself.
> - `DEC-027` (Slice 3), `DEC-028` (Slice 4), `DEC-029` (Slice 5): Strictly remain in `AWAITING_OWNER_SIGN_OFF`.
> - Slice 2C Implementation: **STRICTLY NOT AUTHORIZED**.
> - Live Connectors, Public Web Scraping, Live Agent Execution, Live Order Routing, and Capital-Allocation Writes: **STRICTLY PROHIBITED**.

---

## 1. Owner Decision & Normative Amendments — 25 October 2026

The following binding owner directives govern Slice 2C contracts. Where any section of this document or prior design drafts conflicts with this section, **this section is authoritative**:

```
================================================================================
POC-001 — SLICE 2C OWNER DECISION RECORD (DEC-030: PROPOSED)
================================================================================
Decision ID:                 DEC-030 (Proposed — Pending Owner Ledger Entry)
Title:                       Slice 2C Architecture Specification — Contract Refinement Only
Decision Date:               25 October 2026
Scope:                       Investigation Orchestration Contracts, Interfaces & Schemas
Status:                      PROPOSED — OWNER APPROVAL PENDING
Implementation Auth:         STRICTLY NOT AUTHORIZED
Live Connectors / Scraping:  STRICTLY PROHIBITED
Dual-Ledger Capital Writes:  STRICTLY PROHIBITED
================================================================================
```

### A. Binding Governance Invariants
1. **Scope Boundary:** Authorized solely for specification refinement, TypeScript interface definitions, database schemas, state-transition contracts, threat models, and acceptance test specifications. Code implementation, worker queue activation, live agent dispatch, and capital writes remain strictly unauthorized.
2. **Worker Pool Provisional Engineering Defaults:**
   - Global concurrency ceiling: **4 tasks**.
   - Per-candidate concurrency ceiling: **2 tasks**.
   - Initial lease duration: **30 seconds**.
   - Maximum execution attempts: **3 attempts** (1 initial + 2 retries) before terminal Dead-Letter Quarantine.
   - *Condition:* Provisional engineering defaults only, conditioned on lease-fencing token validation, atomic PostgreSQL persistence, unexpired lease enforcement, and comprehensive budget controls.
3. **Mandatory Authenticated Operator Authority for Identity Merges:**
   - Agent outputs are strictly advisory. No automated system or heuristic algorithm may merge source-scoped candidates.
   - Match confidence score (e.g. $\ge 9,500\text{ bps}$) is a heuristic escalation trigger for human review, conferring zero authority to converge.
   - Every merge or split of source-scoped candidates requires an authenticated, replay-safe operator decision ([`OperatorIdentityMergeDecision`](#7-identity-resolution-protocol--replay-safe-human-authority)).
4. **Governance Invariants Intact:**
   - [`DEC-027`](file:///d:/ADRs/GATE_AUTHORIZATION_LEDGER.md), [`DEC-028`](file:///d:/ADRs/GATE_AUTHORIZATION_LEDGER.md), and [`DEC-029`](file:///d:/ADRs/GATE_AUTHORIZATION_LEDGER.md) remain in `AWAITING_OWNER_SIGN_OFF`.
   - Dual-ledger safety isolation is absolute (zero real capital, zero live order routing).

---

## 2. Core Operating Boundaries & Anti-Scaffolding Laws

```
+----------------------------------------------------------------------------------------------------+
|                                    POC-001 DISCOVERY FUNNEL                                        |
+----------------------------------------------------------------------------------------------------+
|  [Slice 2A: Source Contract] -> [Slice 2B: Sieve & Prioritization] -> [Slice 2C: Orchestration]     |
|   - RawSourceCapture             - ScreeningPolicyEngine               - InvestigationPlanner      |
|   - ProvenanceEnvelope           - Priority Scoring (0-10,000 bps)     - Specialist Agent Swarm    |
|   - FixtureReplayAdapter         - Delta Detection & Signals           - Fenced Durable Queue      |
|                                                                        - Hash-Verified Dossier     |
+----------------------------------------------------------------------------------------------------+
                                                  |
                                                  v
                         +--------------------------------------------------+
                         |       SAFETY FIREWALL & AUTHORIZATION GATE       |
                         |  (OpportunityLifecycleEngine.authorizePaperCommit) |
                         |   - Evidence Sufficiency: 100% Critical Fields   |
                         |   - Economic Eligibility: Deterministic Model    |
                         |   - Conflict & Stale Signal Rejection            |
                         |   - Dual-Ledger Isolation: Zero Real Capital    |
                         +--------------------------------------------------+
```

### The Four Anti-Scaffolding Laws of Investigation Orchestration

1. **Law 1: Agents Extract Sourced Inputs; Deterministic Engines Authorize State & Capital:**  
   Agents and planners extract missing parameters and propose evidence findings. They are **strictly prohibited** from transitioning candidates to `PAPER_ELIGIBLE` or invoking [`authorizePaperCommit()`](file:///d:/Market%20HFT%20OS/src/research/opportunityLifecycleEngine.ts#L572-L646). The deterministic state machine and financial calculation core remain the sole authoritative arbiters.
2. **Law 2: Dual-Ledger Isolation Is Invariant:**  
   Slice 2C contains zero live capital execution, zero live order routing, and zero write authority over capital allocation ledgers.
3. **Law 3: Zero Uncontrolled Live Connectors:**  
   Slice 2C executes 100% offline using recorded provenance-backed fixtures ([`GoldenDiscoveryFixtureRegistry`](file:///d:/Market%20HFT%20OS/src/discovery/fixtures/goldenDiscoveryFixtures.ts)) and synthetic benchmark scenarios. No unvetted public web scraping or unthrottled live API crawling.
4. **Law 4: Epistemic Truthfulness & Zero Economic Fabrication:**  
   Missing economic inputs (hosting costs, freight rates, factory quotes) remain strictly `null`. Neither agents, queue workers, nor lifecycle engines may substitute zero, interpolate averages, or fabricate margins. Missing inputs fail closed.

---

## 3. Deterministic Underwriting & Financial Cash-Flow Engine Contract

To resolve review findings **P0-17 (Accounting Contract for Reconciliation)**, **P0-18 (Same-Day Cash Recovery Proof)**, **P1-04 (Known Unregistered Seller vs Unknown Status)**, and **P1-05 (Explicit Commercial Viability Hurdles)**:

```
[Raw Capture] 
     │
     ▼
[Stage 0: Screening Margin Policy] ──(Fails Closed: Drops negative or thin gross spread < 1000 bps)
     │
     ▼ (Candidates prioritized for investigation)
[Slice 2C: Investigation Orchestration] ──(Extracts missing cost inputs: freight, factory gate, fees)
     │
     ▼ (Complete evidence & verified parameters)
[Stage 1: Deterministic Underwriting] ──(Constructs Discrete OperatingCashFlowEntry[] Schedule)
     │                                    │
     │                                    ├──(Verifies Delta_reconciliation === 0n invariant)
     │                                    ▼
     │                           [computeOperatingCashFlowSeries()] ──(Derives true K_peak & empirical D_recovery)
     ▼                                    │
[authorizePaperCommit()] ─────────────────┴──(Enforces Auditable Hurdle Policies: Margin >= 12%, RoPF >= 25%)
```

### A. Signed Half-Up Rounding Semantics (`round_div_signed`)
Integer division uses symmetric half-away-from-zero rounding. Safe conversion to basis points asserts safe JavaScript integer bounds:

```typescript
export function round_div_signed(numerator: bigint, denominator: bigint): bigint {
  if (denominator <= 0n) {
    throw new Error('E-FINANCIAL-DIVISOR-NON-POSITIVE: Denominator must be strictly positive');
  }
  if (numerator === 0n) return 0n;
  const half = denominator / 2n;
  if (numerator > 0n) {
    return (numerator + half) / denominator;
  } else {
    return -((-numerator + half) / denominator);
  }
}

export function bigintToSafeBps(val: bigint): number {
  if (val > BigInt(Number.MAX_SAFE_INTEGER) || val < BigInt(Number.MIN_SAFE_INTEGER)) {
    throw new Error('E-INTEGER-OVERFLOW-SAFE-RANGE: Value exceeds safe integer bounds');
  }
  return Number(val);
}
```

### B. Input/Output GST, Credit Eligibility, and Cost Capitalization
1. **Output GST (Customer Checkout):**  
   $$P_{\text{ex}} = \text{round\_div\_signed}(P_{\text{inc}} \times 10,000n, 10,000n + R_{\text{gst\_out\_bps}})$$
   $$\text{GST}_{\text{output}} = P_{\text{inc}} - P_{\text{ex}}$$
2. **COGS Input GST & ITC Capitalization:**  
   $$C_{\text{ex}} = \text{round\_div\_signed}(C_{\text{inc}} \times 10,000n, 10,000n + R_{\text{gst\_in\_cogs\_bps}})$$
   $$\text{ITC}_{\text{cogs}} = \begin{cases} C_{\text{inc}} - C_{\text{ex}} & \text{if } \text{is\_itc\_eligible} = \text{true} \\ 0n & \text{if } \text{is\_itc\_eligible} = \text{false} \end{cases}$$
   *Capitalization Rule:* If ITC is ineligible (e.g. blocked under Section 17(5) CGST Act), uncreditable GST remains part of effective expense:
   $$C_{\text{effective}} = \begin{cases} C_{\text{ex}} & \text{if } \text{is\_itc\_eligible} = \text{true} \\ C_{\text{inc}} & \text{if } \text{is\_itc\_eligible} = \text{false} \end{cases}$$
3. **Freight Input GST & ITC Capitalization:**  
   $$F_{\text{freight\_ex}} = \text{round\_div\_signed}(F_{\text{freight\_inc}} \times 10,000n, 10,000n + R_{\text{gst\_in\_freight\_bps}})$$
   $$\text{ITC}_{\text{freight}} = \begin{cases} F_{\text{freight\_inc}} - F_{\text{freight\_ex}} & \text{if } \text{is\_freight\_itc\_eligible} = \text{true} \\ 0n & \text{if } \text{is\_freight\_itc\_eligible} = \text{false} \end{cases}$$
   $$F_{\text{freight\_effective}} = \begin{cases} F_{\text{freight\_ex}} & \text{if } \text{is\_freight\_itc\_eligible} = \text{true} \\ F_{\text{freight\_inc}} & \text{if } \text{is\_freight\_itc\_eligible} = \text{false} \end{cases}$$
4. **Marketplace Platform Fees & SAC 998371 ITC:**  
   $$F_{\text{platform\_ex}} = F_{\text{ref\_ex}} + F_{\text{close\_ex}} + F_{\text{ful\_ex}}$$
   $$\text{ITC}_{\text{platform}} = \text{round\_div\_signed}(F_{\text{platform\_ex}} \times R_{\text{gst\_platform\_bps}}, 10,000n) \quad (R_{\text{gst\_platform\_bps}} = 1800n)$$
   $$F_{\text{platform\_inc}} = F_{\text{platform\_ex}} + \text{ITC}_{\text{platform}}$$
   $$F_{\text{platform\_effective}} = \begin{cases} F_{\text{platform\_ex}} & \text{if } \text{is\_platform\_itc\_eligible} = \text{true} \\ F_{\text{platform\_inc}} & \text{if } \text{is\_platform\_itc\_eligible} = \text{false} \end{cases}$$
5. **Net Unit Contribution Margin ($M_{\text{paise}}$ & $M_{\text{bps}}$):**  
   $$M_{\text{paise}} = P_{\text{ex}} - C_{\text{effective}} - F_{\text{freight\_effective}} - F_{\text{platform\_effective}}$$
   $$M_{\text{bps}} = \begin{cases} 
   \text{bigintToSafeBps}(\text{round\_div\_signed}(M_{\text{paise}} \times 10,000n, P_{\text{ex}})) & \text{if } P_{\text{ex}} > 0n \\
   \text{UNDEFINED (Fails Closed)} & \text{if } P_{\text{ex}} \le 0n 
   \end{cases}$$
   - *Denominator:* Strictly $P_{\text{ex}}$ (Ex-GST net customer checkout revenue).
   - *Included Costs:* All direct effective COGS, inbound freight, handling, and marketplace fees.

### C. Explicit Accounting Contract & Versioned Statutory Tax Rules
To ensure complete accounting integrity under **P0-17** and **P1-04**:

1. **Economic Meaning & Sign Conventions:**
   - **Bank Cash Outflows:** Represented as strictly negative integer paise ($E_1 < 0n$, $E_3 \le 0n$).
   - **Bank Cash Inflows:** Represented as strictly positive integer paise ($E_2 > 0n$).
   - **Contribution Margin ($M_{\text{paise}}$):** Pre-tax economic unit operating surplus ($P_{\text{ex}} - \sum \text{Costs}_{\text{effective}}$).
2. **Status and Nature of Tax Assets:**
   - **`Accumulated GST Tax Asset`:** $\max(0n, \text{ITC}_{\text{total}} + \text{TCS}_{\text{withheld}} - \text{GST}_{\text{output}})$. Represents an **accrued, legally recognized, but illiquid** non-cash balance residing in the seller's Electronic Credit Ledger on the GST Portal. It cannot be drawn as bank cash; it is realized solely against future output GST liabilities on subsequent sales or via statutory refund under Section 54(3)(ii) CGST Act for inverted duty structures (subject to Rule 89(5) administrative formula calculations and 60–180 day statutory payment lags).
   - **`TDS_withheld` (`direct_tax_credit_asset_paise`):** Advance income tax credit withheld at source under Section 194-O (or Income-tax Act, 2025) and deposited into the Central Government treasury under the seller's PAN. It is an **accrued and unutilized** direct tax asset, **completely distinct and non-fungible** with GST credit ledgers. It cannot offset GST liabilities; it is realized strictly against quarterly advance income tax obligations or annual income tax filings. It represents an immutable reduction in merchant bank disbursement at $E_2$.
3. **Refunds, Reversals, and Adjustments:**
   - *Ineligible Credits:* Blocked credits under Section 17(5) are capitalized into $C_{\text{effective}}$, $F_{\text{freight\_effective}}$, and $F_{\text{platform\_effective}}$, directly reducing $M_{\text{paise}}$, and do not enter the tax asset ledger.
   - *Inverted Duty Refunds:* If a statutory refund is received from the tax department, it represents a non-operating transfer from the tax asset ledger to the bank account: $+\Delta \text{BankCash}$, $-\Delta \text{GST Tax Asset}$, preserving the sum identically.
   - *Reversals/Adjustments:* Any statutory credit reversal under Rule 42/43 is accounted for as `ReversalAdjustment_paise` and recognized as an operating expense.
4. **Tax Applicability Context & Distinction Between Known Unregistered vs Unknown Status:**

```typescript
export interface TaxRuleConfig {
  readonly config_version: string;                // e.g. "TAX-REGIME-2026-V1"
  readonly operative_regime: 'INCOME_TAX_ACT_1961' | 'INCOME_TAX_ACT_2025';
  readonly effective_start_date: string;           // ISO date: "2024-10-01"
  readonly effective_end_date: string;             // ISO date: "2026-03-31"
  readonly gst_tcs_bps: bigint;                    // 50n (0.50% Notification 15/2024-CT)
  readonly direct_tax_tds_bps: bigint;            // 10n (0.10% Finance (No. 2) Act 2024 / 2025 Act)
  readonly tds_threshold_exemption_paise: bigint;  // 50000000n (₹5 Lakh annual threshold for individual/HUF)
  readonly requires_gst_registration: boolean;     // true (model scope requires GST registered sellers)
  readonly marketplace_commission_gst_bps: bigint;// 1800n (18% SAC 998371)
}

export interface TaxApplicabilityContext {
  readonly transaction_date_utc: string;
  readonly seller_entity_type: 'INDIVIDUAL' | 'HUF' | 'PRIVATE_LIMITED' | 'LLP';
  readonly seller_pan_verified: boolean;
  readonly gst_registration_status: 'REGISTERED_VERIFIED' | 'KNOWN_UNREGISTERED' | 'STATUS_UNVERIFIED';
  readonly annual_gross_turnover_paise: bigint;
}
```

*Applicability Decision Matrix:*
- If `gst_registration_status === 'KNOWN_UNREGISTERED'`: The seller is known not to be registered for GST. Because Slice 2C underwriting scope strictly requires inter-state fulfillment and ITC eligibility, this seller is classified as **`SELLER_INELIGIBLE_FOR_MODEL_SCOPE`** (disqualified by policy, routed to `REJECTED`).
- If `gst_registration_status === 'STATUS_UNVERIFIED'` or `seller_pan_verified === false`: Registration status is unknown. Underwriting fails closed to **`DATA_REQUIRED`** (`E-UNDERWRITING-TAX-APPLICABILITY-UNRESOLVED`, routed to `DEFERRED`).
- If `transaction_date_utc` falls outside the effective range of any known versioned configuration: Underwriting fails closed to **`DATA_REQUIRED`**.

### D. Strict Liquid Bank Cash Schedule ($E_1$ to $E_3$) & Terminal Reconciliation Accounting Contract
The discrete bank schedule passed to [`computeOperatingCashFlowSeries()`](file:///d:/Market%20HFT%20OS/src/financial/cashFlowEngine.ts#L118-L174) models actual movements in the bank operating account:

| Sequence | Simulated Day ($t$) | Flow Kind | Cash Amount (Inflow / Outflow) |
| :--- | :--- | :--- | :--- |
| **$E_1$** | Day $0$ | `PROCUREMENT_OUTLAY` | $-(C_{\text{inc}} + F_{\text{freight\_inc}})$ |
| **$E_2$** | Day $D_{\text{inv}} + D_{\text{settle}}$ | `NET_MERCHANT_DISBURSEMENT` | $+(P_{\text{inc}} - F_{\text{platform\_inc}} - \text{TCS}_{\text{withheld}} - \text{TDS}_{\text{withheld}})$ |
| **$E_3$** | Day $\max(E_2.t, D_{\text{gst\_filing\_lag}})$ | `STATUTORY_TAX_REMIT` | $-\text{Net GST Cash Remittance}$ (Cash Outflow) |

Where:
$$\text{Net GST Cash Remittance} = \max\left(0n, \text{GST}_{\text{output}} - \text{ITC}_{\text{total}} - \text{TCS}_{\text{withheld}}\right)$$
$$\text{Accumulated GST Tax Asset} = \max\left(0n, \text{ITC}_{\text{total}} + \text{TCS}_{\text{withheld}} - \text{GST}_{\text{output}}\right)$$

#### Universal Terminal Reconciliation Identity:
Summing the three bank movements and substituting tax identities:
$$\begin{aligned}
\sum_{j=1}^3 E_j &= -(C_{\text{inc}} + F_{\text{freight\_inc}}) + (P_{\text{inc}} - F_{\text{platform\_inc}} - \text{TCS} - \text{TDS}) - \max(0n, \text{GST}_{\text{out}} - \text{ITC} - \text{TCS}) \\
&= (P_{\text{ex}} - C_{\text{effective}} - F_{\text{freight\_effective}} - F_{\text{platform\_effective}}) - (\text{ITC}_{\text{total}} + \text{TCS} - \text{GST}_{\text{out}}) - \max(0n, \text{GST}_{\text{out}} - \text{ITC} - \text{TCS}) - \text{TDS} \\
&= M_{\text{paise}} - \max(0n, \text{ITC}_{\text{total}} + \text{TCS} - \text{GST}_{\text{out}}) - \text{TDS}_{\text{withheld}} \\
&= M_{\text{paise}} - \text{Accumulated GST Tax Asset} - \text{TDS}_{\text{withheld}}
\end{aligned}$$

Rearranging gives the exact accounting identity:
$$\sum_{j=1}^3 E_j + \text{Accumulated GST Tax Asset} + \text{TDS}_{\text{withheld}} \equiv M_{\text{paise}}$$

#### Mandatory Checked Invariant (`delta_reconciliation`):
```typescript
const calculated_reconciliation_sum =
  operating_cash_series.terminal_liquid_cash +
  tax_ledger.accumulated_gst_asset_paise +
  tax_ledger.direct_tax_tds_asset_paise +
  tax_ledger.statutory_reversal_adjustments_paise;

const delta_reconciliation = calculated_reconciliation_sum - m_paise;

if (delta_reconciliation !== 0n) {
  throw new Error(`E-UNDERWRITING-RECONCILIATION-INVARIANT-VIOLATION: Delta ${delta_reconciliation} paise detected across cash and tax ledgers`);
}
```
If $\Delta_{\text{reconciliation}} \neq 0n$, the engine aborts and emits status `MODEL_INCONSISTENCY_ERROR`. No commercial viability status is emitted.

### E. Capital Recovery Semantics, Same-Day Cash Recovery Proof, and `AnnualizedUnitRoPF`

To resolve review findings **P0-18 (Same-Day Cash Recovery Proof)** and **P1-05 (Explicit Commercial Viability Hurdles)**:

1. **Authoritative Meaning of "Capital Recovery":**
   Capital recovery is defined strictly as **sustained recovery of the initial operating cash outlay**:
   The physical day $k_{\text{rec}}$ after which the cumulative bank operating cash balance $B_{\text{ops}}(k) \ge 0$ **and never relapses into deficit** after subsequent cash outflows (including $E_3$ statutory tax remittances).
   - Evaluated strictly via [`computePostOutlayRecoveryMetrics()`](file:///d:/Market%20HFT%20OS/src/financial/cashFlowEngine.ts#L190-L294).
   - $D_{\text{recovery}} = k_{\text{rec}} \in \mathbb{N}_0$.
   - If balance never permanently recovers to $\ge 0$, $D_{\text{recovery}} = \text{null}$ (`INFINITY`).
2. **Proof Conditions for Genuine Same-Day Cash Recovery ($D_{\text{recovery}} = 0$):**
   $D_{\text{recovery}} = 0$ occurs IF AND ONLY IF cumulative bank operating cash satisfies $B_{\text{ops}}(0) \ge 0$ on Day 0 and remains $\ge 0$ across all subsequent simulation days.
   - *Requirement:* A customer cash receipt must be credited to the bank on Day 0 ($E_2.t = 0$), such that $E_2 \ge |E_1 + E_3|$ (e.g. prepaid customer checkout with instant payment gateway merchant settlement).
   - *Supplier Credit Clarification:* If supplier credit defers the procurement cash payment past customer settlement ($E_1.t > E_2.t$), the merchant operates on supplier capital. Peak operating funding $K_{\text{peak}} = 0n$. This state is classified as **`ZERO_OPERATING_OUTLAY`** (`K_peak == 0n`), where RoPF is mathematically undefined ($0/0$), **NOT same-day recovery**!
   - *Missing Lead-Time Rule:* A supplier dispatch SLA proves fulfillment dispatch timing, not customer payment settlement timing. A missing or unverified $D_{\text{inv}}$ or $D_{\text{settle}}$ can **never** be treated as zero days. Missing lead times fail closed to `DATA_REQUIRED` (`E-UNDERWRITING-MISSING-INVENTORY-LEAD-TIME`).
3. **Separation of Arithmetic Annualization Floor:**
   To calculate the annualized rate of return without falsifying empirical recovery speed:
   $$\text{annualization\_days} = \max(1, D_{\text{recovery}})$$
   $$\text{AnnualizedUnitRoPF}_{\text{bps}} = \begin{cases}
   \text{bigintToSafeBps}\left(\text{round\_div\_signed}(\text{Net Liquid Cash} \times 365n \times 10,000n, K_{\text{peak}} \times \text{BigInt}(\text{annualization\_days}))\right) & \text{if } K_{\text{peak}} > 0n \text{ and } \text{Net Liquid Cash} > 0n \\
   \text{null (DISQUALIFIED\_LOSS)} & \text{if } \text{Net Liquid Cash} \le 0n \\
   \text{null (UNDEFINED\_ZERO\_OUTLAY)} & \text{if } K_{\text{peak}} == 0n
   \end{cases}$$
4. **Explicit Commercial Viability Hurdle Policy:**
   A candidate satisfies the economic hurdle for `PAPER_ELIGIBLE` IF AND ONLY IF all four conditions are met:
   1. **Liquidity Surplus:** `terminal_liquid_cash > 0n`
   2. **Margin Hurdle:** $M_{\text{bps}} \ge 1,200\text{ bps}$ ($12.0\%$ net contribution margin on $P_{\text{ex}}$)
   3. **Annualized Velocity Hurdle:** $\text{AnnualizedUnitRoPF}_{\text{bps}} \ge 2,500\text{ bps}$ ($25.0\%$ annualized return on peak capital)
   4. **Recovery Horizon:** $0 \le D_{\text{recovery}} \le 60\text{ days}$
   - *Undefined / Negative Cases:* `ZERO_OPERATING_OUTLAY` (undefined RoPF), `COMMERCIAL_LOSS`, `INVERTED_DUTY_CASH_TRAP`, `LIQUIDITY_DEFICIT_REVIEW`, and `CAPITAL_NOT_RECOVERED` **never pass commercial hurdles** under any circumstance.

### F. Rigorous 4-Part Causal Predicate for Liquidity Traps
Terminal bank cash reflects pre-tax liquidity. Liquidity status is strictly decoupled from commercial viability:

```typescript
export type LiquidityStatus =
  | 'LIQUIDITY_SURPLUS'           // Terminal bank cash is strictly positive
  | 'COMMERCIAL_LOSS'             // Underlying trade margin is non-positive
  | 'INVERTED_DUTY_CASH_TRAP'     // Liquid deficit strictly caused by unabsorbed GST credits
  | 'LIQUIDITY_DEFICIT_REVIEW'    // Liquid deficit caused by direct tax TDS or high platform frictions
  | 'MODEL_INCONSISTENCY_ERROR';  // Terminal reconciliation check failed

export function evaluateLiquidityCausality(
  m_paise: bigint,
  tds_withheld_paise: bigint,
  accumulated_gst_asset_paise: bigint,
  terminal_liquid_cash_paise: bigint,
  delta_reconciliation: bigint
): LiquidityStatus {
  // 0. Model Invariant Check
  if (delta_reconciliation !== 0n) {
    return 'MODEL_INCONSISTENCY_ERROR';
  }

  // 1. Commercial Loss Check
  if (m_paise <= 0n) {
    return 'COMMERCIAL_LOSS';
  }

  // 2. Liquid Surplus
  if (terminal_liquid_cash_paise > 0n) {
    return 'LIQUIDITY_SURPLUS';
  }

  // 3. Causal Test for Inverted Duty Trap:
  const counterfactual_cash_pre_trap = m_paise - tds_withheld_paise;

  if (counterfactual_cash_pre_trap > 0n && accumulated_gst_asset_paise >= counterfactual_cash_pre_trap) {
    return 'INVERTED_DUTY_CASH_TRAP';
  }

  // 4. Non-tax liquidity deficit (e.g. TDS wipes out thin margin or excessive frictions)
  return 'LIQUIDITY_DEFICIT_REVIEW';
}
```

### G. Normative Financial Status & Output Resolution Matrix
| Financial Evaluation Status | Trigger Condition | Empirical $D_{\text{rec}}$ | `annualization_days` | `AnnualizedUnitRoPF` Output | Underwriting Hurdle Outcome |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `SUCCESS_COMMERCIALLY_VIABLE` | $K_{\text{peak}} > 0$, $M \ge 12\%$, `LIQUIDITY_SURPLUS`, $1 \le D_{\text{rec}} \le 60\text{d}$, $\text{RoPF} \ge 2500$ | $1 \le D_{\text{rec}} \le 60$ | $D_{\text{rec}}$ | Positive integer bps ($\ge 2,500$) | **PASSED** (Eligible for `PAPER_ELIGIBLE`) |
| `SAME_DAY_RECOVERY` | Verified Day-0 cash receipt, $K_{\text{peak}} > 0$, $M \ge 12\%$, `LIQUIDITY_SURPLUS`, $D_{\text{rec}} = 0$, $\text{RoPF} \ge 2500$ | `0` | `1` | Positive integer bps ($\ge 2,500$) | **PASSED** (Eligible for `PAPER_ELIGIBLE`) |
| `SUCCESS_SUB_HURDLE` | $K_{\text{peak}} > 0$, $M > 0$, but margin $< 12\%$ or RoPF $< 2500$ or $D_{\text{rec}} > 60\text{d}$ | Finite days | $\max(1, D_{\text{rec}})$ | Positive integer bps ($< 2,500$) | **FAILED_CLOSED** (Transitions to `DEFERRED`) |
| `ZERO_OPERATING_OUTLAY` | $K_{\text{peak}} == 0n$ (Zero capital at risk; supplier funded trade) | `0` | `1` | `null` (`UNDEFINED_ZERO_OUTLAY`) | **FAILED_CLOSED** (Requires human policy review) |
| `COMMERCIAL_LOSS` | $M_{\text{paise}} \le 0n$ (Underlying trade loses money) | `null` | `null` | `null` (`DISQUALIFIED_LOSS`) | **FAILED_CLOSED** (Transitions to `REJECTED`) |
| `INVERTED_DUTY_CASH_TRAP` | $M_{\text{paise}} > 0$, but unabsorbed GST credit traps bank cash ($\le 0$) | `null` | `null` | `null` (`DISQUALIFIED_TAX_TRAP`) | **FAILED_CLOSED** (Transitions to `DEFERRED`) |
| `LIQUIDITY_DEFICIT_REVIEW` | $M_{\text{paise}} > 0$, but direct tax withholdings drive liquid cash $\le 0$ | `null` | `null` | `null` (`DISQUALIFIED_LIQUIDITY`) | **FAILED_CLOSED** (Transitions to `DEFERRED`) |
| `SELLER_INELIGIBLE_FOR_MODEL_SCOPE`| Known unregistered seller (`KNOWN_UNREGISTERED`) | `null` | `null` | `null` (`SELLER_INELIGIBLE`) | **FAILED_CLOSED** (Transitions to `REJECTED`) |
| `DATA_REQUIRED` | Missing lead-time or unverified tax registration status | `null` | `null` | `null` (`DATA_REQUIRED`) | **FAILED_CLOSED** (Transitions to `DEFERRED`) |
| `CAPITAL_NOT_RECOVERED` | Balance remains negative at end of simulation ($D_{\text{rec}} = \infty$) | `null` | `null` | `null` (`DISQUALIFIED_UNRECOVERED`) | **FAILED_CLOSED** (Transitions to `REJECTED`) |
| `MODEL_INCONSISTENCY_ERROR` | $\Delta_{\text{reconciliation}} \neq 0n$ (Ledger cash mismatch) | `null` | `null` | `null` (`MODEL_INCONSISTENT`) | **FAILED_CLOSED** (Immediate system abort) |

---

## 4. Authoritative PostgreSQL Queue & Executable Lease-Fencing Protocol

### A. Closed Task State Domain (`TaskState`)
```typescript
export type TaskState =
  | 'QUEUED'                  // Available for worker claim
  | 'LEASED'                  // Leased by an active worker under unexpired fence
  | 'RETRYING'                // Execution failed with attempts < 3; awaiting backoff
  | 'SUCCEEDED'               // Terminal success; immutable commit persisted
  | 'CANCELLED_SUPERSEDED'    // Lease superseded by newer candidate generation
  | 'DEAD_LETTER_QUARANTINE'  // Terminal failure (>= 3 attempts); requires human replay
  | 'CANCELLED';              // Cancelled via operator intervention
```

### B. Canonical 8-Field Commit Envelope Specification (`CommitEnvelopeV1`)
Every task completion is bound to an immutable 8-field envelope:
1. `task_id: string`
2. `candidate_id: string`
3. `generation_id: string`
4. `task_type: string`
5. `lease_owner_id: string`
6. `fencing_token: number`
7. `result_payload_sha256: string`
8. `observation_id: string`

*Persistence Guarantee:* When a task transitions to `SUCCEEDED`, the full 8-field envelope is permanently recorded in `committed_envelope_json` and immutable task columns. It is **never** cleared or overwritten by subsequent sweeper passes.

### C. Executable Atomic Commit Protocol (`commitTaskResultAtomic`)
To guarantee that lost acknowledgements can be safely replayed even after a worker's original lease has expired or the candidate has advanced to a newer generation, `commitTaskResultAtomic` compares **all eight stored envelope fields** in Branch 1:

```typescript
export interface CommitTaskParams {
  readonly task_id: string;
  readonly candidate_id: string;
  readonly generation_id: string;
  readonly task_type: string;
  readonly lease_owner_id: string;
  readonly fencing_token: number;
  readonly result_payload_sha256: string;
  readonly result_envelope: Record<string, unknown>;
  readonly observation: {
    readonly observation_id: string;
    readonly target_field: string;
    readonly extracted_subunits: string;
  };
}

export async function commitTaskResultAtomic(
  client: pg.PoolClient,
  params: CommitTaskParams
): Promise<{ status: 'COMMITTED' | 'IDEMPOTENT_REPLAY_ACK' }> {
  await client.query('BEGIN;');
  try {
    // 1. Lock candidate row FIRST (Global Lock Order: Candidate -> Task)
    const candRes = await client.query(
      `SELECT candidate_id, active_generation_id, lifecycle_state, entity_version
       FROM market_candidates WHERE candidate_id = $1 FOR UPDATE;`,
      [params.candidate_id]
    );
    if (candRes.rowCount === 0) {
      throw new Error(`E-QUEUE-CANDIDATE-NOT-FOUND: Candidate '${params.candidate_id}' does not exist`);
    }
    const candidate = candRes.rows[0];

    // 2. Lock task row SECOND
    const taskRes = await client.query(
      `SELECT task_id, candidate_id, lease_owner_id, fencing_token, generation_id, task_type,
              state, leased_until_utc, result_payload_sha256, committed_envelope_json
       FROM market_investigation_tasks WHERE task_id = $1 FOR UPDATE;`,
      [params.task_id]
    );
    if (taskRes.rowCount === 0) {
      throw new Error(`E-QUEUE-TASK-NOT-FOUND: Task '${params.task_id}' does not exist`);
    }
    const task = taskRes.rows[0];

    // 3. Task-to-Candidate Binding Check
    if (task.candidate_id !== params.candidate_id) {
      throw new Error(`E-QUEUE-BINDING-MISMATCH: Task '${params.task_id}' belongs to '${task.candidate_id}', not '${params.candidate_id}'`);
    }

    // =========================================================================
    // BRANCH 1: ALREADY SUCCEEDED (REPLAY PATH)
    // Handled BEFORE checking lease expiry or candidate active generation!
    // Survives lease expiration and candidate generation supersession.
    // Compares ALL EIGHT fields against stored committed_envelope_json.
    // =========================================================================
    if (task.state === 'SUCCEEDED') {
      if (!task.committed_envelope_json) {
        throw new Error(`E-QUEUE-INCONSISTENT-STATE: Task '${params.task_id}' marked SUCCEEDED but missing committed envelope`);
      }
      const stored = typeof task.committed_envelope_json === 'string'
        ? JSON.parse(task.committed_envelope_json)
        : task.committed_envelope_json;

      // Full 8-field verification against stored envelope:
      const matchesAllEightFields =
        params.task_id === stored.task_id &&
        params.candidate_id === stored.candidate_id &&
        params.generation_id === stored.generation_id &&
        params.task_type === stored.task_type &&
        params.lease_owner_id === stored.lease_owner_id &&
        params.fencing_token === stored.fencing_token &&
        params.result_payload_sha256 === stored.result_payload_sha256 &&
        params.observation.observation_id === stored.observation_id;

      if (matchesAllEightFields) {
        // Verify observation exists in market_candidate_observations matching stored observation_id
        const obsRes = await client.query(
          `SELECT observation_id, raw_payload_sha256, candidate_id, task_id
           FROM market_candidate_observations WHERE observation_id = $1;`,
          [stored.observation_id]
        );
        if (
          obsRes.rowCount! > 0 &&
          obsRes.rows[0].raw_payload_sha256 === stored.result_payload_sha256 &&
          obsRes.rows[0].candidate_id === stored.candidate_id &&
          obsRes.rows[0].task_id === stored.task_id
        ) {
          // Persist replay telemetry without mutating observation
          await client.query(
            `INSERT INTO market_observation_replays (replay_id, observation_id, worker_id, replayed_at_utc)
             VALUES ($1, $2, $3, clock_timestamp())
             ON CONFLICT (replay_id) DO NOTHING;`,
            [`REP-${params.task_id}-${Date.now()}`, stored.observation_id, params.lease_owner_id]
          );
          await client.query('COMMIT;');
          return { status: 'IDEMPOTENT_REPLAY_ACK' };
        }
      }
      throw new Error(`E-QUEUE-COMMIT-ENVELOPE-MISMATCH: Task '${params.task_id}' was completed under differing parameters (including observation_id)`);
    }

    // =========================================================================
    // BRANCH 2: NOT YET SUCCEEDED (FIRST COMMIT PATH)
    // Requires task.state === 'LEASED', valid fence, future expiry, and active gen.
    // =========================================================================
    if (task.state !== 'LEASED' || task.lease_owner_id !== params.lease_owner_id || task.fencing_token !== params.fencing_token) {
      throw new Error(`E-QUEUE-STALE-LEASE-FENCE-REJECTED: Worker '${params.lease_owner_id}' does not hold active fence on task '${params.task_id}'`);
    }

    // Strict Future Wall-Clock Expiration Check
    const timeRes = await client.query(`SELECT clock_timestamp() as now_time;`);
    const nowTime = new Date(timeRes.rows[0].now_time).getTime();
    if (new Date(task.leased_until_utc).getTime() <= nowTime) {
      throw new Error(`E-QUEUE-LEASE-EXPIRED-AT-COMMIT: Lease expired at ${task.leased_until_utc}`);
    }

    // Active Generation Validation
    if (candidate.active_generation_id !== params.generation_id) {
      throw new Error(`E-QUEUE-GENERATION-SUPERSEDED: Active candidate generation is now '${candidate.active_generation_id}'`);
    }

    // Construct Canonical Envelope
    const committedEnvelope = {
      task_id: params.task_id,
      candidate_id: params.candidate_id,
      generation_id: params.generation_id,
      task_type: params.task_type,
      lease_owner_id: params.lease_owner_id,
      fencing_token: params.fencing_token,
      result_payload_sha256: params.result_payload_sha256,
      observation_id: params.observation.observation_id
    };

    // Commit Task State
    await client.query(
      `UPDATE market_investigation_tasks
       SET state = 'SUCCEEDED',
           result_payload_sha256 = $2,
           result_envelope = $3,
           committed_envelope_json = $4,
           completed_at_utc = clock_timestamp(),
           updated_at_utc = clock_timestamp()
       WHERE task_id = $1;`,
      [params.task_id, params.result_payload_sha256, JSON.stringify(params.result_envelope), JSON.stringify(committedEnvelope)]
    );

    // Persist Immutable Observation
    await client.query(
      `INSERT INTO market_candidate_observations (
         observation_id, candidate_id, generation_id, task_id, task_type,
         target_field, extracted_subunits, raw_payload_sha256, captured_at_utc
       ) VALUES ($1, $2, $3, $4, $5, $6, $7, $8, clock_timestamp());`,
      [
        params.observation.observation_id,
        params.candidate_id,
        params.generation_id,
        params.task_id,
        params.task_type,
        params.observation.target_field,
        params.observation.extracted_subunits,
        params.result_payload_sha256
      ]
    );

    await client.query('COMMIT;');
    return { status: 'COMMITTED' };
  } catch (err) {
    await client.query('ROLLBACK;');
    throw err;
  }
}
```

---

## 5. Fenced Superseded Generation Archival Protocol

When a commit throws `E-QUEUE-GENERATION-SUPERSEDED`, the late worker executes a dedicated, fenced archival transaction that **strictly preserves newer worker leases**:

```typescript
export async function archiveSupersededTaskExecution(
  client: pg.PoolClient,
  params: {
    execution_id: string;
    task_id: string;
    candidate_id: string;
    task_generation_id: string;
    active_candidate_generation_id: string;
    worker_id: string;
    fencing_token: number;
    result_payload_sha256: string;
    result_envelope: Record<string, unknown>;
  }
): Promise<void> {
  await client.query('BEGIN;');
  try {
    // 1. Record execution output immutably in superseded audit ledger
    await client.query(
      `INSERT INTO market_task_superseded_executions (
         execution_id, task_id, candidate_id, task_generation_id, active_candidate_generation_id,
         worker_id, fencing_token, result_payload_sha256, result_envelope, recorded_at_utc
       ) VALUES ($1, $2, $3, $4, $5, $6, $7, $8, $9, clock_timestamp())
       ON CONFLICT (execution_id) DO NOTHING;`,
      [
        params.execution_id,
        params.task_id,
        params.candidate_id,
        params.task_generation_id,
        params.active_candidate_generation_id,
        params.worker_id,
        params.fencing_token,
        params.result_payload_sha256,
        JSON.stringify(params.result_envelope)
      ]
    );

    // 2. Fenced task state transition: conditionally cancel task ONLY IF this worker still holds the lease
    await client.query(
      `UPDATE market_investigation_tasks
       SET state = 'CANCELLED_SUPERSEDED', updated_at_utc = clock_timestamp()
       WHERE task_id = $1 
         AND lease_owner_id = $2 
         AND fencing_token = $3 
         AND state = 'LEASED';`,
      [params.task_id, params.worker_id, params.fencing_token]
    );

    await client.query('COMMIT;');
  } catch (err) {
    await client.query('ROLLBACK;');
    throw err;
  }
}
```

---

## 6. Atomic Queue Admission & Retry Lifecycle

1. **Serialized Queue Capacity Admission:** Serialized via namespace advisory lock `pg_advisory_xact_lock(65537)` to prevent capacity race conditions across concurrent dispatchers.
2. **Worker Error Backoff vs Sweeper State Transitions:**
   - Worker execution failure sets `state = 'RETRYING'` with exponential delay: `retry_after_utc = clock_timestamp() + interval '1 second' * (2 ^ attempt_count)`.
   - Sweeper scans for `state = 'RETRYING' AND retry_after_utc <= clock_timestamp()` and resets to `QUEUED`.
   - Sweeper scans for `state = 'LEASED' AND leased_until_utc <= clock_timestamp()`. If attempts $< 3$, resets to `QUEUED` and clears `lease_owner_id = NULL` without incrementing `fencing_token`. If attempts $\ge 3$, transitions atomically to `DEAD_LETTER_QUARANTINE`.

---

## 7. Identity Resolution Protocol & Replay-Safe Human Authority

### A. Global Identity Lock Hierarchy
Across all merge and split operations, database locks must be acquired in a strict global hierarchy:
1. **Tier 1 (Canonical Product Lock):** Lock canonical product row first (`SELECT ... FROM market_canonical_products WHERE canonical_product_id = $1 FOR UPDATE`). (If creating, acquire advisory lock `pg_advisory_xact_lock(131072 + hashtext(canonical_product_id))` to serialize creation).
2. **Tier 2 (Candidate Rows Lock):** Lock candidate rows second, sorted in strictly ascending alphanumeric order (`ORDER BY candidate_id ASC FOR UPDATE`).

### B. Database Schema & Concurrent Collision Handling (Rollback & Re-read Path)
`market_operator_governance_log` enforces a database-level unique constraint on `decision_id`:

```sql
CREATE TABLE market_operator_governance_log (
  decision_id VARCHAR(64) PRIMARY KEY,
  action_type VARCHAR(64) NOT NULL,
  operator_id VARCHAR(64) NOT NULL,
  auth_session_id VARCHAR(64) NOT NULL,
  auth_credential_fingerprint VARCHAR(64) NOT NULL,
  target_canonical_product_id VARCHAR(64),
  candidate_ids TEXT[] NOT NULL,
  substantive_rationale TEXT NOT NULL,
  record_jcs_sha256 VARCHAR(64) NOT NULL,
  recorded_at_utc TIMESTAMPTZ NOT NULL DEFAULT clock_timestamp(),
  CONSTRAINT uq_operator_governance_decision_id UNIQUE (decision_id)
);
```

If two concurrent transactions submit the same `decision_id` simultaneously, the losing transaction catches PostgreSQL error `23505 (unique_violation)`. It rolls back, queries the winning decision, re-verifies the RFC 8785 JCS digest, and returns `IDEMPOTENT_DUPLICATE`:

```typescript
export async function executeOperatorIdentityDecision(
  client: pg.PoolClient,
  decision: OperatorIdentityMergeDecision
): Promise<{ status: 'APPLIED' | 'IDEMPOTENT_DUPLICATE' }> {
  // 1. Authenticity: Recompute RFC 8785 canonical digest from submitted fields
  const recomputedDigest = sha256(canonicalizeJCS({
    decision_id: decision.decision_id,
    operator_id: decision.operator_id,
    auth_session_id: decision.auth_session_id,
    auth_credential_fingerprint: decision.auth_credential_fingerprint,
    candidate_version_map: decision.candidate_version_map,
    evidence_digests_snapshot_sha256: decision.evidence_digests_snapshot_sha256,
    candidate_ids_to_merge: [...decision.candidate_ids_to_merge].sort(),
    target_canonical_product_id: decision.target_canonical_product_id,
    decision: decision.decision,
    substantive_rationale: decision.substantive_rationale,
    decided_at_utc: decision.decided_at_utc
  }));

  if (decision.record_jcs_sha256 !== recomputedDigest) {
    throw new Error('E-IDENTITY-DIGEST-VERIFICATION-FAILED: Submitted record digest does not match recomputed JCS digest');
  }

  // Helper to verify existing decision on replay or concurrent collision
  async function verifyExistingDecision(): Promise<{ status: 'IDEMPOTENT_DUPLICATE' }> {
    const dupCheck = await client.query(
      `SELECT decision_id, record_jcs_sha256 FROM market_operator_governance_log WHERE decision_id = $1;`,
      [decision.decision_id]
    );
    if (dupCheck.rowCount! > 0) {
      if (dupCheck.rows[0].record_jcs_sha256 === decision.record_jcs_sha256) {
        return { status: 'IDEMPOTENT_DUPLICATE' };
      }
      throw new Error(`E-IDENTITY-DECISION-COLLISION-MUTATED: Decision '${decision.decision_id}' exists with differing digest`);
    }
    throw new Error(`E-IDENTITY-DECISION-INCONSISTENT: Decision collision occurred but winning record not found`);
  }

  // 2. Initial Replay Check before opening write transaction
  const initialCheck = await client.query(
    `SELECT decision_id, record_jcs_sha256 FROM market_operator_governance_log WHERE decision_id = $1;`,
    [decision.decision_id]
  );
  if (initialCheck.rowCount! > 0) {
    if (initialCheck.rows[0].record_jcs_sha256 === decision.record_jcs_sha256) {
      return { status: 'IDEMPOTENT_DUPLICATE' };
    }
    throw new Error(`E-IDENTITY-DECISION-COLLISION-MUTATED: Decision '${decision.decision_id}' exists with differing digest`);
  }

  await client.query('BEGIN ISOLATION LEVEL SERIALIZABLE;');
  try {
    // 3. Tier 1 Lock: Canonical product row / advisory creation lock
    await client.query(`SELECT pg_advisory_xact_lock(131072 + hashtext($1));`, [decision.target_canonical_product_id]);

    // 4. Tier 2 Lock: Candidates in sorted alphanumeric order
    const sortedIds = [...decision.candidate_ids_to_merge].sort();
    const candRes = await client.query(
      `SELECT candidate_id, entity_version, evidence_digest_sha256, canonical_product_id
       FROM market_candidates WHERE candidate_id = ANY($1) ORDER BY candidate_id ASC FOR UPDATE;`,
      [sortedIds]
    );

    if (candRes.rowCount !== sortedIds.length) {
      throw new Error(`E-IDENTITY-CANDIDATES-NOT-FOUND: Expected ${sortedIds.length} candidates, found ${candRes.rowCount}`);
    }

    // 5. Verify candidate versions and existing canonical associations
    for (const cand of candRes.rows) {
      const expectedVersion = decision.candidate_version_map[cand.candidate_id];
      if (cand.entity_version !== expectedVersion) {
        throw new Error(`E-IDENTITY-STALE-VERSION-REJECTED: Candidate '${cand.candidate_id}' version is ${cand.entity_version}, expected ${expectedVersion}`);
      }
      if (decision.decision === 'APPROVE_CONVERGENCE' && cand.canonical_product_id !== null) {
        throw new Error(`E-IDENTITY-ALREADY-MERGED: Candidate '${cand.candidate_id}' already linked to '${cand.canonical_product_id}'`);
      }
    }

    // 6. Branch Logic: APPROVE_CONVERGENCE vs REJECT_MAINTAIN_SPLIT
    if (decision.decision === 'APPROVE_CONVERGENCE') {
      await client.query(
        `INSERT INTO market_canonical_products (canonical_product_id, updated_at_utc)
         VALUES ($1, clock_timestamp())
         ON CONFLICT (canonical_product_id) DO UPDATE SET updated_at_utc = clock_timestamp();`,
        [decision.target_canonical_product_id]
      );
      await client.query(
        `UPDATE market_candidates
         SET canonical_product_id = $1,
             identity_review_status = 'MERGE_APPROVED',
             entity_version = entity_version + 1,
             updated_at_utc = clock_timestamp()
         WHERE candidate_id = ANY($2);`,
        [decision.target_canonical_product_id, sortedIds]
      );
    } else {
      await client.query(
        `UPDATE market_candidates
         SET canonical_product_id = NULL,
             identity_review_status = 'SPLIT_CONFIRMED',
             entity_version = entity_version + 1,
             updated_at_utc = clock_timestamp()
         WHERE candidate_id = ANY($1);`,
        [sortedIds]
      );
    }

    // 7. Append immutable governance log
    await client.query(
      `INSERT INTO market_operator_governance_log (
         decision_id, action_type, operator_id, auth_session_id, auth_credential_fingerprint,
         target_canonical_product_id, candidate_ids, substantive_rationale,
         record_jcs_sha256, recorded_at_utc
       ) VALUES ($1, $2, $3, $4, $5, $6, $7, $8, $9, clock_timestamp());`,
      [
        decision.decision_id,
        decision.decision,
        decision.operator_id,
        decision.auth_session_id,
        decision.auth_credential_fingerprint,
        decision.target_canonical_product_id,
        sortedIds,
        decision.substantive_rationale,
        decision.record_jcs_sha256
      ]
    );

    await client.query('COMMIT;');
    return { status: 'APPLIED' };
  } catch (err: any) {
    await client.query('ROLLBACK;');
    // Handle concurrent duplicate insertion race: catch unique constraint 23505
    if (err && err.code === '23505') {
      return await verifyExistingDecision();
    }
    throw err;
  }
}
```

### C. Targeted Split Reversal Protocol (`OperatorIdentitySplitDecision`)
```typescript
export async function executeOperatorIdentitySplit(
  client: pg.PoolClient,
  params: {
    split_decision_id: string;
    operator_id: string;
    auth_session_id: string;
    auth_credential_fingerprint: string;
    canonical_product_id: string;
    candidate_ids_to_detach: string[];
    substantive_rationale: string;
    record_jcs_sha256: string;
  }
): Promise<void> {
  await client.query('BEGIN ISOLATION LEVEL SERIALIZABLE;');
  try {
    // Tier 1 Lock: Canonical product row
    await client.query(
      `SELECT canonical_product_id FROM market_canonical_products WHERE canonical_product_id = $1 FOR UPDATE;`,
      [params.canonical_product_id]
    );

    // Tier 2 Lock: Sorted candidates
    const sortedIds = [...params.candidate_ids_to_detach].sort();
    await client.query(
      `SELECT candidate_id FROM market_candidates WHERE candidate_id = ANY($1) ORDER BY candidate_id ASC FOR UPDATE;`,
      [sortedIds]
    );

    await client.query(
      `UPDATE market_candidates
       SET canonical_product_id = NULL,
           identity_review_status = 'SPLIT_CONFIRMED',
           entity_version = entity_version + 1,
           updated_at_utc = clock_timestamp()
       WHERE candidate_id = ANY($1) AND canonical_product_id = $2;`,
      [sortedIds, params.canonical_product_id]
    );

    const remRes = await client.query(
      `SELECT count(*) as count FROM market_candidates WHERE canonical_product_id = $1;`,
      [params.canonical_product_id]
    );
    if (parseInt(remRes.rows[0].count, 10) === 0) {
      await client.query(
        `UPDATE market_canonical_products
         SET lifecycle_state = 'DEPRECATED_EMPTY_SPLIT', updated_at_utc = clock_timestamp()
         WHERE canonical_product_id = $1;`,
        [params.canonical_product_id]
      );
    }

    await client.query(
      `INSERT INTO market_operator_governance_log (
         decision_id, action_type, operator_id, auth_session_id, auth_credential_fingerprint,
         target_canonical_product_id, candidate_ids, substantive_rationale,
         record_jcs_sha256, recorded_at_utc
       ) VALUES ($1, 'REVERSE_CANONICAL_MERGE', $2, $3, $4, $5, $6, $7, $8, clock_timestamp());`,
      [
        params.split_decision_id,
        params.operator_id,
        params.auth_session_id,
        params.auth_credential_fingerprint,
        params.canonical_product_id,
        sortedIds,
        params.substantive_rationale,
        params.record_jcs_sha256
      ]
    );

    await client.query('COMMIT;');
  } catch (err) {
    await client.query('ROLLBACK;');
    throw err;
  }
}
```

---

## 8. Authoritative Paper Commitment Gate Alignment

To resolve review finding **P1-06 (Global Lock-Participation Contract & Explicit Concurrency Protocols)**:

### A. Global Lock-Participation Contract & Advisory Key Conventions
1. **Advisory Lock Key Namespace Conventions:**
   To guarantee zero collisions across application domains, all 64-bit advisory lock keys follow an explicit global partition:
   - `65537` (`0x0001_0001`): `LOCK_QUEUE_CAPACITY_ADMISSION` — Serializes queue admission depth checks.
   - `65538` (`0x0001_0002`): `LOCK_CHECKPOINT_EPOCH_COORDINATOR` — Serializes all checkpoint epoch transitions.
   - `131072 + hash` (`0x0002_xxxx`): `LOCK_CANONICAL_PRODUCT_CREATION` — Serializes new canonical product row insertion.
2. **Global Participation Mandate:**
   Every code path that advances, invalidates, exports, anchors, or replaces a current checkpoint epoch **must** acquire `pg_advisory_xact_lock(65538)` and the current epoch row `FOR UPDATE`.
3. **Partial Unique Index:**
   ```sql
   CREATE UNIQUE INDEX uq_market_ledger_current_epoch 
   ON market_ledger_checkpoint_epochs (is_current) 
   WHERE is_current = true;
   ```
   Ensures at most one active current epoch exists across the entire lifecycle, including migrations and crash recovery.
4. **Atomic Rollback Guarantee:**
   If a checkpoint transition fails at any point after marking the prior epoch non-current but before inserting the new epoch, PostgreSQL aborts the entire transaction (`ROLLBACK`), preserving the prior anchored epoch intact.

### B. Session Revocation Mutual Exclusion & Non-Retroactive Semantics
1. **Cryptographic Secret Placement:**
   The HMAC signing secret $K_{\text{auth}}$ resides exclusively in the isolated **System Security Kernel / Hardware Security Module / Vault**, completely inaccessible to client browsers, workers, or callers.
2. **Authoritative Session Table & Exclusive Locking:**
   ```sql
   CREATE TABLE market_operator_sessions (
     session_id VARCHAR(64) PRIMARY KEY,
     operator_id VARCHAR(64) NOT NULL,
     status VARCHAR(32) NOT NULL DEFAULT 'ACTIVE', -- 'ACTIVE' | 'REVOKED' | 'EXPIRED'
     revoked_at_utc TIMESTAMPTZ,
     expires_at_utc TIMESTAMPTZ NOT NULL,
     updated_at_utc TIMESTAMPTZ NOT NULL DEFAULT clock_timestamp()
   );
   ```
   - In `authorizePaperCommitAtomic`, the transaction locks the session row exclusively:
     ```sql
     SELECT session_id, status, expires_at_utc FROM market_operator_sessions 
     WHERE session_id = $1 FOR UPDATE;
     ```
     If row not found, `status !== 'ACTIVE'`, or `expires_at_utc <= clock_timestamp()`, the transaction aborts with `E-AUTH-SESSION-REVOKED-OR-INVALID`.
   - In `revokeOperatorSessionAtomic`, revocation acquires the same row `FOR UPDATE` and sets `status = 'REVOKED'`.
   - *Non-Retroactive Serialization Guarantee:* If revocation starts first, it locks the row, sets `status = 'REVOKED'`, and commits. The racing paper commit then reads `status = 'REVOKED'` and fails closed. If the paper commit starts first, it consumes the single-use grant and completes before revocation takes effect. Revocation does **not** retroactively cancel an already-committed paper authorization.

### C. Atomic Execution Protocol (`authorizePaperCommitAtomic`)
```typescript
export async function authorizePaperCommitAtomic(
  client: pg.PoolClient,
  grant: OperatorAuthorizationGrant,
  candidate_id: string
): Promise<{ status: 'PROMOTED_TO_PAPER_ELIGIBLE'; event_id: string; new_epoch_id: string }> {
  // 1. Gateway Signature Verification using Kernel Secret
  const payloadToVerify = {
    grant_id: grant.grant_id,
    issuer_id: grant.issuer_id,
    operator_id: grant.operator_id,
    auth_session_id: grant.auth_session_id,
    role_verified: grant.role_verified,
    candidate_id: grant.candidate_id,
    candidate_version: grant.candidate_version,
    evidence_digest_sha256: grant.evidence_digest_sha256,
    permitted_action: grant.permitted_action,
    issued_at_utc: grant.issued_at_utc,
    valid_until_utc: grant.valid_until_utc
  };
  const expectedSig = hmacSha256(canonicalizeJCS(payloadToVerify), process.env.SYSTEM_AUTH_KERNEL_SECRET!);
  if (grant.grant_signature_sha256 !== expectedSig) {
    throw new Error('E-AUTH-GRANT-SIGNATURE-FORGERY: Grant cryptographic signature is invalid');
  }

  await client.query('BEGIN ISOLATION LEVEL SERIALIZABLE;');
  try {
    // 2. Exclusive Checkpoint Epoch Coordination Lock (Namespace 65538)
    await client.query(`SELECT pg_advisory_xact_lock(65538);`);

    // 3. Pre-Commit Anchor Verification with Exclusive Row Lock
    const epochRes = await client.query(
      `SELECT epoch_id, status FROM market_ledger_checkpoint_epochs 
       WHERE is_current = true FOR UPDATE;`
    );
    if (epochRes.rowCount === 0 || epochRes.rows[0].status !== 'EXPORTED_AND_ANCHORED') {
      throw new Error(`E-OPP-UNANCHORED-CHECKPOINT-BLOCKED: Active epoch is not EXPORTED_AND_ANCHORED`);
    }
    const currentEpoch = epochRes.rows[0];

    // 4. Session Revocation Mutual Exclusion
    const sessionRes = await client.query(
      `SELECT session_id, status, expires_at_utc FROM market_operator_sessions 
       WHERE session_id = $1 FOR UPDATE;`,
      [grant.auth_session_id]
    );
    if (sessionRes.rowCount === 0 || sessionRes.rows[0].status !== 'ACTIVE') {
      throw new Error(`E-AUTH-SESSION-REVOKED-OR-INVALID: Operator session is not active`);
    }
    const session = sessionRes.rows[0];

    // Wall-Clock Expirations
    const timeRes = await client.query(`SELECT clock_timestamp() as now_time;`);
    const nowTime = new Date(timeRes.rows[0].now_time).getTime();
    if (new Date(session.expires_at_utc).getTime() <= nowTime) {
      throw new Error(`E-AUTH-SESSION-EXPIRED: Operator session has expired`);
    }
    if (new Date(grant.valid_until_utc).getTime() <= nowTime) {
      throw new Error(`E-AUTH-GRANT-EXPIRED: Authorization grant has expired`);
    }

    // 5. Grant Single-Use Consumption
    await client.query(
      `INSERT INTO market_consumed_authorization_grants (grant_id, consumed_at_utc)
       VALUES ($1, clock_timestamp());`,
      [grant.grant_id]
    );

    // 6. Candidate Row Lock & Version Binding
    const candRes = await client.query(
      `SELECT candidate_id, entity_version, evidence_digest_sha256, lifecycle_state
       FROM market_candidates WHERE candidate_id = $1 FOR UPDATE;`,
      [candidate_id]
    );
    const candidate = candRes.rows[0];
    if (candidate.entity_version !== grant.candidate_version || candidate.evidence_digest_sha256 !== grant.evidence_digest_sha256) {
      throw new Error(`E-OPP-CONCURRENT-EVIDENCE-MUTATION: Candidate version or evidence has mutated`);
    }

    // 7. Update Candidate Lifecycle State
    await client.query(
      `UPDATE market_candidates
       SET lifecycle_state = 'PAPER_ELIGIBLE',
           entity_version = entity_version + 1,
           updated_at_utc = clock_timestamp()
       WHERE candidate_id = $1;`,
      [candidate_id]
    );

    // 8. Append Lifecycle Event to Ledger
    const eventId = `EVT-${candidate_id}-${Date.now()}`;
    await client.query(
      `INSERT INTO market_event_ledger (event_id, candidate_id, event_type, payload_json, created_at_utc)
       VALUES ($1, $2, 'CANDIDATE_PROMOTED_TO_PAPER_ELIGIBLE', $3, clock_timestamp());`,
      [eventId, candidate_id, JSON.stringify({ grant_id: grant.grant_id, operator_id: grant.operator_id })]
    );

    // 9. Epoch Invalidation: Close old current epoch, open new unanchored 'OPEN' epoch
    const newEpochId = `EPOCH-${Date.now()}`;
    await client.query(
      `UPDATE market_ledger_checkpoint_epochs
       SET is_current = false, updated_at_utc = clock_timestamp()
       WHERE epoch_id = $1;`,
      [currentEpoch.epoch_id]
    );
    await client.query(
      `INSERT INTO market_ledger_checkpoint_epochs (epoch_id, start_event_id, status, is_current, opened_at_utc)
       VALUES ($1, $2, 'OPEN', true, clock_timestamp());`,
      [newEpochId, eventId]
    );

    await client.query('COMMIT;');
    return { status: 'PROMOTED_TO_PAPER_ELIGIBLE', event_id: eventId, new_epoch_id: newEpochId };
  } catch (err) {
    await client.query('ROLLBACK;');
    throw err;
  }
}
```

---

## 9. Exhaustive State Domain Ownership Matrix & Lifecycle Transitions

### A. Four Orthogonal State Domains
Every state in the platform belongs strictly to one declared domain:
1. **Domain 1: Candidate Lifecycle State (`CandidateLifecycleState`)**  
   `NEW` | `INVESTIGATE` | `UNDER_REVIEW` | `VERIFIED` | `PAPER_ELIGIBLE` | `DEFERRED` | `REJECTED`  
   *(Owner: `OpportunityLifecycleEngine`. Note: Candidate identity convergence is strictly partitioned into Domain 4).*
2. **Domain 2: Investigation Macro Status (`InvestigationMacroStatus`)**  
   `UNSCHEDULED` | `PENDING` | `IN_PROGRESS` | `COMPLETED` | `FAILED` | `DEFERRED_QUEUE_SATURATED` | `AWAITING_HUMAN_REVIEW`  
   *(Owner: `InvestigationOrchestratorService`).*
3. **Domain 3: Task Execution State (`TaskState`)**  
   `QUEUED` | `LEASED` | `RETRYING` | `SUCCEEDED` | `CANCELLED_SUPERSEDED` | `DEAD_LETTER_QUARANTINE` | `CANCELLED`  
   *(Owner: `DurableInvestigationQueue`).*
4. **Domain 4: Identity Review Status (`IdentityReviewStatus`)**  
   `UNREVIEWED` | `REVIEW_PENDING` | `CONVERGENCE_PROPOSED` | `MERGE_APPROVED` | `SPLIT_CONFIRMED`  
   *(Owner: `EntityIdentityResolver`).*

### B. Authoritative Exhaustive Lifecycle Transition Table:
| Source State | Trigger Event | Target State | Prerequisites & Guard Conditions |
| :--- | :--- | :--- | :--- |
| `NEW` | `SIEVE_PASSED` | `INVESTIGATE` | Gross spread $\ge 1,000\text{ bps}$; malformed fields absent. |
| `NEW` | `SIEVE_FAILED` | `REJECTED` | Gross spread $< 1,000\text{ bps}$ or unparseable schema. |
| `INVESTIGATE` | `EVIDENCE_SUFFICIENT` | `UNDER_REVIEW` | All 5 mandatory fields captured and verified. |
| `INVESTIGATE` | `SEASONAL_DEFERRAL` | `DEFERRED` | Operational seasonal window inactive. |
| `INVESTIGATE` | `CRITICAL_SPEC_FAILED`| `REJECTED` | Fatal flaw detected (e.g. counterfeit signal). |
| `UNDER_REVIEW`| `VERIFICATION_PASSED` | `VERIFIED` | 100% critical evidence corroborated; zero active conflicts. |
| `UNDER_REVIEW`| `EXTERNAL_UNKNOWN` | `DEFERRED` | Supplier quote unverified within TTL window. |
| `UNDER_REVIEW`| `VERIFICATION_FAILED` | `REJECTED` | Uncorroborated specs or defect rate $> 500\text{ bps}$. |
| `VERIFIED` | `UNDERWRITING_PASSED` | `PAPER_ELIGIBLE` | Net margin $\ge 12\%$, RoPF $\ge 25\%$, capital recovery $\le 60\text{d}$. |
| `VERIFIED` | `SUB_HURDLE_MARGIN` | `DEFERRED` | Economically marginal ($0\% \le \text{Margin} < 12\%$). |
| `VERIFIED` | `COMMERCIAL_LOSS` | `REJECTED` | Negative net contribution margin ($M_{\text{paise}} \le 0$). |
| `PAPER_ELIGIBLE`| `REVOCATION_STALE` | `DEFERRED` | Price delta detected or field TTL expired. |
| `PAPER_ELIGIBLE`| `REVOCATION_COLLAPSE`| `REJECTED` | Retail price collapsed below breakeven floor. |
| `DEFERRED` | `OBSERVATION_REFRESHED`| `INVESTIGATE` | New observation captured; generation incremented. |
| `REJECTED` | `OPERATOR_REACTIVATED`| `INVESTIGATE` | Authenticated human action (`OPERATOR_REACTIVATE_CANDIDATE`). |

---

## 10. Defensible Field-Specific Validation Matrix & Piecewise Comparison

| Field Class | Target Field Name | Measurement Unit | Freshness TTL | Discrepancy Tolerance ($\Delta_{\text{tol}}$) | Absolute Floor ($\Delta_{\text{abs}}$) | Conflict Trigger Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Retail ASP** | `prevailing_retail_asp_paise` | Integer paise | **7 days** | $\Delta > 300\text{ bps}$ ($3.0\%$) | $\Delta > 200\text{ paise}$ ($\text{₹}2.00$) | Record conflict; mark `EVIDENCE_CONFLICT_DETECTED` |
| **Supplier Quote** | `factory_gate_quote_paise` | Integer paise | **14 days** | $\Delta > 200\text{ bps}$ ($2.0\%$) | $\Delta > 100\text{ paise}$ ($\text{₹}1.00$) | Record conflict; mark `EVIDENCE_CONFLICT_DETECTED` |
| **Freight Quote** | `estimated_freight_paise` | Integer paise | **30 days** | $\Delta > 500\text{ bps}$ ($5.0\%$) | $\Delta > 500\text{ paise}$ ($\text{₹}5.00$) | Flag advisory variance; retain higher cost |
| **Reviews / Defects**| `observed_defect_rate_bps` | Basis points | **45 days** | $\Delta > 150\text{ bps}$ ($1.5\%$) | $\Delta > 50\text{ bps}$ ($0.5\%$) | Trigger `GRIEVANCE_SURFACED`; require red-team |
| **HSN / Tax Rates** | `gst_rate_bps`, `hsn_code` | Categorical / bps | **180 days** | Strict binary equality | Binary ($A \neq B$) | **Immediate Escalation to AWAITING_HUMAN_REVIEW** |
| **Product Specs** | `dimensions`, `material_grade` | Standard spec | **365 days** | Strict spec equality | Spec ($A \neq B$) | **Disqualify Merge; Maintain Source Split** |

---

## 11. Multi-Dimensional Resource Limits & Bounded Admission Policy

| Dimension | Scope | Hard Ceiling | Unit | Failure Action |
| :--- | :--- | :--- | :--- | :--- |
| External Provider Usage | Platform-wide | 0 | API Calls | Strictly Blocked (Offline Fixtures Only) |
| Wall-Clock Lease Timeout | Per-task execution | 30 | Seconds | Task expires; re-queued or DLQ |
| Agent Execution Timeout | Per-task dispatch | 3,000 | Milliseconds | Abort task execution; RETRYING |
| Candidate Macro Timeout | Per-candidate run | 120 | Seconds | Halt; AWAITING_HUMAN_REVIEW |
| Maximum Dispatches | Per-candidate per gen | 5 | Tasks | Sieve halts; evaluate status |
| Maximum Task Attempts | Per-task lifetime | 3 | Attempts | Terminal DEAD_LETTER_QUARANTINE |
| Dispatch Payload Size | Per-task message | 32 | Kilobytes | Reject dispatch (E-PAYLOAD-TOO-LARGE) |
| Result Envelope Size | Per-task output | 64 | Kilobytes | Reject commit (E-RESULT-TOO-LARGE) |
| Candidate Lifetime Tokens| Per-candidate run | 10,000 | Heuristic Tok. | Halt; AWAITING_HUMAN_REVIEW |
| Global Concurrent Tasks | Platform-wide | 4 | Workers | Throttle claim queue |
| Per-Candidate Concurrency| Per-candidate tasks | 2 | Workers | Throttle candidate tasks |
| Queue Depth Capacity | Platform-wide | 100 | Tasks | Non-silent admission policy |

---

## 12. Local Observability & Telemetry (No External API Expansion)
Telemetry is restricted to **bounded local structured logging and in-memory test observers** with tags `[ORCHESTRATION_QUEUE]`, `[AGENT_DISPATCH]`, and `[LEASE_FENCING]`.

---

## 13. Acceptance Suite 49 Test Specification & Reconciled Test Manifest

To resolve review finding **P0-16 (Decoupling Historical Baseline from Active Specification Inventory)**:

### A. Authoritative Deterministic Historical Baseline Manifest (`BASELINE_HISTORICAL_SNAPSHOT_V1`)
- **Git Commit Anchor:** [`4ba8191`](https://github.com/Shrom-Main/Market-HFT-OS/commit/4ba8191)
- **Historical Inventory (47 Tracked Files):**
  - **46 Files in `tests/acceptance/`:** `suite01` through `suite16` (16 files), `suite18` through `suite41` (24 files), `suite42` (1 file), `suite44` through `suite48` (5 files). *(Suite 17 is located in integration; Suite 43 was never created).*
  - **1 File in `tests/integration/`:** `tests/integration/suite17_real_postgres_integration.test.ts`.
- **Historical Exclusion:** `suite42` is an external live network probe and is excluded from deterministic runs.
- **Historical Pass Status:** **427 / 427 passing tests across 46 deterministic test files** (`EXECUTED_AND_PASSED`).
- **Command:** `npx vitest run --exclude "**/suite42*"`.

### B. Acceptance Suite 49 Active Specification Inventory (27 Test Cases)
- **File Location:** `tests/acceptance/suite49_slice2c_investigation_orchestration.test.ts`
- **Current Status:** **`SPECIFIED — AWAITING_IMPLEMENTATION_AUTHORIZATION`**. (No code is written in this file during the specification design phase).
- **Post-Authorization Target Combined Baseline:** Upon future owner authorization of `DEC-030` and implementation of Phase 1–3, the complete platform test suite will assert **$427 + 27 = 454$ passing tests across 47 deterministic test files**.

| Ref ID | Test Identifier | Specification Status | Adversarial Verification Focus |
| :--- | :--- | :--- | :--- |
| **TR-01** | `S49-001-SCREENING-VS-UNDERWRITING` | `SPECIFIED` | High gross spread with negative RoPF passes screening but fails closed at paper commit. |
| **TR-02** | `S49-002-INTEGER-SUBUNIT-CALCULATION` | `SPECIFIED` | Evaluates synthetic $E_1$–$E_3$ schedule; asserts bit-exact signed rounding. |
| **TR-03** | `S49-003-POSTGRES-QUEUE-FAIL-CLOSED` | `SPECIFIED` | Simulates DB disconnect; queue throws `E-QUEUE-DB-UNAVAILABLE` without falling back. |
| **TR-04** | `S49-004-LEASE-FENCING-TOKEN-REJECTION` | `SPECIFIED` | Paused worker resumes after re-claim; commit rejected via `E-QUEUE-STALE-LEASE-FENCE-REJECTED`. |
| **TR-05** | `S49-005-EXPIRED-LEASE-COMMIT-REJECTION` | `SPECIFIED` | Worker commits at $t > t_{\text{expires}}$; commit rejected via `E-QUEUE-LEASE-EXPIRED-AT-COMMIT`. |
| **TR-06** | `S49-006-CRASH-TIMEOUT-LEASE-RECOVERY` | `SPECIFIED` | Simulated worker crash mid-lease; expired lease recovered safely by secondary worker after 30s. |
| **TR-07** | `S49-007-GENERATION-REVISION-DEDUP` | `SPECIFIED` | Identical dispatch within gen is no-op; price delta triggers `GEN-02` with distinct ID. |
| **TR-08** | `S49-008-LATE-COMMIT-GENERATION-SUPERSEDED` | `SPECIFIED` | Generation increments while worker active; commit archived without mutating active state. |
| **TR-09** | `S49-009-DLQ-QUARANTINE-ESCALATION` | `SPECIFIED` | Task fails 3 consecutive attempts; transitions to `DEAD_LETTER_QUARANTINE`. |
| **TR-10** | `S49-010-PIECEWISE-CONFLICT-EVALUATION` | `SPECIFIED` | First observation sets baseline; ₹0.02 vs ₹0.04 ignores bps; ₹85 vs ₹95 detects conflict. |
| **TR-11** | `S49-011-GRANULAR-TTL-EXPIRATION` | `SPECIFIED` | 8-day price marked stale; 8-day spec and HSN code remain valid. |
| **TR-12** | `S49-012-REPLAY-SAFE-MERGE-AND-SPLIT` | `SPECIFIED` | Rejects merge if version stale; targeted split restores source candidates. |
| **TR-13** | `S49-013-NON-SILENT-QUEUE-CAPACITY-DROP` | `SPECIFIED` | Saturated queue logs rejection in `market_task_rejections` and sets candidate DEFERRED. |
| **TR-14** | `S49-014-PINNED-BASELINE-REGRESSION-CHECK` | `SPECIFIED` | Verifies the historical 427-test baseline from commit `4ba8191` remains clean. |
| **TR-15** | `S49-015-REPLAY-OBSERVATION-ID-MISMATCH-REJECTION` | `SPECIFIED` | Retry supplying `OBS-B` instead of committed `OBS-A` fails closed with `E-QUEUE-COMMIT-ENVELOPE-MISMATCH`. |
| **TR-16** | `S49-016-CONCURRENT-PAPER-COMMIT-EPOCH-SERIALIZATION` | `SPECIFIED` | At most one paper commit succeeds; second fails with `E-OPP-UNANCHORED-CHECKPOINT-BLOCKED`. |
| **TR-17** | `S49-017-SESSION-REVOCATION-GRANT-RACE` | `SPECIFIED` | Row lock `FOR UPDATE` serializes operations; revoked session aborts with `E-AUTH-SESSION-REVOKED-OR-INVALID`. |
| **TR-18** | `S49-018-TAX-CREDIT-ISOLATION-AND-RECONCILIATION` | `SPECIFIED` | Bank cash, GST assets, and direct-tax assets reconcile without double-counting. |
| **TR-19** | `S49-019-TAX-APPLICABILITY-UNKNOWN-FAIL-CLOSED` | `SPECIFIED` | Unverified seller PAN or date outside config fails closed to `DATA_REQUIRED`. |
| **TR-20** | `S49-020-MISSING-LEAD-TIME-FAIL-CLOSED` | `SPECIFIED` | Missing $D_{\text{inv}}$ cannot be assumed zero; fails closed to `DATA_REQUIRED`. |
| **TR-21** | `S49-021-TERMINAL-CASH-MISMATCH-ABORT` | `SPECIFIED` | Delta check $\Delta_{\text{reconciliation}} \neq 0n$ surfaces `MODEL_INCONSISTENCY_ERROR`; zero viability emitted. |
| **TR-22** | `S49-022-EXPANDED-SUITE-INDEPENDENT-TARGET` | `SPECIFIED` | Verifies that historical 427-test baseline is verifiable without requiring expanded suite to remain at 427. |
| **TR-23** | `S49-023-RECONCILIATION-DETECTS-OMITTED-OR-DOUBLED-TAX` | `SPECIFIED` | Reconciliation detects deliberately omitted or double-counted tax asset and fails closed. |
| **TR-24** | `S49-024-JIT-DISPATCH-WITHOUT-DAY-ZERO-CASH-REJECTED` | `SPECIFIED` | JIT dispatch without evidence of genuine Day-0 customer cash receipt cannot qualify as zero-day recovery. |
| **TR-25** | `S49-025-KNOWN-UNREGISTERED-VS-UNKNOWN-REGISTRATION` | `SPECIFIED` | Known unregistered seller yields `SELLER_INELIGIBLE_FOR_MODEL_SCOPE`; unverified status yields `DATA_REQUIRED`. |
| **TR-26** | `S49-026-UNDEFINED-OR-NEGATIVE-ROPF-CANNOT-PASS-HURDLE` | `SPECIFIED` | Zero-duration, negative, and undefined RoPF outcomes cannot accidentally pass commercial hurdles. |
| **TR-27** | `S49-027-CHECKPOINT-MUTATION-ONE-CURRENT-EPOCH-INVARIANT`| `SPECIFIED` | Concurrent checkpoint mutation and paper commit preserve one-current-epoch invariant or roll back cleanly. |

---

## 14. Phased Implementation Roadmap Disclaimer (Proposed Post-Approval)

> [!CAUTION]
> **PROPOSED FUTURE ROADMAP ONLY — NOT AN AUTHORIZATION TO EXECUTE:**  
> The phases listed below are engineering proposals for post-approval execution. Neither this roadmap nor this specification confers authority to write code, activate queues, or invoke agents. Implementation remains strictly gated on explicit Project Owner authorization and formal ledger recording.

```
[Phase 1: Fenced Queue & Persistence Engine]
  - PostgreSQL schema for market_investigation_tasks and market_task_superseded_executions
  - Atomic claim transaction with fencing_token and clock_timestamp() unexpired lease validation
  - Full 8-field commit envelope verification and idempotent replay
  - Tests: S49-003, S49-004, S49-005, S49-006, S49-009, S49-013, S49-015

[Phase 2: Specialist Agent Contracts & Pure Extraction]
  - InvestigationPlanner (max 5 tasks, generation_id)
  - EconomicsAgent (integer paise extraction, zero math)
  - EvidenceAgent (piecewise tolerances, verbatim spans)
  - IdentityReviewerAgent (advisory proposals, zero silent merges)
  - IndependentVerifier (hash-verified audit trail)
  - Tests: S49-001, S49-002, S49-007, S49-008, S49-010, S49-011, S49-012, S49-018, S49-019, S49-020, S49-023, S49-024, S49-025, S49-026

[Phase 3: End-to-End Orchestration & Baseline Reconciliation]
  - InvestigationOrchestratorService coordinating the pipeline
  - Hash-verified Investigation Dossier compilation
  - Execution of complete Acceptance Suite 49 (27 tests)
  - Verification of 427 prior baseline tests (Total: 454 tests clean)
  - Tests: S49-014, S49-016, S49-017, S49-021, S49-022, S49-027
```