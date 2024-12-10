---
description: Overview of the TreasuryBridge Smart Contract
---

# 🌉 TreasuryBridge Smart Contract

<figure><img src="../.gitbook/assets/TreasuryBridge Smart Contract.png" alt=""><figcaption></figcaption></figure>

## Community Treasury Allocation

The Community Treasury was initially allocated 5.0% of the token supply, with 766,703 ethDYDX vesting in the treasury each epoch. However, as a result of several governance proposals, this allocation gradually increased to 26.1% over time.

In [DIP 29](https://dydx.community/dashboard/proposal/16), the dYdX community voted to reduce Trading & Liquidity Provider Rewards on dYdX v3 by 1/3 for Epoch 30-31. After Epoch 31, there are no Trading & Liquidity Provider Rewards on dYdX v3.&#x20;

On November 18, 2023, the dYdX community [voted](https://dydx.community/dashboard/proposal/16) to bridge the ethDYDX balance accrued in the Community Treasury from Ethereum to dYdX Chain. Once bridged, the DYDX can be used by the dYdX community with a governance vote on dYdX Chain.

More information about the dYdX Chain Community Treasury is available [here](https://app.gitbook.com/s/7eKRye9zrZIr1Pp3Q3Mu/modules/community-treasury).

## **TreasuryBridge Contract**

Since the [`TreasuryVester Smart Contract`](https://github.com/dydxfoundation/governance-contracts/blob/master/contracts/treasury/TreasuryVester.sol) is immutable, an updated [`Treasury Smart Contract`](https://github.com/dydxfoundation/governance-contracts/blob/master/contracts/treasury/Treasury.sol), `TreasuryBridge Smart Contract` was developed. The `TreasuryBridge Smart Contract,` was deployed for each of the community treasury and rewards treasury. The `TreasuryBridge Smart Contract`:

* **One time**: rejects new vesting from the `TreasuryVester Smart Contract` by calling the `setRecipient` function on this contract to set the recipient to a burn address, and
* **Ongoing Basis**: allows governance to bridge any amount of existing tokens in the community treasury or the rewards treasury (the current `Treasury Smart Contract` only allows `transfer()` and `approve()`).

Note, the `TreasuryBridge smart contract` is similar to the current corresponding `Treasury Smart Contract` except for the two differences referenced above.&#x20;

## Resources

* [Github TreasuryBridge Smart Contract](https://github.com/dydxfoundation/governance-contracts/blob/master/contracts/treasury/TreasuryBridge.sol)
* [Peckshield Audit Report](https://github.com/dydxfoundation/governance-contracts/blob/master/audits/PeckShield-Audit-Report-dYdX-Bridge-v1.1.pdf)

