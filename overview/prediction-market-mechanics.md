# Prediction Market Mechanics

The <mark style="color:orange;">Kynex</mark> Protocol establishes a trust-less, non-custodial framework for binary prediction markets centered on verifiable on-chain portfolio performance. Unlike subjective event markets, Kynex utilizes deterministic execution: every market is anchored to immutable blockchain state data, ensuring that resolutions are objective, mathematically verifiable, and resistant to centralized manipulation.

The system is architected to prioritize signal accuracy and capital efficiency, utilizing a specialized settlement layer that removes human intervention from the resolution lifecycle.

### Market Initialization & Configuration

Markets on the Kynex protocol function as binary derivative contracts tied to measurable, on-chain portfolio behaviors. All markets are initialized via smart contracts with strict parameter enforcement to ensure solvability.

1. **Supported Event Classes**

The protocol currently supports the instantiation of markets based on the following verifiable metrics:

* Alpha Generation: Portfolio Return on Investment (ROI) relative to a benchmark.
* Absolute Performance: Net ROI over a specific epoch.
* Liquidity Flux: Asset inflow/outflow volume breaching defined thresholds.
* Conditional Price Action: Asset price behavior conditional on specific wallet interactions.

Technical Constraint: Every market must map to a Boolean (`True`/`False`) condition resolvable via the protocol’s integrated oracle layer.

**2. Wallet & Signal Integrity**

To mitigate "wash trading" or signal fabrication, the protocol enforces an eligibility filter at the contract level:

* Heuristic Analysis: Target wallets must meet minimum constraints regarding account age, transaction frequency, and historical volume.
* Sybil Resistance: Wallets exhibiting circular transaction patterns or derivative funding sources are automatically disqualified.
* Data Availability: Historical state data must be indexable and complete.

**3. Temporal Parameters & Expiry**

Markets operate within a rigorous state machine defined by three timestamps:

1. Inception: The block height at which the market opens for liquidity provisioning.
2. Maturity: The precise timestamp at which the outcome is measured. Post-maturity, the contract enters a locked state; no further staking is permitted.
3. Resolution Window: A bounded period for oracle aggregation and consensus before payout distribution.

**4. Capital Controls & Risk Management**

To prevent capital dominance attacks and ensure healthy liquidity distribution, the protocol enforces:

* Global Liquidity Caps: Maximum Total Value Locked (TVL) per market contract.
* Position Limits: Per-wallet stake caps to prevent single-entity market sway.
* Dynamic Risk Scaling: Automated cap adjustments based on the volatility profile of the underlying asset or portfolio.

### Participation & Liquidity Dynamics

<mark style="color:orange;">Kynex</mark> utilizes a Stake-Weighted Conviction Model, effectively operating as a localized pari-mutuel system where payout odds are derived from the liquidity imbalance between opposing outcome pools.

**1. Staking Architecture**

The user interaction flow is atomic and non-custodial:

1. Position Entry: Participants select a directional outcome (YES/NO).
2. Capital Allocation: KNX tokens are deposited into the specific outcome pool.
3. Escrow: Funds are held in the market’s smart contract until the resolved state is achieved.

**2. Pool Weighting & Implied Probability**

Liquidity pools are isolated per outcome. The market mechanism aggregates total stake ($$ $S$ $$) for Outcome A ($$ $S_A$ $$) versus Outcome B ($$ $S_B$ $$). The ratio $$ $S_A / S_B$ $$ determines the implied probability of the event. Larger capital allocation signals higher collective conviction, compressing the yield for that specific outcome.

**3. Dynamic Odds Algorithm**

The protocol employs an algorithmic pricing function that adjusts potential returns in real-time based on:

* Liquidity Ratios: The real-time delta between Pool A and Pool B.
* Time-Decay Function: Adjustments based on the proximity to time expiry.
* Concentration Metrics: Incentives designed to balance liquidity depth.

Market Behavior: As capital flows into the "YES" pool, the implied odds for "YES" decrease, while the potential payout multiplier for the "NO" pool increases. This creates an arbitrage opportunity for contrarian information, ensuring organic market equilibrium.

### Automated Resolution Layer

Market resolution is the process of importing off-chain or on-chain data to finalize the contract state. This process is fully automated, removing centralized dependencies.

**1. Deterministic Resolution Logic**

Every market contract contains immutable logic defining the winning condition.

* Example Logic: `IF (Wallet_A_ROI_7d > SOL_Index_ROI_7d + 500bps) THEN Outcome_YES = TRUE`
* Precision: All numerical comparisons utilize high-precision fixed-point arithmetic to prevent rounding errors.

**2. Oracle Aggregation & Verification**

To ensure data integrity, <mark style="color:orange;">Kynex</mark> employs a multi-layered verification stack:

* Redundancy: Aggregation of multiple price feeds and portfolio indexers.
* Block-Level Verification: Portfolio balances and transfers are verified against specific block heights to ensure snapshot accuracy.
* Consensus Check: Final resolution requires data consistency across multiple independent sources.

**3. Exception Handling & Fail-Safes**

In the event of oracle unavailability or data discrepancies:

* Grace Period: The Resolution Window extends automatically to allow for data stabilization.
* Invalidation Protocol: If consensus cannot be reached within the maximum bounds, the market is declared VOID. In this state, a safety function executes, returning all staked principal to users (minus unavoidable gas costs).

**4. Settlement & Economic Distribution**

Upon the confirmation of the winning outcome, the smart contract executes an atomic settlement routine.



### Winner Determination

The contract identifies the winning pool and aggregates the total liquidity from the losing pool. This process is code-governed and immutable; no admin key exists to override the result.

**1. Payout Logic**

Winning participants receive a payout composed of:

1. Principal Return: 100% of their original stake.
2. Yield Distribution: A pro-rata share of the losing pool’s liquidity.
3. Net Settlement: The total amount is transferred immediately to the user's wallet, net of protocol fees.

> $$Payout = Stake_{User} + (Stake_{User} / Pool_{TotalWinning}) \times (Pool_{TotalLosing} - Fees)$$

**2. Protocol Revenue Capture**

A configurable protocol fee is deducted from the losing pool prior to distribution. This revenue is systematically allocated to:

* Staking Rewards: Yield for <mark style="color:orange;">Kynex</mark> governance participants.
* Treasury Reserve: Funding for protocol maintenance and insurance funds.

**3. Economic Properties & Game Theory**

The Kynex mechanism design is aligned to produce high-signal market intelligence.

* Accuracy Incentives: Returns are strictly correlated with correct prediction; volume alone generates no yield.
* Penalty for False Conviction: Incorrect predictions result in a 100% loss of staked capital (transferred to the winning side).
* Discovery Scale: The system naturally scales liquidity around high-integrity data points, rewarding early and informed participants who correct market mispricing.

{% hint style="info" %}
Disclaimer: There are no fixed yields or guaranteed returns. The system is a zero-sum game regarding the principal stake, facilitated by a peer-to-peer liquidity protocol.
{% endhint %}
