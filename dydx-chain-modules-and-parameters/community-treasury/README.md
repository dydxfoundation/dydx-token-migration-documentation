---
description: An overview of the dYdX Chain Community Treasury.
---

# 🏦 Community Treasury

## Overview

The [Community Treasury](https://www.mintscan.io/dydx/address/dydx15ztc7xy42tn2ukkc0qjthkucw9ac63pgp70urn) is a community-controlled module account on dYdX Chain. DYDX will vest to the Community Treasury on a continuous basis until August 3, 2026. Any dYdX community member satisfying the [`min_initial_deposit_ratio`](https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2881) can submit a Community Spending proposal to spend DYDX in the Community Treasury.

The Community Treasury was created with the following objectives:

* Fund programs and initiatives that drive the growth of dYdX.
* Develop grant programs to fund community hackathons, analytics dashboards, swag, third-party tools, translations, and other projects.
* Develop a best-in-class governance system and incentivize robust governance.

## Module Accounts

| Name                 | Address                                     |
| -------------------- | ------------------------------------------- |
| `community_treasury` | dydx15ztc7xy42tn2ukkc0qjthkucw9ac63pgp70urn |
| `community_vester`   | dydx1wxje320an3karyc6mjw4zghs300dmrjkwn7xtk |

## Vest Module

<table data-header-hidden><thead><tr><th width="151"></th><th width="424"></th><th width="408"></th><th width="153"></th><th width="169"></th><th width="148"></th><th></th></tr></thead><tbody><tr><td>Field name</td><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L3813">vester_account</a></td><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L3814">treasury_account</a></td><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L3815">denom</a></td><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L3816">start_time</a></td><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L3817">end_time</a></td><td></td></tr><tr><td>Description</td><td>The account to vest tokens from</td><td>The account to vest tokens to</td><td>The token that is vested</td><td>The start time of vesting</td><td>The end time of vesting</td><td></td></tr><tr><td>Value</td><td>community_vester</td><td>community_treasury</td><td>adydx</td><td>2021-08-03T15:00:00Z</td><td>2026-08-03T15:00:00Z</td><td></td></tr><tr><td>Account </td><td>dydx1wxje320an3karyc6mjw4zghs300dmrjkwn7xtk</td><td>dydx15ztc7xy42tn2ukkc0qjthkucw9ac63pgp70urn</td><td></td><td></td><td></td><td></td></tr></tbody></table>

## Community Treasury

Currently, **26.1%** of the total token supply of `ethDYDX`, which amounts to `261,133,225 ethDYDX`, is allocated to the Community Treasury. This allocation is designed to sustainably support contributor grants, community initiatives, liquidity mining, and other assorted programs.&#x20;

Initially,`5.0%` of the token supply (`50,000,000 ethDYDX`) was [allocated](https://docs.dydx.community/dydx-governance/start-here/dydx-allocations) to the Community Treasury, and 766,703 `ethDYDX` vests in the community treasury each epoch. Currently, 3,787,251 `ethDYDX` vest in the community treasury because several governance proposals resulted in a 3,020,548 `ethDYDX` increase in the amount of `ethDYDX` available to the dYdX community each epoch:

* [DIP 14](https://dydx.community/dashboard/proposal/7) - set the rewards for staking USDC to 0 (383,562 `ethDYDX` per epoch),&#x20;
* [DIP 16](https://dydx.community/dashboard/proposal/8) - reduce trading rewards by 25% (958,904 `ethDYDX` per epoch),&#x20;
* [DIP 17](https://dydx.community/dashboard/proposal/9) - set the rewards for staking $DYDX to 0 (383,562 `ethDYDX` per epoch),
* [DIP 20](https://dydx.community/dashboard/proposal/11) - further reduce trading rewards by 45% (1,294,520 `ethDYDX` per epoch), and
* [DIP 24](https://github.com/dydxfoundation/dip/blob/master/content/dips/DIP-24.md) - reduce Liquidity Provider Rewards by 50% (575,342 `ethDYDX` per epoch).&#x20;
*   [DIP 29](https://dydx.community/dashboard/proposal/16) - reduce Liquidity Provider Rewards by ⅓ from Epoch 30-32 on dYdX v3 to the following values:

    * Epoch 30: 383,562 $ethDYDX
    * Epoch 31: 191,781 $ethDYDX
    * Epoch 32: 0 $ethDYDX

    After Epoch 31, there will not be any Liquidity Provider Rewards on dYdX v3. In DIP 29, the dYdX community voted to reduce Trading Rewards by ⅓ from Epoch 30-32 on dYdX v3, however the remaining allocation of Trading Rewards was migrated to the dYdX Chain for Trading Rewards.&#x20;

In [DIP 29](https://dydx.community/dashboard/proposal/16) on dYdX v3, the dYdX community also voted to migrate 40,703,630 vested ethDYDX from the Rewards Treasury and 39,788,640 vested ethDYDX from the Community Treasury to the dYdX Chain Community Treasury. In addition to the 80,492,270 DYDX from the dYdX v3 Rewards Treasury and Community Treasury, DYDX vests every second from the community\_vester to the community\_treasury.

## Community Vester

In [DIP 2](https://www.mintscan.io/dydx/proposals/2) on the dYdX Chain, the dYdX community voted to credit the dYdX Community Vester with 172,762,268.210688518 unvested DYDX tokens based on the balance of the dYdX v3 [Community Treasury Vester](https://etherscan.io/address/0x08a90Fe0741B7DeF03fB290cc7B273F1855767D8) and the dYdX v3 [Rewards Treasury Vester](https://etherscan.io/address/0xb9431e19b29b952d9358025f680077c3fd37292f), less the DYDX that was sent to the dYdX Chain Rewards Vester for Trading Rewards.&#x20;

## FAQ

<details>

<summary><strong>How to Submit a Community Spending Proposal?</strong></summary>

Any dYdX community member with enough unstaked DYDX tokens to satisfy the `min_initial_deposit_ratio` may submit a Community Spending proposal on dYdX Chain. A governance vote will be required to spend any DYDX from the Community Treasury.&#x20;

To submit a proposal, please follow the steps laid out on the [Proposal Lifecycle](https://docs.dydx.community/dydx-token-migration/dydx-chain-modules-and-parameters/governance/proposal-lifecycle). The main inputs for a Community Spending Proposal are (1) the number of DYDX and (2) the recipient address.

</details>

<details>

<summary><strong>How does DYDX vest from the Community Vester to the Community Treasury?</strong></summary>

The Vest Module allows the vesting process to happen on the dYdX Chain. The module is responsible for determining the rate of tokens that vest from Vester Accounts to other accounts such as a `community_treasury` and a `rewards_treasury`. The rate of token transfers is linear with respect to time. Thus, block timestamps are used to vest tokens.

The dYdX Community through a governance vote has the ability to create, update, or delete `vest_entries` through a governance vote.

Based on the `start_time` and `end_time`, DYDX will vest from the Community Vester to the Community Treasury at approximately \~2.04 DYDX per second.

</details>

<details>

<summary><strong>What types of proposals can be submitted to the Community Treasury?</strong></summary>

A community-managed treasury opens up a world of possibilities. We hope to see various experiments and initiatives, including ecosystem grants, which can foster dYdX Chain's ecosystem growth.

</details>

