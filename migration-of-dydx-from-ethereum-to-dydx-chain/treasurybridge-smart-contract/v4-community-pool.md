---
description: An overview of the v4 Community Pool
---

# v4 Community Pool

<figure><img src="../../.gitbook/assets/Community Pool.png" alt=""><figcaption></figcaption></figure>

Currently, **24.2%** of the total token supply of `ethDYDX`, which amounts to 241,735,862 `ethDYDX`, is allocated to the Community Treasury. This allocation is designed to sustainably support contributor grants, community initiatives, liquidity mining, and other assorted programs.&#x20;

Initially,`5.0%` of the token supply (`50,000,000 ethDYDX`) was [allocated](https://docs.dydx.community/dydx-governance/start-here/dydx-allocations) to the Community Treasury, and 766,703 `ethDYDX` vests in the community treasury each epoch. Currently, 3,787,251 `ethDYDX` vest in the community treasury because several governance proposals resulted in a 3,020,548 `ethDYDX` increase in the amount of `ethDYDX` available to the dYdX community each epoch:

* [DIP 14](https://dydx.community/dashboard/proposal/7) - set the rewards for staking USDC to 0 (383,562 `ethDYDX` per epoch),&#x20;
* [DIP 16](https://dydx.community/dashboard/proposal/8) - reduce trading rewards by 25% (958,904 `ethDYDX` per epoch),&#x20;
* [DIP 17](https://dydx.community/dashboard/proposal/9) - set the rewards for staking $DYDX to 0 (383,562 `ethDYDX` per epoch),
* [DIP 20](https://dydx.community/dashboard/proposal/11) - further reduce trading rewards by 45% (1,294,520 `ethDYDX` per epoch), and
* [DIP 24](https://github.com/dydxfoundation/dip/blob/master/content/dips/DIP-24.md) - reduce Liquidity Provider Rewards by 50% (575,342 `ethDYDX` per epoch).&#x20;

### How is the Community Treasury replenished on dYdX Chain?

Under the [x/distribution module](https://docs.cosmos.network/main/modules/distribution#reward-to-the-community-pool) of the Cosmos SDK, the `community tax` specifies that a fraction of the fees can be reserved for the given chain's community pool.&#x20;

On August 3, 2023, dYdX Trading [announced](https://dydx.exchange/blog/v4-rewards-and-parameters) that the dYdX v4 open source software would initially reflect a `community tax` of 0%. Notably, the `community tax` parameter is subject to adjustments by the [x/gov module](https://docs.cosmos.network/main/modules/gov) by the dYdX community and can be set to different values at Genesis by any deployer of the dYdX v4 open source software.&#x20;
