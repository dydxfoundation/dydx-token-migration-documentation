---
description: An overview of the slashing module.
---

# Slashing

## Overview

The slashing module is a mechanism to penalize validators for a violation of protocol rules by slashing their bonded tokens. Penalties under the slashing module include burning a portion of a validator’s bonded tokens and/or temporarily removing their ability to vote on future blocks.

## Summary

* [Signing Info](slashing.md#signing-info)
* [Liveness Tracking](slashing.md#liveness-tracking)
* [Messages](slashing.md#messages)
* [Social Slashing](slashing.md#social-slashing)

## Key Concepts and Definitions

* States: In the state machine, a variable number of validators are registered, and during each block, the top `max_validators` (defined in the [Staking module](staking/)) who are not jailed become bonded and can propose and vote on blocks, with a `ValidatorSigningInfo` record tracking their liveness and potential protocol faults.
* Double Signing: When a validator is proven to have signed two blocks at the same height, causing conflicting blocks or transactions on multiple branches of the dYdX Chain.
* Downtime: When a validator does not vote on a dYdX Chain block for a period of time.
* Jailed: A period of time when a validator is not allowed to rejoin the Active Set due to a violation of protocol rules.
* [Staking Tombstone](https://github.com/cosmos/cosmos-sdk/blob/6afece635cef9f8e044a04ce67d06e55ca300249/x/evidence/keeper/infraction.go#L27): When a validator is permanently removed from the Active Set due to a double signing infraction. More information about Staking Tombstone is available [here](https://docs.cosmos.network/v0.45/modules/slashing/07\_tombstone.html).

More information about the slashing module is available [here](https://docs.cosmos.network/main/build/modules/slashing).

## Parameters

These parameters may be adjusted by the dYdX Community with an on-chain governance proposal.

<table data-header-hidden><thead><tr><th width="258.3333333333333"></th><th width="212"></th><th></th></tr></thead><tbody><tr><td>Title</td><td>Value</td><td>Definition</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L3766">signed_blocks_window</a></td><td><p>8192</p><p><br></p><p>~ 3 hours 11 minutes</p><p>(assuming 1.4s block time)</p></td><td><p>The window in terms of the number of blocks for which a validator's signing activity is monitored.</p><p><br><br></p></td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L3767">min_signed_per_window</a></td><td>0.2</td><td>The minimum of blocks in the <code>signed_blocks_window</code> that a validator must sign to avoid being jailed.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L3768">downtime_jail_duration</a></td><td><p>7200s</p><p><br></p><p>2 hours</p></td><td>The length of time a validator is temporarily removed from the Active Set.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L3769">slash_fraction_double_sign</a></td><td>0.0</td><td>The fraction of a validator's staked tokens that will be slashed in the event of a double signing violation.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L3770">slash_fraction_downtime</a></td><td>0.0</td><td>The fraction a validator will be slashed by if they miss a fraction (<code>min_signed_per_window</code>) of blocks within a sliding window (<code>signed_blocks_window</code>).</td></tr></tbody></table>

## Signing Info

In every block, validators contribute to a set of precommits for the previous block, forming the `LastCommitInfo` in CometBFT. This `LastCommitInfo` is valid if it includes precommits from +2/3 of the total voting power.

If a validator fails to be included in the `LastCommitInfo` for a certain number of blocks, they will be automatically jailed, slashed or unbonded.

## Liveness Tracking

dYdX Chain stores Information about validator's liveness activity on `ValidatorSigningInfo`. At the start of each block, the `ValidatorSigningInfo` for each validator is updated, and their liveness status over `signed_blocks_window` is checked.

The sliding window is defined by `signed_blocks_window` and the index is determined by the `IndexOffset` in each validator’s `ValidatorSigningInfo`. The `IndexOffset` is incremented with each block whether the validator signed or not, and the `MissedBlocksBitArray` and `MissedBlocksCounter` are updated accordingly once the index is determined.&#x20;

To make sure whether a validator falls below the liveness threshold, the maximum number of blocks missed (`maxMissed`) and minimum height of liveness threshold (`minHeight`) are retrieved.

```
maxMissed = signed_blocks_window - min_signed_per_window * signed_blocks_window
```

If the current block is past `minHeight` and the `MissedBlocksCounter` exceeds `maxMissed`, the validator is slashed by `slash_fraction_downtime`, jailed for `downtime_jail_duration`, and has their `MissedBlocksBitArray`, `MissedBlocksCounter`, and `IndexOffset` reset.

Note, slashing due to liveness tracking failure does not lead to tombstoning.

## Messages

* Unjail

Should a validator want to return and potentially rejoin the Active Set after being removed due to Downtime, they must send a `MsgUnjail`.

```batch
message MsgUnjail {
string validator_addr = 1;
}
```

## Social Slashing

The extraction of MEV (Maximal Extractable Value) by validators can undermine a fair and transparent trading environment. MEV refers to the profit a dishonest validator can gain by censoring and/or re-ordering orders and cancellations to their advantage. Validators could take advanatge of the architecture of the dYdX Chain - an in-memory orderbook design - to manipulate, re-order, or censor trades before suggesting a new block for profit extraction, resulting in trades executing at worse prices relative to the best price possible and cancellations potentially being ignored.&#x20;

To show how much MEV value could be extracted by each validator, dYdX Trading, Inc. ("dYdX Trading") and Skip Protocol have collaborated to create a [dashboard](https://dydx.skip.money/) that displays data on orderbook discrepancies.

Currently, there is no protocol level solution to mitigate MEV on dYdX Chain, despite MEV extraction being considered a harmful validator behavior. However, the dYdX community through a governance vote could approve the implementation of a social slashing framework to penalize validators engaged in MEV extraction.

\
