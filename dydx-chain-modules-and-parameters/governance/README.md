---
description: An overview of the governance module.
---

# 🏛️ Governance

## Overview

dYdX Chain is a proof-of-stake blockchain network and holders of DYDX can participate in governing the dYdX Chain. dYdX Chain uses the standard [x/gov module](https://docs.cosmos.network/main/build/modules/gov) in the Cosmos SDK.

The governance module empowers DYDX holders to propose and vote on proposals, directly influencing the evolution of the dYdX Chain through a democratic process. The subject matter of proposals can vary from changing a governable parameter on the dYdX Chain, spending dYdX community funds, and updating the software that dYdX Chain nodes are running, among other things.

## Summary&#x20;

* [Proposal Submission and Deposits](./#proposal-submission-and-deposits)
* [Proposal Types](./#proposal-types)
  * [Text Proposals](./#text-proposals)
  * [Community Spending Proposals](./#community-spending-proposals)
  * [Parameter Change Proposals](./#parameter-change-proposals)
  * [Software Upgrade Proposals](./#software-upgrade-proposals)
  * [New Market Proposals](./#new-market-proposals)
* [Proposal Voting Options](./#proposal-voting-options)

## Key Concepts and Definitions

* Deposits: Unstaked DYDX tokens pledged by the proposer and potentially other DYDX holders in support of the creation of a governance proposal.&#x20;
* Inheritance: If a DYDX staker does not vote on a proposal, they will inherit the vote of their validator for the respective proposal.
* Vote Weight: A DYDX holder's vote weight is equal to the amount of DYDX the user has actively staked (1-1). DYDX tokens that are not staked or are in the unbonding period will not count towards a DYDX holder's vote weight.
* Tallying: After the voting period concludes, the [TallyParams](https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2878-L2880) aggregate the vote results to determine if the proposal was accepted or rejected by the dYdX community.&#x20;
* Execution: If a proposal passes, the execution process depends on the type of proposal.

{% embed url="https://docs.cosmos.network/v0.46/modules/gov/" %}

## Parameters

These parameters may be adjusted by the dYdX Community with an on-chain governance proposal.



<table><thead><tr><th width="256.3333333333333">Title </th><th width="262">Value </th><th>Description</th></tr></thead><tbody><tr><td>DepositParams</td><td></td><td>The parameters for deposits on governance proposals.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2870"><code>min_deposit</code></a></td><td><p>2000000000000000000000 adydx</p><p><br></p><p>2,000 DYDX</p><p><br></p></td><td><p>The minimum token deposit for a governance proposal to enter the voting period.</p><p><br></p></td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2876"><code>max_deposit_period</code></a></td><td><p>604800s</p><p><br></p><p>7 days</p><p><br></p></td><td>The maximum time permitted for DYDX holders to deposit enough DYDX tokens to satisfy the <code>min_deposit</code> for a governance proposal to enter the voting period.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2881"><code>min_initial_deposit_ratio</code></a></td><td>0.20000</td><td>The percentage of the <code>min_deposit</code> that needs to be submitted by the address that creates the proposal.</td></tr><tr><td>VotingParams</td><td></td><td>The parameter for vote length of governance proposals.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2877"><code>voting_period</code></a></td><td><p>345600s</p><p><br></p><p>~4 days</p><p><br></p></td><td>The duration of the voting period.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2878"><code>quorum</code></a></td><td>0.33400</td><td>The parameters for tallying votes on governance proposals.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2879"><code>threshold</code></a></td><td>0.50000</td><td><p>The minimum proportion of <code>Yes</code> votes for a proposal to pass. </p><p><br>*<code>Abstain</code> votes are not counted.</p></td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2880"><code>veto_threshold</code></a></td><td>0.33400</td><td>The minimum percentage of <code>NoWithVeto</code> votes required to reject a proposal, regardless of the number of <code>Yes</code> votes.</td></tr><tr><td>BurnableParams</td><td></td><td>The parameters for burning or returning a proposal deposit to depositors.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2884"><code>burn_vote_veto</code></a></td><td>True</td><td>If <code>True</code>, this boolean parameter will burn the proposal deposit for any proposals that are vetoed.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2882"><code>burn_vote_quorum</code></a></td><td>False</td><td>If <code>True</code>, this boolean parameter will burn the proposal deposit if the proposal vote does not reach <code>quorum</code>.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2883"><code>burn_proposal_deposit_prevote</code></a></td><td>False</td><td>If <code>True</code>, this boolean parameter will burn the proposal deposit if the proposal does not enter the voting period.</td></tr></tbody></table>

##

<figure><img src="../../.gitbook/assets/dYdX Chain Governance Deposits and Voting_v9.png" alt=""><figcaption></figcaption></figure>

## Proposal Submission and Deposits

All DYDX holders have the right to create a proposal. A DYDX holder can only use unstaked DYDX tokens to contribute to a given proposal deposit.&#x20;

To create a proposal, a DYDX holder needs to send a `msgsubmitproposal` transaction and satisfy the `min_initial_deposit_ratio` parameter by sending a `deposit` transaction.&#x20;

After the proposal is created, any DYDX holder can contribute to the deposit by sending a `deposit` transaction.&#x20;

For the voting period to start, the `min_deposit` parameter needs to be satisfied within the `max_deposit_period`. Note, (1) the proposal is in an `inactive proposal queue` until the `min_deposit` is satisfied and (2) the `voting_period` will start as soon as the `min_deposit` is reached.&#x20;

The deposit is kept in escrow and held by the governance `ModuleAccount` until the proposal is finalized (passed or rejected).

If a proposal fails to satisfy the `min_deposit` within the `max_deposit_period` and the `burn_proposal_deposit_prevote` parameter is set “`False`”, any DYDX holder who contributed to the respective deposit of a proposal will have their deposit refunded.&#x20;

## Proposal Types

Governance of the dYdX Chain includes 5 distinct types of proposals: text proposals, parameter change proposals, community spending proposals, software upgrade proposals, and new market proposals.&#x20;

### _Text Proposals_

Text proposals are votes that occur on-chain without directly triggering any changes on the dYdX Chain. Text proposals can be used (1) to establish dYdX community consensus for an off-chain matter, such as a strategic plan, a dYdX DAO action, or a dYdX DAO commitment, or (2) as signalling for a future vote that will directly cause changes on the dYdX Chain.

### _Community Spending Proposals_

Community Spending Proposals involve a request to spend DYDX from the community treasury, community pool, or any other community-controlled account. The inputs for a Community Spending Proposal are (1) the number of DYDX and (2) the recipient address.

### _Parameter Change Proposals_

Parameter change proposals are for changing one or more of the dYdX Chain parameters that are controlled by the governance module.&#x20;

If a parameter change proposal is successful, the parameter change takes effect in the block after the voting period ends.

### _Software Upgrade Proposals_

The [upgrade module](https://docs.cosmos.network/main/build/modules/upgrade) facilitates smoothly upgrading a live Cosmos chain to a new (breaking) software version. Software Upgrade Proposals need to be created with a `plan`. Such a plan outlines when the update will occur (`block height`), the name of the new version of the software, and the `UpgradeHandler` which instructs the upgrade module on how to carry out the upgrade (the latest consensus version of each module and other software).

After the dYdX community accepts a software upgrade proposal there are two important steps:

* Signal - After a `SoftwareUpgradeProposal` is accepted, validators are expected to download and install the new version of the software while continuing to run the previous version. Once a validator has downloaded and installed the upgrade, it will start signaling to the network that it is ready to switch by including the proposal's `proposalID` in its precommits.&#x20;
* Switch - Once a block contains more than 2/3rd precommits where a common `SoftwareUpgradeProposal` is signaled, all the nodes (including validator nodes and full nodes) are expected to switch to the new version of the software.

### _New Market Proposals_

Any dYdX Community member can propose to add a new market pair to dYdX Chain through the following ways:

* [Market listing widget](https://dydx.trade/#/markets/new): users can search or choose from a list of markets they would like to add, using this tool would require a wallet containing at least 2,000 unstaked DYDX to be used as a proposal deposit. dYdX Trading Inc. ("dYdX Trading") maintains an open-sourced list of market parameters. Information on methodologies and how the compatibility of markets with the software is determined can be found [here](https://docs.dydx.exchange/governance/proposing\_a\_new\_market#example-of-markets-with-robust-oracle-sources).
* [Programmatic proposal submission](https://docs.dydx.trade/governance/proposing\_a\_new\_market): users can submit a new market proposal through the Command Line Interface, the markets proposed this way are not limited to the markets listed in the widget above, although users are encouraged to adhere to the parameters set out in the documentation. Submitting a new market proposal this way would require a minimum deposit of 400 unstaked DYDX, and the proposal would only enter the voting period when the deposit reaches 2,000 DYDX.

## Proposal Voting Options

The voting options for governance proposals on dYdX Chain are:&#x20;

* `Yes`
* `No`
* `NoWithVeto` - allows voters to express strong disagreement with a proposal to the extent that if burn\_vote\_veto is “True” and the veto\_threshold is reached the respective deposit in the governance module account for the proposal is burned.&#x20;
* `Abstain` - allows voters to signal that they do not intend to vote in favor or against the proposal but accept the result of the vote.\
