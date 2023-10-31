---
description: An overview of the Staking Module.
---

# Staking&#x20;

## Overview

dYdX Chain leverages the Cosmos SDK Staking module which supports a Proof-of-Stake blockchain and enables DYDX holders to become validators and/or delegate the validation rights (stake) of their DYDX to a dYdX Chain validator.

## Summary

* [Staking to a dYdX Chain Validator](./#staking-to-a-dydx-chain-validator)
* [Unbonding delegations / Unstaking](./#unbonding-delegations-unstaking)
* [Redelegation](./#redelegation)

## Key Concepts and Definitions

* Staking: the act of delegating and locking up (‘bonding’) DYDX tokens to a dYdX Chain validator to secure and govern the network.
* Bonded Validator: once the validator receives sufficient bonded tokens they automatically join the Active Set during `EndBlock` and their status is updated to Bonded. A bonded validator (1) is signing blocks and receiving rewards (2) can receive further delegations, and (3) can be slashed for misbehavior.
* Active Set: the Active Set represents the validators that can participate in consensus, receive rewards, and secure the dYdX Chain at a given time. The active set includes the top validators according to staked tokens (delegated from third parties and self-delegation) and is determined by the `max _validators` parameter. The Active Set is updated during `EndBlock` by retrieving v`alidatorsbypower` and the `max _validators parameter`.
* EndBlock: A function is called after all transactions in a block have been processed. `Endblock` is generally used to execute logic that should happen after a block is executed to finalize state transitions, such as, determining the active validator set of the dYdX Chain.&#x20;
* Inactive Set: Validators who are not in the Active Set, do not participate in consensus and do not receive rewards.&#x20;
* Unbonded Validator: The validator (1) is not in the Active Set, (2) cannot sign blocks and (3) does not earn rewards, but they can receive delegations. DYDX holders who stake to an unbonded validator will not earn any staking rewards.&#x20;
* Validator Commission: Commission set by each validator and applied to the staking rewards of each delegator. Validators are required to follow the `min_commission_rate` parameter, but are otherwise free to set their own commission rates.

More information about the staking module is available [here](https://docs.cosmos.network/v0.46/modules/staking/).

## Parameters

These parameters may be adjusted by the dYdX Community with an on-chain governance proposal.

<table><thead><tr><th width="261.3333333333333">Title </th><th width="149">Value </th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/dydxopsdao/networks/pull/39/commits/8915a65da04932dfdedea255feadd6b380c94865#diff-74b06241cbb20c39839cc9341cc4cb5ed24a9f290cc61435d29094f9af70afe3R3781"><code>bond_denom</code></a></td><td>adydx</td><td>Denomination of the L1 staking token.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/pull/39/commits/8915a65da04932dfdedea255feadd6b380c94865#diff-74b06241cbb20c39839cc9341cc4cb5ed24a9f290cc61435d29094f9af70afe3R3780"><code>historical_entries</code></a></td><td>10000</td><td>Number of records of a validator's past performance at a given point in time.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/pull/39/commits/8915a65da04932dfdedea255feadd6b380c94865#diff-74b06241cbb20c39839cc9341cc4cb5ed24a9f290cc61435d29094f9af70afe3R3779"><code>max_entries</code></a></td><td>7</td><td>Limit on the number of entries for unbonding delegations or redelegations per staker account for each validator they interact with.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/pull/39/commits/8915a65da04932dfdedea255feadd6b380c94865#diff-74b06241cbb20c39839cc9341cc4cb5ed24a9f290cc61435d29094f9af70afe3R3778"><code>max _validators</code></a></td><td>60</td><td>The maximum number of Validators in the Active Set.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/pull/39/commits/8915a65da04932dfdedea255feadd6b380c94865#diff-74b06241cbb20c39839cc9341cc4cb5ed24a9f290cc61435d29094f9af70afe3R3782">min_commission_rate</a></td><td>0.05</td><td>The chain-wide minimum commission rate that a validator can charge their delegators.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/pull/39/commits/8915a65da04932dfdedea255feadd6b380c94865#diff-74b06241cbb20c39839cc9341cc4cb5ed24a9f290cc61435d29094f9af70afe3R3777"><code>unbonding_time</code></a></td><td><p>2592000s</p><p><br></p><p>~30 days</p></td><td>The time it takes to unbond (full/partial) from a validator.</td></tr></tbody></table>

## Staking to a dYdX Chain Validator

On the dYdX Chain, DYDX holders have the option to serve as validators or to delegate their stake to existing validators. Such delegation increases the likelihood of the chosen validator(s) entering or staying in the active validator set, thereby becoming or maintaining their position as a participant in the network’s consensus process.&#x20;

More information is available in the [How to Stake Guide](how-to-stake-guide.md).

## Unbonding delegations / Unstaking

DYDX holders who stake DYDX to a validator can send a transaction to unstake and remove their tokens (fully or partially) from being staked to a validator. After this transaction is sent, the DYDX tokens enter an unbonding period which lasts for the duration of the [unbonding\_time](https://github.com/dydxopsdao/networks/pull/39/commits/8915a65da04932dfdedea255feadd6b380c94865#diff-74b06241cbb20c39839cc9341cc4cb5ed24a9f290cc61435d29094f9af70afe3R3777) parameter.&#x20;

More information is available in the [How to Stake Guide](how-to-stake-guide.md).

## Redelegation

Redelegation in the Cosmos SDK is a feature that allows a delegator to shift their staked tokens (delegations) from one validator to another without having to wait for the unbonding period.&#x20;

During the redelegation process, the tokens remain staked, meaning they continue to contribute to the network's security and potentially earn rewards for the delegator.

However, a user’s slashing risk with the original validator remains until the unbonding period concludes. For example, a user stakes 20 DYDX to validator A for 59 days, on day 60 the user decides to redelegate their 20 DYDX to validator B. If validator A is slashed between days 60-90, the user is at a risk of having a portion of their 20 staked DYDX slashed. After the 90th day, the slashing risk transitions to validator B.

After redelegating, you must wait 30 days before redelegating again from this new validator.

More information is available in the [How to Redelegate Guide](how-to-redelegate-guide.md).

\


\


\




