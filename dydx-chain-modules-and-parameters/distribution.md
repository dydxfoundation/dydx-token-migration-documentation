---
description: An overview of the Distribution Module.
---

# Distribution

## Overview

The distribution module enables a simple collection and distribution mechanism to passively distribute rewards between validators and delegators.

## Summary

* [Staking Rewards](distribution.md#staking-rewards)
* [How rewards are distributed on dYdX Chain](distribution.md#how-rewards-are-distributed-on-dydx-chain)
* [How staking rewards are calculated](distribution.md#how-staking-rewards-are-calculated)

## Key Concepts and Definitions

* Community Pool: a pool of tokens funded by a portion of staking rewards (`community_tax`) that the dYdX community could use to fund contributor grants, community initiatives, liquidity mining, and other initiatives.&#x20;
* Distribution `ModuleAccount` Account: an account that collects and distributes trading and transaction fees among validators, delegators, and the community pool. &#x20;
* Staking Rewards: the total portion of the Fee Pool that a DYDX staker can claim at a given block.
* Fee Pool: fee pool from maker trading fees (USDC), taker trading fees (USDC), DYDX denominated gas fees from transactions, and USDC denominated gas fees from transactions for a given block.
* Staking Rewards Withdrawal: each block a DYDX staker may claim their portion of Fee Pool. If a DYDX staker does not claim staking rewards, their respective rewards will accrue in the Distribution `ModuleAccount` Account.
* Total Bonded Power: the sum of all tokens that are currently staked by validators to themselves and tokens staked to validators by DYDX holders.&#x20;
* Block Rewards: fees distributed to validators and delegators for successfully proposing and validating a new block on the blockchain.

More information about the distribution module is available [here](https://docs.cosmos.network/main/build/modules/distribution).

## Parameters

These parameters may be adjusted by the dYdX Community with an on-chain governance proposal.

<table><thead><tr><th width="277.3333333333333">Title </th><th width="170">Value </th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/dydxopsdao/networks/pull/39/commits/8915a65da04932dfdedea255feadd6b380c94865#diff-74b06241cbb20c39839cc9341cc4cb5ed24a9f290cc61435d29094f9af70afe3R1142"><code>community_tax</code></a></td><td>0</td><td>A tax that directs a percentage of the fee pool to the community pool.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/pull/39/commits/8915a65da04932dfdedea255feadd6b380c94865#diff-74b06241cbb20c39839cc9341cc4cb5ed24a9f290cc61435d29094f9af70afe3R1143"><code>base_proposer_reward</code></a></td><td>0</td><td>Part of the block reward reserved for the validator that proposes a given block.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/pull/39/commits/8915a65da04932dfdedea255feadd6b380c94865#diff-74b06241cbb20c39839cc9341cc4cb5ed24a9f290cc61435d29094f9af70afe3R1144"><code>bonus_proposer_reward</code></a></td><td>0</td><td>Bonus incentive for block proposers based on the number of transactions included in a given block.</td></tr><tr><td><a href="http://withdraw_addr_enabled"><code>withdraw_addr_enabled</code></a></td><td>True</td><td>Whether a delegator can set a different withdrawal address (other than their delegator address) for their rewards.</td></tr></tbody></table>

## Staking Rewards

<figure><img src="../.gitbook/assets/Staking_Rewards_on_dYdX_Chain_v5 (1).png" alt=""><figcaption></figcaption></figure>

On the dYdX Chain, all transaction fees (trading fees denominated in USDC, DYDX denominated gas fees from transactions, and USDC denominated gas fees from transactions) collected by the protocol will be distributed to validators and DYDX holders that stake to dYdX Chain validators.&#x20;

The Cosmos [x/distribution module](https://docs.cosmos.network/main/modules/distribution) is a simple mechanism to allocate rewards earned by Validators and Stakers. For a detailed understanding of the Cosmos rewards mechanism, read [here](https://github.com/cosmos/cosmos-sdk/blob/main/docs/spec/fee\_distribution/f1\_fee\_distr.pdf).&#x20;

## How rewards are distributed on dYdX Chain

<figure><img src="../.gitbook/assets/Fee_Distribution_on_dYdX_Chain_v6 (1).png" alt=""><figcaption></figcaption></figure>

DYDX holders who stake to (a) validator(s) are entitled to a portion of the following fees:&#x20;

* DYDX denominated gas fees from transactions,
* USDC denominated gas fees from transactions,
* USDC maker trading fees, and &#x20;
* USDC taker trading fees.

Fees will accrue in the `Distribution ModuleAccount Account` each block. Each block a DYDX staker may claim their portion of Staking Rewards. If a DYDX staker does not claim Staking Rewards, their respective rewards will accrue in the distribution ModuleAccount account.&#x20;

Note, Staking Rewards are not automatically staked to a dYdX Chain validator. Any DYDX earned by a staker as Staking Rewards will need to be claimed from the `Distribution ModuleAccount Account` and staked to a dYdX Chain validator to contribute to the security of the network and qualify to earn staking rewards.

## How staking rewards are calculated

<figure><img src="../.gitbook/assets/Staking Rewards Formula.png" alt=""><figcaption></figcaption></figure>

* Fee Pool = fee pool from maker trading fees (USDC), taker trading fees (USDC), DYDX denominated gas fees from transactions, and USDC denominated gas fees from transactions for a given block.
* Number of DYDX staked by DYDX holder = total DYDX tokens that a dYdX Chain address has staked to (a) validator(s) at a given block. &#x20;
* Total bonded power = the sum of all DYDX that are currently staked by validators to themselves and DYDX staked to validators by DYDX holders.
* Staking Rewards  = the total portion of the Fee Pool that a DYDX staker can claim at a given block.
* Community tax = A tax that directs a percentage of the fee pool to the community pool.
* Validator commission rate = commission set by each validator and applied to the staking rewards of each delegator. Validators are required to follow the `min_commission_rate` parameter, but are otherwise free to set their own commission rates.
