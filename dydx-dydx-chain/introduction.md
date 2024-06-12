---
description: An overview of DYDX (dYdX Chain)
---

# ⚙️ Introduction

After an ethDYDX holder interacts with the wethDYDX Smart Contract, dYdX Chain validators can read and ingest the information from the contract. Once Step 1 is complete and ethDYDX is permanently locked in the wethDYDX Smart Contract, validators can distribute the corresponding amount of DYDX (1-1) to users on the dYdX Chain.&#x20;

<figure><img src="../.gitbook/assets/Bridging Step 3(b) NEW.png" alt=""><figcaption></figcaption></figure>

### How dYdX Chain Validators Credit User Accounts on dYdX Chain&#x20;

#### Validator's Reading of the Logs

dYdX Chain validators must track Ethereum blockchain events by querying an Ethereum node through RPC calls. They should process only finalized blocks. Validators will specify the Ethereum RPC endpoint in the start command, with the option to store the URL in a configuration file. The node can be self-run or a hosted node from Alchemy or Infura, but for decentralization, no more than 1/3 of the stake weight should rely on any one centralized service.

#### Adding the Information to State

There would be a new injectable transaction that dYdX Chain validators can add in their blocks that mints tokens to the dYdX Chain as long as there is a corresponding event on Ethereum. dYdX Chain validators should only validate blocks with valid transactions (i.e., if they have also seen this event finalized on the Ethereum blockchain).

Each transaction should match (then increment) the `eventId` which is kept in dYdX Chain state so that no events are skipped (without manual intervention) and only one integer is needed to track state for this module (limiting the amount of state needed for the module). The `eventId` should be set to some non-zero number at genesis to prevent replaying the events that were already added at genesis.
