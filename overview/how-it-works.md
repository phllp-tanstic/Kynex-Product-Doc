# How it works

### Operational Architecture: How Kynex Works

#### Overview

The Kynex Protocol operates as a deterministic state machine that transmutes On-Chain Data into Settled Value. The workflow is a linear progression from data ingestion to economic settlement, designed to be entirely transparent, automated, and trust-minimized.

The life-cycle of a Kynex market follows four distinct phases: Indexing, Instantiation, Execution, and Settlement.

### Step 1: Capital Tracking & Indexing (The Data Layer)

_<mark style="color:orange;">Objective: To source, sanitize, and verify actionable signal from raw blockchain state.</mark>_

<mark style="color:orange;">Kynex</mark> begins by indexing the "ground truth" of the chain. This is not sentiment analysis; it is the rigorous accounting of capital flow.

**1.1 Portfolio Discovery & Attribution**

The protocol allows users and indexers to subscribe to specific capital streams. This layer transforms raw addresses into identifiable strategies.

* Individual Entity Tracking: Monitoring specific high-net-worth wallets or DAO treasuries.
* Cluster Analysis: Aggregating "Smart Money" cohorts or sector-specific funds (e.g., "Top 10 L2 Yield Farmers").
* Custom Watchlists: Users can compose bespoke indices of wallets to serve as the underlying asset for a prediction market.

**1.2 Signal Sanitization (Anti-Sybil)**

Raw data is noisy. To ensure market integrity, the <mark style="color:orange;">Kynex</mark> Indexer applies a filtration mesh to remove non-economic activity.

* Activity Thresholds: Wallets must meet minimum volume and transaction frequency requirements to be eligible for market creation.
* Wash-Trading Exclusion: Heuristics detect and exclude circular transactions designed to fake volume or performance.
* Consistency Checks: Algorithms flag and filter erratic behavior that suggests key compromise or botting, ensuring only "organic" capital behavior is tracked.

**1.3 Alpha Confidence Scoring**

Before a market is spun up, the underlying data source is rated. The <mark style="color:orange;">Kynex</mark> Confidence Score (KCS) evaluates the reliability of the signal provider.

* Historical Accuracy: How often has this wallet’s behavior correlated with positive ROI?
* Risk-Adjusted Returns: Does the wallet generate alpha via skill or extreme leverage?
* Capital Efficiency: A metric assessing yield generated per unit of gas/fees.

### Step 2: Market Instantiation (The Creation Layer)

_<mark style="color:orange;">Objective: To define the terms of engagement and launch the financial contract.</mark>_

Once a valid data stream is identified, a Performance-Based Prediction Market (PBPM) is initialized via the Market Factory smart contract.

**2.1 Protocol-Governed Initiation**

Market creation is permissionless but rule-bound to ensure solvability.

* Verifiable Reference: Every market must query a specific, immutable on-chain data point.
* Resolution Logic: The "Definition of Success" must be binary (True/False) or scalar (Range) and mathematically provable.
* Liquidity Bootstrapping: Creators must seed the initial liquidity pool to guarantee immediate tradability.

**2.2 Smart Contract Parameters**

The creating actor defines the immutable variables of the market contract:

* Outcome Condition: The specific metric to be tested (e.g., _ROI > 5%_).
* Epoch Duration: The precise start and end block numbers.
* Benchmark Asset: The comparative asset for relative performance markets (e.g., _vs. SOL , vs. BTC_).
* Position Caps: Maximum exposure limits to prevent pool domination by single entities.

**2.3 Spam Resistance Fees**

To prevent ledger bloat and low-quality markets, a creation fee is payable in KNX.

* Quality Control: Serves as an economic barrier to spam.
* Revenue Stream: Fees are routed to the Protocol Treasury and Staking Rewards pool.

### Step 3: Staking & Execution (The Liquidity Layer)

_<mark style="color:orange;">Objective: To price the probability of the outcome via capital allocation.</mark>_

This is where insight becomes inventory. Participants trade against the probability of the event occurring.

**3.1 Binary Outcome Pools (YES / NO)**

Liquidity is deposited into opposing vaults.

* YES Vault: Long exposure. Stakers believe the wallet/portfolio _will_ achieve the metric.
* NO Vault: Short exposure. Stakers believe the wallet/portfolio _will fail_ the metric. These pools are isolated per market, meaning risk is contained solely within the specific contract.

**3.2 Automated Market Maker (AMM) Pricing**

<mark style="color:orange;">Kynex</mark> does not use an order book; it uses a bonding curve or AMM logic.

* Dynamic Odds: The price of "YES" and "NO" shares floats freely based on the ratio of capital in each pool.
* Imbalance Opportunities: As sentiment shifts, odds change. Early stakers or contrarian traders capture higher potential upside if the market swings back in their favor.

**3.3 MEV & Risk Protection**

To protect retail participants from predatory latency arbitrage (MEV), the protocol implements:

* Slippage Tolerances: Users define acceptable price impacts during staking.
* Transaction Ordering: Mechanisms to prevent front-running of large stakes.
* Position Limits: Caps on individual wallet contributions to maintain a healthy distribution of holders.

### Step 4: Deterministic Settlement (The Resolution Layer)

_<mark style="color:orange;">Objective: To finalize the market state and distribute value.</mark>_

Upon the expiration block, the market enters the Resolution Phase. This process is fully automated.

**4.1 On-Chain Verification**

The Settlement Engine executes a read-only call to the blockchain state at the precise snapshot block.

* Data Points: It retrieves wallet balances, transaction logs, and benchmark asset prices.
* Logic Execution: The contract computes the final performance metric (e.g., _Did Wallet X ROI = 6%?_) against the initial condition.

**4.2 Oracle Redundancy**

To ensure the data is incorruptible, <mark style="color:orange;">Kynex</mark> utilizes a multi-layered verification stack.

* Primary: Direct on-chain state reading (trustless).
* Secondary: Chainlink or Pyth feeds for benchmark asset pricing (ETH/USD).
* Fallback: A dispute window where KNX token holders can challenge a result if malicious manipulation is detected (rare).

**4.3 Distribution & Payouts**

Once the result is confirmed:

1. Aggregation: The losing pool’s liquidity is aggregated.
2. Fee Capture: The protocol fee (e.g., 2%) is deducted for the Treasury.
3. Pro-Rata Claim: The remaining pot is unlocked for the winning pool. Winners claim their original principal + their share of the winnings.
   * _Example:_ If you contributed 10% of the winning pool, you claim 10% of the total pot.



> ### The Closed-Loop Economy
>
> Kynex creates a self-reinforcing flywheel of intelligence and liquidity:
>
> 1. Capital moves on-chain (generating signal).
> 2. Markets form around the signal (pricing the probability).
> 3. Traders stake on the outcome (creating liquidity).
> 4. Accuracy is rewarded (incentivizing better analysis).
>
> This structure ensures that Kynex is not just a betting platform, but a decentralized pricing engine for portfolio alpha.
