---
description: Overview of the GovernanceStrategyV2 Smart Contract
---

# GovernanceStrategyV2 Smart Contract

<figure><img src="../.gitbook/assets/GovernanceStrategyV2 Smart Contract.png" alt=""><figcaption></figcaption></figure>

## Resources

* [Github GovernanceStrategyV2 Smart Contract](https://github.com/dydxfoundation/governance-contracts/blob/master/contracts/governance/strategy/GovernanceStrategyV2.sol)
* [Peckshield Audit Report](https://github.com/dydxfoundation/governance-contracts/blob/master/audits/PeckShield-Audit-Report-dYdX-Bridge-v1.1.pdf)&#x20;

## Voting & Proposal Power&#x20;

Currently, the dYdX [`GovernanceStrategy Smart` Contract](https://github.com/dydxfoundation/governance-contracts/blob/master/contracts/governance/GovernanceStrategy.sol) determines the proposal and voting power of each individual address at a specific block number. This contract weighs the proposal and voting power from both ethDYDX as well as StkDYDX tokens equally. In addition to being considered for on-chain voting, this contract is also used by Snapshot to determine a given user's voting power and/or proposal power for off-chain voting.

## `GovernanceStrategyV2 Smart contract`

An updated `GovernanceStrategy Smart Contract`, `GovernanceStrategyV2 Smart Contract,`has been created and if deployed and if the dYdX community decided through dYdX governance, could replace the original  [`GovernanceStrategy Smart` Contract](https://github.com/dydxfoundation/governance-contracts/blob/master/contracts/governance/GovernanceStrategy.sol). The `GovernanceStrategyV2 Smart Contract` is essentially the same as the current corresponding contract with added support for the `wethDYDX` token address, which will be treated equivalently to the `ethDYDX` and `stkDYDX`. The `GovernanceStrategyV2 Smart Contract` has minimal changes compared to the original contract.&#x20;

Note, `wethDYDX` would be treated the same as `ethDYDX` and `stkDYDX` in both on-chain and off-chain governance proposals.

Also note, if the dYdX community decides to update the `GovernanceStrategy Smart Contract` to the `GovernanceStrategyV2 Smart Contract` through dYdX governance, the subject matter would fall under the  [**Long Timelock Executor**](https://docs.dydx.community/dydx-governance/voting-and-governance/governance-process#long-timelock-executor)**.**

