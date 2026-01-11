---
layout:
  width: default
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
metaLinks:
  alternates:
    - https://app.gitbook.com/s/yE16Xb3IemPxJWydtPOj/basics/markdown
---

# Prediction Markets

### The Execution Layer

_<mark style="color:orange;">Converting signal into a liquid derivative.</mark>_

This module is the economic engine of Kynex. It allows users to express financial conviction on the data surfaced by the Intelligence Layer. Unlike traditional prediction markets, Kynex markets are deterministically resolved via on-chain data, removing human bias and oracle manipulation.

#### Market Types

* Portfolio ROI Markets: Binary options on whether a specific portfolio will achieve a target ROI (e.g., _">10% APY"_) within a specific epoch.
* Wallet Alpha Markets: Markets predicting if a specific wallet will outperform a benchmark (e.g., _"Wallet X vs. SOL"_).
* Asset Behavior Markets: Speculation on macro-level capital flows (e.g., _"Will Net Inflows to Protocol Y exceed $5M this week?"_).

#### The Market Life-cycle (State Machine)

Each market operates as a self-contained smart contract following a strict state transition logic:

1. Initialization: Parameters (Target, Metric, Epoch, Strike Price) are defined and the contract is deployed.
2. Open (Staking Phase): The pool accepts liquidity for "YES" and "NO" positions. Pricing is dynamic based on pool weighting.
3. Locked (Execution Phase): Deposits are halted. The market tracks the live data but positions are immutable.
4. Resolution: The contract queries the Intelligence Layer for the final data point at the specific block height.
5. Settlement: The winning outcome is verified, and the contract enables claim functionality for winning shares.

#### Algorithmic Pricing

Kynex utilizes an Automated Market Maker (AMM) model for prediction pricing.

* Dynamic Odds: Prices adjust instantly based on the ratio of liquidity in the YES/NO pools.
* Slippage Protection: Mechanisms to prevent front-running and manipulation on low-liquidity markets.
* Liquidity Caps: Ceilings placed on specific markets to maintain manageable risk profiles and ensure solvable liquidity.
