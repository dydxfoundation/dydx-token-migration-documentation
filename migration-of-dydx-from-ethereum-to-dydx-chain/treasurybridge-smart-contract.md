---
description: Overview of the TreasuryBridge Smart Contract
---

# 🌉 TreasuryBridge Smart Contract

<figure><img src="../.gitbook/assets/TreasuryBridge Smart Contract.png" alt=""><figcaption></figcaption></figure>

## Community Treasury Allocation

The Community Treasury was initially allocated 5.0% of the token supply, with 766,703 ethDYDX vesting in the treasury each epoch. However, as a result of several governance proposals, this allocation gradually increased to 26.1% over time.

In [DIP 29](https://dydx.community/dashboard/proposal/16), the dYdX community voted to reduce Trading & Liquidity Provider Rewards on dYdX v3 by 1/3 for Epoch 30-31. After Epoch 31, there are no Trading & Liquidity Provider Rewards on dYdX v3.&#x20;

## **TreasuryBridge Contract**

Since the [`TreasuryVester Smart Contract`](https://github.com/dydxfoundation/governance-contracts/blob/master/contracts/treasury/TreasuryVester.sol) is immutable, an updated [`Treasury Smart Contract`](https://github.com/dydxfoundation/governance-contracts/blob/master/contracts/treasury/Treasury.sol), `TreasuryBridge Smart Contract` was developed. The `TreasuryBridge Smart Contract,` was deployed for each of the community treasury and rewards treasury. The `TreasuryBridge Smart Contract`:

* **One time**: rejects new vesting from the `TreasuryVester Smart Contract` by calling the `setRecipient` function on this contract to set the recipient to a burn address, and
* **Ongoing Basis**: allows governance to bridge any amount of existing tokens in the community treasury or the rewards treasury (the current `Treasury Smart Contract` only allows `transfer()` and `approve()`).

Note, the `TreasuryBridge smart contract` is similar to the current corresponding `Treasury Smart Contract` except for the two differences referenced above.&#x20;



## Resources

* [Github TreasuryBridge Smart Contract](https://github.com/dydxfoundation/governance-contracts/blob/master/contracts/treasury/TreasuryBridge.sol)
* [Peckshield Audit Report](https://github.com/dydxfoundation/governance-contracts/blob/master/audits/PeckShield-Audit-Report-dYdX-Bridge-v1.1.pdf)

**V3 Treasury Contracts**

Currently, **26.1%** of the total token supply of `ethDYDX`, which amounts to `261,133,225 ethDYDX`, is allocated to the Community Treasury. This allocation is designed to sustainably support contributor grants, community initiatives, liquidity mining, and other assorted programs.&#x20;

Initially,`5.0%` of the token supply (`50,000,000 ethDYDX`) was [allocated](https://docs.dydx.community/dydx-governance/start-here/dydx-allocations) to the Community Treasury, and 766,703 `ethDYDX` vested in the community treasury each epoch. The allocation of the Community Treasury increased as a result of several governance proposals.&#x20;

* [DIP 14](https://dydx.community/dashboard/proposal/7) - set the rewards for staking USDC to 0 (383,562 `ethDYDX` per epoch),&#x20;
* [DIP 16](https://dydx.community/dashboard/proposal/8) - reduce trading rewards by 25% (958,904 `ethDYDX` per epoch),&#x20;
* [DIP 17](https://dydx.community/dashboard/proposal/9) - set the rewards for staking $DYDX to 0 (383,562 `ethDYDX` per epoch),
* [DIP 20](https://dydx.community/dashboard/proposal/11) - further reduce trading rewards by 45% (1,294,520 `ethDYDX` per epoch), and
* [DIP 24](https://github.com/dydxfoundation/dip/blob/master/content/dips/DIP-24.md) - reduce Liquidity Provider Rewards by 50% (575,342 `ethDYDX` per epoch).&#x20;
*   [DIP 29](https://dydx.community/dashboard/proposal/16) - reduce Trading Rewards and Liquidity Provider Rewards by ⅓ from Epoch 30-32 on dYdX v3 to the following values:

    * Epoch 30:&#x20;
      * Trading: 1,054,795 $ethDYDX
      * LP: 383,562 $ethDYDX
    * Epoch 31:&#x20;
      * Trading: 527,398 $ethDYDX
      * LP: 191,781 $ethDYDX
    * Epoch 32:&#x20;
      * Trading: 0 $ethDYDX
      * LP: 0 $ethDYDX

    After Epoch 31, there are no Trading Rewards and Liquidity Provider Rewards on dYdX v3.&#x20;

**Objectives**

* Fund programs and initiatives that drive the growth of dYdX.
* Develop grant programs to fund community NFTs, hackathons, analytics dashboards, memes, swag, third-party tools, translations, and other projects.
* Develop a best-in-class governance system and incentivize robust governance.

## Overview

The community treasury will retain `ethDYDX` to use as `ethDYDX` holders decide whether it be for grants, new liquidity mining pools, or any other program. `ethDYDX` will vest to the community treasury continuously over five years. A governance vote will be required to spend any `ethDYDX` from the community treasury.

If, after five years, governance decides to enact perpetual inflation (at a maximum annual inflation of `2%`), any newly minted ethDYDX will be available to the community treasury.

## FAQ

### How did $ethDYDX vest in the Community Treasury?

The Community Treasury Vester (see details [here](https://docs.dydx.community/dydx-governance/resources/technical-overview#governance-architecture-overview)) used to vest [`0.3169242627`](tel:03169242627) `ethDYDX` every second to the Community Treasury. Once `ethDYDX` had been vested, calling the `claim` function on the Community Treasury Vester would transfer the vested `ethDYDX` to the Community Treasury. Any dYdX community member can call the `claim` function on Etherscan [here](https://etherscan.io/address/0x08a90Fe0741B7DeF03fB290cc7B273F1855767D8#writeContract) (which would require some ETH for gas fees) to move the vested `ethDYDX` from the Community Treasury Vester to the Community Treasury.

In DIP 29, the dYdX v3 community voted to set the recipient of the Community Treasury Vester to `0x0000000000000000000000000000000000000002` , to effectively burn all unvested ethDYDX in the Community Treasury Vester.

Please refer to the dYdX Foundation’s [Terms of Use](https://dydx.foundation/terms) for further details on the control of the Community Treasury by the dYdX community.

<figure><img src="../.gitbook/assets/CT vesting .webp" alt=""><figcaption></figcaption></figure>

### Who can submit proposals to spend `ethDYDX` from the Community Treasury?

Any user with sufficient proposing power can submit proposals. A governance vote will be required to spend any `ethDYDX` from the Community Treasury. To submit a proposal, please submit a dYdX Improvement Proposal (DIP) as laid out in the [DIP Proposal Lifecycle](broken-reference).

### How do you go about building a proposal to spend funds from the Community Treasury?

Reverie has put together a comprehensive, technical, step-by-step guide on how any dYdX community member with more than 5M `ethDYDX` ([proposal threshold](https://docs.dydx.community/dydx-governance/voting-and-governance/governance-parameters#timelock-parameters) for a [short timelock vote](https://docs.dydx.community/dydx-governance/voting-and-governance/governance-process#short-timelock-executor)) of proposal power can create a proposal to transfer `ethDYDX` from the Community Treasury to a destination address. Click [here](https://app.gitbook.com/o/-MeNgGQU0ucT2xo4s8-T/s/-MeNfSkgj48hU0q8Zbjn/\~/changes/EyisuFjLIyJ7K9RzaTfJ/technical-guide-on-building-a-dydx-community-treasury-spending-proposal) to access the technical guide.

### What types of proposals can be submitted to the Community Treasury?

A community-managed treasury opens up a world of possibilities. We hope to see various experiments and initiatives, including ecosystem grants, which can foster the dYdX Layer 2 Protocol’s ecosystem growth.

The TreasuryVester contract was inspired by [Uniswap](https://github.com/Uniswap/governance/blob/master/contracts/TreasuryVester.sol).



<table><thead><tr><th width="261">Contract</th><th>Address</th></tr></thead><tbody><tr><td>Rewards Treasury</td><td>0x639192D54431F8c816368D3FB4107Bc168d0E871</td></tr><tr><td>Rewards Treasury Vester</td><td>0xb9431E19B29B952d9358025f680077C3Fd37292f</td></tr><tr><td>Community Treasury</td><td>0xE710CEd57456D3A16152c32835B5FB4E72D9eA5b</td></tr><tr><td>Community Treasury Vester</td><td>0x08a90Fe0741B7DeF03fB290cc7B273F1855767D8</td></tr><tr><td>Short Timelock Executor</td><td>0x64c7d40c07EFAbec2AafdC243bF59eaF2195c6dc</td></tr><tr><td>Merkle Distributor</td><td>0x01d3348601968aB85b4bb028979006eac235a588</td></tr><tr><td>Safety Module</td><td>0x65f7BA4Ec257AF7c55fd5854E5f6356bBd0fb8EC</td></tr><tr><td>Liquidity Staking</td><td>0x5Aa653A076c1dbB47cec8C1B4d152444CAD91941</td></tr><tr><td>DydxToken</td><td>0x92D6C1e31e14520e676a687F0a93788B716BEff5</td></tr><tr><td>DydxGovernor</td><td>0x7E9B1672616FF6D6629Ef2879419aaE79A9018D2</td></tr></tbody></table>



[https://docs.dydx.community/dydx-governance/resources/technical-overview](https://docs.dydx.community/dydx-governance/resources/technical-overview)



<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

The Short Timelock can only execute governance-approved actions.

There are two vesting contracts, the Rewards Treasury Vester and the Community Treasury Vester. Each vester vests `ethDYDX` to the respective treasury contract - Rewards Treasury Vester to the Rewards Treasury and Community Treasury Vester to the Community Treasury. &#x20;

dYdX governance under the [Short Timelock Executor](https://docs.dydx.community/dydx-governance/voting-and-governance/governance-process#short-timelock-executor), controls the Rewards Treasury and the Community Treasury. As such, the dYdX community through dYdX governance can transfer funds in the Rewards Treasury and the Community Treasury to any address and/or approve any address to spend funds from either treasury.&#x20;

Each treasury vester will vest tokens linearly over \~5 years (August 3rd 2021 - August 3rd 2026) to the corresponding treasury.
