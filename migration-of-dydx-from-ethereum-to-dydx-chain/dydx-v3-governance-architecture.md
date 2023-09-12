---
description: Overview of the dYdX v3 Governance Architecture
---

# dYdX v3 Governance Architecture

<figure><img src="../.gitbook/assets/dYdX v3 Governance Architecture.png" alt=""><figcaption></figcaption></figure>

### V3 Governance Architecture

DYDX grants holders the right to propose and vote on changes to the dYdX v3 protocol on Ethereum. DYDX governance is based on the AAVE governance contracts, and supports voting based on DYDX token holdings.

Proposals must pass a given threshold and percent of yes votes based on the type of [timelock](https://docs.dydx.community/dydx-governance/voting-and-governance/governance-parameters#timelock-parameters) that the subject matter of the respective proposal falls under.

These DYDX tokens can be used to make [governance proposals or vote on governance proposals](https://docs.dydx.community/dydx-governance/voting-and-governance/voting#proposing-and-voting-powers) or be delegated to other Ethereum addresses.

Per the V3 governance architecture available [here](https://docs.dydx.community/dydx-governance/voting-and-governance/governance-process), there are 6 smart contracts at the core of dYdX v3 Governance on Ethereum:

* **The `DYDX Token` contract**: has snapshots of each address’ voting power at different blocks in time.
* **The `GovernanceStrategy` contract**: contains logic to measure users' relative power to propose and vote.
* **The `Safety Module` contract**: contains logics to stake DYDX tokens, tokenize the position and get rewards. Token staked the safety module retain full governance rights.
* **The `Governor` contract**: tracks proposals and can execute proposals via the Timelock smart contract.
* **The `Timelock` contracts**: can queue, cancel, or execute transactions voted by Governance. The functions in a proposal are initiated by the Timelock contract. Queued transactions can be executed after a delay and before the expiration of the grace period.
* **The `Priority Timelock` contract**: The same as the timelock contract, but allows a priority controller to execute transactions within the **Priority Period** (7 days) before the end of the timelock delay.

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption><p>Simplified dYdX v3 Governance Architecture</p></figcaption></figure>



The following subset of contracts have been deployed on Ethereum mainnet:

<table><thead><tr><th width="261">Contract</th><th>Address</th></tr></thead><tbody><tr><td>DydxToken</td><td>0x92D6C1e31e14520e676a687F0a93788B716BEff5</td></tr><tr><td>DydxGovernor</td><td>0x7E9B1672616FF6D6629Ef2879419aaE79A9018D2</td></tr><tr><td>Short Timelock Executor</td><td>0x64c7d40c07EFAbec2AafdC243bF59eaF2195c6dc</td></tr><tr><td>Rewards Treasury</td><td>0x639192D54431F8c816368D3FB4107Bc168d0E871</td></tr><tr><td>Community Treasury</td><td>0xE710CEd57456D3A16152c32835B5FB4E72D9eA5b</td></tr><tr><td>Safety Module</td><td>0x65f7BA4Ec257AF7c55fd5854E5f6356bBd0fb8EC</td></tr><tr><td>GovernanceStrategy</td><td>0x90Dfd35F4a0BB2d30CDf66508085e33C353475D9</td></tr><tr><td>Rewards Treasury Vester</td><td>0xb9431E19B29B952d9358025f680077C3Fd37292f</td></tr><tr><td>Community Treasury Vester</td><td>0x08a90Fe0741B7DeF03fB290cc7B273F1855767D8</td></tr></tbody></table>

## Open-source code & audited

All smart contract source code for the governance contracts and staking pools can be found at [https://github.com/dydxfoundation/governance-contracts](https://github.com/dydxfoundation/governance-contracts).

The source code for the governance frontend hosted at dydx.community can be found [here](https://github.com/dydxfoundation/pnyx).

All major smart contracts have been audited by Peckshield. No significant or high priority security issues were found. The core governance and token contracts are forked from the Aave governance contracts which were audited by [CertiK](https://www.certik.io/), [Certora](https://www.certora.com/), and [Peckshield](https://peckshield.com/en) and have been battle-tested live on mainnet.

### Resources

* [V3 Governance Documentation](https://docs.dydx.community/dydx-governance/)
