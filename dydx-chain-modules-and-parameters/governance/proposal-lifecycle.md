---
description: An overview of the dYdX Improvement Proposal (“DIP”) lifecycle.
---

# Proposal Lifecycle

## Proposal Stages

Below we outline the flow of dYdX Chain governance, from inception of the idea to the implementation. These processes are subject to change according to feedback from the dYdX community.



## Summary

* [ Forum Discussion](proposal-lifecycle.md#0.-forum-discussion)
* [(Off-chain) DRC Creation](proposal-lifecycle.md#1.-off-chain-drc-creation)
* [(Off-chain) DRC Discussion and Feedback](proposal-lifecycle.md#2.-off-chain-drc-discussion-and-feedback)
* [(Off-chain) DIP Creation](proposal-lifecycle.md#3.-off-chain-dip-creation)
* [(On-chain) Submitting a Proposal](proposal-lifecycle.md#4.-on-chain-submitting-a-proposal)
* [(On-chain) Proposal Deposits](proposal-lifecycle.md#5.-on-chain-proposal-deposits)
* [(On-chain) DIP Voting](proposal-lifecycle.md#6.-on-chain-dip-voting)
* [(On-chain) Proposal Tallying and Execution](proposal-lifecycle.md#7.-on-chain-proposal-tallying-and-execution)



<figure><img src="../../.gitbook/assets/dYdX Improvement Proposal (DIP) Lifecycle.png" alt=""><figcaption></figcaption></figure>



## 0. Forum Discussion&#x20;

Anyone can sign up and set up a thread on any topic on dYdX’s governance forums hosted at[ https://dydx.forum/](https://dydx.forum/). dYdX community members are required to register using an email address or an Ethereum wallet.

## 1. (Off-chain) DRC Creation

dYdX Request for Comments (DRCs) creation is the first step in the governance improvement process. Anyone can participate in the dYdX governance forum, create an off-chain DRC, and discuss potential improvements to the dYdX Chain and/or dYdX ecosystem.

To create a DRC, dYdX community members should use [this template](https://docs.google.com/document/d/1LYK3A7aOVAIyobDJPGn-nSiPoFCz63kmFT6dGF-Ob3E/edit?usp=sharing).&#x20;

The DRC should cover all the information of the potential final DIP.

## 2. (Off-chain) DRC Discussion and Feedback&#x20;

Once posted on the dYdX governance forum, the proposer should make a reasonable effort to respond to questions and incorporate constructive feedback to further improve the DRC. The goal of the DRC Discussion and Feedback step is to establish a rough consensus before a vote starts.

While a rigid timeline is unnecessary, four days likely makes sense to ensure the dYdX community has sufficient time to review and comment on the DRC.

## 3. (Off-chain) DIP Creation&#x20;

Before submitting a transaction to create a governance proposal, the prospective proposer must create a `json` file containing relevant information for the governance proposal. Depending on the type of proposal, the contents of the `json` file will differ.&#x20;

1. Text Proposals: the file should contain title, description and deposit (in aDYDX units).
2. Community Spending Proposals: the file should contain title, description, recipient, number of tokens, and deposit (in `aDYDX` units).
3. Parameter Change Proposals: the file should contain title, description, changes, subspace (module with the parameter that is being changed), key (the parameter that is being changed), value (value of the parameter that will be changed by the governance mechanism), and deposit (in `aDYDX` units).
4. Software Upgrade Proposals: the file should contain title, description, deposit and plan.&#x20;
   * The plan outlines when the update will occur (block height), the name of the new version of the software, and the `UpgradeHandler` which instructs the upgrade module how to carry out the upgrade (the latest consensus version of each module and other software).

As a general rule, any information specific to a proposal (e.g., Title, description, deposit, parameters, recipient) can be placed in a `json` file, while information general to a transaction of any kind (e.g., chain-id, node-id, gas, fees) can remain in the CLI (the command-line interface).

## 4. (On-chain) Submitting a Proposal

An on-chain DIP may be submitted by a dYdX community member using the following generic command format (on the the command-line interface):

```sh
dydxprotocold tx gov submit-proposal <proposal type> \
-- <json file> \
--from <submitter address> \
--deposit <deposit in DYDX> \
--chain-id <chain id> \
--gas <max gas allocated> \
--fees <fees allocated> \
--node <node address> \
```

Here is an example using the above command format to submit a software upgrade proposal:

```sh
dydxprotocold tx gov submit-proposal software-upgrade \ 
--upgrade_plan.json \
--from dydx1vvc9vl6z9pu0vt2y79d0ln8zp6qmpmrhrcnnuy \ 
--deposit 10000000000DYDX \ 
--chain-id dydx-mainnet \ 
--gas 500000 \ 
--fees 200000000000000DYDX \ 
--node https://rpc.dydx.exchange:443 \
```

If `<proposal type>` is left blank, the type will be a Text proposal. Otherwise, it can be set to `param-change`, `software-upgrade`, or `community-treasury-spend`.&#x20;

1. `dydxprotocold` is the command-line interface client that is used to send transactions and query the dYdX Chain and `tx gov submit-proposal software-upgrade` indicates that the transaction is submitting a community pool spend proposal.
2. `--~/upgrade_plan.json` indicates the file containing the plan.
3. `--from dydx1vvc9vl6z9pu0vt2y79d0ln8zp6qmpmrhrcnnuy` is the account key that pays the transaction fee and deposit amount. This account key must exist in the keyring on your device and it must be an address you control.
4. `--deposit` is the number of DYDX&#x20;
5. `--chain-id dydx-mainnet` is dYdX Chain.
6. `--gas 500000` is the maximum amount of gas permitted to be used to process the transaction.
   * The more content there is in the description of your proposal, the more gas your transaction will consume.
   * If this number isn't high enough and there isn't enough gas to process your transaction, the transaction will fail.
   * The transaction will only use the amount of gas needed to process the transaction.
7. `--fees` is a flat-rate incentive for a validator to process your transaction.
   * The network still accepts zero fees, but many nodes will not transmit your transaction to the network without a minimum fee.
   * Many nodes use a minimum fee to disincentivize transaction spamming.
   * 200000000000000DYDX is equal to 0.0002 DYDX.
8. `--node` is \[...]

To submit the proposal on-chain, the proposer will need to deposit a number of DYDX that is equal to or greater than the `min_initial_deposit_ratio`.

## 5. (On-chain) Proposal Deposits&#x20;

As soon as the proposal is created the `max_deposit_period` begins and the `min_deposit` must be satisfied before the `max_deposit_period` concludes for the vote to start.&#x20;

After the proposal is created, any DYDX holder can contribute to the deposit by sending a deposit transaction.&#x20;

1. To contribute to the deposit of a governance proposal, the prospective depositor must know the `proposalID` that they intend to add a deposit to. The prospective depositor can query list of proposals on dYdX Chain by entering this command on the CLI:&#x20;

```sh
dydxprotocold query gov proposals
```

2. Once the prospective depositor knows the ID of the proposal, they can add a deposit using this command:&#x20;

```sh
dydxprotocold tx gov deposit <proposal-id> <deposit> --from <key>
```

If a proposal fails to satisfy the `min_deposit` within the `max_deposit_period` and the `burn_proposal_deposit_prevote` parameter is set “False”, any DYDX holder who contributed to the respective deposit of a proposal will have their deposit refunded.&#x20;

If the `min_deposit` is satisfied within the `max_deposit_period`, the vote will start and the deposit is kept in escrow and held by the governance `ModuleAccount` until the proposal is finalized (passed or rejected). Depositors of a proposal will have their deposit refunded, unless enough voters vote `NoWithVeto` and satisfy the `veto_threshold`.

## 6. (On-chain) DIP Voting

If the `min_deposit` is satisfied within the `max_deposit_period`, the vote will start and voting will last for the `voting_period`.

Note, only staked DYDX tokens can vote on dYdX Chain governance proposals.&#x20;

1. To cast a vote, the prospective voter must know the `proposalID` that they intend to vote on. The prospective voter can query the list of proposals on dYdX Chain by entering this command on the CLI:

```
dydxprotocold query gov proposals
```

2. If the prospective voter would like to know more details about the proposal, they can query it by entering this command on the CLI:

```sh
dydxprotocold query gov proposal <proposal-id>
```

3. Once the prospective voter understands the subject matter being voted on and has formed an opinion about it, the prospective voter can cast a vote by entering this command on the CLI:

```sh
dydxprotocold tx gov vote <proposal-id> <option> --from <key>
```

During the voting period, the prospective voter may select a vote of either `Yes`, `No`, `Abstain`, or `NoWithVeto`. The prospective voter may change their vote at any time before the voting period ends.&#x20;

If a DYDX staker does not vote on a proposal, they will inherit the vote of their validator for the respective proposal.

## 7. (On-chain) Proposal Tallying and Execution

When the `voting_period` ends, the `TallyParams` (`quorum`, `threshold`, and `veto_threshold`) determine whether the proposal is approved and implemented or rejected.&#x20;

The execution process according to the respective vote type is as follows:&#x20;

* Text Proposals: will not result in any on-chain changes, but could result in an off-chain action.&#x20;
* Community Spending Proposals: the number of DYDX encoded in the proposal will be transferred from the from the dYdX community account to the address encoded in the proposal.
* Parameter Change Proposals: the parameter will update go into effect without a hard fork.
* Software Upgrade Proposals:&#x20;
  * Signal - Validators upgrade their software to the new version and signal that they are ready for the upgrade.
  * Block Height: The dYdX Chain reaches the specified block height for the upgrade and pauses its operation.
  * Upgrade and Restart: Validators apply the upgrade and restart their nodes, which resumes the blockchain's operation with the new software.

\


\


\
\


\


\
