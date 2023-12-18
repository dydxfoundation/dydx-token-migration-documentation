---
description: >-
  An overview of parameters that are not covered in other sections of the
  governance documentation and are adjustable through a dYdX Chain governance
  Parameter Change Proposals.
---

# Governance Adjustable Parameters

## Overview

This documentation is divided into the following subsections:

* [**Trading Stats and Fees**](https://app.gitbook.com/o/-MeNgGQU0ucT2xo4s8-T/s/cSd7APxHbsYMlFFAeIMP/\~/changes/38/dydx-chain-modules-and-parameters/governance-adjustable-parameters/trading-stats-and-fees): this section covers the trading statistics look-back window and tiers of fees and discounts for each trader on dYdX Chain, based on their taker and maker volume.
* [**Trading Core**](https://app.gitbook.com/o/-MeNgGQU0ucT2xo4s8-T/s/cSd7APxHbsYMlFFAeIMP/\~/changes/38/dydx-chain-modules-and-parameters/governance-adjustable-parameters/trading-core): this section covers the core aspects of trading, namely insurance fund and liquidations config. The insurance fund acts as the first backstop to maintain systemic solvency when an account has a negative balance. The liquidations config defines the mechanism to close an account’s position when it falls below the margin requirements.&#x20;
* [**Markets**](https://app.gitbook.com/o/-MeNgGQU0ucT2xo4s8-T/s/cSd7APxHbsYMlFFAeIMP/\~/changes/38/dydx-chain-modules-and-parameters/governance-adjustable-parameters/markets): this section covers the Prices module (x/prices) parameters on dYdX Chain as well as the liquidity tier of each market based on standardized risk parameters.
* [**Perpetual**](https://app.gitbook.com/o/-MeNgGQU0ucT2xo4s8-T/s/cSd7APxHbsYMlFFAeIMP/\~/changes/38/dydx-chain-modules-and-parameters/governance-adjustable-parameters/perpetual): this section covers the Perpetual module (x/perpetuals) parameters on dYdX Chain, such as funding rate and epoch information. The perpetual funding rate enables the perpetual price to align with the underlying asset's price. Epoch information is a fixed interval where funding is credited or debited to each account.
* [**Clob**](https://app.gitbook.com/o/-MeNgGQU0ucT2xo4s8-T/s/cSd7APxHbsYMlFFAeIMP/\~/changes/38/dydx-chain-modules-and-parameters/governance-adjustable-parameters/clob): this section covers the Clob module (x/clob) that configures the order creation, placement, and cancellations on dYdX Chain.&#x20;
* [**Adding & Updating A Live Market**](https://app.gitbook.com/o/-MeNgGQU0ucT2xo4s8-T/s/cSd7APxHbsYMlFFAeIMP/\~/changes/38/dydx-chain-modules-and-parameters/governance-adjustable-parameters/adding-and-updating-a-live-market): this section explains the message required to add a new or update a live market on dYdX Chain.
* [**Safety**](https://app.gitbook.com/o/-MeNgGQU0ucT2xo4s8-T/s/cSd7APxHbsYMlFFAeIMP/\~/changes/38/dydx-chain-modules-and-parameters/governance-adjustable-parameters/safety): this section explains the safety parameters on dYdX Chain, namely the spam mitigation that is related to order creation and cancellation using the Clob module.
* [Market Tiers](https://app.gitbook.com/o/-MeNgGQU0ucT2xo4s8-T/s/cSd7APxHbsYMlFFAeIMP/\~/changes/38/dydx-chain-modules-and-parameters/governance-adjustable-parameters/market-tiers): this section shows the markets that are currently active on dYdX Chain and the liquidity tier that they are classified into, this section is updated regularly.&#x20;

\
