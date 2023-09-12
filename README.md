---
description: Overview of the potential migration of DYDX from Ethereum to the dYdX Chain.
---

# Introduction

<figure><img src=".gitbook/assets/Potential Migration (1).png" alt=""><figcaption></figcaption></figure>

The dYdX ecosystem is rapidly approaching the potential mainnet release of the [dYdX v4 open-source software – the “dYdX Chain”](https://dydx.exchange/blog/dydx-chain). The dYdX Chain will be a proof-of-stake blockchain network and, as such, if and when deployed on mainnet, it will require a Layer 1 (“L1”) protocol token for staking to validators in order to secure the chain and for stakers of the L1 token to [govern](https://dydx.exchange/blog/v4-deep-dive-governance) the network.

The dYdX community could elect to use Ethereum-based [DYDX](https://etherscan.io/token/0x92D6C1e31e14520e676a687F0a93788B716BEff5), the governance token of dYdX v3, as the L1 token of the dYdX Chain (if and when deployed after the mainnet release). If such an election were to materialize, given that DYDX is an Ethereum-based ERC-20 token, the DYDX token would need to be migrated from Ethereum to the dYdX Chain.

On August 2, 2023, the dYdX Foundation published [Exploring the Future of DYDX: A Take on the Potential Migration of DYDX from Ethereum to the dYdX Chain](https://dydx.foundation/blog/exploring-the-future-of-dydx) ("Exploring the Future of DYDX"), and on September 12, 2023, the dYdX Foundation published an [Update on the Potential Migration of DYDX from Ethereum to the dYdX Chain](https://dydx.foundation/blog/update-on-exploring-the-future-of-dydx).

In those posts, the dYdX Foundation presented that in furtherance of its mission to support and promote the dYdX ecosystem by enabling communities, developers, and decentralized governance, the dYdX Foundation commissioned:

1. The development of an [Ethereum smart contract](migration-of-dydx-from-ethereum-to-dydx-chain/wethdydx-smart-contract.md) (the “`wethDYDX Smart Contract`”) that, if deployed, would enable a permissionless and autonomous one-way bridge for the `DYDX` token to be migrated from Ethereum to the dYdX Chain,&#x20;
2. The development of a [`GovernanceStrategyV2`](migration-of-dydx-from-ethereum-to-dydx-chain/governancestrategyv2-smart-contract.md) smart contract (the “`GovernanceStrategyV2 Smart Contract`”) that, if deployed and if the dYdX community decided through dYdX governance, could enable the wrapped version of the Ethereum-based DYDX token (“`wethDYDX`”) to have the same governance and utility function as Ethereum-based DYDX (hereinafter “`ethDYDX`”) in dYdX v3,&#x20;
3. The development of a [TreasuryBridge smart contract](migration-of-dydx-from-ethereum-to-dydx-chain/treasurybridge-smart-contract/) (the “`TreasuryBridge Smart Contract`”) that, if deployed and if the dYdX community decided through dYdX governance, could (i) burn newly vested `ethDYDX` from the community treasury vester and the rewards treasury vester and (ii) enable `ethDYDX` vested in the Community Treasury and Rewards Treasury to be migrated to the dYdX Chain, and
4. The development of source code that will be open-sourced such that others may use it to implement a [user interface](migration-of-dydx-from-ethereum-to-dydx-chain/open-source-bridge-user-interface.md) (also sometimes referred to as a “front-end”) to interact with such `wethDYDX` Smart Contract (the “`User Interface Code`”).
