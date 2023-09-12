---
description: An overview of DYDX (dYdX Chain)
---

# Introduction

In the section below we discuss how dYdX Chain validators would credit dYdX Chain user accounts with `DYDX`, if the dYdX community decided through dYdX governance to replace the `GovernanceStrategy smart contract` with the `GovernanceStrategyV2 smart contract.`

### Overview of the `wethDYDX Smart Contract`

If a user interacts with the `wethDYDX Smart Contract` before a certain cut-off date prior to the genesis of the dYdX Chain (“Genesis”), the amount of `ethDYDX` tokens sent by the user to the `wethDYDX Smart Contract` would be registered as event information of the `wethDYDX Smart Contract`. At this point, the user’s dYdX Chain wallet cannot be allocated with `DYDX` tokens because the dYdX Chain would not exist yet.



<figure><img src="../.gitbook/assets/Bridging Step 3(a) (2).png" alt=""><figcaption></figcaption></figure>

If a user interacts with the `wethDYDX Smart Contract` after Genesis, then each dYdX Chain validator participating in the consensus process would read the event information of the `wethDYDX Smart Contract` and allocate `DYDX` tokens on the dYdX Chain to a given user’s dYdX Chain address based on the corresponding amount (1-1) of `ethDYDX` tokens that the user sent to the `wethDYDX Smart Contract`. Note, a user who interacts with the `wethDYDX Smart Contract` after the relevant cut-off time referred to above but before Genesis would be credited with L1 dYdX Chain tokens by the dYdX Chain validators in the blocks confirmed after Genesis.



<figure><img src="../.gitbook/assets/Bridging Step 3(b) (3).png" alt=""><figcaption></figcaption></figure>

### How dYdX Chain Validators Credit User Accounts on dYdX Chain&#x20;

#### Pre-Genesis Cut-off Time

At Genesis, the deployer of the dYdX Chain open source software will need to select a cut-off time before Genesis, Ethereum block height `H.` Any bridging that occurred before block height `H` can be considered to be included in Genesis. Any bridging that occurs after Ethereum block height `H`will be credited in a later dYdX Chain block after Genesis.&#x20;

#### Validator's Reading of the Logs

Each dYdX Chain validator will have to understand which events have or haven’t occurred on the Ethereum blockchain. Validators can do this by making RPC calls to an Ethereum node to get relevant logs. dYdX Chain validators should only process `finalized` blocks.

Validators will need to provide Ethereum RPC endpoint as a flag in the start command, instead of in a config file. Eventually, the URL of the node can be stored in the configuration file of the given validator. Ideally, this node is run by the validator themselves, but it could also be a hosted node from Alchemy or Infura. Ideally, to achieve a decentralized network, no more than 1/3 of the stake weight should use any one centralized service.&#x20;

#### Adding the Information to State

There would be a new injectable transaction that dYdX Chain validators can add in their blocks that mints tokens to the dYdX Chain as long as there is a corresponding event on Ethereum. dYdX Chain validators should only validate blocks with valid transactions (i.e., if they have also seen this event finalized on the Ethereum blockchain).

Each transaction should match (then increment) the `eventId` which is kept in dYdX Chain state so that no events are skipped (without manual intervention) and only one integer is needed to track state for this module (limiting the amount of state needed for the module). The `eventId` should be set to some non-zero number at genesis to prevent replaying the events that were already added at genesis.
