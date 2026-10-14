# ADR-0002: Anchored Cumulative COGS Allocation and Long-Only Inventory Policy

* **Status:** Accepted
* **Date:** 2026-10-14
* **Deciders:** Project Owner, System Architect, Financial Engine Lead
* **Technical Domain:** Portfolio Valuation, Accounting, Inventory Invariants

---

## Context and Problem Statement

In Gate M1, the financial engine specified standard inventory tracking. During Gate M2 implementation (`src/portfolio/simulationPortfolio.ts`), testing revealed two critical accounting and domain requirements:
1. **Rounding Drift in Incremental Partial Fills:** When inventory tranches are liquidated across successive partial executions, computing cost of goods sold (COGS) on an incremental basis ($\text{quantity} \times \text{unit\_cost}$) with integer subunit currency rounding causes rounding errors that accumulate over time. In a multi-fill tranche, the sum of incremental COGS did not match the initial acquisition cost $C_0$ when the tranche reached full liquidation.
2. **Physical Commercial Arbitrage Model:** Physical inventory arbitrage (e.g., hose clamps, fasteners, MRO supplies) does not permit naked short selling. A trading strategy or order routing error that sells more units than available on hand violates physical delivery constraints and creates unbounded financial liability.

## Decision Drivers

1. Exact conservation of currency subunits: $\sum \Delta\text{COGS} \equiv C_0$ upon 100% liquidation.
2. Complete determinism and reproducibility under RFC 8785 canonical representations.
3. Strict fail-closed rejection of short selling across all portfolio and execution layers.

## Considered Options

* **Option 1 (Incremental Floating/Subunit COGS):** Compute $\text{unit\_cost} = C_0 / Q_0$ once, round to subunit, and multiply by fill quantity.
  - *Deficiency:* For tranches where $C_0$ is not evenly divisible by $Q_0$, accumulated rounding drift creates unallocated cost residuals.
* **Option 2 (Epoch-Anchored Cumulative Allocation):** Maintain the cumulative allocated quantity $s_k = \sum_{i=1}^k q_i$. Calculate total cumulative allocated COGS $A(s_k)$ using Banker's rounding (`HALF_EVEN`), and determine incremental COGS as the difference:
  $$\Delta \text{COGS}_k = A(s_k) - A(s_{k-1})$$

## Decision Outcome

Chosen option: **Option 2**. We adopt epoch-anchored cumulative COGS allocation and strict long-only inventory invariants.

### Mathematical Specification

Let:
- $Q_0 \in \mathbb{N}^+$: Initial inventory quantity acquired in the epoch tranche.
- $C_0 \in \mathbb{N}$: Total acquisition cost of tranche in integer currency subunits.
- $s_k \in [0, Q_0]$: Cumulative quantity sold up to and including fill $k$, where $s_0 = 0$.

The cumulative allocated COGS function $A(s)$ is defined as:
$$A(s) = \operatorname{divideHalfEven}(C_0 \cdot s, Q_0)$$

The incremental COGS allocated to fill $k$ ($q_k = s_k - s_{k-1}$) is:
$$\Delta \text{COGS}_k = A(s_k) - A(s_{k-1})$$

**Boundary Proof:**
- At $s = 0$: $A(0) = \operatorname{divideHalfEven}(0, Q_0) = 0$.
- At $s = Q_0$: $A(Q_0) = \operatorname{divideHalfEven}(C_0 \cdot Q_0, Q_0) = C_0$.
- Therefore: $\sum_{k=1}^N \Delta \text{COGS}_k = A(Q_0) - A(0) = C_0$.
- Zero rounding drift is guaranteed regardless of fill segmentation.

### Long-Only Inventory Policy

1. **Short Position Prohibition:** Any execution fill or simulated order submission that would reduce inventory quantity below zero is rejected fail-closed with error:
   `E-ERR-044: SHORT_POSITIONS_FORBIDDEN`
2. **Allocation Cap:** Available inventory for order creation is strictly bounded by unallocated on-hand stock:
   $$Q_{\text{available}} = Q_{\text{on\_hand}} - Q_{\text{reserved}} \ge 0$$

## Traceability and Compliance

- **Implementation:** `src/portfolio/simulationPortfolio.ts` (`SimulationPortfolio.recordFill`, `computeAnchoredCumulativeCOGS`).
- **Test Evidence:**
  - `tests/acceptance/suite13_market_feed_execution.test.ts` (M2-EXEC-PORTFOLIO-COGS-007, M2-EXEC-PORTFOLIO-SHORT-008)
  - `tests/acceptance/suite14_websocket_portfolio.test.ts`
  - `tests/acceptance/suite15_e2e_simulation_pipeline.test.ts`
- **Error Codes:** `E-ERR-044` (Short positions forbidden), `E-ERR-039` (Inventory shortfall).
