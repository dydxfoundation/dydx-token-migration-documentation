---
description: >-
  An overview of parameters that are not covered in other sections of the
  governance documentation and are adjustable through a dYdX Chain governance
  Parameter Change Proposals.
---

# ⛓️ Governance Adjustable Parameters

## Overview

This documentation is divided into the following subsections:

* [**Trading Stats and Fees**](trading-stats-and-fees.md): this section covers the trading statistics look-back window and tiers of fees and discounts for each trader on dYdX Chain, based on their taker and maker volume.
* [**Trading Core**](trading-core.md): this section covers the core aspects of trading, namely insurance fund and liquidations config. The insurance fund acts as the first backstop to maintain systemic solvency when an account has a negative balance. The liquidations config defines the mechanism to close an account’s position when it falls below the margin requirements.&#x20;
* [**Markets**](markets.md): this section covers the Prices module (x/prices) parameters on dYdX Chain as well as the liquidity tier of each market based on standardized risk parameters.
* [**Perpetual**](perpetual.md): this section covers the Perpetual module (x/perpetuals) parameters on dYdX Chain, such as funding rate and epoch information. The perpetual funding rate enables the perpetual price to align with the underlying asset's price. Epoch information is a fixed interval where funding is credited or debited to each account.
* [**Clob**](clob.md): this section covers the Clob module (x/clob) that configures the order creation, placement, and cancellations on dYdX Chain.&#x20;
* [**Adding & Updating A Live Market**](adding-and-updating-a-live-market.md): this section explains the message required to add a new or update a live market on dYdX Chain.
* [**Safety**](safety.md): this section explains the safety parameters on dYdX Chain, namely the spam mitigation that is related to order creation and cancellation using the Clob module.
* [**Market Tiers**](market-tiers.md): this section shows the markets that are currently active on dYdX Chain and the liquidity tier that they are classified into, this section is updated regularly.&#x20;

\
