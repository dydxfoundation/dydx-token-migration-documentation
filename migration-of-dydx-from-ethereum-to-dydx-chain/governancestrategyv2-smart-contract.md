---
description: Overview of the GovernanceStrategyV2 Smart Contract
---

# GovernanceStrategyV2 Smart Contract

<figure><img src="../.gitbook/assets/GovernanceStrategyV2 Smart Contract.png" alt=""><figcaption></figcaption></figure>

On September 24, 2023, the dYdX community almost unanimously [supported](https://dydx.community/dashboard/proposal/15) upgrading the GovernanceStrategy Smart Contract to `v2`. This upgrade ratified the implementation of wethDYDX into dYdX v3’s governance system so that wethDYDX has the same voting and proposal power as ethDYDX.&#x20;

## Resources

* [Github GovernanceStrategyV2 Smart Contract](https://github.com/dydxfoundation/governance-contracts/blob/master/contracts/governance/strategy/GovernanceStrategyV2.sol)
* [Peckshield Audit Report](https://github.com/dydxfoundation/governance-contracts/blob/master/audits/PeckShield-Audit-Report-dYdX-Bridge-v1.1.pdf)&#x20;

## Voting & Proposal Power&#x20;

The dYdX [`GovernanceStrategy Smart` Contract](https://github.com/dydxfoundation/governance-contracts/blob/master/contracts/governance/GovernanceStrategy.sol) and the [GovernanceStrategyV2 Smart Contract](https://github.com/dydxfoundation/governance-contracts/blob/master/contracts/governance/strategy/GovernanceStrategyV2.sol) determine the proposal and voting power of each individual address at a specific block number. This [GovernanceStrategyV2 Smart Contract](https://github.com/dydxfoundation/governance-contracts/blob/master/contracts/governance/strategy/GovernanceStrategyV2.sol) weighs the proposal and voting power from ethDYDX, stkDYDX and wethDYDX tokens equally. In addition to being considered for on-chain voting, this contract is also used by Snapshot to determine a given user's voting power and/or proposal power for off-chain voting.

## `GovernanceStrategyV2 Smart contract`

The [`GovernanceStrategyV2 Smart Contract`](https://github.com/dydxfoundation/governance-contracts/blob/master/contracts/governance/strategy/GovernanceStrategyV2.sol) is essentially the same as the  [`GovernanceStrategy Smart` Contract](https://github.com/dydxfoundation/governance-contracts/blob/master/contracts/governance/GovernanceStrategy.sol) with added support for the `wethDYDX` token address, which is treated equivalently to the `ethDYDX` and `stkDYDX`. The `GovernanceStrategyV2 Smart Contract` has minimal changes compared to the original contract.&#x20;

Note, `wethDYDX` would be treated the same as `ethDYDX` and `stkDYDX` in both on-chain and off-chain governance proposals.

