---
description: An overview of migration of DYDX from Ethereum to the dYdX Chain.
---

# 🧱 Migration & Bridge Overview

<figure><img src="../../.gitbook/assets/Migration &#x26; Bridge Overview.png" alt=""><figcaption></figcaption></figure>

## Disclaimer

**The DYDX token is entirely controlled by the dYdX community, and it was ultimately up to the dYdX community to decide, through** [**dYdX governance**](https://dydx.community/dashboard/proposal/15) **that DYDX should be the L1 protocol token of the dYdX Chain and how to effect any required token migration and/or any other necessary actions, as well as any other matters that affect or relate to the ethDYDX token or dYdX v3 Governance.**

**The dYdX Foundation urges the dYdX ecosystem, community members, and the general public to remain vigilant as we anticipate an increase in potential scams and phishing attacks via social media, messaging apps, and websites. Phishing is a common way for scammers to target internet users. Scammers may reach out to you on social media platforms pretending to be representing dYdX or affiliated with dYdX.**&#x20;

## Context

On August 3, 2021, dYdX Foundation [launched](https://dydx.foundation/blog/introducing-dydx-token) DYDX (hereinafter "`ethDYDX`"), a governance token that allows the dYdX community to govern certain aspects of the dYdX Layer 2 protocol on Ethereum (“dYdX v3”) to align incentives between traders, liquidity providers, and partners. The `ethDYDX` token enables a robust ecosystem around governance, rewards, and staking - each of which is designed to drive future growth and decentralization of dYdX v3.

On October 26, 2023, the [dYdX Chain open source software](https://dydx.exchange/blog/dydx-chain-official-release) was deployed and the first block of the dYdX Chain was created by the dYdX Chain validators.

The dYdX Chain is a proof-of-stake blockchain network built using the Cosmos SDK and leveraging CometBFT for consensus.&#x20;

The dYdX community, through dYdX governance, voted ([Snapshot](https://snapshot.org/#/dydxgov.eth/proposal/0x17026e18317dc29fe745d3130246a83b1485612da9c97e7261e8f659cf33663c) and [on-chain](https://dydx.community/dashboard/proposal/15)) in favor of adopting DYDX as the Layer 1 token of the dYdX Chain for staking to validators in order to secure the chain and for stakers of the L1 token to [govern](https://dydx.exchange/blog/v4-deep-dive-governance) the network.

When interacted with, the one-way bridge smart contract, the `wethDYDX Smart Contract,`  would carry out the following functions in a fully permissionless and automated manner:

1. Receive and permanently lock the `ethDYDX` tokens sent by the user to the `wethDYDX Smart Contract`,&#x20;
2. Send `wethDYDX` to the user on a 1-1 proportion basis on Ethereum, and
3. dYdX Chain validators can also read and ingest the information in the `wethDYDX Smart Contract` such that corresponding DYDX can be distributed to users by validators on the dYdX Chain once there is confirmation that Step 1 above is complete and the respective `ethDYDX` is permanently locked in the `wethDYDX Smart Contract`.
