---
description: Overview of the wethDYDX Smart Contract
---

# wethDYDX Smart Contract

<figure><img src="../.gitbook/assets/wethDYDX Smart Contract.png" alt=""><figcaption></figcaption></figure>

### Disclaimer

**The `wethDYDX Smart Contract` enables a permissionless and autonomous one-way bridge for the `ethDYDX` token to be migrated from Ethereum to the dYdX Chain. The dYdX Foundation will not provide a user interface or front-end related to access the `wethDYDX Smart Contract`.**

**Neither the dYdX Foundation or any other party will be able to exercise any kind of power over the `wethDYDX Smart Contract`. Consequently, the dYdX Foundation does not make any representations, warranties, or covenants as to the technical properties, performance and will not be responsible for the use made by the people of the `wethDYDX Smart Contract`, including, without limitation, with regard to (i) potential deployments of the `wethDYDX Smart Contract`, (ii) potential adaptations, forks or modified versions of the `wethDYDX Smart Contract`, and its deployment, or (iii) users’ interactions with the `wethDYDX Smart Contract`.**

**Note, users should refrain from interacting with the `wethDYDX Smart Contract` without proper knowledge of how to derive private keys on the dYdX Chain.**

## Resources

* [Github wethDYDX Smart Contract](https://github.com/dydxfoundation/governance-contracts/blob/master/contracts/governance/bridge/WrappedEthereumDydxToken.sol)
* [Peckshield Audit Report ](https://github.com/dydxfoundation/governance-contracts/blob/master/audits/PeckShield-Audit-Report-dYdX-Bridge-v1.1.pdf)

## Overview

When interacted with, the one-way bridge `wethDYDX Smart Contract` would carry out the following functions in a fully permissionless and automated manner:

**Step 1:** Receive and permanently lock the `ethDYDX` tokens sent by the user to the `wethDYDX Smart Contract,`&#x20;

<figure><img src="../.gitbook/assets/Bridging Step 4.png" alt=""><figcaption></figcaption></figure>

**Step 2:** Send `wethDYDX` to the user on a 1-1 proportion basis on Ethereum, and

<figure><img src="../.gitbook/assets/Bridging Step 5.png" alt=""><figcaption></figcaption></figure>

**Step 3:** dYdX Chain validators can also read and ingest the information in the `wethDYDX Smart Contract` such that corresponding DYDX can be distributed to users by validators on the dYdX Chain once there is confirmation that Step 1 above is complete and the ethDYDX is permanently locked in the `wethDYDX Smart Contract`.&#x20;

For users who migrate(d) their `ethDYDX` tokens to the dYdX Chain using the `wethDYDX Smart Contract`referred to in this documentation, the method that users would be credited with DYDX tokens on the dYdX Chain is expected to depend on when they interact with the `wethDYDX Smart Contract`, as follows:

* **Step 3(a):** If a user interacted with the `wethDYDX Smart Contract` before a certain cut-off date prior to the genesis of the dYdX Chain (“Genesis”), the amount of `ethDYDX` tokens sent by the user to the `wethDYDX Smart Contract` was registered as event information in the `wethDYDX Smart Contract`. At this point, the user’s dYdX Chain wallet could not be allocated with DYDX tokens because the dYdX Chain did not exist yet.

<figure><img src="../.gitbook/assets/Bridging Step 3(a) (2).png" alt=""><figcaption></figcaption></figure>

[At Genesis, all accounts (including validator accounts) that interacted with the](https://tutorials.cosmos.network/tutorials/9-path-to-prod/4-genesis.html) `wethDYDX Smart Contract`[ prior to the relevant cut-off time before Genesis were allocated with DYDX tokens on the dYdX Chain by the validators of the network.](https://tutorials.cosmos.network/tutorials/9-path-to-prod/4-genesis.html)

* **Step 3(b):** If a user interacts with the `wethDYDX Smart Contract` (after Genesis), then each dYdX Chain validator participating in the consensus process would read the event information of the `wethDYDX Smart Contract` and allocate DYDX tokens on the dYdX Chain to a given user’s dYdX Chain address based on the corresponding amount (1-1) of `ethDYDX` tokens that the user sent to the `wethDYDX Smart Contract`.&#x20;



<figure><img src="../.gitbook/assets/Bridging Step 3(b) (4).png" alt=""><figcaption></figcaption></figure>

## Contract Design

### `Wrapped Ethereum DYDX (wethDYDX)`

`The wethDYDX` token contract is a new ERC-20 contract that is similar to the`DYDX` token contract with the following specifications:

* A new `bridge()` function that takes `ethDYDX` tokens from the caller and mints them an equivalent amount of `wethDYDX` tokens
  * This function will emit an event log indicating it has occurred
  * **Note, there is no way to reverse the bridge function**
* No transfer or minting restrictions
* Zero `INITIAL_SUPPLY`
* A new
  * `NAME`: Wrapped Ethereum DYDX
  * `SYMBOL: wethDYDX`

#### Transferability and Utility

The `wethDYDX` token is freely transferable like a normal ERC-20 contract.&#x20;

On September 24, 2023, the dYdX community almost unanimously [supported](https://dydx.community/dashboard/proposal/15) upgrading the `GovernanceStrategy Smart Contract` to v2. This upgrade ratified the implementation of wethDYDX into dYdX v3’s governance system so that wethDYDX has the same voting and proposal power as ethDYDX.&#x20;

Similar to `DYDX`, if the market value of `wethDYDX` drops, it may introduce a governance security issue because the `wethDYDX` tokens retain the same voting rights as the `ethDYDX` token.

#### Event Emission

The `wethDYDX Smart Contract` emits an event log in order for the dYdX Chain to understand when a call to `bridge()` has occurred.

Below are some helpful links that describe Ethereum logs:&#x20;

* Event logs on the Ethereum blockchain ([link](https://medium.com/mycrypto/understanding-event-logs-on-the-ethereum-blockchain-f4ae7ba50378))&#x20;
* Deep-dive on `eth_getLogs` RPC call ([link](https://docs.alchemy.com/docs/deep-dive-into-eth\_getlogs))

The following log would be emitted:

```
event Bridge(
  uint256 indexed id,
  uint256 amount,
  address from,
  bytes accAddress,
  bytes data
);
```

The description of each field in the log is as follows:

* `id` is an incrementing number guaranteed to be unique for each log with no gaps.
  * `id` allows anyone to refer to a unique event easily.
  * `id` allows de-duplication of event processing by the v4 chain without requiring additional storage for each unique event. If the chain processes each `eventId` in order, then it can store a single integer of the most recently processed`eventId`.
* `amount` is the amount of `ethDYDX`tokens that was transferred.
* `from` is the Ethereum address the `ethDYDX` tokens were transferred from.
* `accAddress` is the address to which the <mark style="color:purple;">**L1 token of the dYdX Chain**</mark> should be minted. This field is an arbitrary value provided by the caller of the function.
* `data` is additional arbitrary data that the caller provides. This field can be used to signal additional intent. For example, it can be used when migrating funds from a treasury to indicate that the funds should not go to a normal end-user account and instead should be bridged to a module account.

## Locked Tokens Transfer Restrictions

Per the original blog [post](https://dydx.foundation/blog/introducing-dydx-token) introducing `ethDYDX`, 50% of the 1 billion supply of `ethDYDX` was reserved for:

* past investors of dYdX Trading Inc. (27.7%),
* founders, employees, advisors, and consultants of dYdX Trading Inc. and dYdX Foundation (15.3%); and,
* future employees and consultants of dYdX Trading Inc. or dYdX Foundation (7.0%).

Certain `ethDYDX` tokens held by investors and team members are subject to transfer restrictions. Those `ethDYDX` tokens are referred to as locked tokens (the "**Locked Tokens**"). The transfer restriction shall expire pursuant to a schedule that is publicly available and can be viewed [here](https://dydx.foundation/blog/lock-up-extension).&#x20;

Locked Tokens will be released from the transfer restrictions on the same schedule as follows:

* 30% on December 1, 2023 (the “Initial Unlock Date”);
* 40% in equal monthly installments on the first day of each month from January 1, 2024, to June 1, 2024;&#x20;
* 20% in equal monthly installments on the first day of each month from July 1, 2024, to June 1, 2025; and&#x20;
* 10% in equal monthly installments on the first day of each month from July 1, 2025, to June 1, 2026.

All employees and consultants with ethDYDX tokens are also subject to various vesting schedules that could result in them losing their right to receive Locked Tokens.\


#### Bridging & Staking Locked Tokens

Locked Tokens can still be bridged from Ethereum to the dYdX Chain  via the `wethDYDX Smart Contract`, and like all other `ethDYDX` token-holders, the locked ethDYDX token-holders will be entitled to receive:&#x20;

1. `wethDYDX`, on a 1-1 proportional basis, on Ethereum, and&#x20;
2. `DYDX` tokens, on a 1-1 proportional basis, on the dYdX Chain. &#x20;

Any `wethDYDX` and/or dYdX-Chain `DYDX` tokens received in exchange for locked `ethDYDX` tokens shall continue to be subject to the same transfer restrictions and release schedule. As with the current locked `ethDYDX` tokens, locked wethDYDX tokens and locked dYdX-Chain `DYDX` tokens may also be bridged to another blockchain, used for voting or delegating purposes and/or staked to a validator, if applicable.

Any liquid staking tokens (LSTs) received in exchange for locked `ethDYDX`, `wethDYDX` and/or `DYDX` tokens, including, without limitation, `stDYDX` or `stkDYDX`, shall also continue to be subject to the same transfer restrictions and release schedule. As with locked `ethDYDX` tokens, locked `wethDYDX` tokens and locked dYdX-Chain `DYDX` tokens, locked LSTs received when liquid-staking `ethDYDX`, `wethDYDX` and/or `DYDX` tokens may also be bridged to another blockchain, used for voting or delegating purposes and/or staked to a validator, if applicable.\


### Helpful Links:

* [https://dydx.foundation/blog/introducing-dydx-token](https://dydx.foundation/blog/introducing-dydx-token)
* [https://dydx.foundation/blog/lock-up-extension](https://dydx.foundation/blog/lock-up-extension)
* [https://docs.dydx.community/dydx-governance/start-here/dydx-allocations](https://docs.dydx.community/dydx-governance/start-here/dydx-allocations)
* [https://docs.dydx.community/dydx-governance/start-here/dydx-allocations#what-is-the-lockup-for-usddydx-issued-to-investors-existing-and-future-employees-and-consultants](https://docs.dydx.community/dydx-governance/start-here/dydx-allocations#what-is-the-lockup-for-usddydx-issued-to-investors-existing-and-future-employees-and-consultants)
* [https://dydx.foundation/blog/exploring-the-future-of-dydx](https://dydx.foundation/blog/exploring-the-future-of-dydx)
* [https://dydx.community/dashboard/proposal/15](https://dydx.community/dashboard/proposal/15)
* [https://snapshot.org/#/dydxgov.eth/proposal/0x17026e18317dc29fe745d3130246a83b1485612da9c97e7261e8f659cf33663c](https://snapshot.org/#/dydxgov.eth/proposal/0x17026e18317dc29fe745d3130246a83b1485612da9c97e7261e8f659cf33663c)
* [https://dydx.community/dashboard/proposal/15](https://dydx.community/dashboard/proposal/15)
* [https://dydx.forum/t/drc-v4-adoption-dydx-token-migration-to-dydx-chain/970](https://dydx.forum/t/drc-v4-adoption-dydx-token-migration-to-dydx-chain/970)

## FAQ

<details>

<summary>How is accAddress on the dYdX Chain derived?</summary>

Interacting with the `wethDYDX Smart Contract` will involve using an Ethereum private key to generate a mnemonic/master private key and that mnemonic can be used to create accounts across any Cosmos chain.&#x20;

</details>

<details>

<summary>What fees are payable in connection with the token migration (gas fees on either of the two networks and/or other applicable fees)?</summary>

`ethDYDX` holders that are transfering `ethDYDX` to the `wethDYDX Smart Contract` will only need to pay gas fees one time to send ethDYDX to the `wethDYDX Smart Contract` and to receive `wethDYDX`.

</details>

<details>

<summary>Is wethDYDX transferable?</summary>

`wethDYDX` is an ERC-20 token and is freely transferable.

</details>

<details>

<summary>Can wethDYDX be sent to the bridge (<code>wethDYDX Smart Contract)</code> ?</summary>

No. `wethDYDX` can not be sent to the bridge (`wethDYDX Smart Contract)`. Note, there is no way to reverse the bridge function.

</details>

<details>

<summary>Can wethDYDX be staked / sent to the Safety Module?</summary>

Initially, `wethDYDX` cannot be staked to the Safety Module. The Safety Module on dYdX v3 is no longer active as of November 28, 2022. In [DIP 17](https://dydx.community/dashboard/proposal/9), the dYdX community [voted](https://dydx.community/dashboard/proposal/7) to effectively wind down the Safety Module by setting the Safety Module rewards per second to 0. The dYdX community through dYdX Governance on dYdX v3 could upgrade the Safety Module to accept `wethDYDX` as another form of collateral.

</details>
